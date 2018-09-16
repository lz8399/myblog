+++
title= "[UE4]引擎源码分析之：Memory"
date= "2018-02-07T17:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "GC"]
+++

内存管理的入口：

    Engine\Source\Runtime\Core\Public\HAL\UnrealMemory.h

内存池中的内存开辟和销毁

    Engine\Source\Runtime\Core\Private\HAL\MallocBinned.cpp
    
### MallocBinned.cpp主要函数

内存池的创建：

    static FPoolInfo* AllocatePoolMemory(FMallocBinned& Allocator, FPoolTable* Table, uint32 PoolSize, uint16 TableIndex)
	{
		const uint32 PageSize = Allocator.PageSize;

		// Must create a new pool.
		uint32 Blocks   = PoolSize / Table->BlockSize;
		uint32 Bytes    = Blocks * Table->BlockSize;
		UPTRINT OsBytes = Align(Bytes, PageSize);

		checkSlow(Blocks >= 1);
		checkSlow(Blocks * Table->BlockSize <= Bytes && PoolSize >= Bytes);

		// Allocate memory.
		FFreeMem* Free = nullptr;
		SIZE_T ActualPoolSize; //TODO: use this to reduce waste?
		Free = (FFreeMem*)OSAlloc(Allocator, OsBytes, ActualPoolSize);

		checkSlow(!((UPTRINT)Free & (PageSize - 1)));
		if( !Free )
		{
			OutOfMemory(OsBytes);
		}

		// Create pool in the indirect table.
		FPoolInfo* Pool;
		{
    #ifdef USE_FINE_GRAIN_LOCKS
			FScopeLock PoolInfoLock(&Allocator.AccessGuard);
    #endif
			Pool = GetPoolInfo(Allocator, (UPTRINT)Free);
			for (UPTRINT i = (UPTRINT)PageSize, Offset = 0; i < OsBytes; i += PageSize, ++Offset)
			{
				FPoolInfo* TrailingPool = GetPoolInfo(Allocator, ((UPTRINT)Free) + i);
				check(TrailingPool);

				//Set trailing pools to point back to first pool
				TrailingPool->SetAllocationSizes(0, 0, Offset, Allocator.BinnedOSTableIndex);
			}

			
			BINNED_PEAK_STATCOUNTER(Allocator.OsPeak,    BINNED_ADD_STATCOUNTER(Allocator.OsCurrent,    OsBytes));
			BINNED_PEAK_STATCOUNTER(Allocator.WastePeak, BINNED_ADD_STATCOUNTER(Allocator.WasteCurrent, (OsBytes - Bytes)));
		}

		// Init pool.
		Pool->Link( Table->FirstPool );
		Pool->SetAllocationSizes(Bytes, OsBytes, TableIndex, Allocator.BinnedOSTableIndex);
		Pool->Taken		 = 0;
		Pool->FirstMem   = Free;

    #if STATS
		Table->NumActivePools++;
		Table->MaxActivePools = FMath::Max(Table->MaxActivePools, Table->NumActivePools);
    #endif
		// Create first free item.
		Free->NumFreeBlocks = Blocks;
		Free->Next          = nullptr;

		return Pool;
	}
    
内存池内分配内存：

    static FORCEINLINE FFreeMem* AllocateBlockFromPool(FMallocBinned& Allocator, FPoolTable* Table, FPoolInfo* Pool, uint32 Alignment)
	{
		// Pick first available block and unlink it.
		Pool->Taken++;
		checkSlow(Pool->TableIndex < Allocator.BinnedOSTableIndex); // if this is false, FirstMem is actually a size not a pointer
		checkSlow(Pool->FirstMem);
		checkSlow(Pool->FirstMem->NumFreeBlocks > 0);
		checkSlow(Pool->FirstMem->NumFreeBlocks < PAGE_SIZE_LIMIT);
		FFreeMem* Free = (FFreeMem*)((uint8*)Pool->FirstMem + --Pool->FirstMem->NumFreeBlocks * Table->BlockSize);
		if( !Pool->FirstMem->NumFreeBlocks )
		{
			Pool->FirstMem = Pool->FirstMem->Next;
			if( !Pool->FirstMem )
			{
				// Move to exhausted list.
				Pool->Unlink();
				Pool->Link( Table->ExhaustedPool );
			}
		}
		BINNED_PEAK_STATCOUNTER(Allocator.UsedPeak, BINNED_ADD_STATCOUNTER(Allocator.UsedCurrent, Table->BlockSize));
		return Align(Free, Alignment);
	}
    
内存池内回收内存（非物理销毁）

    /**
	* Releases memory back to the system. This is not protected from multi-threaded access and it's
	* the callers responsibility to Lock AccessGuard before calling this.
	*/
	static void FreeInternal(FMallocBinned& Allocator, void* Ptr)
	{
		MEM_TIME(MemTime -= FPlatformTime::Seconds());
		BINNED_DECREMENT_STATCOUNTER(Allocator.CurrentAllocs);

		UPTRINT BasePtr;
		FPoolInfo* Pool = FindPoolInfo(Allocator, (UPTRINT)Ptr, BasePtr);
    #if PLATFORM_IOS || PLATFORM_MAC
        if (Pool == NULL)
        {
            UE_LOG(LogMemory, Warning, TEXT("Attempting to free a pointer we didn't allocate!"));
            return;
        }
    #endif
		checkSlow(Pool);
		checkSlow(Pool->GetBytes() != 0);
		if (Pool->TableIndex < Allocator.BinnedOSTableIndex)
		{
			FPoolTable* Table = Allocator.MemSizeToPoolTable[Pool->TableIndex];
    #ifdef USE_FINE_GRAIN_LOCKS
			FScopeLock TableLock(&Table->CriticalSection);
    #endif
    #if STATS
			Table->ActiveRequests--;
    #endif
			// If this pool was exhausted, move to available list.
			if( !Pool->FirstMem )
			{
				Pool->Unlink();
				Pool->Link( Table->FirstPool );
			}

			void* BaseAddress = (void*)BasePtr;
			uint32 BlockSize = Table->BlockSize;
			PTRINT OffsetFromBase = (PTRINT)Ptr - (PTRINT)BaseAddress;
			check(OffsetFromBase >= 0);
			uint32 AlignOffset = OffsetFromBase % BlockSize;

			// Patch pointer to include previously applied alignment.
			Ptr = (void*)((PTRINT)Ptr - (PTRINT)AlignOffset);

			// Free a pooled allocation.
			FFreeMem* Free		= (FFreeMem*)Ptr;
			Free->NumFreeBlocks	= 1;
			Free->Next			= Pool->FirstMem;
			Pool->FirstMem		= Free;
			BINNED_ADD_STATCOUNTER(Allocator.UsedCurrent, -(int64)(Table->BlockSize));

			// Free this pool.
			checkSlow(Pool->Taken >= 1);
			if( --Pool->Taken == 0 )
			{
    #if STATS
				Table->NumActivePools--;
    #endif
				// Free the OS memory.
				SIZE_T OsBytes = Pool->GetOsBytes(Allocator.PageSize, Allocator.BinnedOSTableIndex);
				BINNED_ADD_STATCOUNTER(Allocator.OsCurrent,    -(int64)OsBytes);
				BINNED_ADD_STATCOUNTER(Allocator.WasteCurrent, -(int64)(OsBytes - Pool->GetBytes()));
				Pool->Unlink();
				Pool->SetAllocationSizes(0, 0, 0, Allocator.BinnedOSTableIndex);
				OSFree(Allocator, (void*)BasePtr, OsBytes);
			}
		}
		else
		{
			// Free an OS allocation.
			checkSlow(!((UPTRINT)Ptr & (Allocator.PageSize - 1)));
			SIZE_T OsBytes = Pool->GetOsBytes(Allocator.PageSize, Allocator.BinnedOSTableIndex);

			BINNED_ADD_STATCOUNTER(Allocator.UsedCurrent,  -(int64)Pool->GetBytes());
			BINNED_ADD_STATCOUNTER(Allocator.OsCurrent,    -(int64)OsBytes);
			BINNED_ADD_STATCOUNTER(Allocator.WasteCurrent, -(int64)(OsBytes - Pool->GetBytes()));
			OSFree(Allocator, (void*)BasePtr, OsBytes);
		}

		MEM_TIME(MemTime += FPlatformTime::Seconds());
	}

***
`对一个男人来说 最无能为力的事儿就是 在最没有能力的年纪，碰见了，最想照顾一生的姑娘。`
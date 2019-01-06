+++
title= "[C++]Address source line from crash callstack using binary"
date= "2019-01-02T11:26:40+08:00"
categories= ["C++"]
tags= ["C++"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-001.jpg"
+++

Get the crash callstack.  

<!--more-->

keywords: Windows Debugging Tools, PDB file, Crash, Dump file

### WinDbg for Windows

Steps

1. Get the crash callstack. e.g.:

		TestTP2   0x00000000fff20000 + 2c44aa2 
		TestTP2   0x00000000fff20000 + 987262  
		TestTP2   0x00000000fff20000 + 3ab0cc4 
		TestTP2   0x00000000fff20000 + 362fbbc 
		TestTP2   0x00000000fff20000 + 3643325 
		TestTP2   0x00000000fff20000 + 362d8e4 
		TestTP2   0x00000000fff20000 + 3642128 
		TestTP2   0x00000000fff20000 + 2c20100 
		TestTP2   0x00000000fff20000 + 39a2c25 
		TestTP2   0x00000000fff20000 + 39ba846 
		TestTP2   0x00000000fff20000 + 9cae56  
		TestTP2   0x00000000fff20000 + 9cb376  
		TestTP2   0x00000000fff20000 + 3a07c61 
		TestTP2   0x00000000fff20000 + 3a16ef8 
		TestTP2   0x00000000fff20000 + 32dff6f 
		TestTP2   0x00000000fff20000 + 32e8e3f 
		TestTP2   0x00000000fff20000 + 3146e59 
		TestTP2   0x00000000fff20000 + 43f1c9  
		TestTP2   0x00000000fff20000 + 44ec1c  
		TestTP2   0x00000000fff20000 + 44ec7a  
		TestTP2   0x00000000fff20000 + 45d265  
		TestTP2   0x00000000fff20000 + 47dc1c6 
		KERNEL32  0x0000000005b70000 + 18102   
		ntdll     0x00000000070f0000 + 5c5b4   

2. Open WinDbg, set symbol file and open binary file. e.g.:  
set symbol file directory
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-01.jpg">}}
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-02.jpg">}}
then WinDbg would search symbol file in this directory:
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-03.jpg">}}
3. Open Executable file:
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-04.jpg">}}
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-05.jpg">}}
4. Execute command to address source line. e.g. 

		ln TestTP2.exe+2c44aa2
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-06.jpg">}}
then would output the source line. In there, because SetActorLocation is the source of engine, and we didn't set the symbol file directory of engine binary, so it didn't display the engine source line.
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-07.jpg">}}
then we search the last address, we can find ourself source, and display the source file path and line
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-08.jpg">}}
5. Finally we can locate place where cause a crash: the line above the display line 
{{< figure src="/img/20190105-[C++]Address source line from crash callstack using binary/[C++]Address source line from crash callstack using binary-09.jpg">}}
{{< alert warning >}}
Note: the line displayed in WinDbg isn't the exact place where cause a crash, the real line cause the crash is above it.
{{< /alert >}}

WinDbg download  
https://github.com/dawnarc/DevTools/tree/master/Debug/Windows/WinDbg

WinDbg analysis dump file  
https://www.jianshu.com/p/ee979eaadf34

Where to put the PDBs in WinDbg  
https://stackoverflow.com/a/573796/1645289

##### Windows Driver

Manually Walking a Stack  
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/manually-walking-a-stack

### GDB command for Linux

Command:

	addr2line -e /path/to/non-stripped/.../my-buggy-app \
		0x4a6889 0x4a8b43 0x4e8765

Or
		
	info line *0x10045740

Using gdb to convert addresses to lines  
https://stackoverflow.com/questions/8545931/using-gdb-to-convert-addresses-to-lines
+++
title= "[UE4]error C3668: 'UTextureCube::UpdateResourceW'"
date= "2018-07-02T20:04:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

4.19 编译错误：

    2>F:\EpicGames\UE_4.19\Engine\Source\Runtime\Engine\Classes\Engine/TextureCube.h(69): error C3668: 'UTextureCube::UpdateResourceW': method with override specifier 'override' did not override any base class methods
    2>F:\EpicGames\UE_4.19\Engine\Source\Runtime\Engine\Classes\Engine/CanvasRenderTarget2D.h(43): error C3668: 'UCanvasRenderTarget2D::UpdateResourceW': method with override specifier 'override' did not override any base class methods

4.18 编译错误：
    
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(67): error C2039: '_InterlockedIncrement': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(67): error C2665: '_InterlockedIncrement': none of the 4 overloads could convert all the argument types
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8844): note: could be 'unsigned __int64 _InterlockedIncrement(volatile unsigned __int64 *)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8833): note: or       'unsigned long _InterlockedIncrement(volatile unsigned long *)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8824): note: or       'unsigned int _InterlockedIncrement(volatile unsigned int *)'
    2>C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\INCLUDE\intrin.h(259): note: or       'long _InterlockedIncrement(volatile long *)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(67): note: while trying to match the argument list '(volatile int64 *)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(79): error C2039: '_InterlockedAdd': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(79): error C2664: 'LONG _InterlockedAdd(volatile LONG *,LONG)': cannot convert argument 1 from 'volatile int64 *' to 'volatile LONG *'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(79): note: Types pointed to are unrelated; conversion requires reinterpret_cast, C-style cast or function-style cast
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(90): error C2039: '_InterlockedDecrement': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(90): error C2665: '_InterlockedDecrement': none of the 4 overloads could convert all the argument types
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8875): note: could be 'unsigned __int64 _InterlockedDecrement(volatile unsigned __int64 *)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8864): note: or       'unsigned long _InterlockedDecrement(volatile unsigned long *)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8855): note: or       'unsigned int _InterlockedDecrement(volatile unsigned int *)'
    2>C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\INCLUDE\intrin.h(209): note: or       'long _InterlockedDecrement(volatile long *)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(90): note: while trying to match the argument list '(volatile int64 *)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(102): error C2039: '_InterlockedAdd': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(102): error C2664: 'LONG _InterlockedAdd(volatile LONG *,LONG)': cannot convert argument 1 from 'volatile int64 *' to 'volatile LONG *'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(102): note: Types pointed to are unrelated; conversion requires reinterpret_cast, C-style cast or function-style cast
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(114): error C2039: '_InterlockedExchange': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(114): error C2665: '_InterlockedExchange': none of the 4 overloads could convert all the argument types
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8910): note: could be 'unsigned __int64 _InterlockedExchange(volatile unsigned __int64 *,unsigned __int64)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8898): note: or       'unsigned long _InterlockedExchange(volatile unsigned long *,unsigned long)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8888): note: or       'unsigned int _InterlockedExchange(volatile unsigned int *,unsigned int)'
    2>C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\INCLUDE\intrin.h(222): note: or       'long _InterlockedExchange(volatile long *,long)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(114): note: while trying to match the argument list '(volatile int64 *, int64)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(125): error C2039: '_InterlockedExchange': is not a member of 'FWindowsPlatformAtomics'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Core\Public\Windows/WindowsPlatformAtomics.h(14): note: see declaration of 'FWindowsPlatformAtomics'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(125): error C2665: '_InterlockedExchange': none of the 4 overloads could convert all the argument types
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8910): note: could be 'unsigned __int64 _InterlockedExchange(volatile unsigned __int64 *,unsigned __int64)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8898): note: or       'unsigned long _InterlockedExchange(volatile unsigned long *,unsigned long)'
    2>C:\Program Files (x86)\Windows Kits\8.1\include\um\winbase.h(8888): note: or       'unsigned int _InterlockedExchange(volatile unsigned int *,unsigned int)'
    2>C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\INCLUDE\intrin.h(222): note: or       'long _InterlockedExchange(volatile long *,long)'
    2>f:\epicgames\ue_4.18\engine\source\runtime\core\public\HAL/ThreadSafeCounter64.h(125): note: while trying to match the argument list '(volatile int64 *, int)'
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Engine\Classes\Engine/TextureCube.h(69): error C3668: 'UTextureCube::UpdateResourceW': method with override specifier 'override' did not override any base class methods
    2>F:\EpicGames\UE_4.18\Engine\Source\Runtime\Engine\Classes\Engine/CanvasRenderTarget2D.h(43): error C3668: 'UCanvasRenderTarget2D::UpdateResourceW': method with override specifier 'override' did not override any base class methods

上述两种编译错误的解决办法：  
MyProject.h中添加头文件：

    #include "Runtime/UMG/Public/UMG.h"
    #include "Runtime/UMG/Public/UMGStyle.h"
    #include "Runtime/UMG/Public/Slate/SObjectWidget.h"
    #include "Runtime/UMG/Public/IUMGModule.h"
    #include "Runtime/UMG/Public/Blueprint/UserWidget.h"
    
参考自：  
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/113028-getting-build-error-in-my-engine-plugin-while-building-in-ue4-editor-while-packaging-the-project?140208-Getting-build-error-in-my-engine-plugin-while-building-in-UE4-editor-while-packaging-the-project=
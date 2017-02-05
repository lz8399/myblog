---
title: "[Android NDK]STL linking issues (bug)"
date: "2016-10-15T02:24:40+08:00"
categories:
- Android
tags:
- NDK
- UE4
- Error
---


原文：
http://boguscoder.blogspot.jp/2013/08/android-ndk-stl-linking-issues-bug.html


ld.exe: libmoduleA.a(moduleA.o): in function std::priv::_String_base<char, std::allocator<char> >::_M_allocate_block(unsigned int):<android-ndk>/sources/cxx-stl/stlport/stlport/stl/_alloc.h:158: error: undefined reference to 'std::_node_alloc::_M_allocate(unsigned int&)'
ld.exe: libmoduleA.a(moduleA.o): in function std::priv::_String_base<char, std::allocator<char> >::_M_allocate_block(unsigned int):<android-ndk>/sources/cxx-stl/stlport/stlport/stl/_string.c:600: error: undefined reference to 'std:__stl_throw_length_error(char const*)'
ld.exe: libmoduleA.a(moduleA.o): in function functionA():<android-ndk>/sources/cxx-stl/stlport/stlport/stl/_alloc.h:161: error: undefined reference to 'std::__node_alloc::_M_deallocate(void*, unsigned int)'collect2: ld returned 1 exit status

Android.mk中添加库libstlport_static.a：

    LOCAL_LDLIBS  := -lmoduleA \
                     <NDK_PATH>/libstlport_static.a

如果是UE4工程编译Android，到android-ndk-r10e\sources\cxx-stl\stlport\libs\armeabi\下拷贝一个libstlport_static.a到你工程的库文件目录下即可。
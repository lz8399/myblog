+++
title= "[C++]Address source line from crash callstack using pdb (Display Stack Backtrace)"
date= "2019-01-02T11:26:40+08:00"
categories= ["C++"]
tags= ["C++"]
+++

keywords: Windows Debugging Tools, commands display the stack frame of the given thread

### Windows

Manually Walking a Stack  
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/manually-walking-a-stack

k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)  
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-

### Linux

Command:

	addr2line -e /path/to/non-stripped/.../my-buggy-app \
		0x4a6889 0x4a8b43 0x4e8765

Or
		
	info line *0x10045740

Using gdb to convert addresses to lines  
https://stackoverflow.com/questions/8545931/using-gdb-to-convert-addresses-to-lines
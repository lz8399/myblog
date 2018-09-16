+++
title= "[UE4]Assertions"
date= "2018-09-16T17:49:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Assertion", "断言"]
+++


1. Reporting errors and halting execution.
    + `check()`: like assert() in C, can be disabled by DO_CHECK 0
    + `verify()`: like check(), but the expression is still executed on DO_CHECK 0 (e.g. for variable assignments)
{{< alert info >}}
disadvantage: halts program execution (application ends, Editor users can loose unsaved work).  
when to use: catch fatal errors
{{< /alert >}}
2. Reporting errors and halting execution exclusively in debug builds.
    + `checkSlow()`, `checkfSlow()`, `verifySlow()` (see (1))
{{< alert info >}}
difference to (1): they are only active in debug builds (when DO_GUARD_SLOW 1)
{{< /alert >}}
3. Reporting errors (and do not halt the execution).
    + `ensure()`: like `check()`, but the program execution can be continued after the break
{{< alert info >}}
when to use: to get informed about unexpected state.  
useful when you want runtime code verification but you're handling the error case anyway
{{< /alert >}}

Reference：  
https://stackoverflow.com/questions/52127432/when-to-use-assertions-that-halt-the-execution-of-the-program-in-ue4
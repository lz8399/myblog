---
title: "[C++]可变参数_VA_ARGS__ "
date: "2017-04-19T16:17:40+08:00"
categories:
- C++
tags:
- C++
---

参考自：https://stackoverflow.com/questions/2124339/c-preprocessor-va-args-number-of-arguments

    #include <stdio.h>
    #include <string.h>
    #include <stdarg.h>

    #define NUMARGS(...)  (sizeof((int[]){__VA_ARGS__})/sizeof(int))
    #define SUM(...)  (sum(NUMARGS(__VA_ARGS__), __VA_ARGS__))

    void sum(int numargs, ...);

    int main(int argc, char *argv[]) {

        SUM(1);
        SUM(1, 2);
        SUM(1, 2, 3);
        SUM(1, 2, 3, 4);

        return 1;
    }

    void sum(int numargs, ...) {
        int     total = 0;
        va_list ap;

        printf("sum() called with %d params:", numargs);
        va_start(ap, numargs);
        while (numargs--)
            total += va_arg(ap, int);
        va_end(ap);

        printf(" %d\n", total);

        return;
    }
    
***
`晚食以当肉，安步以当车，无罪以当贵，清静贞正以当虞。---《战国策》`
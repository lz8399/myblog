+++
title= "[Python]Common syntax collections"
date= "2018-12-20T21:07:40+08:00"
categories= ["Python"]
tags= ["Python"]
+++

### Print

Python2

    print("a=%d,b=%d" % (f(x,n), g(x,n)))

Python3

    print('x={:d}, y={:d}'.format(f(x,n), g(x,n)))
    
Python3.6

    print(f'a={f(x,n):d}, b={g(x,n):d}')


How to print like printf in Python3?  
https://stackoverflow.com/questions/19457227/how-to-print-like-printf-in-python3
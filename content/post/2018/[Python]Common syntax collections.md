+++
title= "[Python]Common syntax collections"
date= "2018-12-20T21:07:40+08:00"
categories= ["Python"]
tags= ["Python"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-006.jpg"
+++

How to print like printf in Python3?   
Case-insensitive string comparison  
<!--more-->

### Print

Python2

    print("a=%d,b=%d" % (f(x,n), g(x,n)))

Python3

    print('x={:d}, y={:d}'.format(f(x,n), g(x,n)))
    
Python3.6

    print(f'a={f(x,n):d}, b={g(x,n):d}')


How to print like printf in Python3?  
https://stackoverflow.com/questions/19457227/how-to-print-like-printf-in-python3


### Case-insensitive string comparison

Python2

    string1 = 'Hello'
    string2 = 'hello'

    if string1.lower() == string2.lower():
        print "The strings are the same (case insensitive)"
    else:
        print "The strings are not the same (case insensitive)"
        
Python3

    s = 'ß'
    s.lower() #  'ß'
    s.casefold() # 'ss'
    
{{< alert info >}}
casefold() not only can be used for ASCII strings, but also for Non-ASCII strings, e.g. German script
{{< /alert >}}

How do I do a case-insensitive string comparison?  
https://stackoverflow.com/questions/319426/how-do-i-do-a-case-insensitive-string-comparison/29247821#29247821
---
title: "[CPP]指针数组以及数组初始化"
date: "2016-09-10T16:48:40+08:00"
categories:
- C++
tags:
- Initialize
---

关键字：C++数组初始化

原文：
http://www.cnblogs.com/mywebname/articles/2291540.html


定义：

    int *pia = new int[10]; // array of 10 uninitialized ints

此 new 表达式分配了一个含有 10 个 int 型元素的数组，`并返回指向该数组第一个元素的指针`，此返回值初始化了指针 pia。
在自由存储区中创建的数组对象是`没有名字`的，`只能通过其地址`间接地`访问`堆中的对象。
**注意：C++使用new和delete在堆（自由存储区）上分配和释放动态数组。**

#### 动态数组初始化：
1.`元素只能初始化为元素类型的默认值`，而不能像数组变量一样，用初始化列表为数组元素提供各不相同的初值。
2.对于内置数据类型元素的数组，必须使用()来显示指定程序执行初始化操作，否则程序不执行初始化操作：

    int *pia = new int[10]; // 每个元素都没有初始化
    int *pia2 = new int[10] ();  // 每个元素初始化为0

3.类类型元素的数组，则无论是否使用（），都会自动调用其默认构造函数来初始化：

    string *psa = new string[10];  // 每个元素调用默认构造函数初始化
    string *psa = new string[10]();  // 每个元素调用默认构造函数初始化

##### 动态分配空数组：

    char *cp = new char[0];
之后，可以动态改变cp的维数。

##### 动态释放：

    delete [] pia;

##### 典型使用示例：

    const char *pc = "a very long literal string"; // 处理C风格字符串时使用const指针
    const size_t len = strlen(pc) +1;      // size_t用于数组的大小和下标
    for (size_t ix = 0; ix != 1000000; ++ix) {
        char *pc2 = new char[len]; // pc2指向的存储空间的内容会动态改变，因此不使用const
        strncpy (pc2, pc, len); // 使用strncpy比使用strcpy安全
        // do something;
        delete [] pc2;
    }
参考：http://blog.csdn.net/winjack11/article/category/559603
 
 
### 一、数组定义和初始化
##### 一维数组初始化：
标准方式一： 

    int value[100]; // value[i]的值不定，没有初始化
    
标准方式二： 

    int value[100] = {1,2}; // value[0]和value[1]的值分别为1和2，而没有定义的value[i>1]则初始化为0
    
指针方式： 
    int* value = new int[n]; // 未初始化
    delete []value;  // 一定不能忘了删除数组空间
  
##### 二维数组初始化：
标准方式一： 

    int value[9][9]; // value[i][j]的值不定，没有初始化
    
标准方式二： 

    int value[9][9] = {{1,1},{2}}； //value[0][0,1]和value[1][0]的值初始化，其他初始化为0

指针方式一： 

    int (*value)[n] = new int[m][n];
    delete []value; // n必须为常量，调用直观。未初始化
    
指针方式二： 

    int** value = new int* [m];
    for(i) value[i] = new int[n];
    for(i) delete []value[i];
    delete []value; // 多次析构，存储麻烦，未初始化
        
指针方式三： 

    int * value = new int[3][4]; // 数组的存储是按行存储的
    delete []value; // 一定要进行内存释放，否则会造成内存泄露
  
多维数组初始化(指针方式)：

    int * value = new int[m][3][4]; // 只有第一维可以是变量，其他几维必须都是常量，否则会报错
    delete []value; // 一定要进行内存释放，否则会造成内存泄露
 
`数组初始化的大括号后面要加“;”来表示结束。`


数组访问：
指针形式：如二维数组value[i][j]的访问：

    *(value[i] + j) 或
    (*(value + i))[j]

### 二、数组作为参数传递
 
一维数组参数传递：

    void Func(int *value);
    
或者是

    void Func(int value[]);
  
二维数组传递：
定义是 int **value;的传递

    void Func(int **value);
    
定义是 int (*value)[n] = new int[m][n];的传递

    void func(int (*value)[n]); // sizeof(p)=4,sizeof(*value)=sizeof(int)*n;
 

### 三、数组与指针关系
1、数组名的内涵在于其指代实体是一种数据结构，这种数据结构就是数组；
2、数组名的外延在于其可以转换为指向其指代实体的指针，而且是一个指针常量；
3、指向数组的指针则是另外一种变量类型，（在win32平台下，长度为4），仅仅意味着数组存放地址。
4、`数组名作为函数形参时，在函数体内，其失去了本身的内涵，仅仅只是一个指针，而且在其失去其内涵的同时，它还失去了其常量特性，可以作自增、自减等操作，可以被修改。`

### 四、数组的存储格式
多维数组在内存中存储时是按照最低维连续的格式存储的，如`二维数组{{1,2}，{3,4}}在内存中的位置是这样顺序的“1,3,2,4”`，这跟matlab是有区别的，`matlab是按列进行存储的`。在使用指针进行索引时很有用。

### 五、字符数组
char类型的数组被称作字符数组，通常用来存储字符串。字符串是附加有特殊字符（串尾标志）的字符序列。串终止字符表明字符串已经结束，该字符由转义序列‘\0’定义，有时被称为空字符，占用一个字节，其中8位全为0。这种形式的字符串通常被称为C型字符串，因为以这样的方式定义字符串是在C语言中推出的，在C++一般使用string，而MFC中则定义了CString类。
字符串中每个字符占用一个字节，算上最后的空字符，字符串需要的字节数要比包含的字节数多一个。如：
char movie_star[15] = “Marilyn Monroe”;
这里字符串是14个字符，但是要定义15个字符串的数组。也可以不指定字符数组的个数。如：
char movie_star[] = “Marilyn Monroe”;

### 六、内存泄露
我们定义了一个指针，然后给它赋予了一个地址值，然后又不再使用，但是没有delete，那么当给指针赋予其他的地址值时，原来的内存将无法释放，这就叫做内存泄露。
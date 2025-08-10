+++
date = '2025-08-10T16:18:51+08:00'
draft = false
title = 'c语言 函数'

author = "bigbosscyb"

description = "函数的声明、定义与调用"

categories = [
    "c","c++"
]

tags = [
    "编程基础"
]

+++

在我们学习c语言之初，第一个接触的函数就是：

`printf`函数，他是一个库函数。如果c语言不提供给我们这个库函数，我们就得自己实现。

### **库函数**

我们就把：c语言内置的一系列函数，成为库函数。在这个网站可以查询并学习：[C Library](https://legacy.cplusplus.com/reference/)

### **自定义函数**

库函数不是万能的，他能够解决一些通用场景的编程工作；但是有些时候为完成特定目标的工作，则需要自己编写函数进行实现。

#### 函数的格式

函数返回值类型  函数名 (函数参数类型 函数参数的变量名)

{

​	//函数功能实现部分 一般由一些语句组成

}

请注意，花括号也属于函数的一部分；在花括号中进行功能实现。

#### 函数的声明与定义

**函数声明**：告诉编译器，有这么一个函数：函数名是什么、返回值类型是什么、参数是什么。仅此而已，但是否真的存在这个函数，仅仅有函数声明是决定不了的。

**函数调用**：函数声明一定写在要在函数调用之前，否则编译器会提示找不到这个函数。

**函数定义**：函数的具体功能实现的过程，就是函数定义。

下面以一个add函数的声明、定义、调用来了解上面这些话：

- 调用未声明的函数

```c
int a = 1;
int ret = Add(a, a);
printf("%d + %d = %d \n", a, a, ret);

//编译出错：error: call to undeclared function 'Add'; --意思是：调用了未声明的函数
```



- 仅进行函数声明，未进行函数实现

```c
int Add(int x, int y);

int main(void) {
    int a = 1;
    int ret = Add(a, a);
    printf("%d + %d = %d \n", a, a, ret);
    return 0;
}

//编译出错：Undefined symbols for "_Add"... --意思是：符号Add，未定义
```



- 函数的定义在调用函数之后

```c
int main(void) {
    int a = 1;
    int ret = Add(a, a);
    printf("%d + %d = %d \n", a, a, ret);
    return 0;
}

int Add(int x, int y) {
    return x + y;
};

//编译出错：error: call to undeclared function 'Add'; --意思是：调用了未声明的函数
```

上面演示了一些未遵循函数声明、定义、调用规定的错误情形，下面提供一个无错误的版本：

```c
#include <stdio.h>

int Add(int x, int y);

int main(void) {
    int a = 1;
    int ret = Add(a, a);
    printf("%d + %d = %d \n", a, a, ret);
    return 0;
}

int Add(int x, int y) {
    return x + y;
};

//输出：1 + 1 = 2 
```



### 函数调用时的传参

> **函数的形参是实参值的拷贝，改变形参的值不会对实参产生任何影响。**

举个例子，编写一个函数Swap(int x,int y)，目的是：调用Swap函数，实现两个数的值的交换。

我们很容易写出如下代码：

```c
#include <stdio.h>

void Swap(int x, int y);


int main(void) {
    int a = 1;
    int b = 2;
    printf("a is :%d ;b is: %d \n", a, b);
    Swap(a, b);
    printf("after swap ,a is :%d ;b is: %d \n", a, b);
    return 0;
}

void Swap(int x, int y) {
    printf("in swap function begin,x is :%d ;y is: %d \n", x, y);
    int temp = x;
    x = y;
    y = temp;
    printf("in swap function end,x is :%d ;y is: %d \n", x, y);
}

```

程序输出

```bash
a is :1 ;b is: 2 
in swap function begin,x is :1 ;y is: 2 
in swap function end,x is :2 ;y is: 1 
a is :1 ;b is: 2 
in swap function begin,x is :1 ;y is: 2 
in swap function end,x is :2 ;y is: 1 
after swap ,a is :1 ;b is: 2 
```

为什么a、b没有发生交换？因为形参x,y的值是从实参a，b的复制而来的，x，y有值后就和a，b没有关系了；

可以认为这里隐藏了一个赋值操作，即：

```c
int x =a; int y=b; //如果这样写，更容易弄清 x 与 a；y 与 b的关系了吧？对，他俩没关系。
```

#### 函数参数的传递

- **函数的参数值传递本质就只有一种：那就是值传递。**
- 地址传递，引用传递其实都是值传递。只不过因为根据他们带来的一些效果，人们特别这样称呼他们而已；
  - 就比如：**打篮球，不管你做出什么动作最终效果就是进球。有人将跳起来直接将篮球灌入篮框这一酷炫动作特称为：灌篮！**

我们可以通过断点调试的方式，来了解一下函数参数的值传递：

**请注意，每次调试时变量的地址都有可能不同，我的电脑中变量的地址和你的电脑中变量的地址也几乎不会相同；当你调试时不要对这些差异感到焦虑。**

在调用Swap函数前打上断点，观察到a、b的地址是：

a的地址 `0x000000016b66b4c8` 

b的地址 `0x000000016b66b4c0`

<img src="https://picture.939826.xyz/pictures/img/image-20250810171908194.png" alt="image-20250810171908194" style="zoom:50%;" />

进入到Swap函数中，观察到x、y的地址是：

x的地址 `0x000000016b66b49c`

y的地址 `0x000000016b66b498`

![image-20250810171742922](https://picture.939826.xyz/pictures/img/image-20250810171742922.png)

**可以看到a、b的地址和x、y的地址不相同，那操作x、y影响的也只是x、y所在内存处的内容；与a、b没有任何关系了**。

那么有什么办法，能实现调用Swap后交换a、b的值？方法不止一种，这里介绍一种：

#### 函数参数传递方式之：地址传递

将a、b的地址传递给x、y；通过`*x`和`*y` 操作指定地址上的内存，就等于在操作函数外部的a、b。

```c
#include <stdio.h>

void Swap(int *x, int *y);


int main(void) {
    int a = 1;
    int b = 2;
    printf("a is :%d ;b is: %d \n", a, b);
    Swap(&a, &b);
    printf("after swap ,a is :%d ;b is: %d \n", a, b);
    return 0;
}

void Swap(int *x, int *y) {
    printf("in swap function begin,*x is :%d ;*y is: %d \n", *x, *y);
    int temp = *x;
    *x = *y;
    *y = temp;
    printf("in swap function end,*x is :%d ;*y is: %d \n", *x, *y);
}

```

观察a的地址 `0x000000016cfcb4c8`

观察b的地址 `0x000000016cfcb4c4`

<img src="https://picture.939826.xyz/pictures/img/image-20250810173651743.png" alt="image-20250810173651743" style="zoom:50%;" />

x存储的值是 `0x000000016cfcb4c8` 这个地址指向的就是变量a；y存储的值是 `0x000000016cfcb4c4` 这个地址指向的就是变量b。

最后程序输出：

```bash
a is :1 ;b is: 2 
in swap function begin,*x is :1 ;*y is: 2 
in swap function end,*x is :2 ;*y is: 1 
after swap ,a is :2 ;b is: 1 
```

如此一来，我们通过`*x`和`*y`进行交换变量的操作，就是对a、b本身进行的操作。

总结：

- **函数的形参是实参值的拷贝、改变形参不会对实参产生影响；**
- **在函数内想要操作函数外的变量，可以将外部变量的地址传递进来。**

思考：形参是实参值的拷贝，改变形参不会对实参产生影响；那上面例子中通过`*x=*y;*y=temp;`最终改变了外部变量a、b的值，不就和前面的“不会对实参产生影响”自相矛盾了么？

我的理解：**并没有冲突，因为a、b并不是实参，而&a，&b才是实参**

可以通过下面例子印证：形参的改变，不会影响实参--因为函数调用前后实参&a和&b的值没有变。

```c
#include <stdio.h>

void Swap(int *x, int *y);


int main(void) {
    int a = 1;
    int b = 2;
    printf("a address is :%p ;b address is: %p \n", &a, &b);
    Swap(&a, &b);
    printf("a address is :%p ;b address is: %p \n", &a, &b);
    return 0;
}

//现在函数内部 将x与y的值进行交换 这样x、y的值改变 并不会影响实参 &a 和 &b的值
void Swap(int *x, int *y) {
    printf("in swap function begin,x  is :%d ;y  is: %d \n", *x, *y);
    int *temp = x;
    x = y;
    y = temp;
    printf("in swap function end,x  is :%d ;y  is: %d \n", *x, *y);
}

```

输出：

```c
a address is :0x16f9374c8 ;b address is: 0x16f9374c4 
in swap function begin,x  is :1 ;y  is: 2 
in swap function end,x  is :2 ;y  is: 1 
a address is :0x16f9374c8 ;b address is: 0x16f9374c4 
```


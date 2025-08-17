+++
date = '2025-08-17T07:56:19+08:00'
draft = false
title = 'c语言 数组'

author = "bigbosscyb"

description = "数组初识"

categories = [
    "C","C++"
]

tags = [
    "编程基础"
]

+++

### 数组

- 一群同类型元素组成的集合
- 在内存中连续排列
- 可以使用下标访问数组中的元素

为什么要有数组，假如我需要1000个整数变量，难道需要一个变量一个变量创建么？引进数组来解决这个问题。

### 一维数组创建

一维数组的格式 类型名 数组变量名[元素个数]

```c
int int_arr[4];
// const int pp = 4;
// int intarr[pp];//这种版本高的话(c99以后)才支持
```

### 一维数组初始化

数组初始化：在创建数组时给数组赋值

#### 完全初始化

标准的初始化形式，即使用和声明数组时指定的个数一致的元素给数组初始化

```c
char input[3] = {'a', 'c', 'e'};
// char input2[3]={'a','c','e','d'};//初始化时个数可以短 但不可以长
```

初始化时，元素个数不能比数组长度长；否则编译报错。

#### 不完全初始化

初始化时，元素个数比数组的长度短

```c
char input4[10] = {'a', 'b', 'c'}; //不完全初始化 其余未被初始化的位置会被初始化成默认值
```

数组元素的值的情况：

![image-20250817092222375](https://picture.939826.xyz/pictures/img/image-20250817092222375.png)

前几个元素被正常赋值；后几个元素被系统初始化成该类型的默认值；

**可以利用不完全初始化这一特点，将数组元素全部初始化成默认值，如char类型元素组成的数组，初始化成全0**

```c
char input5[10] = {0}; //通过此特性，将数组初始化成全0
```

![image-20250817092533162](https://picture.939826.xyz/pictures/img/image-20250817092533162.png)



#### 不指定数组大小

当数组创建时不指定长度，则初始化时给定多少个元素，那么数组的长度就是多长。

```c
char input3[] = {'a', 'l', 'i'};
```

![image-20250817092744122](https://picture.939826.xyz/pictures/img/image-20250817092744122.png)

### 字符数组与字符串

下面这两种形式数组的区别：

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char input3[] = {'a', 'l', 'i'}; //不指定数组大小的初始化
    char str[] = "ali";//使用字符串字面量初始化字符数组
    //它与input3有什么区别?
    //空间不同：字符串自带一个\0字符；所以str在空间占用上比input3大
    //strlen函数求字符串长度结果不同：因为strlen函数遇到str数组中的\0字符会结束 然后返回除\0外还有多少个字符
    //而strlen处理字符数组input3时，什么时候遇到\0字符是未知的，所以得到的结果是随机的
    size_t size_str = sizeof(str);
    size_t size_input3 = sizeof(input3);
    printf("str size is:%d,input3 size is:%d \n", size_str, size_input3);
    size_t len_str = strlen(str);
    size_t len_input3 = strlen(input3);
    printf("str strlen is:%d,input3 str len is:%d \n", len_str, len_input3);
    return 0;
}
```

输出：

```shell
str size is:4,input3 size is:3 
str strlen is:3,input3 str len is:9 //input3由于没有字符串结束符\0，所以strlen结果是随机的
```

![image-20250817094121833](https://picture.939826.xyz/pictures/img/image-20250817094121833.png)

- 所占据的空间不同，使用sizeof操作符，求两个数组的大小，显然后者的长度要大
- strlen函数求字符串长度，结果不同：strlen函数从第一个字符开始，看到str数组中的\0字符返回，除\0外共多少个字符个数，就是字符串的长度；对于字符数组input3来说，由于其中并没有包含\0字符，所以其结果是随机的未知的

**后来有人告诉我们，strlen这样理解：就好比你朗读课文时句号你不会读出来一样。在计算字符串长度时strlen只把`\0`当标记，不会把它统计入长度的**

### 一维数组的使用

- 按索引访问元素：数组名[索引值] 就可以访问到数组中的指定位置的元素
- 数组元素个数计算：用sizeof求数组总共占用的空间、用sizeof(arr[0])求数组中一个元素占用的空间、最后用总空间除以单个元素的空间得到数组元素个数。

如何修改数组中某个位置的元素的值

```
char input[3] = {'a', 'c', 'e'};
size_t size = sizeof(input); //sizeof可以计算出数组所占空间大小
size_t size_item = sizeof(input[0]); //计算数组中第一个元素所占空间大小
size_t count = size / size_item;
printf("数组修改前：\n");

for (size_t i = 0; i < count; i++) {
    printf("index of %d,value is %c \n", i, input[i]);
    char item = input[i];
    item = '\0';
}

printf("数组修改后：\n");
for (size_t i = 0; i < count; i++) {
    printf("index of %d,value is %c \n", i, input[i]);
}
```

输出：

```shell
数组修改前：
index of 0,value is a 
index of 1,value is c 
index of 2,value is e 
数组修改后：
index of 0,value is a 
index of 1,value is c 
index of 2,value is e 
```

可以看出上面的修改数组的方式是错误❌的；item在初始化后便和数组元素没有关系了(下图从内存地址可以看出)；所以修改item并不会对数组中的元素造成任何影响。

![image-20250817100133328](https://picture.939826.xyz/pictures/img/image-20250817100133328.png)

![image-20250817100229058](https://picture.939826.xyz/pictures/img/image-20250817100229058.png)

所以正确的修改数组元素的方式应该是：要么**使用指针**，要么**直接使用下标**进行修改。

```c
char input[3] = {'a', 'c', 'e'};
size_t size = sizeof(input); //sizeof可以计算出数组所占空间大小
size_t size_item = sizeof(input[0]); //计算数组中第一个元素所占空间大小
size_t count = size / size_item;
printf("数组修改前：\n");
for (size_t i = 0; i < count; i++) {
    printf("index of %d,value is %c \n", i, input[i]);
}
printf("请输入三个字符串，输入完成后按下回车键确认\n");
for (size_t i = 0; i < count; i++) {
    scanf("%c", &input[i]);
}

printf("数组修改后：\n");
for (size_t i = 0; i < count; i++) {
    printf("index of %d,value is %c \n", i, input[i]);
}
```

输出

```shell
数组修改前：
index of 0,value is a 
index of 1,value is c 
index of 2,value is e 
请输入三个字符串，输入完成后按下回车键确认
hhh
数组修改后：
index of 0,value is h 
index of 1,value is h 
index of 2,value is h
```

- 使数组不可被修改

在数组声明时，前面加上const，那么数组中的每一个元素就变成了只读量，只能访问不能修改。

```c
const int intarr[3] = {'a', 'c', 'e'};
intarr[0] = 1;
```

编译错误：

```shell
/Users/a77/Code/clangbasedemo/main.c:6:15: error: cannot assign to variable 'intarr' with const-qualified type 'const int[3]'
    intarr[0] = 1;
    ~~~~~~~~~ ^
```

由此，我们联想到 **在一个函数中，若不希望形参被修改，可以给形参加上const修饰，起到保护形参的作用**。

- 一维数组在内存中的存储

```
int intarr[3] = {'a', 'c', 'e'};
size_t size = sizeof(intarr); //sizeof可以计算出数组所占空间大小
size_t size_item = sizeof(intarr[0]); //计算数组中第一个元素所占空间大小
size_t count = size / size_item;
for (size_t i = 0; i < count; i++) {
    printf("index of %d,address is %p \n", i, &intarr[i]);
}
```

输出

```
index of 0,address is 0x16d8534b8 
index of 1,address is 0x16d8534bc 
index of 2,address is 0x16d8534c0
```

a0和a1相差4；为什么？因为一个int值在内存中占4个字节。（**回忆旧知识：内存中最小单位是字节，故地址与地址之间差值最小是1字节**）

- 数组越界访问

什么是越界访问：下标是不在数组元素范围内。如：

```c
int arr[3]={1,2,3}; int item= arr[99];
```

数组越界访问，编译器是允许的；因为编译器足够信任程序员，认为程序员不会做出越界访问这种事情。另外不进行这种检查，还可以提高运行效率。

### 二维数组

比一维数组多了一个[]；

```c
//格式 类型名 数组名[m][n]
char list[3][4];
```

从左往右 list先与[3]结合，所以list是一个由三个元素组成的数组；然后去掉list[3]剩下的就是元素类型；可以看到组成list[3]的每个元素都是一个数组。这个数组长度是4。

**还可以将二维数组看成3行4列的网格**

### 二维数组初始化

#### 完全初始化

3*4=12，所以共需要12个数来初始化二维数组。

```c
char list[3][4] = {'h', 'u', 'g', 'o', 'l', 'o', 'v', 'e', 'p', 'i', 'n', 'g'};
```

来看数组的情况：

![image-20250817105544318](https://picture.939826.xyz/pictures/img/image-20250817105544318.png)

#### 不完全初始化

和一维数组一样，只要我们给定的元素个数不足以填充数组长度；那么这种初始化方式就称为不完全初始化

```c
char list1[3][4] = {'h', 'u'};
```

看数组内元素的情况：

![image-20250817105832604](https://picture.939826.xyz/pictures/img/image-20250817105832604.png)

与一维数组处理一致，未赋值的元素，会被默认初始化成该元素类型的默认值；

#### 使用一维数组初始化

二维数组中，是由几个一维数组组成；所以在此例中使用三个长度为4的一维数组，即可完成初始化

```c
char list2[3][4] = {{'h', 'u', 'g', 'o'}, {'l', 'o', 'v', 'e'}, {'p', 'i', 'n', 'g'}};
```

也可以这样

```c
char list3[3][4] = {{'h'}, {'l'}};
```

### 二维数组在内存中的分布

```c
char list[3][4] = {'h', 'u', 'g', 'o', 'l', 'o', 'v', 'e', 'p', 'i', 'n', 'g'};
size_t row_size = sizeof(list) / sizeof(list[0]);
size_t col_size = sizeof(list[0]) / sizeof(list[0][0]);
for (size_t i = 0; i < row_size; i++) {
    for (size_t j = 0; j < col_size; j++) {
        printf("position is :(%d,%d),value is %c,address is %p\n", i, j, list[i][j], &list[i][j]);
    }
}
```

输出

```shell
position is :(0,0),value is h,address is 0x16f2234b8
position is :(0,1),value is u,address is 0x16f2234b9
position is :(0,2),value is g,address is 0x16f2234ba
position is :(0,3),value is o,address is 0x16f2234bb
position is :(1,0),value is l,address is 0x16f2234bc
position is :(1,1),value is o,address is 0x16f2234bd
position is :(1,2),value is v,address is 0x16f2234be
position is :(1,3),value is e,address is 0x16f2234bf
position is :(2,0),value is p,address is 0x16f2234c0
position is :(2,1),value is i,address is 0x16f2234c1
position is :(2,2),value is n,address is 0x16f2234c2
position is :(2,3),value is g,address is 0x16f2234c3
```

可以看到地址是连续的，**所以无论是几维数组，在内存中元素都是连续存储的。数组的维度只是我们逻辑上的，计算机上一直线性顺序存储。**


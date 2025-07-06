+++
date = '2025-07-06T23:38:10+08:00'
draft = false
title = '使用vscode开发c/c++'

author = "bigbosscyb"

description = "Vscode 配置c/c++开发环境"
categories = [
    "vscode","c","c++"
]
tags = [
    "实用工具",
]

+++

### 整体流程

- 安装vscode
- 下载mingw
- 配置mingw
- 下载c/c++插件
- 使用vscode编写c/c++代码
  - 设置编译选项
  - 配置生成任务
  - 启动项配置

### VScode的安装

官网：[Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)

非官方加速站点：

### Mingw的安装

官网：[x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains targetting Win64/Personal Builds/mingw-builds/8.1.0/threads-win32/seh/x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z/download)

非官方加速站点：[mingw64-x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z](https://gitee.com/link?target=https%3A%2F%2Fmbd.pub%2Fo%2Fbread%2FZpyUkp9q)

从网上找到了一个文章介绍mingw各个版本的区别

![img](https://i-blog.csdnimg.cn/blog_migrate/86edc1025f3fe2b4d0423e952e4a30a7.png#pic_center)

参考：[【c/cpp 开发工具】MingGW 各版本区别及安装说明]([【c/cpp 开发工具】MingGW 各版本区别及安装说明_mingw sjlj seh-CSDN博客](https://blog.csdn.net/qq_29856169/article/details/119380663))

### 配置mingw

- 解压：上一步下载好的压缩文件 建议直接将解压后的Mingw64文件夹直接剪切到C盘或者其它盘的根目录
- 设置环境变量：将mingw的bin目录添加到环境变量中

![image-20250707002700359](https://picture.939826.xyz/pictures/img/image-20250707002700359.png)

![image-20250707002832665](https://picture.939826.xyz/pictures/img/image-20250707002832665.png)

打开cmd窗口，输入gcc --version 输出类似如下信息，则代表mingw配置完成

![image-20250707003011994](https://picture.939826.xyz/pictures/img/image-20250707003011994.png)

### c/c++插件

在Vscode的扩展中搜索c/c++，点击安装即可

![image-20250707003214208](https://picture.939826.xyz/pictures/img/image-20250707003214208.png)

### 使用vscode编写c/c++代码

- 本地磁盘创建一个用于存放c/c++代码的目录

![image-20250707003459777](https://picture.939826.xyz/pictures/img/image-20250707003459777.png)

- 使用vscode打开某个代码目录

![image-20250707003721349](https://picture.939826.xyz/pictures/img/image-20250707003721349.png)

#### 设置编译选项

Ctrl+Shift+P 打开命令面板

![image-20250707004119434](https://picture.939826.xyz/pictures/img/image-20250707004119434.png)

![image-20250707004147751](https://picture.939826.xyz/pictures/img/image-20250707004147751.png)

![image-20250707004303057](https://picture.939826.xyz/pictures/img/image-20250707004303057.png)

![image-20250707004424782](https://picture.939826.xyz/pictures/img/image-20250707004424782.png)

**注意：我这里默认的编译器路径是cl.exe，因为我安装了VS 2022，这个是vs的编译器，我们不使用这个路径！！！**

![image-20250707004458497](https://picture.939826.xyz/pictures/img/image-20250707004458497.png)

配置完成后 .vscode文件夹下的配置如下：

![image-20250707004552305](https://picture.939826.xyz/pictures/img/image-20250707004552305.png)

#### 创建执行任务

设置完编译器之后，如何来编译c代码呢？需要创建执行任务，让Vscode知道如何执行编译(构建)任务。

- 在顶部"终端"菜单下拉选项中选择，"配置任务"

![image-20250707005251351](https://picture.939826.xyz/pictures/img/image-20250707005251351.png)

- 在新弹出的菜单中选择gcc编译器，生成配置文件

![image-20250707005311024](https://picture.939826.xyz/pictures/img/image-20250707005311024.png)

- 对tasks.json的解读

![image-20250707005611839](https://picture.939826.xyz/pictures/img/image-20250707005611839.png)

#### 编译

- 想要编译哪个文件就打开哪个文件
- 在顶部"终端"菜单的下拉选项中选择"运行生成任务"

![image-20250707005947596](https://picture.939826.xyz/pictures/img/image-20250707005947596.png)

![image-20250707010056956](https://picture.939826.xyz/pictures/img/image-20250707010056956.png)

#### 执行

- 在顶部"查看"菜单的下拉选项中选择"终端"选项

![image-20250707010311931](https://picture.939826.xyz/pictures/img/image-20250707010311931.png)

- 在下方新打开的终端工具中，输入./test.exe即可运行编译生成的程序

![image-20250707010438833](https://picture.939826.xyz/pictures/img/image-20250707010438833.png)

### 还想写其它代码

#### 在本目录中新增了一个.c文件



#### 在一个新的目录中编写代码



### 有多个.c文件如何编译

有多个.c文件，我们可以成这个目录连同所有的文件为"工程"

#### 改造task.json



### 如何编译c++代码



#### 配置g++.exe为编译器



#### 配置c++源文件的任务信息



#### 编译c++代码

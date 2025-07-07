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

![mingw各个版本qu'bie](https://picture.939826.xyz/pictures/img/86edc1025f3fe2b4d0423e952e4a30a7.png)

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

例如又新增了一个test2.c文件来跑另外一个demo

- 要编译哪个文件就选中这个文件

![image-20250707081811152](https://picture.939826.xyz/pictures/img/image-20250707081811152.png)

- Ctrl+Shift+B 运行生成任务
- 在终端工具中 输入./test2.exe即可运行

#### 在一个新的目录中编写代码

如下图新增了一个seconddemo文件夹，来写代码；如何快速完成?

![image-20250707082153600](https://picture.939826.xyz/pictures/img/image-20250707082153600.png)

- vscode打开文件夹
- 将之前文件夹的.vscode文件夹拷贝到这个文件夹下
- 新建.c文件编写代码
- 终端-->执行生成任务 完成编译

**总之就是我们不必再从头进行环境配置！！！**

### 有多个.c文件如何编译

有多个.c文件，在hello.c文件中调用了util.c中的sub函数

![image-20250707231956132](https://picture.939826.xyz/pictures/img/image-20250707231956132.png)

此时进行代码生成，会提示如下错误：

``` bash
cmd /c chcp 65001>nul && D:/mingw64/bin/gcc.exe -fdiagnostics-color=always -g E:\cppdemos\seconddemo\hello.c -o E:\cppdemos\seconddemo\hello.exe
D:/mingw64/bin/../lib/gcc/x86_64-w64-mingw32/8.5.0/../../../../x86_64-w64-mingw32/bin/ld.exe: C:\Users\48723\AppData\Local\Temp\ccGODLI4.o: in function `main':
E:/cppdemos/seconddemo/hello.c:9: undefined reference to `sub'
collect2.exe: error: ld returned 1 exit status
```

我们如何能运行生成任务时，能将所有的C代码都进行编译、最后输出一个文件目.exe的可执行文件?

答案是：修改tasks.json文件

#### 改造tasks.json

- 修改args节点，-g参数：让编译器编译目录下所有的.c文件；
- [可选]修改args节点，-o参数：让生成的输出文件，文件名是以工作目录文件夹名命名的exe文件；

``` json
{
	"version": "2.0.0",
	"tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: gcc.exe 生成活动文件",
            "command": "D:/mingw64/bin/gcc.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${workspaceFolder}\\*.c",
                "-o",
                "${workspaceFolder}\\${workspaceFolderBasename}.exe"
            ],
            "options": {
                "cwd": "D:/mingw64/bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build",
            "detail": "编译器: D:/mingw64/bin/gcc.exe"
        }
    ]
}
```

![image-20250707232813419](https://picture.939826.xyz/pictures/img/image-20250707232813419.png)

这样就可以正常编译和运行程序了。

### 如何编译c++代码

- 新增一个.cpp结尾的文件
- 同上面.c文件的配置类似，需要设置编译选项、创建执行任务

#### 配置g++.exe为编译器

#### 配置c++源文件的任务信息

#### 编译c++代码

以上步骤直接放到下面录屏中：

![cpp配置v2](https://picture.939826.xyz/pictures/img/cpp配置v2.gif)

注意两点：

- 配置g++.exe为编译器时，需要添加配置
- 配置任务时，需要打开.cpp文件后，点击"终端"-->"配置任务"

### 如何调试代码

以上只介绍了，如何编译代码和运行程序；在VsCode中想要调试，需要创建launch.json

#### 创建launch.json

点击左侧"调试"菜单，点击"创建launch.json文件"，在弹出的菜单中，选择"C++(GBD/LLDB)"

![image-20250707234910293](https://picture.939826.xyz/pictures/img/image-20250707234910293.png)

点击添加配置按钮，在弹出菜单中选择"c/c++ (gdb) 启动"

![image-20250707235235809](https://picture.939826.xyz/pictures/img/image-20250707235235809.png)

![image-20250707235652667](https://picture.939826.xyz/pictures/img/image-20250707235652667.png)

修改完成后launch.json内容如下：

```json
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "(gdb) 启动",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}\\${workspaceFolderBasename}.exe",//这里修改后保持和tasks.json中的-o参数一致
      "args": [],
      "stopAtEntry": false,
      "cwd": "${fileDirname}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "gdb",
      "miDebuggerPath": "D:\\mingw64\\bin\\gdb.exe",//这里修改为你的电脑上gdb.exe路径
      "setupCommands": [
        {
          "description": "为 gdb 启用整齐打印",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        },
        {
          "description": "将反汇编风格设置为 Intel",
          "text": "-gdb-set disassembly-flavor intel",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```

#### 开始调试

- 介绍一些快捷键
  - F5 启动调试
  - F9 设置断点
  - Ctrl+Shift+B 编译代码

![image-20250708000521706](https://picture.939826.xyz/pictures/img/image-20250708000521706.png)

以上便是VsCode进行C/C++环境配置的全部内容。

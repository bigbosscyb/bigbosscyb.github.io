+++
date = '2025-06-15T23:52:17+08:00'
draft = false
title = 'python 初识python'

author = "bigbosscyb"

description = "跟着官方文档学python"
categories = [
    "python",
]
tags = [
    "python基础",
]

+++

### 为什么"又"开始学python了

最近因为在git上学到了一个python写的小爬虫项目，这个小项目里面有一个requirements.txt文件和main.py文件；我刚下载下来的时候竟然跑不起来，由于之前我在[简介 - Python教程 - 廖雪峰的官方网站](https://liaoxuefeng.com/books/python/introduction/index.html)学过一遍python，但也因为长时间没有玩过Python了，这个十分简单的小项目我使用Pycharm竟然没有跑起来，一些死去的回忆开始攻击自己的大脑。pip包管理、模块引入、入口点、解释器、虚拟环境这些词儿在我脑海里打转，似乎我可以抓住但又抓不住。

### 为什么决定记录博客了

我开始思考为什么会忘记？我想一是因为学完没有持续使用，保持热度；二是因为没有做好笔记。在全网搜了一下，最终让代码跑起来之后；我决定再次系统地把python的知识点快速过一遍，我要达到的最终效果就是，能适应日常需求，如：爬虫、文件下载、IO操作、http服务、socket通信等。

### 为什么跟着官方文档来学

从哪里开始学？之前从廖雪峰老师的python教程中学过一遍，这次我想换个口味从别的地方学习，首先我想到的是看视频，然后我就从BliBli上找到播放量最高的几个教程迅速看了一下大纲和他们的几节课程；是挺好的，该有的知识点都提到了，还有的还带着实战。但对于我来说我觉得不太合适，因为：我觉的这些视频讲的节奏太慢！！！我的目的是快速将知识点都过一遍。所以最终我选择了每一个下载python安装包的官方网站中的文档。我看了一下他的大纲：

![image-20250616001721062](C:\Users\48723\AppData\Roaming\Typora\typora-user-images\image-20250616001721062.png)

很精炼、很符合我的口味。

那就跟着官方文档:[3.13.5 Documentation](https://docs.python.org/zh-cn/3/index.html)，开始python学习之旅吧。

### 一口气看完前三节

#### 安装python解释器

就在这里：[Welcome to Python.org](https://www.python.org/)下载python安装包；安装教程在往上一搜一大把，这里没必要再介绍。

#### 安装pycharm编辑器

可以使用vscode，但我喜欢Jetbrains家族的IDE，所以我选择下载了pycharm。

![image-20250616002431297](C:\Users\48723\AppData\Roaming\Typora\typora-user-images\image-20250616002431297.png)

#### 跟着官方文档开始吧

第一节大概讲了一下Python的好处；"**简洁**"、"**轻量**"这些词儿希望吸引到学习的人。

第二节大概讲了一下Python解释器；我姑且把Python解释器狭隘地理解为：命令行吧。

第三节开始初探Python世界；把控制台输出、变量、数值计算、文本操作、列表操作都大致带着学习的人过了一遍，让你领略一下什么叫"**人生苦短，我用Python**"，为什么这样讲？我觉得大家可以对比自己掌握的其它编程语言，看看想要实现列表的拼接、切片、列表的打印这些简单动作，比Python简单还是复杂。

对于第三节，我是对照着案例，把每一种操作几乎都敲了一遍代码：

```python
# 这是一个注释
# 纯数字计算
print('初识python中的数字')
5 + 5  # 这条语句虽然没有什么意义但是也是一条合法语句 也可以看出python不需要分号
# 变量赋值 在python中变量赋值就相当于变量定义了
a = 5 + 6  # 加法
# 如果出现了一个变量在使用前没有赋值过 就认为这个变量是未定义的 这是不合法的使用方式
# print('n is undefined',n) #这里变量n未定义
print(r'print函数自带一个\n换行符', r'print函数还会在多个参数之间加入一个空格');
print('5+6=', a)  # print函数将参数值直接输出 print接收多个参数
# 在Python中字符串常量可以用三种表示
# 第一种：'内容'
# 第二种："内容"
# 第三种：'''多行内容'''
b = 5 * 6  # 乘法
print('5*6=', b)
c = 3 - 2  # 减法
print('3-2=', c)
d = 12 / 5  # 除法
print('12/5=', d)
e = 12 // 5  # 地板除 整数地板除必然是整数
print('12//5=', e)
f = 12 % 5  # 求余数
print('12%5=', f)
g = 2 ** 5  # 计算乘方
print('2**5=', g)

# 文本
print('初识python中的文本')
'hello'
"hello"
'''h
e
l
l
o
'''
s = 'first line\nsecond line.'  # 单引号表示字符串 \n是转义字符
print(s)
print(r'使用r表示文本原样输出:first line\nsecond line')  # 使用r则表示里面的转义字符也只是普通字符
print('字符串*数值n可以让字符串重复次,如：ikun*3-->', 'ikun' * 3)  # 重复字符串
print('字符串其实是字符组成的数组,那么可以像数组那样使用下标访问某个位置的字符串，如:\"nihao\"[2]->', 'nihao'[2])  # 索引操作
print('字符串下标还可以倒着来,如\"nihao\"[-1]直接可以取到最后一个字符->', 'nihao'[-1])
print('字符串切片,即：可以从指定的区间(不包含结束位置)取出一段字符串,如：\"nihao\"[1:-2]->', 'nihao'[1:-2])  # 切片操作
print('字符串切片,只指定开始,如：\"nihao\"[1:]->', 'nihao'[1:])  # 从指定位置切片到末尾
print('字符串切片,只指定结束,如：\"nihao\"[:1]->', 'nihao'[:1])  # 从头切到指定位置之前
print('字符串切片,这样写再拼接起来正好是自己本身,\"nihao\"[:1]+\"nihao\"[1:]->', 'nihao'[:1] + 'nihao'[1:])
print('python中字符串不能修改,如：\"nihao\"[0]=\"l\",会报错')
# 'nihao'[0] = 'l'
print('但是可以使用拼接,\"l\"+\"nihao\"[1:]->', 'l' + 'nihao'[1:])

# 列表
print('初识python中的列表')
pylist = [1, 2, 3, 4, 5]
print('打印列表元素->', pylist)  # 打印列表元素
print('切片时，既不写开始也不写结束 那就是全切', pylist[:])  # 既不写开始也不写结束 那就是全切
print('列表支持索引,如：pylist[-1]->', pylist[-1])
print('列表哦支持切片,如：pylist[-3:]->', pylist[-3:])
pylist[0] = 999
print('列表允许修改某个元素的值,如：pylist[0]=99->', pylist)
pylist = pylist + [7, 8, 9]
print('合并列表,如：pylist+[7,8,9]->', pylist)
pylist.append(10)
print('向列表某位添加元素,如：pylist.append(10)', pylist)
copyList = pylist
print('直接将列表赋值给一个新变量copyList,那么这时copyList和pylist都指向的是同一个东西')
copyList.append(1234)
print('修改copyList，那么pylist也会收到影响，如：copyList.append(1234)')
print('copyList->', copyList)
print('pylist->', pylist)
newList = pylist[:]
print('切片赋值给一个新变量,newList=pylist[:],那newList就是->', newList)
print('这时候再操作newList就和pylist无关了,如：newList[0]=1111')
newList[0] = 11111
print(newList)
print(pylist)
pylist[3:6] = [999, 888]
print('为切片赋值，可以改变列表的大小，甚至清空列表,如：pylist[3:6]=[999,888]->', pylist)
pylist[:] = []
print('直接给切片赋值一个空列表，可以清空列表,如：pylist[:]=[]->', pylist)
```

下面是输出：

```bash
初识python中的数字
print函数自带一个\n换行符 print函数还会在多个参数之间加入一个空格
5+6= 11
5*6= 30
3-2= 1
12/5= 2.4
12//5= 2
12%5= 2
2**5= 32
初识python中的文本
first line
second line.
使用r表示文本原样输出:first line\nsecond line
字符串*数值n可以让字符串重复次,如：ikun*3--> ikunikunikun
字符串其实是字符组成的数组,那么可以像数组那样使用下标访问某个位置的字符串，如:"nihao"[2]-> h
字符串下标还可以倒着来,如"nihao"[-1]直接可以取到最后一个字符-> o
字符串切片,即：可以从指定的区间(不包含结束位置)取出一段字符串,如："nihao"[1:-2]-> ih
字符串切片,只指定开始,如："nihao"[1:]-> ihao
字符串切片,只指定结束,如："nihao"[:1]-> n
字符串切片,这样写再拼接起来正好是自己本身,"nihao"[:1]+"nihao"[1:]-> nihao
python中字符串不能修改,如："nihao"[0]="l",会报错
但是可以使用拼接,"l"+"nihao"[1:]-> lihao
初识python中的列表
打印列表元素-> [1, 2, 3, 4, 5]
切片时，既不写开始也不写结束 那就是全切 [1, 2, 3, 4, 5]
列表支持索引,如：pylist[-1]-> 5
列表哦支持切片,如：pylist[-3:]-> [3, 4, 5]
列表允许修改某个元素的值,如：pylist[0]=99-> [999, 2, 3, 4, 5]
合并列表,如：pylist+[7,8,9]-> [999, 2, 3, 4, 5, 7, 8, 9]
向列表某位添加元素,如：pylist.append(10) [999, 2, 3, 4, 5, 7, 8, 9, 10]
直接将列表赋值给一个新变量copyList,那么这时copyList和pylist都指向的是同一个东西
修改copyList，那么pylist也会收到影响，如：copyList.append(1234)
copyList-> [999, 2, 3, 4, 5, 7, 8, 9, 10, 1234]
pylist-> [999, 2, 3, 4, 5, 7, 8, 9, 10, 1234]
切片赋值给一个新变量,newList=pylist[:],那newList就是-> [999, 2, 3, 4, 5, 7, 8, 9, 10, 1234]
这时候再操作newList就和pylist无关了,如：newList[0]=1111
[11111, 2, 3, 4, 5, 7, 8, 9, 10, 1234]
[999, 2, 3, 4, 5, 7, 8, 9, 10, 1234]
为切片赋值，可以改变列表的大小，甚至清空列表,如：pylist[3:6]=[999,888]-> [999, 2, 3, 999, 888, 8, 9, 10, 1234]
直接给切片赋值一个空列表，可以清空列表,如：pylist[:]=[]-> []
```

可以看到，对于一个简单的练习Demo，可以连入口都不用写；直接写你想写的，这种低束缚，对于我只是想写一些小项目的人来说，确实很有吸引力。今天先到这里，Night！

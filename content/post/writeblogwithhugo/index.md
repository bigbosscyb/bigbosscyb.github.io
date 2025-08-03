+++
date = '2025-06-14T14:14:01+08:00'
draft = false
title = '使用hugo写博客'

author = "bigbosscyb"

description = "Guide how to use Hugo"
categories = [
    "hugo","github pages"
]
tags = [
    "实用工具",
]

+++

### 介绍Hugo

基于GO语言编写的**静态网站生成器**，能够托管在Github Pages上，可以集成git discuss的评论系统，无需数据库，不需要写代码，就可以快速帮助你搭建一个属于自己的博客网站。

### 下载Hugo

- 方式一：从github下载release版
- 方式二：如果访问github速度太慢，可以在浏览器搜索Hugo下载

总之，下载的是这个压缩包：

<img src="https://picture.939826.xyz/pictures/img/image-20250614142959933.png" alt="image-20250614142959933" style="zoom:55%;" />

### 使用Hugo

#### 创建站点

我们主要是在使用hugo.exe来进行一系列操作的，这里建议新开一个要写博客的目录，（**由于我们没有把hugo.exe配置到环境变量中**）接着把hugo.exe拷贝到那个目录。

<img src="https://picture.939826.xyz/pictures/img/image-20250614143436876.png" alt="image-20250614143436876" style="zoom:80%;" />

然后使用 hugo new site 命令创建一个博客站点，如下：

```shell
hugo new site hugo-test
```

命令执行成功后，会生成一个hugo-test的目录，那么一个本地博客站点就已经搭建好了。

<img src="https://picture.939826.xyz/pictures/img/image-20250614144054698.png" alt="image-20250614144054698" style="zoom: 80%;" />

可以观察到目录里面的内容

<img src="https://picture.939826.xyz/pictures/img/image-20250614144135229.png" alt="image-20250614144135229" style="zoom:90%;" />

#### 浏览博客站点

虽然我们还没有写一篇博客，但我们已经可以浏览这个站点了；这里我们还是把hugo.exe往hugo-test目录下拷贝，以便于能继续使用hugo命令

```shell
hugo server -D #-D中的D是buildDrafts的简写
```

<img src="https://picture.939826.xyz/pictures/img/image-20250614144546898.png" alt="image-20250614144546898" style="zoom:60%;" />

键盘按住CTRL键，然后鼠标点击控制台中的链接，即可在浏览器中打开这个站点：

<img src="https://picture.939826.xyz/pictures/img/image-20250614144412454.png" alt="image-20250614144412454" style="zoom:125%;" />

#### 配置主题

主题文件夹其实类似一个站点模板，这里将主题文件夹下的配置文件hugo.yaml及examplesite目录下的内容拷贝到我们的站点下，从而达到快速应用主题的目的。

1. 下载主题：点击链接[hugo stack]([Hugo Themes](https://themes.gohugo.io/))，找到stack主题下载后解压缩：然后将主题文件夹复制到之前创建的hugo-test站点目录的themes文件夹下，并将主题文件改名，最后效果如下：

   <img src="https://picture.939826.xyz/pictures/img/image-20250614153314011.png" alt="image-20250614153314011" style="zoom:96%;" />

2. 把主题文件夹hugo-theme-stack中exampleSite\content\post路径下的rich-content目录删掉，然后把hugo-theme-stack\exampleSite\下面的content目录和hugo.yaml复制到hugo-test站点目录下，最后还要把hugo-test目录下的hugo.toml文件删掉

<img src="https://picture.939826.xyz/pictures/img/image-20250614153603838.png" alt="image-20250614153603838" style="zoom:82%;" />

<img src="https://picture.939826.xyz/pictures/img/image-20250614153636596.png" alt="image-20250614153636596" style="zoom:90%;" />

3. 打开hugo.yaml，确认里面的theme节点的配置使用的站点目录下themes目录里面的主题文件夹名即：

<img src="https://picture.939826.xyz/pictures/img/image-20250614154248291.png" alt="image-20250614154248291" style="zoom: 64%;" />

4. 重新启动站点服务，查看效果：

```shell
hugo server -D
```

![image-20250614155512875](https://picture.939826.xyz/pictures/img/image-20250614155512875.png)

### github部署

这里我们介绍如何使用github管理hugo站点并且自动化发布站点应用

#### 创建github pages类型的仓库

创建一个以{github用户名}.github.io命名的仓库，就会被github认为你创建了一个静态页面网站；github会以https://仓库名 作为静态网站的地址，仓库创建后稍后可访问。

![image-20250614164036299](https://picture.939826.xyz/pictures/img/image-20250614164036299.png)

#### 上传hugo站点文件到仓库

1. 在本地hugo-test目录下，创建一个.gitignore文件，添加以下内容：

```shell
# 自动生成的文件
public
resources
.hugo_build.lock

# hugo命令
hugo.exe
```

通过以上操作，将站点自动生成的文件如：public发布目录、.hugo_build.lock自动生成文件 等进行了过滤；这些文件不提交至远程仓库

2. 创建本地仓库，然后将本地仓库上传至远程仓库

```shell
git init
git add .
git commit -m "first commit"
git remote add origin {你的github仓库地址}
git push -u origin mater
```

#### 创建github workflows

![image-20250614164928986](https://picture.939826.xyz/pictures/img/image-20250614164928986.png)

在远程仓库使用Github Actions创建一个工作流，来帮助我们自动发布编写的博客：当我们在本地写好一篇博客，推送至远程时，触发工作流最后是实现自动部署。这里我的workflows目录下，需要填写的内容摘抄自另外一个github博主【[**.github/workflows/deploy.yml**]([byjrk.github.io/.github/workflows/deploy.yml at master · BYJRK/byjrk.github.io](https://github.com/BYJRK/byjrk.github.io/blob/master/.github/workflows/deploy.yml))】。

```yaml
name: Deploy to Github Pages

on:
    push:
        branches: [master]
    pull_request:
        branches: [master]

jobs:
    build:
        runs-on: ubuntu-latest

        permissions:
            # Give the default GITHUB_TOKEN write permission to commit and push the
            # added or changed files to the repository.
            contents: write

        steps:
            - uses: actions/checkout@v4
              with:
                  fetch-depth: 0

            - name: Cache Hugo resources
              uses: actions/cache@v4
              env:
                  cache-name: cache-hugo-resources
              with:
                  path: resources
                  key: ${{ env.cache-name }}

            - uses: actions/setup-go@v5
              with:
                  go-version: "1.24.0"
            - run: go version

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: "0.139.4"
                  extended: true

            - name: Build
              run: hugo --minify --gc

            - name: Deploy 🚀
              uses: JamesIves/github-pages-deploy-action@v4
              with:
                  branch: gh-pages
                  folder: public
                  clean: true
                  single-commit: true
```

上面的工作流配置，可直接拷贝。大致效果就是，实际部署时将文件发布到了另外一个[gh-pages]分支上。

#### 在本地新增一篇文章上传测试自动部署效果

- 创建一篇新的博客

```
hugo new content post/testblog/index.md
```

使用编辑器打开该目录下的index.md文件，编辑好博客内容后。

- 本地启动查看效果

```
hugo server -D
```

- 推送至远程观察工作流

```
git add.
git commit -m "post blog"
git push -u origin master
```

![image-20250614170926014](https://picture.939826.xyz/pictures/img/image-20250614170926014.png)

### 添加评论系统

hugo默认集成的是disqus评论系统，但是这里我推荐使用的是giscus评论系统：因为它简单、容易继承。

#### 如何引入[giscus]([giscus](https://giscus.app/zh-CN))

![image-20250614172618627](https://picture.939826.xyz/pictures/img/image-20250614172618627.png)

1. 选择一个仓库：这里就用博客所在的仓库，我的博客仓库是https://github.com/bigbosscyb/bigbosscyb.github.io
2. 安装[giscus app](https://github.com/apps/giscus)

![giscus-install-preview](https://picture.939826.xyz/pictures/img/giscus-install-preview.png)

点击安装会提示选一个仓库，选择上一步指定的仓库就行。

3. 开启Discussions

![image-20250614173118023](https://picture.939826.xyz/pictures/img/image-20250614173118023.png)

4. 填写仓库地址获取评论系统配置信息

![image-20250614173340255](https://picture.939826.xyz/pictures/img/image-20250614173340255.png)

按照上述步骤操作完成后，便可以得到下面配置信息：

![image-20250614173433533](https://picture.939826.xyz/pictures/img/image-20250614173433533.png)

5. 将红框内的配置信息复制，然后替换博客所在仓库的主题文件夹下的评论/服务/giscus.yaml文件的这一段内容：

![image-20250614173844404](https://picture.939826.xyz/pictures/img/image-20250614173844404.png)

6. 修改博客所在仓库根目录下的hugo.yaml文件，将评论系统从disqus改为giscus

![image-20250614174047163](https://picture.939826.xyz/pictures/img/image-20250614174047163.png)

提交修改后，待自动部署完成后可看到博客中出现评论功能：

![image-20250614174250600](https://picture.939826.xyz/pictures/img/image-20250614174250600.png)

### 添加图床功能

这部分功能再新开一个文章继续介绍，不然文章篇幅太长了，会让人看不下去~

#### 使用github仓库当图床?

#### 使用cloudflare R2当图床！

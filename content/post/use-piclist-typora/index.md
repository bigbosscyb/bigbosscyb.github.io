+++
date = '2025-08-03T08:38:22+08:00'
draft = true
title = 'typora写博客时使用自己的图床'

author = "bigbosscyb"

description = "设置typora关联piclist"

categories = [
    "piclist","typora"
]

tags = [
    "图床"
]

+++

使用 Cloudflare 的免费的 R2 对象存储搭建图床、然后在 piclist 工具中进行 R2 存储桶实现图片的上传、删除、最后在 md 文档编辑器 typora 中关联 piclist，实现博客中的图片自动上传至图床中。

### piclist 配置

下面是 Piclist 的介绍

<img src="https://picture.939826.xyz/pictures/img/image-20250803114557621.png" alt="image-20250803114557621" style="zoom:50%;" />

#### 下载配置

- [下载地址](https://piclist.cn/app.html#mac)

- 由于我使用的是 Cloudflare 的 R2 对象存储做图床，而 R2 走的是 S3 协议，所以这里介绍 Piclist 自带[Aws S3](https://piclist.cn/configure.html#%E5%86%85%E7%BD%AEaws-s3)插件进行配置,**不需要再像 picgo 那样额外下载 s3 插件了**跟着链接中的教程输入

  - accessKeyID/api 令牌
  - secretAccessKey/api 访问密钥
  - bucketName/存储桶名称

  - uploadPath/上传路径
  - endpoint/自定义终端节点
  - urlPrefix/自定义域名

其余未提及的保持默认即可。

<img src="https://picture.939826.xyz/pictures/img/image-20250803121331910.png" alt="image-20250803121331910" style="zoom:50%;" />

#### 测试是否成功

使用截图工具截一张图，从到 PicList 的"上传"菜单中，选择从"剪切板上传"

<img src="https://picture.939826.xyz/pictures/img/image-20250803123040126.png" alt="image-20250803123040126" style="zoom:50%;" />

### typora 配置

在 typora 中打开"格式"-"图像"-"全局图像设置"。

<img src="https://picture.939826.xyz/pictures/img/image-20250803123324384.png" alt="image-20250803123324384" style="zoom:50%;" />

<img src="https://picture.939826.xyz/pictures/img/image-20250803123725152.png" alt="image-20250803123725152" style="zoom:50%;" />

最后，当文章写完之后，可以一键将本地图片上传至图床中。

<img src="https://picture.939826.xyz/pictures/img/image-20250803123931892.png" alt="image-20250803123931892" style="zoom:50%;" />

以上便 typora 使用图床的相关配置。

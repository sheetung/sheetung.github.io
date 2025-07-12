# Hugo：零成本搭建一个带有评论和搜索系统的静态博客


简单但是功能完善的静态博客搭建教程，希望帮到你
<!--more-->

## 前提

搭建Hugo博客首先需要满足以下条件：

1. 拥有一个GitHub账号
2. 拥有一台服务器或者电脑也可以
3. 额外：拥有一个域名用来做cname映射，非必需

> [!NOTE]
> 本文主要使用Ubuntu即Linux操作系统完成，win等其他系统在安装和使用上会略有不同。
> win系统对于命令操作可以打开终端进行

按照本文教程结束后你将拥有一个前后端分离的Hugo静态博客以及Fixit主题，并且拥有搜索功能，评论功能，友链功能。

## Hugo博客系统搭建

### 1. 安装

首先到Hugo官方下载满足系统要求的**Hugo extended** 版本，推荐在HugoReleases中下载指定版本，推荐最新版（图片仅为旧版截图未及时更换） [v0.148.1](https://github.com/gohugoio/hugo/releases/tag/v0.148.1), 我是使用树莓派安装的Ubuntu操作系统，所以我选择的是 `hugo_extended_0.145.0_linux-arm64.deb` 版本，教程中稍有不同。

![](/assets/build_hugo_blog/20250712091511624.png)

下载后win系统需要解压使用，`.deb` 格式的Linux安装包需要使用命令 `sudo dkpg -i hugo_extended_0.145.0_linux-arm64. deb ` 安装使用

安装完成后可以查看版本号验证是否安装成功, 如果有版本号返回代表安装成功

```bash
hugo version
```

### 2.创建你的第一个博客

Hugo提供了一个简单的指令来创建一个新的博客网站，找到一个合适的位置，`my_website` 可以修改为任意你期望的名字
```bash
hugo new site my_website
cd my_website
```

当然此时已经搭建好了一个初始博客，但是还没有安装主题和写文章罢了，使用 `hugo server` 命令来本地浏览你的博客

```bash
# bind=0.0.0.0 用于指定服务器绑定的 IP 地址，可以让局域网内任意设备访问
hugo server --bind=0.0.0.0
```

然后打开你的浏览器输入 `http://你的服务器IP:1313` 来验证吧

### 3. 安装主题

我这里使用的是 [FixIt](https://github.com/hugo-fixit/FixIt/blob/main/README.zh-cn.md) 主题，有着丰富的社交和评论系统支持，拥有扩展功能以及性能优越。使用git命令安装主题包，如果不会使用git可以看这篇[教程](https://moontung.top/archives/gitadvance.html)或者手动下载。

```bash
# 可以直接克隆或者选择子模块方式二选一安装
#git clone https://github.com/hugo-fixit/FixIt.git themes/LoveIt
git submodule add https://github.com/hugo-fixit/FixIt.git themes/LoveIt
```

> [!tip] 
> 可以去官方手动[下载](https://github.com/hugo-fixit/FixIt/releases/tag/v0.3.20)稳定版 `0.3.20` Source code即可，解压到theme文件夹下

### 4. 主题基础配置

这里直接从你下载的主题内，即 `theme/FixIt` 下复制 `hugo.toml` 到博客目录下 `hugo.toml`, 或者直接复制其中内容覆盖

```bash
# your site 目录，使用命令复制配置文件
cp themes/FixIt/hugo.toml .
```

此时你的博客目录下就有了一个完整的配置文件，可以先将如下内容进行修改，使得博客为中文语言

```toml
baseURL = "http://example.org/"

# 更改使用 Hugo 构建网站时使用的默认主题
theme = "FixIt"

# 网站标题
title = "我的全新 Hugo 网站"

# 网站语言, 仅在这里 CN 大写 ["en", "zh-CN", "fr", "pl", ...]
languageCode = "zh-CN"
# 语言名称 ["English", "简体中文", "Français", "Polski", ...]
languageName = "简体中文"
# 是否包括中日韩文字
hasCJKLanguage = true
```



---

> 作者: 西塘  
> URL: https://sheetung.github.io/build_hugo_blog/  


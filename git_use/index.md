# GIT使用教程 通关版


一篇完整的git命令使用教程
<!--more-->

>记得很久以前，大概两年左右吧，为了方便自己查阅以及实验室朋友们的使用，搓了一篇git使用教程，很惭愧它特别的粗糙，并且还躺在我的blog里，现在作为gitee/github专业单词拼写专家，还是想精细化这个教程，同样是为了自己查阅，还有方便搜索到的朋友查看。

### 前提
>写每一篇我都希望您具备这些前提条件 

1. 拥有一个**gitee**/**github**账号
2. 会创建一个基础的仓库
3. **Linux**/**Win**下已经安装了**git**，并且**Win**下知道右键打开**Git Bash**
### 新建仓库
首先，你需要在**gitee**/**github**上新建一个仓库，新建好后不要着急退出。会看到类似于这样的代码块
```bash
echo "# testgit" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:sheetung/testgit.git
git push -u origin main

#…or push an existing repository from the command line
git remote add origin git@github.com:sheetung/testgit.git
git branch -M main
git push -u origin main
```
这里给出了一个使用**SSH**的基础的连接操作~~其实也就这么多操作~~，接下来来到电脑端，我使用的是**Ubuntu**，**Win**下一样
### 添加SSH公钥
>当然使用http远程管理仓库也是可行的，方法更简单。这里使用SSH是为了~~专业~~

首先不管是**Linux**还是**Win**，均可使用相同的命令生成**SSH Key**，命令后回车三次
```bash
# -t key 类型  -C 注释,随意可以是 计算机名，你的名字，Email...
ssh-keygen -t rsa -C "email"
```
生成后，有类似如下显示
```bash
ubt@ubt:~$ ssh-keygen -t rsa -C "email"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ubt/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ubt/.ssh/id_rsa
Your public key has been saved in /home/ubt/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:0fefZMlW9pYVBnOZ3urEl6yMzyCjtzvM8UivXkYvtCQ email
The key's randomart image is:
+---[RSA 3072]----+
|             o.+o|
|         .    +o.|
|        . . . . =|
|         . . ..oB|
|        SE + .oO+|
|         o= o B=o|
|        +o=*o+.o.|
|        .*=++o.  |
|       .o== .o   |
+----[SHA256]-----+
```
可见，**Linux**下**SSH**保存在`/home/ubt/.ssh/id_rsa.pub`内
```bash
# cat copy
cat /home/ubt/.ssh/id_rsa.pub
```
**Win**则保存在C盘用户>用户名>.ssh(隐藏文件夹)下，可直接用记事本打开
将复制好的**SSH Key**，来到**gitee**/**github**的设置页面，找到**SSH 公钥**粘贴进去即可
### 初始化仓库
在工程内打开终端，Win下右键打开**Git Bash**
首先配置你的**git config**
```bash
git config --global user.name “你的名字” 
git config --global user.email "注册的邮箱"
```
仓库初始化
```bash
git init
# 如果已有文件或者不需要readme可不执行这一步
echo "# testgit" >> README.md
git add README.md

# 推送三件套,三件套中不包括git remote
#  git add 也可以单个文件或者文件夹添加，-->baidu
git add .
git commit -m "first commit"
git remote add origin ******.git
# -u 第一次的参数  以后只需 git push origin main  此处gitee是master
git push -u origin main
```
此时不出意外已经完成了仓库的推送，刷新你的仓库即可看到文件

### 同步远程仓库
>如果已经拥有一个仓库，需要本地同步，那就这样这样这样

```bash
# 初始化本地仓库
git init
# 链接远程仓库
git remote add origin ******.git
# pull远程仓库的main分支
git pull origin main
```
### 仓库提交三件套
```bash
# 一般情况下，可以对所有文件进行直接提交，三件套如下
git add .
git commit -m "[M]:又掉了一根头发"
git push origin main
```

------
### git相关知识点
#### git remote删除本地对应的远程地址

```bash
#查看远程
git remote -v
```

```bash
# 删除并重建
git remote remove origin
# 重建，建议使用ssh密钥
git remote add origin git@***.com:******.git
```

#### push忽略
`.gitignore`，放入不想上传的文件或者文件夹，例如编译产生的`build`文件，与工程无关的测试文件等
#### git commit规范化

当然，开心就好，这个随意
`git commit -m "[M]:update..."`
```bash
??：表示未被 Git 跟踪的新文件（Untracked files）。
A：表示新添加到暂存区（staged）的文件（Added）。
M：表示文件被修改了（Modified）。
D：表示文件被删除了（Deleted）。
R：表示文件被重命名了（Renamed）。
C：表示文件复制了一份（Copied）。
U：表示文件在合并时发生了冲突（Unmerged）。
```
#### 分支的提交与合并
1. 将本地的 tabbar 分支进行本地的 commit 提交：
```bash
git add .
git commit -m "完成了 tabBar 的开发"
```
2. 将本地的 tabbar 分支推送到远程仓库进行保存：
```bash
git push -u origin tabbar
```
3. 将本地的 tabbar 分支合并到本地的 master 分支：
```bash
git checkout master
git merge tabbar
```
4. 删除本地的 tabbar 分支：
```bash
git branch -d tabbar
```

#### git版本的切换

1.查看历史版本 

可以在仓库中或者使用命令 `git log` 查看

2.然后切换到指定版本

```bash
git checkout [ID]
```

3.如果不放心使用 `git branch` 查看当前本地分支

-----






---

> 作者: sheetung  
> URL: https://sheetung.github.io/git_use/  


---
title: Blog搭建流程
date: 2020-01-01 23:11:10
tags: 
- hexo
categories:
- 博客
thumbnail: https://tva1.sinaimg.cn/large/006tNbRwly1gajhygh737j317y0u04qu.jpg
---

>本文转自: [Blog搭建流程(Mac系统完结帖)](http://www.ivan-zcy.top/)
>
>原文地址: http://www.ivan-zcy.top/2018/09/30/Blog

<!--more-->

### Step1 安装Node.js

可通过以下两种方式在 Mac OS 上安装 node.js：

方式一： 在[官方下载网站](https://nodejs.org/en/download/)下载 pkg 安装包，直接点击安装即可

方式二： 使用 brew 命令来安装：

```bash
brew install node
```

### Step2 安装Git

首先查看电脑是否安装Git，终端输入：

```bash
git
```

安装过则会输出下表，然后跳过该步

```
WMBdeMacBook-Pro:~ WENBO$ git
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```



 如果没有显示上面内容，我们可以通过homebrew安装GIt，若未安装homebrew 则通过终端执行：

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

 随后执行一下命令进行Git的安装

```bash
brew install git
```

### Step3 注册Github账号并新建仓库

 网站链接：[Github](https://github.com/)

 注册完账号后需新建一个仓库。注意！！新建的仓库名字必须是username.github.io。例如我username是ivan-zcy，那么仓库名字必须是ivan-zcy.github.io

### Step4 配置SSH Key（可省略 建议配置）

这一步能省略 但是配置后更新博客就不用每次都输入用户名密码了

步骤：
​ 1 检查主机是否已存在SSH Key

```
cd .ssh
ls -la
```

若输出的文件列表中存在id_rsa.pub 或 id_dsa.pub 文件，则直接跳到第三小步



 2 创建SSH Key
在终端输入如下命令

```
ssh-keygen -t rsa -C "your_email@example.com"
```

按下回车 会让输入文件名，直接回车会创建默认文件名的文件 然后会提示输入两次密码(可为空)

 3 添加SSH Key到Github

（如果之前在Github中添加过SSH 则跳过该步）

如果你没有指定文件名（也就是使用默认文件名），那么在.ssh文件夹下会有一个id_rsa.pub文件，打开该文件并复制里面的内容

登录Github，点击右上角头像右边的三角图标，点击Settings –> SSH and GPG keys –> New SSH key。Title 随便填一个，在Key栏中填入复制的内容，点击Add SSH key，就添加成功了

 4 检验SSH Key是否配置成功
在终端输入如下命令

```
ssh -T git@github.com
```

如果最后出现

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

就说明SSH Key配置成功了

### Step5 安装Hexo

使用npm命令安装Hexo

```
npm install -g hexo
```

接着在任意位置创建一个文件夹，如Blog，cd到该路径下执行

```
hexo init
```

该命令会在目标文件夹内建立网站所需的基础文件

接着安装安装依赖包

```
npm install
```

此时本地博客就搭建好了

执行

```
hexo generate
hexo server
```

此时可在浏览器中输入[http://localhost:4000/](https://link.jianshu.com/?t=http://localhost:4000/)进行本地查看（其他人无法访问）

 当然 此时可修改本地博客路径下的_config文件对博客进行全局设置，里边设置项挺多就不一一列举啦！自行百度



### Step6 同步到远程Github仓库

在本地Blog路径下找到_config.yml，把deploy节点修改为：

```
deploy:
  type: git
  repo: git@github.com:username/username.github.io.git
  branch: master
```

（其中 username为你的Github用户名）

为了能够使Hexo部署到GitHub上，需安装一个插件

```bash
npm install hexo-deployer-git --save
```

然后输入以下命令

```bash
hexo clean
hexo generate
hexo deploy
```

这时候就可以在浏览器通过输入username.github.io就可以访问你的博客了

### Step7 配置主题

 前边写过配置主题的博文 抛出一个传送门：

 [滴滴，我是传送门](http://www.ivan-zcy.top/2018/09/28/hexo更换主题流程/)

 （主题在github上 知乎上 hexo官网上有很多很多 适合自己就好）



### 注意点！！！！

一些主题的功能需要我们自己预先创建好对应的页面，例如标签tags 关于about等等等等

此时我们需要在本地Blog路径下

 1 添加关于页面（可选）

使用：`hexo new page "about"`新建一个 关于我 页面。
主题的 `_config.yml`文件中的 `menu`中进行匹配

```
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签
  about: /about   //关于                  （添加此行即可）
```

 也可在本地博客路径 –> source –> about文件下，通过修改其中的index.md对其页面进行配置

 2 添加标签页面（可选）

使用： `hexo new page tags`新建一个 标签 页面。
主题的 `_config.yml`文件中的 `menu`中进行匹配

```
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签                  （添加此行即可）
  about: /about   //关于
```

 也可在本地博客路径 –> source –> tags文件下，通过修改其中的index.md对其页面进行配置



 除了上边两个之外还有分类categories，自定义页面等等就不一一列举啦 自行百度吧！

### Step8 发布博文

 接着抛链接：

 [滴滴，我也是一个传送门](http://www.ivan-zcy.top/2018/09/28/hexo发表博客常用命令/)

### Step9 绑定个人域名

 步骤：

 1 购买域名

建议从[阿里云平台](https://account.aliyun.com/login/login.htm?oauth_callback=http%3A%2F%2Fnetcn.console.aliyun.com%2Fcore%2Fdomain%2Flist%3Fspm%3Da2c1d.8251892.0.0.4f0f52f2SzXZY4)啦之类的国内大型平台购买（这一步通常需要身份验证之类的 大概需要几天时间吧也记不清楚了 反正挺麻烦挺磨唧的）

 2 配置DNS地址

进入阿里云控制台 –> 域名 –> 域名列表 找到自己的域名 点击下图红圈圈的“管理”

![1](http://www.ivan-zcy.top/2018/09/30/Blog%E6%90%AD%E5%BB%BA%E6%B5%81%E7%A8%8B-Mac%E7%B3%BB%E7%BB%9F%E5%AE%8C%E7%BB%93%E5%B8%96/1.png)



 3 进行域名解析

找到管理界面下的域名解析 在其中添加3条记录（username是github的用户名）

```
@          A             192.30.252.153
@          A             192.30.252.154
www      CNAME         username.github.io.
```

 4添加CNAME文件
新建一个名为CNAME的文件(无后缀)，内容为你的域名地址。将该文件放到本地博客的source文件夹里面，并更新到Github

 这时候你的博客就建完啦！

 最后附上主页地址： [戳我](http://www.ivan-zcy.top/)

 一起造作吧！！！！

#### 参考链接：

https://segmentfault.com/a/1190000008040387

https://blog.csdn.net/ganzhilin520/article/details/79047249

https://www.jianshu.com/p/e5f95eb990ad
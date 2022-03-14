---
title: Mac终端配置代理
date: 2020-01-31 19:45:51
tags:
- 终端
categories:
- 实用知识
thumbnail: https://tva1.sinaimg.cn/large/006tNbRwly1gbfziydz2jj30jd0d9tbs.jpg
---

在使用终端时候难免会浏览和下载墙外的资料，这时候就要用到代理。下面我来为大家介绍一下在Mac环境下终端的代理方法。

<!--more-->

### 准备

在操作以下步骤之前，需要配置好 Shadowsocks。

### 方法一：

在终端中依次执行以下命令的前两个或者直接执行最后一个即可

```
    # 配置http访问的
    export http_proxy=socks5://127.0.0.1:1080
    # 配置https访问的
    export https_proxy=socks5://127.0.0.1:1080
    # 配置http和https访问
    export all_proxy=socks5://127.0.0.1:1080
```

>这里的端口具体要看使用的工具，具体如下。

![Xnip2020-01-31_19-52-00](https://tva1.sinaimg.cn/large/006tNbRwly1gbfzmadu91j30gg0nmjzh.jpg)

这里就要输入1086端口。

这个办法的好处是简单直接，并且影响面很小（只对当前终端有效）。

输入`curl cip.cc`来查看终端是否成功代理。

![Xnip2020-01-31_19-56-20](https://tva1.sinaimg.cn/large/006tNbRwgy1gbfzrlu1ulj30kj0d9grz.jpg)

### 方法二：

把代理服务器地址写入 shell 配置文件 `.bash_profile` 或者 `.zshrc`。

终端执行 `vim ~/.bash_profile` 或者 `vim ~/.zshrc` 配置全局环境变量。

直接在 `. bash_profile` 或者 `.zshrc` 添加下面内容

```
# 终端设置代理
# -------------------------------
# polipo proxy on/off
# ------------------------------
function proxy_on() {
    # 配置http访问的
    export http_proxy=socks5://127.0.0.1:1080
    # 配置https访问的
    export https_proxy=socks5://127.0.0.1:1080
    # 配置http和https访问
    export all_proxy=socks5://127.0.0.1:1080
    echo '********   开启当前终端代理   ********'
}

function proxy_off() {
    # 移除代理
    unset http_proxy
    unset https_proxy
    unset all_proxy
    echo '********   关闭当前终端代理   ********'
}
```

编辑完之后执行 `source ~/.bash_profile` 或者 `source ~/.zshrc` ，编辑的哪个执行哪个就行。

使用时在终端执行

> 启动：`proxy_on`
> 关闭：`proxy_off`

这个办法的好处是随时用随时开关，方便快捷，并且影响面也同样很小（在执行的终端设置代理，只对执行的终端有效，不影响其他终端）。

### 方法三：（配置全局代理 `慎用`）

###### a. 设置代理

```
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

###### b. 查看信息 git 配置信息

```
git config --global -l 
```

###### c. git 移除全局配置代理

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

> 如果 git 配置了全局的代理会影响到 sourcetree 或者其他命令终端的 git 命令，请小心使用！！！

------

### 参考文章

[Mac终端配置代理](http://www.imooc.com/article/285912)
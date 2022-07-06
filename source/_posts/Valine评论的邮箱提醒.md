---
title: Valine评论的邮箱提醒
author: 粉色桃子abc
date: 2020-8-6 13:21:28
tags:
- Valine评论
- hexo
category:
- 博客
thumbnail: https://cdn.jsdelivr.net/gh/pinkpeachabc/images/Blog-imgs/%E5%8D%9A%E5%AE%A23.png
---

>博客搭建了很久了，前两天闲来无事去逛别人博客时发现了别人给我发评论是可以用第三方邮件提醒。突然想起来自己的博客评论却没有这个功能，最早之前用过来必力很可惜加载**龟速**~~服务器不在国内~~，如今使用的是无后端的Valine，精简快捷。今天就给它设置个第三方邮件提醒吧。

![ac7DiD.png](https://s1.ax1x.com/2020/08/06/ac7DiD.png)

## 简介

>此项目是一个对 [Valine](https://valine.js.org/) 评论系统的拓展应用，可增强 `Valine` 的邮件通知功能。基于 Leancloud 的云引擎与云函数。可以提供邮件 `通知站长` 和 `@ 通知` 的功能，而且还支持自定义邮件通知模板。

[Valine Admin](https://github.com/zhaojun1998/Valine-Admin)

## 配置

- 首先进入[Leancloud](https://leancloud.cn/) 中，在**设置-邮件模板-用于重置密码**的邮件主题中修改为：

```html
<p>Hi, {{username}}</p>
<p>
你在 {{appname}} 的评论收到了新的回复，请点击查看：
</p>
<p><a href="你的网址首页链接" style="display: inline-block; padding: 10px 20px; border-radius: 4px; background-color: #3090e4; color: #fff; text-decoration: none;">马上查看</a></p>
```

![acqVRe.png](https://s1.ax1x.com/2020/08/06/acqVRe.png)

- 部署Valine-Admin，在**云引擎-部署-Git部署**中输入 https://github.com/zhaojun1998/Valine-Admin ，并在**分支或提交**中输入master点击部署。

![acqnsA.png](https://s1.ax1x.com/2020/08/06/acqnsA.png)

- 接下来是配置项，在**云引擎-设置-自定义环境变量**中，**添加新变量**，如表所示：

| 变量          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| SITE_NAME     | [必填] 网站名称                                              |
| SITE_URL      | [必填] 网站地址，**最后不要加 `/`**                          |
| SMTP_SERVICE  | [必填] 邮件服务提供商，支持 QQ、163、126、Gmail 以及 [更多](https://nodemailer.com/smtp/well-known/#supported-services)。 — *如这里没有你使用的邮件提供商，请查看[自定义邮件服务器](https://blog.csdn.net/高级配置.md#自定义邮件服务器)* |
| SMTP_USER     | [必填] SMTP登录用户，一般为邮箱地址                          |
| SMTP_PASS     | [必填] SMTP登录密码，一般为授权码，**而不是邮箱的登陆密码**，请自行查询对应邮件服务商的获取方式 |
| SENDER_NAME   | [可选] 发件人                                                |
| ADMIN_URL     | [建议] Web主机二级域名，用于自动唤醒                         |
| TO_EMAIL      | [可选] 指定站长收信邮箱，默认值为`SITE_USER`。用于 SMTP 发件人与站长收件人不一致的情况下使用。 |
| TEMPLATE_NAME | [可选] 通知邮件的模板（default和rainbow），参考高级功能      |

![acq8JS.png](https://s1.ax1x.com/2020/08/06/acq8JS.png)

>关于几点注意：SMTP登录密码（例如qq），不是qq密码而是授权码。自定义环境变量保存完只有重启部署才有用。

![acqlIf.png](https://s1.ax1x.com/2020/08/06/acqlIf.png)

## 后台评论管理

- 在**设置-域名绑定-云引擎、ClientEngine 域名**中，添加一个二级域名。

![acqZxH.png](https://s1.ax1x.com/2020/08/06/acqZxH.png)

- 在**储存-结构化数据-_User**中，点击**添加行**。只需要填写 `email`、`password`、`username`，这三个字段即可, 使用 `email` 作为账号登陆即可。

![acqmMd.png](https://s1.ax1x.com/2020/08/06/acqmMd.png)

- 在浏览器中输入你绑定的web域名，既可以访问到后台评论。

![acjDB9.png](https://s1.ax1x.com/2020/08/06/acjDB9.png)

#### LeanCloud 自带定时器[推荐]

- 首先需要添加环境变量，`ADMIN_URL`：`Web 主机域名`，如图所示（添加后重启容器才会生效）：

![acvXPx.png](https://s1.ax1x.com/2020/08/06/acvXPx.png)

- 然后在**云引擎-定时任务-创建定时任务**中，新增定时器，如下图所示。

![acquqI.png](https://s1.ax1x.com/2020/08/06/acquqI.png)

> 注意, LeanCloud 最近更新了定时器校验规则, 需要将 Cron 表达式写为: `0 */20 7-23 * * ?`

## 测试

用其他邮箱在自己的博客留言板出留言，进入邮箱看是否收到提醒。

![aczZkR.png](https://s1.ax1x.com/2020/08/06/aczZkR.png)
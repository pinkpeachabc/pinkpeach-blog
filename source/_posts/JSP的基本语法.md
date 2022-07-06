---
title: JSP的基本语法
date: 2020-3-4 14:42:17
tags:
- JSP
categories:
- JavaWeb
thumbnail: 
---

## JSP 简介

>前两章写的响应和 session，这次我来说一下 jsp 😀

**什么是 JSP**

JSP 全名为 Java Server Pages，中文名叫 java 服务器页面。在传统的网页HTML文件(*.htm,*.html)中插入 Java 程序段和 JSP 标记，缀名为(*.jsp)。

**为什么要有 JSP**

直接使用 Html 文件是没有办法输出 Java 当中的信息，使用 servlet 来去输出一个网页非常的麻烦。于是就出现了jsp，又能写 html，又能写 Java 代码

**JSP 的组成部分**

静态数据，如 HTML

JSP 脚本元素和变量

JSP 指令，如 include 指令

JSP 标签动作

用户自定义标签

## JSP脚本元素和变量

**在 JSP 当中写 Java 代码**

`<%java代码%>`内部的 java 代码翻译到 service 方法的内部
`<%=java变量或表达式>`会被翻译成 service 方法内部 `out.print()`
`<%!java代码%>`会被翻译成 servlet 的成员的内容
**JSP 注释**

HTML 注释：`<!--注释内容-->`
可见范围 jsp 源码、翻译后的 servlet、页面
**Java 注释**

`//单行注释  /*多行注释*/`
可见范围 jsp 源码 翻译后的 servlet,页面中看不到
**Jsp 注释**

`<%--注释内容--%>`
可见范围 jsp 源码可见

## JSP 指令

**什么是指令**

> JSP 指令用于设置整个 JSP 页面的相关信息，以及用于 JSP 页面与其它容器之间的通信。

**有哪些指令**

> page 指令	include 指令	taglib 指令

**page 指令**

```jsp
<%@page "指令" %>
```

用于设定整个 JSP 页面的属性和相关功能，多个属性之间使用空格隔开。page 指令共有 11 个属性分别是：

​	*contentType*
​	contentType 属性指定 JSP 页面的 MIME 和编码格式

​	*buffer*
​	用来设置输出流缓冲区,缓冲区的作用就是为了提高 IO 性能,也就是说减少 write 的次数

​	*language 属性*
​	指定页面中使用的脚本语言种类,目前只支持 java

​	isErrorPage
​	允许指定的 JSP 页面为错误处理页面

​	*autoFlush*
​	用来指定当输出流缓冲区满了的时候，是否自动刷新缓冲区

​	*errorPage*
​	如果当前页面发生异常,网页会重定向到 errorPage 所指定的页面进行处理

​	*extends*
​	用于指定该 JSP 生成的 servlet 继承自哪个父类,必须指定包名加类名

​	*session*
​	指定当前页面是否能获得当前用户的 session 对象,缺省是 true
​	如果指定为 false,那么在该页面中无法使用 session，使用的话会提示500错误

​	*import*
​	在 JSP 中引入 Java 的包和类，多个包之间以逗号隔开

​	*info*
​	用来设置该 jsp 文件的介绍信息

​	*pageEncoding*
​	pageEncoding 属性用来指定 JSP 文件的编码格式

​	*isELIgnored*
​	用来标示是否支持 EL 表达式

​	*isThreadSafe*
​	缺省值为 true
​	指定该 JSP 文件是否支持多线程访问

**include指令**

表示在JSP编译时插入一个包含文件或者代码的文件，include 指令所包含的文件名不能是一个变量 url,只能是静态的文件名。

> 静态包含

```jsp
<%@include file="header.jsp"%>
<%@include file="footer.jsp"%>
```

将两个 jsp 页面接着到一起， 然后再翻译成 servlet

**taglib指令**

声明 JSP 文件使用了标签库

> 有哪些标签库

JSP 标准标签库，第三方标签库，自定义标签库

## JSP 标签动作

**页面包含**

```java
<jsp:include page="被包含的页面"></jsp:include>
```

>动态包含

各自翻译自己的页面，然后再引入

**请求转发**

```java
<jsp:forward page="要转发的资源"></jsp:forward>
```

## JSP 隐式对象

*out*

```java
	//out的类型：JspWriter
	//out作用就是想客户端输出内容 out.write()
	//out缓冲区默认8kb
	//可以设置成0 代表关闭out缓冲区内容直接写到respons缓冲区
	//out写的内容写到out缓冲区当中
	//最后再把out缓冲区当中的内容合并到response缓冲区当中
```

*request*
得到用户请求信息对象

*response*
服务器向客户端的响应对象

*config*
服务器配置，可以取得初始化参数

*session*
用来保存用户会话的信息

*application*
所有用户的共享信息，就是 servletContext

*page*
指当前页面转换后的 Servlet 类的实例

*pageContext*
jsp 页面的上下文对象

> 是一个域对象

```java
setAttribute(String name,Object obj)
getAttribute(String name)
removeAttrbute(String name)
```

> 可以向指定的其他域中存取数据

```java
setAttribute(String name,Object obj,int scope)
setAttribute(“name”,"lk",PageContext.REQUEST_SCOPE);
```

```java
getAttribute(String name,int scope)
getAttribute("lk",PageContext.REQUEST_SCOPE)
```

```java
removeAttrbute(String name,int scope)
```

```java
findAttribute(String name)
//自动到所有的域当中找数据
//从小到大的范围搜索数据
//依次从 pageContext 域，request 域，session 域，application 域中获取属性
//在某个域中获取后将不在向后寻找
```

>可以获得其他 8 大隐式对象

```java
pageContext.getRequest()
pageContext.getSession()
```

*exception*
表示 JSP 页面所发生的异常，在错误页中才起作用
只有是错误页面的时候，才会有该对象
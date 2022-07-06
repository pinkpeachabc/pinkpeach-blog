---
title: cookie与Session
date: 2020-2-27 20:33:57
tags:
- session
- cookie
- 会话
categories:
- JavaWeb
thumbnail: 
---

## 会话概述

> 什么是会话:从打开浏览器,到访问网页,到最终关闭浏览器,整个过程就是一次会话。
>

**会话的特点**

包含多个请求,一次完整的会话针对一个用户。

**会话管理技术**

- 第一种: cookie 技术,客户端技术
- 第二种: session 技术,服务端技术
  

**购物车案列**

> 买完商品后,加入购入车,买的商品存到什么对象比较合适?

- 使用 request 域对象保存商品信息
  结论:使用 request 保存商品信息不可以,因为每次发送请求,都会产生一个新的请求对象

- 使用 ServletContext 域对象保存商品信息
  结论:使用 ServletContext对象保存商品信息,可以,但是不合理

所以在开发中,保存会话过程中产生的数据,采用会话管理技术,也就是使用 cookie 和  session 技术来保存会话过程产生的数据。

## Cookie

>服务器怎样把 cookie 发给客户端

**创建 Cookie**

```java
Cookie cookie = new Cookie(String cookieName,String cookieValue);
```

**向客户端发送 cookie**

```java
response.addCookie(cookie);
```

**访问**

> 第一次访问时,请求头当中没有 cookie
>
> 第一次访问时, 响应当中会看到 set-cookie
>
> 再一次访问时,请求头当中就能够看到 cookie 信息

访问服务器的任何资源，一般情况下都会把 cookie 带去过。

**Cookie 默认存储时间**

> 默认 cookie 的是会话级别

打开浏览器，关闭浏览器为一次会话，如果不设置持久化时间，cookie 会存储在浏览器的内存中，浏览器关闭 cookie 信息销毁。

**设置 Cookie 在客户端的存储时间**

```java
cookie.setMaxAge(int seconds);
```

设置的时间为秒，如果设置持久化时间，cookie 信息会被持久化到浏览器的磁盘文件里，过期会自动删除。

**Cookie 的携带路径**

> 访问某一个资源时，要不要带 cookie 信息。如果每一外资源都携带，会影响传输速度 。如果不设置携带路径，默认情况下会在访问创建 cookie 的 web 资源相同的路径都携带 cookie 信息。

在 myxq/CookieServlet 下创建的 cookie

在 myxq/下的index.jsp 访问时会携带 cookie

不是在 myxq 下，不会携带 cookie

**设置 Cookie 携带路径**

```java
cookie.setPath(String path);
```

```java
cookie.setPath("/CookiePro/cookieServlet");
//只有访问 cookieServlet 才携带 cookie 信息
```

```java
cookie.setPath("/CookiePro");
//访问指定的工程时，都会携带 cookie 信息
```

```java
cookie.setPath("/");
//访问服务器下部署的所有工程时都会携带 cookie 信息
```

**删除 Cookie**

> 使用同名同路径的持久化时间为0的cookie进行覆盖即可

```java
cookie.setMaxAge(0);
```

**服务器如何获取客户端携带的 Cookie**

> 通过 Request 对象的 getCookies() 方法,获取的是所有的 cookie,要进行遍历，找出自己名称的那一个。

```java
//1.获取所有的cookie的对象
Cookie[] cookies = request.getCookies();
//2.获取的结果不为空
if(cookies != null){
    //3.遍历所有的cookie
    for(Cookie cookie:cookies)
        //遍历出每一小时，取出对应的名称
        String name = cookie.getName();
    	//判断名称是否为自己储存的哪一个
    	if(name.equals("pinkpeach")){
            System.out.println(cookie.getValue());
        }
}
```

## Session对象

**什么是 session**

session 是一种会话管理技术, session 用来保存会话过程中的数据,保存的数据存储到服务器端。

session 原理:基于 cookie 实现的,更确切的说是基于会话级别的 cookie 实现的。

**HttpSession API**  

> session 常用方法

得到 session 的id( JESSIONID对应的值): `getId();`

设置 session 的生命时长: `setMaxInactiveInterval(int interval);`

销毁 session: `invalidate();`

得到 sessIon: `HttpSession session = request.getsession();`

**session 域对象**

> 作用范围一次完整的会话(包含多个请求)

存值: `setAttribute(String key, Object obj);`

取值: `Object obj= getAttribute(String key);`

移除: `removeAttribute(String key);`

总结域对象: request 域对象  session 域对象 servletContext 域对象,作用范围以次变大

**Session超时管理**

> session对象是由生命时长,它的默认存活时间是30分钟。

具体配置找 tomcat 软件的 conf 下的web.xml文件

```html
<session-config>
<session-timeout>30</session-timeout>
</session-config>
```

立即销毁 session 对象: `invalidate();`
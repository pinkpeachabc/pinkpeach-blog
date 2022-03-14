---
title: EL与JSTL
date: 2020-3-8 21:18:24
tags:
- EL 
- JSTL
categories:
- JavaWeb
desc: EL表达式与JSTL
thumbnail: 
---
经历过了 JSP，发现既能写 Html 又能写 Java 代码确实很方便，但是对于JSP 内部脚本的编写，却是很不友好😭 今天来介绍能够替代 JSP 页面中的脚本——EL 与 JSTL

## EL表达式

**作用**

> EL最主要的作用是获得四大域中的数据

**从四大域当中取数据**

pageContext

```jsp
${pageScope.key};
```

request

```jsp
${requestScope.key}
```

session

```jsp
${sessionScope.key}
```

application

```jsp
${applicationScope.key}
```

**简写**

```jsp
${EL表达式}
```

> EL 从四个域中获得某个值 ${key}，依次从 pageContext 域，request 域，session 域，application 域中，获取属性在某个域中获取后将不在向后寻找。

**EL 内置 11 对象**

*pageScope*
获取 JSP 中 pageScope 域中的数据

*requestScope*
获取 JSP 中 requestScope 域中的数据

*sessionScope*
获取 JSP 中 sessionScope 域中的数据

applicationScope
获取 JSP 中 applicationScope 域中的数据

*param*
`request.getParameter()`

*paramValues*
`rquest.getParameterValues()`

*header*
`request.getHeader(name)`

*headerValues*
`request.getHeaderValues()`

*initParam*
`this.getServletContext().getInitParameter(name)`

*cookie*	
`request.getCookies()---cookie.getName()---cookie.getValue()`

*pageContext*
pageContext 获得其他八大对象，获取当前项目的名称
`${pageContext.request.contextPath}`

**EL 执行表达式**

> 内部可以进行运算，只要有结果

```java
${1+1}
${empty user}
${user==null?true:false}
```

## JSTL

**什么是JSTL**

> JSTL（JSP Standard Tag Library)，JSP 标准标签库。可以嵌入在 jsp 页面中使用标签的形式完成业务逻辑等功能，jstl 出现的目的同el一样也是要代替 jsp 页面中的脚本代码。

**导包和引入**

使用 jstl 需要先把 jar 包引入工程当中 (jstl-1.2.jar)，然后引入标签库才能够继续使用。

```java
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
```

**if 标签**

`<c:if test="${1==1 }">`满足条件时，中间的内容才会显示出来`</c:if>`

> 通过是结合 EL 表达式一起使用，EL 从域中取数据，使用JSTL进行判断或者遍历

```java
<%request.setAttribute("money", 3);%>
<c:if test="${money > 50}">金额大于：50</c:if>
<c:if test="${money < 50}">金额小于：50</c:if>
```

做一个 if 标签的使用，**需求：用户登录成功时， 进入首页中，显示用户名。**

>1.登录成功时，把用户写到 session 域当中。

```java
//有值
if(u != null){
    response.getWriter().write("登录成功");
    //把用户存在session当中
    HttpSession session = request.getSeesion();
    session.setAttribute("user",u);
    //跳转到登录
    response.setHeader("refresh","3;url=/项目地址/index.jsp");
}
```

>2.在首页当中进行判断，从 session 域当中取数据。
>
>3.通过EL结合JSTL进行判断

```java
<c:if test="${empty user}">
<a href="Login.jsp">登录</a>
<a href="regist.jsp">免费注册</a>
</c:if>
    
<c:if test="${！empty user}">
欢迎：${user.username}
<a href="#">退出</a>
</c:if>
```

**foreach 标签**

> 普通循环

```java
<!-- 从域当中取数据 自动把数据存储 pageScope -->
<c:forEach begin="0" end="5" var="i">
	${i}<br/>
</c:forEach>
```

>增加 for 循环

遍历字符串集合

```java
<%
    list<String> strList = new ArrayList<String>();
	strList.add("aaa");
	strList.add("aaa");
	strList.add("aaa");
 %>
   <!--会自动把取出来的值放入到pageScope域当中-->
<c:forEach items="${strList}" var="str">
    ${str}
</c:forEach>
     
```

遍历对象集合

```java
<%
    list<User> userList = new ArrayList<User>();
	User u1 = new User();
	u1.setUsername("李四");
	
	User u2 = new User();
	u2.setUsername("王五");
	userList.add(u1);
	userList.add(u2);
	session.setAttribute("userList",userList);
 %>
<c:forEach items="${userList}" var="user">
  ${user.username}
</c:forEach>
```

遍历 map

```java
<%
	Map<String,String> strMap = new HashMap<String,String>();
	strMap.put("name","李四");
	strMap.put("age","28");
	strMap.put("addr","天津");
	session.setAttribute("me",strMap);
%>
<:forEach items="${me}" var="entry">
	${entry.key}:${entry.value}
</:forEach>
```

------

像是 jstl 的标签库还有很多，这里只介绍了两个标签。
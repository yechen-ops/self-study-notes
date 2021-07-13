## EL表达式

### 一、第一章EL工具包介绍

* 由 Java 技术开发的一个 jar 包。
* 作用是降低 JSP 文件开发时 Java 命令的开发强度。
* Tomcat 服务器本身自带了 EL 工具包，位置是 `D:\Environmental\Tomcat\apache-tomcat-9.0.41\lib\el-api.jar`



### 二、传统 JSP 文件主要的开发步骤

* 第一步：从指定的作用域对象中读取处理结果。
* 第二步：将得到的数据进行类型的强转。
* 第三步：将转换后的数据写入响应体中，进行输出。

```jsp
<!--第一步：从指定的作用域对象中读取处理结果。-->
<%
	// 第二步：将得到的数据进行类型的强转。
	String value = (String) request.getAttribute("key");
%>
<!--第三步：将转换后的数据写入响应体中，进行输出。-->
value是：<%=value%>
```



### 三、EL 表达式

1. 命令格式：  `${作用域对象别名.共享数据名}`
2. 命令作用：  
   * EL 表达式是 EL 工具包提供一种**特殊命令格式**【表达式命令格式】。
   * EL 表达式在 JSP 文件上使用。
   * 负责在 JSP 文件上从作用域对象读取指定的共享数据并输出到响应体。



### 四、EL 表达式作用域对象别名

**JSP 文件中可以使用的作用域对象：**

* `ServletContext application`（**全局作用域对象**）
* `HttpSession session`（**会话作用域对象**）
* `HttpServletRequest request`（**请求作用域对象**）
* `PageContext pageContext`（**当前页作用域对象**）

> 1. 当前页作用域对象，这是JSP文件独有的作用域对象。Servlet 中不存在。
>
> 2. 在当前页作用域对象存放的共享数据 **仅能在当前JSP文件中使用** ，不能共享给其他Servlet或则其他JSP文件。
> 3. 真实开发过程，主要用于 `JSTL` 标签与 JSP 文件之间数据共享数据。
>     `JSTL------->pageContext---->JSP`

**EL 表达式中作用域对象的别名**

| 作用域对象  |       别名       |
| :---------: | :--------------: |
| application | applicationScope |
|   session   |   sessionScope   |
|   request   |   requestScope   |
| pageContext |    pageScope     |



### 五、EL表达式将引用对象属性写入到响应体

1. **命令格式：** `${作用域对象别名.共享数据名.属性名}`

2. **命令作用：** 从作用域对象读取指定共享数据关联的引用对象的属性值。并自动将属性的结果写入到响应体
3. EL 表达式没有提供遍历集合方法，因此无法从作用域对象读取集合内容输出。



### 六、EL表达式简化版

1. **命令格式：** `${共享数据名}`

2. **命令作用：** EL表达式允许开发人员开发时**省略作用域对象别名**。

3. **工作原理：**

   首先到【`pageContext`】定位共享数据，如果存在直接读取输出并结束执行。

   如果在【pageContext】没有定位成功，到【`request`】定位共享数据，如果存在直接读取输出并结束执行。

   如果在【request】没有定位成功，到【`session`】定位共享数据，如果存在直接读取输出并结束执行。

   如果在【session】没有定位成功，到【`application`】定位共享数据，如果存在直接读取输出并结束执行。

   如果在【application】没有定位成功，返回`null`。

   `pageContext--->request--->session--->application`

4. **存在隐患：**
   * 容易降低程序执行速度【南辕北辙】
   * 容易导致数据定位错误
5. **应用场景：**   设计目的，就是**简化从 pageContext 读取共享数据**并输出难度。
6. **EL表达式简化版尽管存在很多隐患，但是在实际开发过程中，开发人员为了节省时间，一般都使用简化版，拒绝使用标准版。**



### 七、EL表达式-----支持运算表达式

**在 JSP 文件有时需要将读取共享数据进行一番运算之后，将运算结果写入到响应体。**

==运算表达式：==

1. **数学运算：**

```java
// OneServlet.java
@WebServlet(name = "OneServlet", urlPatterns = "/one")
public class OneServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        ServletContext application = request.getServletContext();
        application.setAttribute("key1", "25");
        application.setAttribute("key2", "10");
        // 请求转发
        request.getRequestDispatcher("/index_1.jsp").forward(request, response);
    }
}

```

```jsp
<!--index_1.jsp-->
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<!--出现了 “+” ，会自动将其他类型转换为 数字类型-->
两数之和为：${key1 + key2}
</body>
</html>
```

2. **关系运算：**

| 关系运算符 | EL 表达式中的代号 |
| :--------: | :---------------: |
|     >      |        gt         |
|     >=     |        ge         |
|     <      |        lt         |
|     <=     |        le         |
|     ==     |        eq         |
|     !=     |        !=         |

3. **逻辑运算：**  &&   ||    ！



### 八、EL表达式提供内置对象

* ==**命令格式: ${param.请求参数名}**==

  命令作用：通过请求对象读取当前其请求包中的请求参数内容，并将请求参数内容写入到相应体中。

```jsp
index.jsp
<!--发送请求：  Http://localhost:8080/myWeb/index.jsp?userName=mike&password=123-->
userName=${param.userName}
password=${param.password}
```

* ==**命令格式：${paramValues.请求参数名[下标]}**==

  命令作用：如果浏览器发送的请求参数是**一个请求参数关联多个值**，此时可以通过`paramVaues` 读取请求参数下指定位置的值并写入到响应体。

```jsp
index.jsp
<!--http://localhost:8080/myWeb/index_2.jsp?pageNo=1&pageNo=2&pageNo=3-->
pageNo01=${paramValues.pageNo[0]}<!--输出：pageNo01=1-->
pageNo02=${paramValues.pageNo[1]}<!--输出：pageNo02=2-->
pageNo03=${paramValues.pageNo[2]}<!--输出：pageNo03=3-->
```
































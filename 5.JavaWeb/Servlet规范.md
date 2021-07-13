## Servlet 规范

### 一、Servlet 规范介绍：

1. Servlet 规范来自于 JavaEE 规范中的一种。
2. **作用：**
   1. 在 Servlet 规范中，指定 ==动态资源文件的开发步骤==。
   2. 在 Servlet 规范中，指定 ==Http 服务器调用动态资源文件的规则==。
   3. 在 Servlet 规范中，指定 ==Http 服务器管理动态资源文件实例对象的规则==。



### 二、Servlet 接口实现类：

1. Servlet 接口是来自于 Servlet 规范下的一个接口，这个接口存在于 Http 服务器提供给的 jar 包内。
2. Tomcat 服务器下的 lib 目录下有一个 `servlet-api.jar` 文件存放 Servlet 接口。（`javax.servlet.Servlet` 接口）。
3. Servlet 规范中，Http 服务器能调用的 【动态资源文件】 必须是一个 Servlet 接口的实现类。

```java
class Student{
	// 没有实现 Servlet 接口
	// 不是动态资源文件，Tomcat无权调用
}

class Teacher implements Servlet{
	//合法动态资源文件，Tomcat有权利调用

	Servlet obj = new Teacher();
	obj.doGet()
}
```



### 三、Servlet接口实现类开发步骤：

==第一步==：创建一个 java 类继承于 `HttpServlet` 父类，使之成为一个 Servlet 接口的实现类。

```java
package cn.yechen;

import javax.servlet.http.HttpServlet;

public class MyServlet extends HttpServlet {
    
}
```

> 为什么不直接实现 Servlet 接口呢？ 

在 Servlet 接口中，有这样几个方法：

```java
public interface Servlet {
    void init(ServletConfig var1) throws ServletException;

    ServletConfig getServletConfig();

    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    String getServletInfo();

    void destroy();
}
```

只有 `service()` 方法对于 Servlet 接口实现类有用，别的没有用，所以通过抽象类 `GenericServlet` 实现 Servlet 接口，将不使用的方法加以实现，再使用 抽象类`HttpServlet` 继承于  GenericServlet ,  降低接口实现类对接口实现的难度，将接口中不需要使用的抽象方法交给抽象类进行完成，这样接口实现类只需要对接口需要方法进行重写。

==第二步==：**重写HttpServlet父类两个方法。doGet 或者 doPost**

```java
package cn.yechen;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("MyServlet 类针对浏览器发送 GET 请求方式处理");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("MyServlet 类针对浏览器发送 POST 请求方式处理");
    }
}
```

==第三步==**：将Servlet接口实现类信息【注册】到Tomcat服务器**

设置 `webapp` 目录下的 `web.xml` 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--将Servlet接口实现类类路径地址交给Tomcat-->
    <servlet>
        <!--声明一个变量存储servlet接口实现类类路径-->
        <servlet-name>myServlet</servlet-name>
        <!--声明servlet接口实现类类路径-->
        <servlet-class>cn.yechen.MyServlet</servlet-class>
    </servlet>
    <!--为了降低用户访问Servlet接口实现类难度，需要设置简短请求别名-->
    <servlet-mapping>

        <servlet-name>myServlet</servlet-name>
        <!--设置简短请求别名,别名在书写时必须以"/"为开头-->
        <url-pattern>/myServlet</url-pattern>
    </servlet-mapping>

</web-app>
```

验证：

![image-20210304204243461](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304204243461.7avajmms9gs0.png)

![image-20210304204257322](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304204257322.1fx98jwh69s0.png)



### 四、Servlet 的生命周期

1.  **网站中所有的 Servlet 接口实现类的实例对象，只能由Http服务器负责创建。**开发人员不能手动创建Servlet接口实现类的实例对象。
2. 在==默认==的情况下，Http 服务器接收到**对于当前 Servlet 接口实现类第一次请求时自动创建这个Servlet接口实现类的实例对象**。

3. 在==手动配置==情况下，可以要求Http服务器在启动时自动创建某个 Servlet 接口实现类的实例对象。

```xml
<!--在 web.xml 文件中设置-->
<servlet>
    <!--通知Tomcat在启动时负责创建TwoServlet实例对象-->
    <load-on-startup>1</load-on-startup>
</servlet>
```

4. 在Http服务器运行期间，**一个 Servlet 接口实现类只能被创建出一个实例对象**。
5. 在Http服务器**关闭时刻**，自动将网站中**所有的 Servlet 对象进行销毁**。

**检验 默认和手动配置 情况下Http服务器对 Servlet 接口实现类对象的创建的时机：**

> 可以使用如下方法快速新建一个 Servlet 接口实现类，并重写 doGet 和 doPost 方法，并在 web.xml 文件中注册。

![image-20210304211440309](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304211440309.6y8za393sls0.png)

![image-20210304211553544](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304211553544.5hosp7zu6ds0.png)

**第一步**：在两个 Servlet 接口实现类中写上构造方法，一边我们观察对象创建的时机

```java
public class MyServlet extends HttpServlet {
    public MyServlet() {
        System.out.println("MyServlet对象被创建了。");
    }
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("MyServlet 类针对浏览器发送 GET 请求方式处理");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("MyServlet 类针对浏览器发送 POST 请求方式处理");
    }
}

public class MyServlet02 extends HttpServlet {
    public MyServlet02 () {
        System.out.println("MyServlet02对象被创建了。");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("MyServlet02 类针对浏览器发送 GET 请求方式处理");
    }

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("MyServlet02 类针对浏览器发送 POST 请求方式处理");
    }
}
```

第二步：将 MyServlet02 类在 web.xml 文件中的注册情况修改为：

```xml
<servlet>
    <servlet-name>MyServlet02</servlet-name>
    <servlet-class>cn.yechen.MyServlet02</servlet-class>
    <!--通知Tomcat在启动时负责创建TwoServlet实例对象-->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>MyServlet02</servlet-name>
    <url-pattern>/myServlet02</url-pattern>
</servlet-mapping>
```

第三步：启动 Tomcat，观察输出

![image-20210304212018094](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304212018094.5geps1oc7ok0.png)

当向浏览器输入 `http://localhost:8080/myWeb/myServlet` 时：

![image-20210304212302436](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304212302436.5mnb8z0jhag0.png)



### 五、HttpServletResponse接口

1. **介绍：**
   * `HttpServletResponse` 接口来自于 Servlet 规范中，在Tomcat 中存在于 servlet-api.jar。
   * HttpServletResponse 接口实现类由 Http 服务器负责提供。
   * HttpServletResponse 接口负责将 doGet/doPost 方法执行结果写入到【响应体】交给浏览器。
   * 开发人员习惯于将 HttpServletResponse 接口修饰的对象称为==响应对象==

2. **主要功能:**

> 将执行结果以二进制形式写入到【响应体】

**使用 IDEA 设置自动更新静态和动态资源到 Tomcat**

![image-20210304220015936](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304220015936.5gho4brugzg0.png)

```java
public class MyServlet03 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 执行结果
        String result = "Hello World";
        // 使用相应对象 response 将结果写入响应体中
        // 通过响应对象，向 Tomcat 索要输出流对象
        PrintWriter out = response.getWriter();
        //2.通过输出流，将执行结果以二进制形式写入到响应体
        out.write(result);
    }
    // doGet 方法执行完毕
    // Tomcat 将响应包推送给浏览器
}
```

执行结果：

![image-20210304220725277](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304220725277.61eq0mqjeg00.png)

**但是当需要将一个 int 类型的数据进行输出的时候，会出现问题。**

```java
/**
 * 问题描述： 浏览器接收到数据是2 ，不是50
 *
 * 问题原因：out.writer方法可以将【字符】，【字符串】，【ASCII码】写入到响应体，而数据 2 对应的 ASCII码就是 50
 *
 * 问题解决方案:  实际开发过程中，都是通过out.print()将真实数据写入到响应体
 */
public class MyServlet04 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int result = 50;
        // 获取输出流
        PrintWriter out = response.getWriter();
        // out.write(result);
        out.print(result);

    }
}
```

解决前

![image-20210304221651642](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304221651642.4qs7g1uwe5q0.png)

解决后

![image-20210304221559268](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304221559268.4k9nykxakv80.png)



> 设置响应头中 [content-type] 属性值，从而控制浏览器使用对应编译器将响应体二进制数据编译为【文字，图片，视频，命令】

```java
/**
 * 问题描述： Java<br>HTML<br>Mysql<br>
 *          浏览器在接收到响应结果时，将<br>作为文字内容在窗口展示出来，没有将<br>当做 HTML 标签命令来执行
 *          我<br>是<br>中<br>国<br>人<br>
 *          浏览器在接收到响应结果时,有有将中文编译出来，而是问号
 *
 * 问题原因：浏览器在接收到响应包之后，根据【响应头中content-type】属性的值，来采用对应【编译器】对【响应体中二进制内容】进行编译处理
 *         在默认的情况下，content-type属性的值“text” content-type="text"，此时浏览器将会采用【文本编译器】对响应体二进制数据进行解析
 *         同时使用的编码格式是 charset=ISO-8859-1，不支持中文编码。
 *
 * 解决方案：一定要在得到输出流之前，通过响应对象对响应头中content-type属性进行一次重新赋值用于指定浏览器采用正确编译器和编码格式（utf-8）。
 */
public class MyServlet05 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 将结果换行输出
        String result = "Java<br>HTML<br>Mysql<br>";
        String result2 = "我<br>是<br>中<br>国<br>人<br>";
        //设置响应头content-type
        response.setContentType("text/html;charset=utf-8");
        // 获取输出流
        PrintWriter out = response.getWriter();
        out.print(result);
        out.print(result2);
    }
}
```

设置 `content-type` 前

![image-20210304222251609](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304222251609.59vdxp900lo0.png)

设置 `content-type` 后

![image-20210304222422535](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304222422535.4fmroqf6mxs0.png)

> 设置响应头中【location】属性，将一个请求地址赋值给location.从而控制浏览器向指定服务器发送请求

```java
/**
 * 浏览器在接收到响应包之后，如果发现响应头中存在location属性,自动通过地址栏向location指定网站发送请求
 *
 * sendRedirect方法远程控制浏览器请求行为【请求地址，请求方式，请求参数】
 */
public class MyServlet06 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String url = "https://www.baidu.com/s?ie=utf-8&word=java";
        //通过响应对象，将地址赋值给响应头中location属性
        response.sendRedirect(url);
    }
}
```

**访问指定网页后会自动跳转至 location 属性指定的 url 地址**

![image-20210304223802873](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210304223802873.7likzg2x12.png)



### 六、HttpServletRequest接口

1. **介绍:**
   * `HttpServletRequest` 接口来自于 Servlet 规范中，在 Tomcat 中存在 servlet-api.jar。
   * HttpServletRequest 接口实现类由 Http 服务器负责提供。
   * HttpServletRequest 接口负责在 doGet/doPost 方法运行时**读取Http请求协议包中信息**。
   * 开发人员习惯于将HttpServletRequest接口修饰的对象称为==请求对象==
2. **作用:**

> 可以读取Http请求协议包中【请求行】信息

```java
public class MyServlet07 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.通过请求对象，读取【请求行】中【url】信息
        StringBuffer requestURL = request.getRequestURL();
        // 2.通过请求对象，读取【请求行】中【method】信息
        String method = request.getMethod();
        /*
         * 3.通过请求对象，读取【请求行】中uri信息
         *      URI：资源文件精准定位地址，在请求行并没有 URI 这个属性。
         *      实际上 URL 中截取一个字符串，这个字符串格式 "/网站名/资源文件名"
         *      URI 用于让 Http 服务器对被访问的资源文件进行定位
         */
        String requestURI = request.getRequestURI();

        // 在控制台中输出请求包中的数据
        System.out.println("URL = " + requestURL);
        System.out.println("Method = " + method);
        System.out.println("URI = " + requestURI);
    }
}
```

![image-20210305203505138](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210305203505138.36i7m2se83y0.png)



> 可以读取保存在Http请求协议包中【请求头】中请求参数信息

通过 myServlet08.html 文件中的超链接访问 myServlet08 并携带参数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <center>
        <a href="/myWeb/myServlet08?username=zhangsan&password=123456">通过超链接访问 MyServlet08 并携带请求参数</a>
    </center>
</body>
</html>
```

```java
public class MyServlet08 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.通过请求对象获得【请求头】中【所有请求参数名】
        // 将所有请求参数名称保存到一个枚举对象进行返回
        Enumeration<String> parameterNames = request.getParameterNames();
        // 编历所有参数
        while (parameterNames.hasMoreElements()) {
            // 获取参数名
            String s = parameterNames.nextElement();
            // 根据参数名，通过 request 对象获取参数值
            String parameter = request.getParameter(s);
            // 将参数信息打印到控制台
            System.out.println("参数名称：" + s + " 参数值：" + parameter);
        }

    }
}
```

![image-20210305205204283](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210305205204283.776gqm6py8k0.png)



> 可以读取保存在Http请求协议包中【请求头】或者【请求体】中请求参数信息

通过 myServlet09.html 文件中的表单以 GET 或 POST 方法访问 myServlet09 并携带参数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <center>
        <form action="/myWeb/myServlet09" method="get">
            username：<input type="text" name="username"><br><br>
            password：<input type="text" name="password"><br><br>
            <input type="submit" value="以 GET 方式访问 myServlet09">
        </form>
        <br><br><br>
        <form action="/myWeb/myServlet09" method="post">
            username：<input type="text" name="username"><br><br>
            password：<input type="text" name="password"><br><br>
            <input type="submit" value="以 POST 方式访问 myServlet09">
        </form>
    </center>
</body>
</html>
```

```java
/*
 *  问题：
 *      以 GET 方式发送中文参数时，得到正常结果
 *      以 POST 方式发送中文参数时，得到【乱码】“è?????????????·???”
 *
 *  原因:
 *      浏览器以 GET 方式发送请求,请求参数保存在【请求头】,在 Http 请求协议包到达 Http 服务器之后，第一件事就是进行解码
 *      请求头二进制内容由 Tomcat 负责解码，Tomcat9.0 默认使用 【utf-8】 字符集，可以解释一切国家文字
 *
 *      浏览器以 POST 方式发送请求，请求参数保存在【请求体】,在 Http 请求协议包到达 Http 服务器之后，第一件事就是进行解码
 *      请求体二进制内容由当前请求对象（request）负责解码。request默认使用 【ISO-8859-1】字符集，一个东欧语系字符集
 *      此时如果请求体参数内容是中文，将无法解码只能得到乱码
 *
 *  解决方案:
 *      在Post请求方式下，在读取请求体内容之前，应该通知请求对象使用 【utf-8】 字符集对请求体内容进行一次重新解码
 *
 *
 */
public class MyServlet09 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 通知请求对象使用 【utf-8】 字符集对请求体内容进行一次重新解码
        request.setCharacterEncoding("utf-8");
        // 1.通过请求对象获得【请求头】中【所有请求参数名】
        // 将所有请求参数名称保存到一个枚举对象进行返回
        Enumeration<String> parameterNames = request.getParameterNames();
        while (parameterNames.hasMoreElements()) {
            String s = parameterNames.nextElement();
            String parameter = request.getParameter(s);
            System.out.println("参数名称：" + s + " 参数值：" + parameter);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.通过请求对象获得【请求头】中【所有请求参数名】
        // 将所有请求参数名称保存到一个枚举对象进行返回
        Enumeration<String> parameterNames = request.getParameterNames();
        while (parameterNames.hasMoreElements()) {
            String s = parameterNames.nextElement();
            String parameter = request.getParameter(s);
            System.out.println("参数名称：" + s + " 参数值：" + parameter);
        }
    }
}
```

修改前：

![image-20210305210601569](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210305210601569.6pxwu1mbvmw.png)

修改后：

![image-20210305211014593](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210305211014593.219v74ufx1ls.png)



> 可以代替浏览器向Http服务器申请资源文件调用





### 七、欢迎资源文件

1. **存在原因：**用户可以记住网站名，但是不会记住网站资源文件名。
2. **默认欢迎资源文件：**用户发送了一个针对某个网站的【默认请求】`http://localhost:8080/myWeb`时，此时由 Http 服务器会自动从当前网站返回的资源文件 `index.html` ，相当于请求 `http://localhost:8080/myWeb/index.html`
3. **Tomcat对于默认欢迎资源文件定位规则：**`D:\Environmental\Tomcat\apache-tomcat-9.0.41\conf\web.xml`

```xml
<!-- ==================== Default Welcome File List ===================== -->
  <!-- When a request URI refers to a directory, the default servlet looks  -->
  <!-- for a "welcome file" within that directory and, if present, to the   -->
  <!-- corresponding resource URI for display.                              -->
  <!-- If no welcome files are present, the default servlet either serves a -->
  <!-- directory listing (see default servlet configuration on how to       -->
  <!-- customize) or returns a 404 status, depending on the value of the    -->
  <!-- listings setting.                                                    -->
  <!--                                                                      -->
  <!-- If you define welcome files in your own application's web.xml        -->
  <!-- deployment descriptor, that list *replaces* the list configured      -->
  <!-- here, so be sure to include any of the default values that you wish  -->
  <!-- to use within your application.                                       -->

	<!--这是Tomcat默认的会寻找的三个欢迎资源文件-->
	<!--如果这三个资源不存在，同时在当前项目中没有自己设置欢迎资源文件，就会返回状态码 404（资源未找到）-->
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
```

4. **网站设置自定义默认文件定位规则，此时Tomcat自带定位规则将失效**

在当前项目的  `webapp/WEB_INF/web.xml` 文件中设置自定义默认欢迎资源文件。 

```xml
<welcome-file-list>
    <welcome-file>user_login.html</welcome-file>
</welcome-file-list>
```



### 八、HTTP 状态码

1. **介绍:**
   * 由**三位数字组成**的一个符号。
   * Http 服务器在推送响应包之前，根据本次请求处理情况将 Http ==状态码写入到响应包中状态行上==。
   * 通过返回的状态码，浏览器可以可以输出不同结果：
     * 如果 Http 服务器针对本次请求，**返回了**对应的资源文件，**就通过 Http 状态码通知浏览器应该如何处理这个结果。**
     * 如果 Http 服务器针对本次请求，**无法返回**对应的资源文件，**就通过 Http 状态码向浏览器解释不能提供服务的原因。**

2. **组成：100---599；分为5个大类**
3. **1XX：**最有特征是是 `100` ，==通知浏览器本次返回的资源文件并不是一个独立的资源文件==，需要浏览器在接收响应包之后，继续向 Http 服务器索要依赖的其他资源文件

4. **2XX：**最有特征 `200` ， ==通知浏览器本次返回的资源文件是一个完整独立资源文件==，浏览器在接收到之后不需要所要其他关联文件。
5. **3XX：** 最有特征 `302` ，==通知浏览器本次返回的不是一个资源文件内容而是一个资源文件地址==，需要浏览器根据这个地址自动发起请求来索要这个资源文件。

```java
// 如：
response.sendRedirect("资源文件地址");
// 写入到响应头中 location
// 而这个行为导致Tomcat将302状态码写入到状态行
```

```java
public class Servlet_302 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.sendRedirect("http://www.baidu.com");
    }
}
// Tomcat在推送响应包之前，看到响应体是空，但是响应头location却存放了一个地址。
// 此时Tomcat将302状态码写入到状态行。
// 在浏览器接收到响应包之后，因为302状态码，浏览器不会读取响应体内容，自动根据响应头中location的地址发起第二次请求
```

![image-20210306214424273](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210306214424273.4j0ynxpu0a20.png)

6. **4XX：** `404` ，==通知浏览器，由于在服务端没有定位到被访问的资源文件因此无法提供帮助==

   ​			  `405` ， 通知浏览器，在服务端已经定位到被访问的资源文件（Servlet）==但是这个Servlet对于浏览器采用的请求方式不能处理==

```java
// 只能针对浏览器发送POST请求方式进行处理，无法对GET方式进行处理
// 但是浏览器通过地址栏发送的请求一定是 GET，由于该 Servlet 中没有 GET 方法
// 因此这个 Servlet 对于浏览器采用的请求方式不能处理
public class Servlet_405 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}
```

![image-20210306215246663](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210306215246663.6cbar3vqnjk0.png)

7. **5XX：** `500` ，通知浏览器，在服务端已经定位到被访问的资源文件（Servlet），这个Servlet可以接收浏览器采用请求方式，==但是Servlet在处理请求期间，由于**Java异常导致**处理失败==

```java
public class Servlet_500 extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 模拟一个空指针异常
        Map map = new HashMap();
        int i = (int) map.get("key");
        System.out.println(i);
    }
}
```

![image-20210306215759387](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210306215759387.49v7g8407os0.png)

### 九、多个Servlet之间调用规则

1. **前提条件：** 某些来自于浏览器发送请求，往往需要**服务端中多个 Servlet 协同处理**。但是浏览器一次只能访问一个 Servlet，**导致用户需要手动通过浏览器发起多次请求才能得到服务**。这样增加用户获得服务难度，导致用户放弃访问当前网站
2. **提高用户使用感受规则：**  无论本次请求涉及到多少个Servlet,用户**只需要手动通知浏览器发起 一次请求即可**
3. **多个Servlet之间调用规则：**
   1. ==重定向解决方案==
   2. ==请求转发解决方案==



### 十、重定向解决方案

1. **工作原理：**  用户第一次**通过手动方式通知浏览器访问 OneServlet**。 OneServlet 工作完毕后，将 TwoServlet地址写入到响应头` locatio` 属性中，导致Tomcat将302状态码写入到状态行。

   在浏览器接收到响应包之后，会读取到 302 状态。此时浏览器自动根据响应头中 location 属性地址发起第二次请求，访问 TwoServlet 去完成请求中剩余任务

2. **实现命令：**

```java
// 将地址写入到响应包中响应头中location属性
response.sendRedirect("请求地址");
```

3. **特征：**  

   > （1）请求地址：
   >
   > ​			既可以把当前网站内部的资源文件地址发送给浏览器 （/网站名/资源文件名）
   >
   > ​			也可以把其他网站资源文件地址发送给浏览器(http://ip地址:端口号/网站名/资源文件名)	     

   > （2）请求次数：
   >
   > ​			浏览器至少发送两次请求，但是只有第一次请求是用户手动发送。后续请求都是浏览器自动发送的。

   > （3）请求方式：
   >
   > ​			重定向解决方案中，**通过地址栏通知浏览器发起下一次请求**，因此通过重定向解决方案调用的资源文件接收的请求方式一定是 `GET`

   > （4）缺点:
   >
   > ​			重定向解决方案需要在浏览器与服务器之间进行多次往返，**大量时间消耗在往返次数上，增加用户等待服务时间**



### 十一、请求转发解决方案

1. **原理：**  用户第一次通过手动方式要求浏览器访问 OneServlet。OneServlet 工作完毕后，==通过当前的请求对象（request）代替浏览器向 Tomcat 发送请求，申请调用 TwoServlet。==Tomcat 在接收到这个请求之后，自动调用 TwoServlet 来完成剩余任务

2. **实现命令：**  

```java
// 1.通过当前请求对象生成资源文件申请报告对象
RequestDispatcher  report = request.getRequestDispatcher("/资源文件名");// 一定要以"/"为开头
// 2.将报告对象发送给Tomcat
report.forward(当前请求对象，当前响应对象);
```

3. **特征：**  

	> （1）请求次数：
   >
   > ​			在请求转发过程中，浏览器**只发送一次请求**

   > （2）请求地址：
   >
   > ​			只能向 Tomcat 服务器申请调用**当前网站下资源文件地址**
   > ​		   `request.getRequestDispathcer("/资源文件名")` 
   >
   > ​			==不要写网站名==

   > （3）请求方式：
   >
   > ​			在请求转发过程中，浏览器只发送一个了个 Http 请求协议包。**参与本次请求的所有Servlet共享同一个请求协议包**，因此这些Servlet接收的请求方式与浏览器发送的请求方式保持一致。

   > （4）优点：
   >
   > ​			无论本次请求涉及到多少个Servlet,用户只需要手动通过浏览器发送一次请求。
   >
   > ​			Servlet 之间调用发生在服务端计算机上，**节省服务端与浏览器之间往返次数增加处理服务速度**

```java
public class Servlet05 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("通过转发解决方案调用 servlet06");
        // 1.通过当前请求对象生成资源文件申请报告对象
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/servlet06");
        // 2.将报告对象发送给Tomcat
        requestDispatcher.forward(request, response);
    }
}
```

```java
public class Servlet06 extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("servlet06 被调用了！");
    }
}
```

![image-20210306222328340](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210306222328340.6z4s7wrnx540.png)



### 十二、多个Servlet之间数据共享实现方案

1. **数据共享：**OneServlet 工作完毕后，将产生数据交给 TwoServlet 来使用，两个 Servlet 之间共享数据。
2. **共享方案：**
   * `ServletContext` 接口
   * `Cookie` 类
   * `HttpSession` 接口
   * `HttpServletRequest` 接口



### 十三、ServletContext 接口

1. **介绍：**

> （1）来自于 Servlet 规范中一个接口。在 Tomcat 中存在于 servlet-api.jar，在 Tomcat 中负责提供这个接口实现类。
>
> （2）如果**两个 Servlet 来自于同一个网站**，彼此之间通过网站的 ServletContext 实例对象实现数据共享。
>
> （3）开发人员习惯于将 ServletContext 对象称为【**全局作用域对象**】

2. **工作原理：**   **每一个网站都存在一个（也只有一个）全局作用域对象**。这个全局作用域对象相当于一个Map。在这个网站中 OneServlet 可以将一个数据存入到全局作用域对象，当前网站中其他 Servlet 此时都可以从全局作用域对象得到这个数据进行使用。

![image-20210307105906290](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210307105906290.6ymnzsfrbtc0.png)

3. **全局作用域对象生命周期：**  
   * 在 Http 服务器启动过程中，自动为当前网站在内存中创建一个全局作用域对象。
   * 在 Http 服务器运行期间，一个网站只有一个全局作用域对象。
   * 在 Http 服务器运行期间，全局作用域对象一直处于存活状态。
   * 在 Http 服务器准备关闭的时候，Http 服务器负责将当前网站中的全局作用域对象进行销毁处理。

> **全局作用域对象的生命周期贯穿于网站的整个运行期间。**

4. **实现命令：**  ==前提是两个 Servlet 存在于一个网站中==

```java
// 添加数据
OneServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 通过 请求对象（request）向 Tomcat 索要当前网站中的 全局作用域对象
        ServletContext application = request.getServletContext();
        // 以（“key”，“value”）的形式将数据添加到全局作用域对象中，作为共享数据
        application.setAttribute("key1", "values1");
    }
}

// 获取数据
TwoServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 通过 请求对象（request）向 Tomcat 索要当前网站中的 全局作用域对象
        ServletContext application = request.getServletContext();
        // 通过 key 获取全局作用域对象中的对应的 value
        Object value = applicaton.getAttribute("key1");
    }
}
```

5. **实际使用：**

```java
public class InputServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 通过 请求对象（request）向 Tomcat 索要当前网站中的 全局作用域对象
        ServletContext application = request.getServletContext();
        // 以（“key”，“value”）的形式将数据添加到全局作用域对象中，作为共享数据
        application.setAttribute("key1", "我是从 InputServlet 中传递过去的数据！");
    }
}


public class OutputServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 通过 请求对象（request）向 Tomcat 索要当前网站中的 全局作用域对象
        ServletContext application = request.getServletContext();
        // 通过 key 获取对应 value
        Object value = application.getAttribute("key1");
        System.out.println(value);
    }
}
```

先访问 InputServlet 在访问 OutputServlet，输出：

![image-20210307112013198](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210307112013198.17l8iv55ki74.png)





### 十四、Cookie

1. **介绍：**  

> （1）Cookie 是来自于 Servlet 规范中的一个工具类，存在于 Tomcat 提供的 servlet-api.jar 中。
>
> （2）如果两个 Servlet 来自于同一个网站，并且为同一个浏览器（用户）提供服务，此时借助 Cookie 对象进行数据共享。
>
> （3）**Cookie 存放当前用户的私人数据**，在共享数据过程中提高服务质量。
>
> （4）在现实生活场景中， Cookie 相当于用户在服务端得到【会员卡】

2. **原理：**  用户通过浏览器第一次向 【MyWeb】 网站发送请求申请 OneServlet。==OneServlet在运行期间创建一个Cookie存储与当前用户相关数据==。OneServlet工作完毕后，==将Cookie写入到响应头交还给当前浏览器。浏览器收到响应响应包之后，将cookie存储在浏览器的缓存==。一段时间之后，用户通过【同一个浏览器】再次向【myWeb网站】发送请求申请 TwoServlet 时。==浏览器需要无条件的将myWeb网站之前推送过来的Cookie，写入到请求头发送过去==，此时 TwoServlet 在运行时，就可以通过读取请求头中 cookie 中信息，得到OneServlet提供的共享数据。
3. **实现命令：**   同一个网站 OneServlet 与  TwoServlet 借助于 Cookie 实现数据共享

```java
OneServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 创建一个 cookie 对象，保存当前用户的共享数据
        Cookie cookie1 = new Cookie("key1", "abc");
        Cookie cookie2 = new Cookie("key2", "def");
        // cookie 相当于一个 map，只能存放键值对，并且键值对的类型只能是 String,键值对中的 key 不能是中文
        // 将 cookie 写入到响应头中，传给浏览器
        response.addCookie(cookie1);
        response.addCookie(cookie2);
    }
}

// OneServlet 执行结束后，将 cookie 信息存储在浏览器的缓存中，当浏览器请求访问 TwoServlet 是，浏览器将缓存中的 cookie 信息取出放入请求包中

TwoServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 调用请求对象从请求头中得到的浏览器返回的 cookie 对象
        Cookie[] cookieArray = request.getCookies();
        // 循环编历数据得到每一个 cookie 的 key 和 value
        for (Cookie cookie : cookieArray) {
            // 读取 key
            String key = cookie.getName();
            // 读取 value
            String value = cookie.getValue();
        }
    }
}
```

4. **Cookie销毁时机：**  
   * 在默认情况下，Cookie 对象存放在浏览器的缓存中。因此只要浏览器关闭，Cookie 对象就被销毁掉。
   * **在手动设置情况下，可以要求浏览器将接收的 Cookie 存放在客户端计算机上硬盘上，同时需要指定Cookie 在硬盘上存活时间**。在存活时间范围内，关闭浏览器，关闭客户端计算机，关闭服务器，都不会导致 Cookie 被销毁。在存活时间到达时，Cookie自动从硬盘上被删除。

```java
cookie.setMaxAge(60); //cookie在硬盘上存活1分钟
```

5. **实际使用：**

```java
public class OutputCookieServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 创建一个 cookie 对象，保存当前用户的共享数据
        Cookie cookie1 = new Cookie("key1", "abc");
        Cookie cookie2 = new Cookie("key2", "def");
        // cookie 相当于一个 map，只能存放键值对，并且键值对的类型只能是 String,键值对中的 key 不能是中文
        // 将 cookie 写入到响应头中，传给浏览器
        response.addCookie(cookie1);
        response.addCookie(cookie2);
    }
}
```

![image-20210309200412332](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210309200412332.6jthf5uuxgg0.png)

```java
public class InputCookieServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 调用请求对象从请求头中得到的浏览器返回的 cookie 对象
        Cookie[] cookieArray = request.getCookies();
        // 循环编历数据得到每一个 cookie 的 key 和 value
        for (Cookie cookie : cookieArray) {
            // 读取 key
            String key = cookie.getName();
            // 读取 value
            String value = cookie.getValue();
            System.out.println("key = " + key + " value = " + value);
        }
    }
}
```



![image-20210309200545967](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210309200545967.4ztj5cbh3540.png)

![image-20210309200708748](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210309200708748.9fm9b4rnr0w.png)



### 十五、HttpSession 接口

1. **介绍：**  

> （1）HttpSession 接口来自于 Serlvet 规范下的一个接口。存在于 Tomcat 中 servlet-api.jar 中。
>
> （2）如果两个 Servlet 来自于同一个网站，并且为同一个浏览器对象（用户）提供服务，此时借助 HttpSession对象进行数据共享。
>
> （3）开发人员习惯将 HttpSession 接口修饰的对象称为 ==会话作用域对象==

2. **==面试题== HttpSession 和 Cookie 区别：**
* 存储位置：一个在天上，一个在地上
     * Cookie：存放在客户端计算机（浏览器的内存或者硬盘）中。
     * HttpSession：存放再服务端计算机的内存中。
   * 数据类型：
     * Cookie：存储的共享数据类型只能是 String。
     * HttpSession：存储的共享数据可以是任意类型的数据（Object）。
   
* 数据数量：
     * Cookie：一个 Cookie 对象只能存储一个共享数据。
     * HttpSession：使用 Map 集合存储共享数据，所以可以存储任意数量的共享数据。
   * 参照物：
     * Cookie：相当于客户在客户端的 ==会员卡==
     * HttpSession：相当于客户在服务端的 ==私人保险柜==
   
3. **实现命令：**  同一个网站下 OneServlet 将数据传递给 TwoServlet

```java
OneServlet {
    public void doGet(HttpServletReqiest request, HttpServletResponse response) {
        // 调用请求对象向 Tomcat 索要当前用户在服务端的私人储物柜
        HttpSession session = request.getSession();
        // 将数据添加到用户的私人存储柜
        session.setAttibute("key", "abc");
    }
}

TwoServlet {
    public void doGet(HttpServletReqiest request, HttpServletResponse response) {
        // 调用请求对象向 Tomcat 索要当前用户在服务端的私人储物柜
        HttpSession session = request.getSession();
        // 将数据添加到用户的私人存储柜
        Object value = session.getAttribute("key");
    }
}
```

4. **Http 服务器如何将用户与 HttpSession 关联起来：**  ==使用 Cookie==

   Tomcat 在创建一个 HttpSession 对象的时候，自动为这个 HttpSession 对象生成一个**唯一的编号**， Tomcat 将编号存储为 Cookie 对象，**key 为 JSESSIONID，value 为 唯一编号**，推送到浏览器缓存，当用户第二次来访问的时候，Tomcat 根据请求头中的 JSESSIONID 确认用户是否有 HttpSession，以及哪一个 HttpSession 是当前用户。

   ![image-20210310204203874](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210310204203874.7ejbzrl4p5g0.png)

5. `getSession()`  与  `getSession(false)` 的区别

   * getSession()：

     如果当前用户在服务端中**已经存在了 HttpSession 对象（私人储物柜）**，要求 Tomcat 将这个私人储物柜进行**返回**。

     如果当前用户在服务端中**尚未有 HttpSession 对象（私人储物柜）**，要求 Tomcat 为当前用户==创建一个全新的 HttpSession 对象并返回==。

   * getSession(false)：

     如果当前用户在服务端中**已经存在了 HttpSession 对象（私人储物柜）**，要求 Tomcat 将这个私人储物柜进行**返回**。

     如果当前用户在服务端中**尚未有 HttpSession 对象（私人储物柜）**，==此时该方法返回 null，不会创建新的 HttpSession 对象返回==。

6. **HttpSession销毁时机：**  

   * 用户与 HttpSession 关联时使用的 Cookie 只能存放在浏览器的缓存中，在浏览器关闭的时候，缓存删除，Cookie 对象被销毁，用户和 HttpSession 对象之间的联系被切断，由于 Tomcat 无法检测浏览器何时关闭，因此浏览器关闭时 Tomcat 并不会将浏览器关联的 HttpSession 对象销毁。

   * Tomcat 为每一个 HttpSession 对象设置 ==空闲时间==，默认为 **30分钟**，当当前的 HttpSession 对象空闲时间到达 30 分钟，Tomcat 就会销毁这个对象。

     * **可以自己手动设置 HttpSession 空闲时间：**  

       在当前网站 / webapps / WEB_INFO / web.xml 文件中添加

     ```xml
     <session-config>
         <!--设置当前网站中每一个 HttpSession 对象的空闲时间为 5分钟-->
     	<session-timeout>5</session-timeout>
     </session-config>
     ```
   
7. **实际操作：**

   `index.html`：商品展示页面（网站首页）

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
       <table border="2" align="center">
           <tr>
               <td>商品名称</td>
               <td>商品单价</td>
               <td>供货商</td>
               <td>加入购物车</td>
           </tr>
           <tr>
               <td>华为笔记本pro13</td>
               <td>7000</td>
               <td>华为</td>
               <td>
                   <a href="/myWeb/one?goodsName=华为笔记本pro13">加入购物车</a>
               </td>
           </tr>
           <tr>
               <td>小米手机11</td>
               <td>5000</td>
               <td>小米</td>
               <td>
                   <a href="/myWeb/one?goodsName=小米手机11">加入购物车</a>
               </td>
           </tr>
           <tr>
               <td>MacBookPro</td>
               <td>11000</td>
               <td>Apple</td>
               <td>
                   <a href="/myWeb/one?goodsName=MacBookPro">加入购物车</a>
               </td>
           </tr>
           <tr align="center">
               <td colspan="4">
                   <a href="/myWeb/two">查看我的购物车</a>
               </td>
           </tr>
       </table>
   </body>
   </html>
   ```

   效果图：

   ![image-20210310210117263](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210310210117263.38dutp7w9s20.png)

   `OneServlet`：将商品加入购物车

   ```java
   public class OneServlet extends HttpServlet {
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           // 调用请求对象，读取e请求头参数，得到用户选择商品名
           String goodsName = request.getParameter("goodsName");
           // 调用请求对象，向Tomcat索要当前用户在服务端的私人储物柜
           HttpSession session = request.getSession();
           // 将用户选购商品添加到当前用户私人储物柜
           // 获取 session 对象中 key 为 goodsName 的 value
           Integer goodsNum = (Integer) session.getAttribute(goodsName);
           // 两种情况
           if (goodsNum == null) {
               // 当购物车中没有当前商品时
               session.setAttribute(goodsName, 1);
           } else {
               // 当前购物车中已经有当前商品，对商品数量 +1
               session.setAttribute(goodsName, goodsNum + 1);
           }
   
       }
   }
   ```

   `TwoServlet`：查看我的购物车

   ```java
   public class TwoServlet extends HttpServlet {
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           // 调用请求对象，向 Tomcat 索要当前用户在服务端私人储物柜
           HttpSession session = request.getSession();
           // 将 session 中所有的 key 读取出来，存放一个枚举对象
           Enumeration<String> attributeNames = session.getAttributeNames();
   
           // 获取向输出流获取对象
           response.setContentType("text/html;charset=utf-8");
           PrintWriter out = response.getWriter();
           while (attributeNames.hasMoreElements()) {
               String goodsName = attributeNames.nextElement();
               int goodsNum = (int) session.getAttribute(goodsName);
               out.println("<font style=\"color:red; font-size:40px\">商品名称：" + goodsName + "&nbsp&nbsp&nbsp商品数量：" + goodsNum + "</font><br>");
           }
       }
   }
   ```

   

### 十六、HttpServletResquest 接口实现数据共享

1. **介绍：**  

> （1）在同一个网站中，如果两个 Servlet 之间通过【**请求转发**】方式进行调用，彼此之间共享同一个请求协议包。而一个请求协议包只对应一个请求对象，因此 Servlet 之间共享同一个请求对象，此时可以利用这个请求对象在两个 Servlet 之间实现数据共享
>
> （2）在请求对象实现 Servlet 之间数据共享功能时，开发人员将请求对象称为【**请求作用域对象**】

2. **命令实现：**   OneServlet通过请求转发申请调用TwoServlet时，需要给TwoServlet提供共享数据

```java
OneServlet {
	public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 将数据添加到【请求作用域对象】中
        request.setAttribute("key", "abc");
        // 向 Tomcat 申请调用 TwoSevlet
        request.getRequestDispatcher("/two").forword(request, response);
    }    
}

TwoServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response) {
        // 从当前请求对象得到从 OneServelt 写入的共享数据
        Object value = request.getAttribute("key");
    }  
}
```



### 十八、监听器接口

1. **介绍：** 

> （1）一组来自于 Servlet 规范下接口，共有 8 个接口。在 Tomcat 存在 servlet-api.jar 包。
>
> （2）**监听器接口需要由开发人员亲自实现**，Http 服务器提供 jar 包并没有对应的实现类。
>
> （3）监听器接口用于监控【**作用域对象生命周期变化时刻**】以及【**作用域对象共享数据变化时刻**】

2. **作用域对象：**  

   * 在 Servlet 规范中，认为**在服务端内存中**可以在某些条件下为两个 Servlet 之间提供**数据共享方案的对象**，被称为==作用域对象==。
   * **Servlet规范下作用域对象：**
     * `ServletContext` ：全局作用与对象；
     * `HttpSession` ：会话作用域对象；
     * `HttpServletRequest` ：请求作用域对象；

3. **监听器接口实现类开发规范（三步）：**  

   1. 根据监听的实际情况，选择对应的监听器接口进行实现。

   2. 重写监听器接口中的监听事件处理方法。

   3. 在 web.xml 文件中将监听器实现类注册到 Http 服务器。

      ```xml
      <listener>
      	<!--将监听器实现类注册到 Http 服务器-->
          <listener-class>监听器实现类的完整类名</listener-class>
      </listener>
      ```

      

4. `ServletContextListener` 接口：

   * **作用：** 通过这个接口合法的监测全局作用域对象**被初始化的时刻以及被销毁的时刻**。

   * **监听事件处理方法：**  

     ```java
     // 在全局作用域对象被 Http 服务器初始化时被调用
     public void contextInitialized(ServletContextEvent sce) {
     
     }
     
     // 在全局作用域对象被 Http 服务器销毁的时候触发调用
     public void contextDestroyed(ServletContextEvent sce) {
     
     }
     ```

5. `ServletContextAttributeListener` 接口：

   * **作用：**  通过这个接口合法的检测全局作用域对象**共享数据变化时刻**。

   * **监听事件处理方法：**  

     ```java
     // 在全局作用域对象添加共享数据时被调用
     public void attributeAdded(ServletContextAttributeEvent event) {
     
     }
     
     // 在全局作用域对象更新共享数据时被调用
     public void attributeRemoved(ServletContextAttributeEvent event) {
     
     }
     
     // 在全局作用域对象删除共享数据时被调用
     public void attributeReplaced(ServletContextAttributeEvent event) {
     
     }
     
     // 全局作用域对象添加、更新、删除共享数据的方法
     ServletContext application = request.getServletContext();
     // 添加
     application.setAttribute("key", 100);
     // 更新
     application.setAttribute("key", 200);
     // 删除
     application.removeAttribute("key");
     ```

     



### 十九、过滤器接口（Filter）

1. **介绍：**  

> （1）来自于 Servlet 规范下的接口，在 Tomcat 中存在于 servlet-api.jar 包。
>
> （2）Filter 接口实现类由开发人员负责提供，Http 服务器不负责提供。
>
> （3）Filter 接口在 Http 服务器调用资源文件之前，对 Http 服务器进行拦截。

2. **具体作用：**  
   * ==拦截 Http 服务器，帮助 Http 服务器检测当前请求合法性==
   
```java
   // 编写一个类继承 Filter，重写 doFilter 方法
   public class MyFilter implements Filter {
       @Override
       public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
           // 通过拦截请求对象得到请求包参数信息，从而得到访问用户的真实年龄
           String age = servletRequest.getParameter("age");
           // 根据年龄，帮助 Http 服务器来判断本次请求的合法性
           if (Integer.parseInt(age) <= 75) {
               // 将拦截的请求对象和相应对象交还给 Tomcat，由 Tomcat 继续调用资源文件
               filterChain.doFilter(servletRequest, servletResponse);
           } else {
               // 过滤器代替 Http 服务器拒绝本次请求
               servletResponse.setContentType("text/html;charset=utf-8");
               PrintWriter out = servletResponse.getWriter();
               out.println("<center><font style='color:red;font-size:40px'>大爷，珍爱生命啊!</font></center>");
           }
       }
   }
```

   将过滤器注册到 `web.xml` 文件中

   ```xml
   <!--将过滤器类文件路径交给 Tomcat-->
   <filter>
       <filter-name>myFilter</filter-name>
       <filter-class>cn.yechen.fliter.MyFilter</filter-class>
   </filter>
   <!--通知 Tomcat 在调用何种资源文件时需要被当前过滤器拦截-->
   <filter-mapping>
       <filter-name>myFilter</filter-name>
       <url-pattern>/mm.jpg</url-pattern>
   </filter-mapping>
   ```

   * ==拦截 Http 服务器，对当前请求进行增强操作==

因为通过 POST 请求方式获取的资源保存在请求体中，请求对象在解析数据的时候默认采用 `iso-8859-1` ，这是一种东欧字符集，不支持中文。所以每次使用 POST 请求时都要设置请求对象的编码格式，**可以使用过滤器方式对编码方式进行设置，简化代码**。

   **控制浏览器以 POST 方式发起请求**

   ```html
   <form action="/myWeb/one" method="post">
       <table align="center">
           <tr>
               <td>用户名</td>
               <td><input type="text" name="username"></td>
               <td><input type="submit" value="以 POST 方式提交"></td>
           </tr>
       </table>
   </form>
   <form action="/myWeb/two" method="post">
       <table align="center">
           <tr>
               <td>用户名</td>
               <td><input type="text" name="username"></td>
               <td><input type="submit" value="以 POST 方式提交"></td>
           </tr>
       </table>
   </form>
   ```

   **两个 Servlet**

   ```java
   public class OneServlet extends HttpServlet {
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           // 直接从【请求对象】中取出请求参数
           String username = request.getParameter("username");
           System.out.println("OneServelt 从请求体得到参数 "+ username);
       }
   }
   ```

   ```
   public class TwoServlet extends HttpServlet {
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           // 直接从【请求对象】中取出请求参数
           String username = request.getParameter("username");
           System.out.println("TwoServelt 从请求体得到参数 "+ username);
       }
   }
   ```

   **过滤器，对所有资源进行排查，将字符集设置为 utf-8**

   ```java
   public class MyFilter02 implements Filter {
       @Override
       public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
           // 通知拦截的请求对象，使用 UTF-8 字符集对当前请求体信息进行一次重新编辑
           servletRequest.setCharacterEncoding("utf-8");
           // 将【请求对象】和 【相应对象】重新交给 Tomcat
           filterChain.doFilter(servletRequest, servletResponse);
       }
   }
   ```

   **将 Servlet 和 过滤器注册到 web.xml 文件中**

   ```xml
   <servlet>
       <servlet-name>OneServlet</servlet-name>
       <servlet-class>cn.yechen.controller.OneServlet</servlet-class>
   </servlet>
   <servlet-mapping>
       <servlet-name>OneServlet</servlet-name>
       <url-pattern>/one</url-pattern>
   </servlet-mapping>
   <servlet>
       <servlet-name>TwoServlet</servlet-name>
       <servlet-class>cn.yechen.controller.TwoServlet</servlet-class>
   </servlet>
   <servlet-mapping>
       <servlet-name>TwoServlet</servlet-name>
       <url-pattern>/two</url-pattern>
   </servlet-mapping>
   <!--将过滤器类文件路径交给 Tomcat-->
   <filter>
       <filter-name>myFilter02</filter-name>
       <filter-class>cn.yechen.fliter.MyFilter02</filter-class>
   </filter>
   <!--通知 tomcat 在调用所有资源文件之前都需要调用 MyFilter02 进行拦截-->
   <filter-mapping>
       <filter-name>myFilter02</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
   ```

![image-20210313221847093](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/image-20210313221847093.2n0k1upx3v80.png)

3. **Filter接口实现类开发步骤：（三步）**  
   
   * 创建一个 java 类实现 Filter 接口。
   * 重写 Filter 接口中的 doFilter 方法。
   * 在 web.xml 文件中将过滤器注册到 Http 服务器中。
   
4. **Filter拦截地址格式：** 

   * 命令格式：

   ```xml
   <filter>
       <filter-name>过滤器对象名称</filter-name>
       <filter-class>过滤器完整类名</filter-class>
   </filter>
   <!--拦截地址通知Tomcat在调用何种资源文件之前需要调用OneFilter过滤进行拦截-->
   <filter-mapping>
       <filter-name>过滤器对象名称</filter-name>
       <url-pattern>/拦截地址</url-pattern>
   </filter-mapping>
   ```

   * 要求 Tomcat 在调用==某一个具体文件==之前，来调用 过滤器 拦截：

   ```xml
   <url-pattern>拦截的文件的具体地址</url-pattern>
   ```

   * 要求Tomcat在调用==某一个文件夹下所有的资源文件==之前，来调用 过滤器 拦截：

   ```xml
   <url-pattern>/文件夹/*</url-pattern>
   ```

   * 要求 Tomcat 在调用==任意文件夹下某种类型文件==之前，来调用 过滤器 拦截：

   ```xml
   <url-pattern>*.jpg</url-pattern>
   ```

   * 要求 Tomcat 在调用==网站中任意文件==时，来调用 过滤器 拦截：

   ```xml
   <url-pattern>/*</url-pattern>
   ```

   

## 互联网通信流程图

![第三版互联网通信流程图](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210424/第三版互联网通信流程图.6ihflst0vho0.png)


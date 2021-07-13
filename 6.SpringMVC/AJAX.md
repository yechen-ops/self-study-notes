## 使用 AJAX 的局部刷新
`局部刷新：` 浏览器在展示数据时，此时在窗口既可以看到本次的响应数据， 同时又可以看到浏览

器内存中原有数据 

`局部刷新原理：`

1. 不能由浏览器发送请求给服务端。

2. 浏览器委托浏览器内存中一个脚本对象（`XMLHttpRequest`）代替浏览器发送请求。

3. 这个行为导致导致服务端直接将【响应包】发送脚本对象内存中。

4. 这个行为导致脚本对象内容被覆盖掉，但是此时浏览器内存中绝大部分内容没有收

   到任何影响。

5. 这个行为导致浏览器在展示数据时候,同时展示原有数据和响应数据。

`AJAX`（Asynchronous JavaScript and XML）（异步的 javascript 和 XML）

* 目前 XML 已经使用 JSON 作为替换

### 使用异步对象的四个步骤

新建  jsp，使用 `XMLHttpRequest` 对象。

#### 一、创建异步对象

```javascript
let xmlHttp = new XMLHttpRequest();
```

#### 二、绑定事件

```JavaScript
xmlHttp.onreadystatechange = function () {
    if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
		// 获取服务端响应的数据
    }
}
```

`readState属性:` AJAX 请求过程中状态的变化 

* 0：请求未初始化，创建异步请求对象，var xmlHttp = new XMLHttpRequest();
* 1：初始化异步请求对象，xmlHttp.open(请求方式，请求地址，true);
* 2：异步对象发送请求，xmlHttp.send();
* 3：异步对象接受从服务端返回的应答数据，在 XMLHttpRequest 内部处理。
* 4：异步请求对象已经将数据解析完毕，此时可以读取数据。

`status属性：`  网络通信状态

* 200：通信成功，请求成功。
* 404：资源没有找到。

获取服务端响应的数据，可以使用 `XMLHttpRequest` 对象的属性

`responseText：` 获得字符串形式的相应数据。

`responseXML：` 获得 XML 形式的相应数据。 

#### 三、初始异步对象

```javascript
let url = "?id="+document.getElementById("proid").value;
xmlHttp.open("get", "queryProvinceServlet"+url, true);
// open() 方法的三个参数
// 第一个参数：请求方法，“GET” 或 “POST”
// 第二个参数：请求的地址（URL）
// 第三个参数：是否使用异步的方式发起请求，true 表示使用异步，false 表示使用同步
```

`异步： `在 send 方法执行之后执行其他代码，可以同时执行多个异步请求

`同步： `一次只能执行一个异步请求，必须请求处理完成之后，才能执行其他的请求处理

#### 四、发送请求

```javascript
xmlHttp.send();
```



### 创建服务器的 servlet，接受并处理数据，把数据输出给异步对象。

在 Servlet 中处理好数据后，通过 `HttpServletResponse` 对象输出数据给异步请求对象

#### 当传递的值是一个普通的字符串时

servlet 中

```java
// 设置响应对象的编码格式
response.setContentType("text/html;charset=utf-8");
// 通过响应对象获取输出流
PrintWriter writer = response.getWriter();
// 输出数据
writer.print(string);
// 刷新流
writer.flush();
// 关闭流
writer.close();
```

js 中

```javascript
xmlHttp.onreadystatechange = function () {
    if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
        // 获取对应的 DOM 对象
        let resultDiv = document.getElementById("resultDiv");
        // 给 DOM 对象赋值
        resultDiv.innerHTML = xmlHttp.responseText;
    }
}
```

#### 当传递的值是一个对象

此时需要使用 JSON 作为传递数据的载体（这里使用的是 [Jackson Databind](https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind) 作为 JSON 的解析的工具类）

servlet 中

```java
// 使用 Jackson 将 Province 对象转为 JSON 格式字符串
ObjectMapper mapper = new ObjectMapper();
json = mapper.writeValueAsString(obj);

// 设置响应对象的编码格式，指定服务器端（servlet 返回给浏览器的是 JSON 格式的数据）
response.setContentType("application/json;charset=utf-8");
PrintWriter writer = response.getWriter();
writer.print(json);
writer.flush();
writer.close();
```

js 中

```javascript
xmlHttp.onreadystatechange = function () {
    if (xmlHttp.readyState === 4 && xmlHttp.status === 200) {
        // 获取到 JSON 格式的字符串
        let data = xmlHttp.responseText;
        // 将 JSON 格式字符串转为 JSON 对象，key 就是 JSON 对象的属性名
        // eval() 方法是将括号中的字符串转换为 JSON 对象
        let jsonObj = eval("("+ data +")");
        // 获取 DOM 对象，给 DOM 对象赋值，更新页面，
        document.getElementById("proname").value = jsonObj.name;
        document.getElementById("projiancheng").value = jsonObj.jiancheng;
        document.getElementById("proshenghui").value = jsonObj.shenghui;

    }
}
```


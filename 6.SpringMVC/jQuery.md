## jQuery

### 一、简单使用

* 指定 jQuery 的库文件位置

```html
// 使用本地的 js 文件
<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
// 或者直接使用官网上提供的 js 文件
<script type="text/javascript" src="https://code.jquery.com/jquery-3.6.0.js"></script>
```

* 使用 jQuery 在页面完全加载后执行指定代码内容

**分步写法**

```javascript
// 1、$(document)，$ 是 jQuery 中的一个函数名，document 是函数的参数，作用是把 document
// 对象变成 jQuery 库函数可以使用的对象。
let jqueryObj = $(document);

// 2、ready，是 jQuery 中的函数，表示当页面中的 DOM 对象都加载成功后会执行 ready 函数中的内容
// ready 相当于 js 中的 onLoad 事件。
jqueryObj.ready(fun1());

// 3、fun1 表示自定义函数，表示在 DOM 对象都加载完成后要执行的操作。
function fun1() {
    // 自定义的功能代码
    alert("Hello jQuery");
}
```

**标准写法**

```javascript
$(document).ready(function () {
    alert("Hello jQuery");
});
```

**简化写法**

```javascript
$(function () {
    alert("Hello jQuery");
})

jQuery(function () {
    alert("Hello jQuery");
});

window.jQuery(function () {
    alert("Hello jQuery");
});
```



### 二、DOM 对象 和 jQuery 对象

`DOM 对象` ： 使用 javaScript 语法创建的对象叫做 DOM 对象，也就是 js 对象。

```java
let obj = document.getElementById("btn");
```

`jQuery对象` ： 使用 jQuery 语法表示的对象叫做 jQuery 对象，注意：**jQuery 表示的对象是数组，数组中的元素是 DOM 对象**。

```javascript
let $obj = $("#btn");
```

* DOM 对象转换为 jQuery 对象

  ```javascript
  // 获取 DOM 对象
  let obj = document.getElementById("btn");
  
  // 把 DOM 对象转换为 jQuery 对象
  let $obj = $(obj);
  ```

* 把 jQuery 对象转换为 DOM 对象

  ```javascript
  // 使用 jQuery 的语法获取页面中的 DOM 对象数组（即 jQuery 对象）
  let $btn = $("#btn");
  // 从 jQuery 对象中获取下标为 0 的 DOM 对象的两种方式
  let btn = $btn[0];
  let btn = $btn.get(0);
  ```



### 三、选择器

1. `id 选择器` ：通过 DOM 对象的 id 属性定位 DOM 对象，id 属性是当前页中的唯一值。

   ```javascript
   $("#DOM对象的id值")
   ```

2. `类（class）选择器` ： 通过 DOM 对象的 class 属性定位 DOM 对象，当前页中可以有多个同名的 class 属性。

   ```javascript
   $(".class属性值")
   ```

3. `标签选择器`  ： 通过 DOM 对象的标签定位 DOM 对象。

   ```javascript
   $("标签名称")
   ```

4. `全部选择器` ： 获取所有的 DOM 对象。

   ```javascript
   $("*")
   ```

5. `组合选择器` ： 多个被选对象之间使用逗号分隔后形成的选择器，可以组合 id ，class， 标签等。

   ```javascript
   $("#id名,.class名,标签名")
   ```

6. `表单选择器` ： 对文本框，单选框，复选框，下拉列表等元素的选择方式，表单选择器是为了更加容易地操作表单，表单选择器是根据元素类型来定义的。

   ```javascript
   // 选取所有单行文本框
   $(":text")
   // 选取所有密码框
   $(":password")
   // 选取所有单选框
   $(":radio")
   // 选取所有复选框
   $(":checkbox")
   ```

   获取到的对象都是 jQuery 对象（DOM 数组），通过 `.val()` **方法只能读取数组中第一个 DOM 对象的 value 属性**。



### 四、过滤器

jQuery 对象中存储的 DOM 对象顺序与标签页声明的顺序一致。

过滤器就是过滤条件，对以定位到数组中的 DOM 对象进行一定条件的过滤筛选。

过滤条件不能独立出现在 jQuery 函数中，如果使用，只能出现在选择器后方。

1. `选择 jQuery 对象中的第一个 DOM 对象`

   ```javascript
   $("选择器:first")
   ```

2. `选择 jQuery 对象中的最后一个 DOM 对象`

   ```javascript
   $("选择器:last")
   ```

3. `选择 jQuery 对象中指定位置处的 DOM 对象`

   ```javascript
   $("选择器:eq(数组索引)")
   ```

4. `选择 jQuery 对象中小于指定位置处的 DOM 对象`

   ```javascript
   $("选择器:lt(数组索引)")
   ```

5. `选择 jQuery 对象中大于指定位置处的 DOM 对象`

   ```javascript
   $("选择器:gt(数组索引)")
   ```

   实际使用

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>过滤器</title>
       <style>
           div {
               background: aquamarine;
           }
       </style>
       <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
       <script type="text/javascript">
           $(function () {
               // 当页面的 DOM 对象都创建好了，给对象绑定事件，因为此时 button 对象在内存中已经创建好了，可以使用
               $("#btn0").click(function () {
                   // 获取第一个 div
                   let $divFirst = $("div:first");
                   $divFirst.css("background", "red");
               })
   
               $("#btn1").click(function() {
                   // 获取最后一个 div
                   let $divLast = $("div:last");
                   $divLast.css("background", "yellow");
               })
   
               $("#btn2").click(function() {
                   // 获取下标为 2 的 div
                   let $div03 = $("div:eq(2)");
                   $div03.css("background", "blue");
               })
   
               $("#btn3").click(function() {
                   // 获取下标小于 3 的 div
                   let $div = $("div:lt(3)");
                   $div.css("background", "orange");
               })
   
               $("#btn4").click(function() {
                   // 获取下标大于 0 的 div
                   let $div = $("div:gt(0)");
                   $div.css("background", "black");
               })
           })
   
       </script>
   </head>
   <body>
       <div id="div0">我是div-0</div>
       <div id="div1">我是div-1</div>
       <div>我是div-2
           <div>我是div-3</div>
           <div>我是div-4</div>
       </div>
   
       <input type="button" value="获取第一个div" id="btn0"><br/>
       <input type="button" value="获取最后一个div" id="btn1"><br/>
       <input type="button" value="获取第三个div" id="btn2"><br/>
       <input type="button" value="获取前三个div" id="btn3"><br/>
       <input type="button" value="获取后四个div" id="btn4"><br/>
   
   </body>
   </html>
   ```

6. `表单对象属性过滤器`

   ```javascript
   // 选择可用的文本框
   $(":text:enable")
   // 选择不可用的文本框
   $(":text:disable")
   // 选择复选框选中的元素
   $(":checkbox:checked")
   // 选择指定下拉列表的被选中的元素
   $("select>option:selected")
   ```

   实际使用

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>表单过滤器</title>
       <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
       <script type="text/javascript">
           $(function () {
               $("#btn1").click(function () {
                   // 选择所有可用的文本框
                   let $text = $(":text:enabled")
                   // 将可用的文本框的值赋为 hello
                   $text.val("hello");
               })
               $("#btn2").click(function () {
                   // 选择复选框选中的元素
                   let $checkbox = $(":checkbox:checked");
                   for (var i = 0; i < $checkbox.length; i++) {
                       alert($checkbox[i].value)
                   }
               })
               $("#btn3").click(function () {
                   // 选择指定下拉列表的被选中的元素
                   let $option = $("select>option:selected");
                   alert($option.val())
               })
           })
       </script>
   </head>
   <body>
       <p>文本框</p>
       <input type="text" id="text1" value="text1"><br/>
       <input type="text" id="text2" value="text2" disabled><br/>
       <input type="text" id="text3" value="text3"><br/>
       <input type="text" id="text4" value="text4" disabled><br/>
   
       <p>复选框</p>
       <input type="checkbox" value="游泳">游泳
       <input type="checkbox" value="健身" checked>健身
       <input type="checkbox" value="电子游戏" checked>电子游戏
   
       <p>下拉框</p>
       <select>
           <option value="java">java 语言</option>
           <option value="go" selected>go 语言</option>
           <option value="sql">sql 语言</option>
       </select>
   
       <P>功能按钮</P>
       <button id="btn1">所有可用的text都设置值为hello</button><br/>
       <button id="btn2">显示被选中的复选框的值</button><br/>
       <button id="btn3">显示下拉列表选中的值</button>
   </body>
   </html>
   ```

   



### 五、函数

1. `val()` ： 操作数组中 DOM 对象的 **value 属性**。

   ```javascript
   // 无参数调用形式，读取数组中【第一个 DOM 对象】的 value 属性值
   $(选择器).val()
   
   // 有参形式调用，对数组中【所有 DOM 对象】的 value 属性值进行统一赋值
   $(选择器).val(值)
   ```

   

2. `text()` ： 操作数组中所有 DOM 对象的 **文字显示内容属性**。

   ```javascript
   // 无参数调用，读取数组中【所有 DOM 对象的文字】显示内容，将得到【内容拼接为一个字符串】返回
   $(选择器).text()
   // 有参数方式，对数组中【所有 DOM 对象的文字】显示内容进行【统一赋值】
   $(选择器).text(值)
   ```

   

3. `attr()` ： 对 val, text 之外的**其他属性操作。**

   ```javascript
   // 获取 DOM 数组【第一个对象的属性值】
   $(选择器).attr(“属性名”)
   // 对数组中【所有 DOM 对象的属性】设为新值
   $(选择器).attr(“属性名”,“值”)
   ```

   ==attr() 和 prop() 区别==

   * [jQuery 中 attr() 和 prop() 方法的区别](https://www.cnblogs.com/zhwl/p/3520162.html)
   * [jQuery中的prop和attr区别](https://www.cnblogs.com/zhumingzhenhao/p/8204940.html)

   实际使用

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>函数</title>
       <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
       <script type="text/javascript">
           $(function () {
               // 获取第一个文本框的值
               $("#btn1").click(function () {
                   // 获取所有文本框对象
                   let $text = $(":text");
                   alert($text.val())
               })
   
               // 设置所有文本框的值
               $("#btn2").click(function () {
                   // 获取所有文本框对象
                   let $text = $(":text");
                   $text.val("三国演义")
               })
   
               // 获取div的所有文本
               $("#btn3").click(function () {
                   // 获取所有 div 对象
                   let $div = $("div");
                   alert($div.text());
               })
   
               // 设置div新文本
               $("#btn4").click(function () {
                   // 获取第一个对象
                   let $div = $("div");
                   $div.text("我是新的div")
               })
   
               // 获取img图片的src
               $("#btn5").click(function () {
                   // 获取 img 对象
                   let $img = $("img");
                   // 获取 img 的 src
                   alert($img.attr("src"));
               })
   
               // 设置 img 图片
               $("#btn6").click(function () {
                   // 获取 img 对象
                   let $img = $("img");
                   // 将图片换成 img 目录下的 ex2.jpg
                   $img.attr("src", "img/ex2.jpg")
               })
           })
       </script>
   </head>
   <body>
       <p>文本框val</p>
       <input type="text" value="刘备"><br/>
       <input type="text" value="关羽"><br/>
       <input type="text" value="张飞"><br/>
   
       <p>文本数据text</p>
       <div>我是第一个div</div>
       <div>我是第二个div</div>
       <div>我是第三个div</div>
   
       <p>图片</p>
       <img id="img" src="img/ex1.jpg">
   
       <P>功能按钮</P>
       <button id="btn1">获取第一个文本框的值</button><br/>
       <button id="btn2">设置所有文本框的值</button><br/>
       <button id="btn3">获取div的所有文本</button><br/>
       <button id="btn4">设置div新文本</button><br/>
       <button id="btn5">获取img图片的src</button><br/>
       <button id="btn6">设置img图片</button>
   </body>
   </html>
   ```

   

4. `hide()`

   ```javascript
   // 将数组中所有 DOM 对象在浏览器中【隐藏起来】
   $(选择器).hide()
   ```

   

5. `show()`

   ```javascript
   // 将数组中所有 DOM 对象在浏览器中【显示起来】
   $(选择器).show()
   ```

   

6. `remove()`

   ```javascript
   // 将数组中【所有 DOM 对象及其子对象】一并删除
   $(选择器).remove()
   ```

   

7. `empty()`

   ```javascript
   // 将数组中【所有 DOM 对象的子对象】删除
   $(选择器).empty()
   ```

   

8. `append()`

   ```javascript
   // 为数组中所有 DOM 对象【添加子对象】
   $(选择器).append("<div>我动态添加的 div</div>")
   ```

   

9. `html()` ：设置或返回被选元素的内容（innerHTML）。

   ```javascript
   // 无参数调用方法，【获取】 DOM 数组【第一个匹元素的内容】
   $(选择器).html()
   // 有参数调用，用于【设置】 DOM 数组中【所有元素的内容】
   $(选择器).html(值)
   ```

   

10. `each()` ： each 是**对数组，json 和 dom 数组等的遍历**，对每个元素调用一次函数。

    ```javascript
    // 语法 1
    $.each( 要遍历的对象, function(index,element) { 处理程序 } )
    
    // 语法 2
    jQuery 对象.each( function( index, element ) { 处理程序 } )
    ```

    * `index` ：数组的下标
    * `element` ：数组的对象

    实际使用

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>函数</title>
        <style type="text/css">
            div {
                background: blue;
            }
        </style>
        <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
        <script type="text/javascript">
            $(function () {
                // 隐藏所有 div
                $("#btn1").click(function () {
                    // 获取所有div对象
                    let $div = $("div");
                    // 隐藏所有 div
                    $div.hide();
                })
    
                // 显示所有 div
                $("#btn2").click(function () {
                    // 获取所有div对象
                    let $div = $("div");
                    // 隐藏所有 div
                    $div.show();
                })
    
                // 清除所有下拉列表中的option子标签
                $("#btn3").click(function () {
                    // 获取所有 select 对象
                    let $select = $("select");
                    $select.empty();
                })
    
                // 删除所有下拉列表
                $("#btn4").click(function () {
                    // 获取所有 select 对象
                    let $select = $("select");
                    $select.remove();
                })
    
                // 添加元素
                $("#btn5").click(function () {
                    let $father = $("#father");
                    $father.append("<div>我是子 div</div>");
                })
    
                // 获取第一个span文本内容
                $("#btn6").click(function () {
                    let $span = $("span");
                    alert($span.html());
                })
    
                // 设置span内容
                $("#btn7").click(function () {
                    let $span = $("span");
                    $span.html("<span style='background: red; color: yellow'>我是修改后的 span</span>");
                })
    
                // each函数遍历数组
                $("#btn8").click(function () {
                    let arr = ["a", "b", "c", "d"];
                    $.each(arr, function (index, element) {
                        alert("数组下标是：" + index + "，数组元素是：" + element);
                    })
                })
    
                // each函数遍历json对象
                $("#btn9").click(function () {
                    let json = {name:"zhangsan", age:20};
                    $.each(json, function (key, value) {
                        alert("key是：" + key + "，value是：" + value);
                    })
                })
    
                // each函数dom数组
                $("#btn10").click(function () {
                    let $text = $(":text");
                    $.each($text, function (index, element) {
                        alert("下标是：" + index + "，元素是：" + element.value);
                    })
                })
            })
        </script>
    </head>
    <body>
        <p>show 和 hide 函数</p>
        <div id="one">我是one div</div>
        <div id="two">我是two div</div>
        <br/>
    
        <p>remove 和 empty 函数</p>
        <select>
            <option>老虎</option>
            <option>狮子</option>
            <option>豹</option>
        </select>
        <br/>
    
        <p>append 函数</p>
        <div id="father" style="background: #ff0000">我是父 div</div>
        <br/>
    
        <p>html 函数</p>
        <span>mysql 是一个<b>数据库</b></span><br/>
        <span>使用 JDBC 访问数据库</span><br/>
    
        <p>each 函数</p>
        <input type="text" value="刘备"><br/>
        <input type="text" value="关羽"><br/>
        <input type="text" value="张飞"><br/>
    
        <p>功能按钮</p>
        <button id="btn1">隐藏所有div</button><br/>
        <button id="btn2">显示所有div</button><br/>
        <button id="btn3">清除所有下拉列表中的option子标签</button><br/>
        <button id="btn4">删除所有下拉列表</button><br/>
        <button id="btn5">添加元素</button><br/>
        <button id="btn6">获取第一个span文本内容</button><br/>
        <button id="btn7">设置span内容</button><br/>
        <button id="btn8">each函数遍历数组</button><br/>
        <button id="btn9">each函数遍历json对象</button><br/>
        <button id="btn10">each函数don数组</button><br/>
    </body>
    </html>
    ```

    

### 六、事件

**为页面元素绑定事件，即对于指定页面元素，当某个事件发生后，执行指定动作。**

`第一种方式：定义元素监听事件`

```javascript
$(选择器).监听事件的名称(处理函数);
```

* 监听事件名称是 js 中事件，例如：

  ```shell
  1、 blur  失去焦点     
  	focus  获得焦点
  2、 click  鼠标单击    
  	dblclick  鼠标双击
  3、 keydown  键盘按下  
  	keyup  键盘弹起
  4、 mousedown  鼠标按下
  	mouseover  鼠标经过
  	mousemove  鼠标移动
  	mouseout  鼠标离开
  	mouseup  鼠标弹起
  5、 submit  表单提交
  	reset  表单重置
  6、 change  下拉列表选中项改变，或文本框内容改变
  7、 load  页面加载完毕（整个 HTML页面中所有元素全部加载完毕之后发生）
  8、 select  文本被选定
  ```



`第二种方式：on()绑定事件`

**on() 方法在被选元素上添加事件处理程序。该方法给 API 带来很多便利，推荐使用该方法。**

```javascript
$(选择器).on(event,,data,function)
```

* `event`：事件，**可以有一个或者多个，多个之间通过空格分隔。**
* `data`：可选。规定传递到函数的的额外数据。
* `function`：可选。规定当事件发生时运行的函数。



实际使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件</title>
    <style>
        div {
            background: gray;
            width: 200px;
            height: 80px;
        }
    </style>
    <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
    <script type="text/javascript">
        $(document).ready(function () {
            $("#btn").click(function () {
                // 动态添加 Button
                $("#mydiv").append("<input type='button' id='newBtn' value='我是动态添加的Button'>");
                // 给新添加的 Button 添加单击事件
                $("#newBtn").on("click mouseover", function () {
                    alert("newBtn 上有鼠标经过或被点击了！")
                })
            })
        })
    </script>
</head>
<body>
    <div id="mydiv">

    </div><br/>
    <button id="btn">动态添加Button</button>
</body>
</html>
```





### 七、AJAX

**jQuery 提供多个与 AJAX 有关的方法。通过 jQuery AJAX 方法，您能够使用 HTTP Get** 

**和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON 同时能够把接收的数据更新**

**到 DOM 对象。**



**三种使用方法：**

* `$.ajax()`：是 jQuery 中 AJAX 请求的核心方法，所有的其他方法都是在内部使用此方法。
* `$.post()`：方法使用 HTTP POST 请求从服务器加载数据。内部使用的是 $.ajax()。
* `$.get()`：方法使用 HTTP GET 请求从服务器加载数据。内部使用的是 $.ajax()。

方法内部使用 `json` 格式的数据，即 `$.ajax({name:value, name:value...})`， 包含了请求方式，请求数据，回调方法等。



**$.ajax() 中 json 数据的 name 值：**

* `async`：布尔值，表示请求是否是异步处理，默认是 `true`
* `contentType`：发送数据到服务器时所使用的内容的类型，默认时：`"application/x-www-form-urlencoded"。`
* `data`：规定发送到服务器的数据，`参数可以是 字符串，数组，但多数是 json`。
* `dataType`：期望从服务器中相应的数据类型。
* `error` ：参数是一个函数，表示当请求发生错误的时候执行的函数。
* `success`：参数是一个函数，表示当请求成功并且从服务端返回了数据后（即 readyState == 4 && status == 200），会执行指定函数。
* `url`：请求的地址。
* `type`：请求方式，get 或者 post，默认是 get。

**主要使用的是 url , data ,dataType, success。**



实际使用

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>AJAX(jQuery) 根据省份 id 获取省份信息</title>
    <script type="text/javascript" src="js/jquery-3.6.0.js"></script>
    <script type="text/javascript">
        $(function () {
            $("#btn").click(function () {
                // 获取 DOM 的 value 值
                let $proid = $("#proid");
                $.ajax({
                    // 请求的地址
                    url: "queryProvinceServlet",
                    // 请求的数据，以 json 格式
                    data: {
                        "id": $proid.val()
                    },
                    // 期望服务器端返回的数据格式
                    dataType:"json",
                    // 如果请求成功时运行指定函数，函数的参数是之前 AJAX 中
                    // xmlHttp.responseText 经过格式转换后的对象
                    success:function (data) {
                        // 对 text 赋值
                        $("#proname").val(data.name);
                        $("#projiancheng").val(data.jiancheng);
                        $("#proshenghui").val(data.shenghui);
                    }
                })
            })
        })
    </script>
</head>
<body>
<p>AJAX 请求使用 JSON 格式数据</p>
<table>
    <tr>
        <td>省份编号：</td>
        <td>
            <input type="text" id="proid">
            <input type="button" value="搜索" id="btn">
        </td>
    </tr>
    <tr>
        <td>省份名称：</td>
        <td><input type="text" id="proname"></td>
    </tr>
    <tr>
        <td>省份简称：</td>
        <td><input type="text" id="projiancheng"></td>
    </tr>
    <tr>
        <td>省会：</td>
        <td><input type="text" id="proshenghui"></td>
    </tr>
</table>
</body>
</html>
```


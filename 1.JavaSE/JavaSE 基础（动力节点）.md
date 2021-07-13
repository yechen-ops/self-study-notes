

# JavaSE 基础（动力节点）

[TOC]

## 1、标识符与关键字

### 1.1  标识符

==标识符就是程序员自己有权利自己去改的单词（黑色高亮字体）==

#### 1.1.1 标识符的命名规则（是语法，不遵守会报错，必须遵守）

* 标识符只能由数字、字母（包括中文）、下划线、美元符号组成，不能含有其他符号。
* 标识符不能以数字开头。
*  关键字不能做标识符，如public 、class、static。
* 标识符是严格个规定大小写的（但类名最好不同）。
* 标识符理论上是没有长度限制的。

#### 1.1.2 标识符的命名规范（不符合规范也行，代码可读性差）

* 见名知意（看到名字就知道啥意思）。
* 遵循驼峰命名方式（单词之间很好的进行分隔）。
* 类名、接口名首字母大写，后面单词首字母大写。
* 变量名、方法名首字母小写，后面单词首字母大写。
* 所有常量，全部大写，并且单词和单词之间用下划线衔接。

### 1.2 关键字

==SUN 公司开发 Java 时，提前定义好的特殊含义的单词，全部小写（蓝色高亮字体），关键字不能做标识符==



## 2、变量

软件在处理数据之前需要能够表示数据，在java代码中怎么去表示数据呢？在java中有这样的一个概念：字面量。

在java语言中“数据”被称为“字面量”。

#### 2.1 字面量可以分为很多种类：

* 整数型字面量
* 浮点型字面量
* 布尔型字面量
* 字符型字面量
* 字符串型字面量

#### 2.2 什么是变量:

* 变量其实就是内存当中存储数据的最基本的单元
* 变量有不同的数据类型，如int，float，double......
* 不同的数据类型在内存中分配的空间大小不同

1. 变量来说有三个要素:
   1. 变量的数据类型（类型决定空间的大小）
   2. 变量的名字（起个名字是为了以后方便访问。（以后在程序中访问这个数据是通过名称来访问的。））
   3. 变量中保存的值（就是字面量）

4. 在java语言中有一个规定，变量必须先声明，再赋值才能访问。（没有值相当于这个空间没有开辟。）

5. **重要的结论：在同一个域当中（这个域怎么理解，后面讲），变量名不能重名，不能重复声明。**
6. 变量可以重新赋值，但在同一个域当中，不能重复声明。

7. 关于变量的一个分类（这个需要“死记硬背”。）：
   * 变量根据出现的位置进行划分：
     1. 在**方法体当中声明**的变量：局部变量。
     2. 在**方法体之外**，**类体内声明**的变量：成员变量。
   * 注意：局部变量只在方法体当中有效，方法体执行结束该变量的内存就释放了。

8. 变量的作用域：

   ```java
   /*
   	变量的作用域？
   		1、什么是作用域？
   			变量的有效范围。
   		2、关于变量的作用域，大家可以记住一句话：
   			出了大括号就不认识了。（死记这句话。）
   		3、java中有一个很重要的原则：
   			就近原则。（不仅java中是这样，其它编程语言都有这个原则。）
   			哪个离我近，就访问哪个。
   */
   
   public class VarTest08{
   
   	// 成员变量
   	int i = 10000;
   
   	public static void main(String[] args){
   		// 局部变量
   		int i = 100; // 这个i的有效范围是main方法。
   		System.out.println(i); // 这个i是多少？
   
   		// 同一个域当中，这是不允许的。
   		// int i = 90;  
   
   		// 考核一下：以下编写for循环你看不懂，没关系，后面会将。
   		for(int n = 0; n < 10; n++){ // 这里声明的n变量只属于for域。for结束后n释放没了。
   			// 这里没有编写代码。
   		}
   
   		// for循环执行结束之后，在这里访问n变量可以吗？
   		//System.out.println(n);  //错误: 找不到符号
   
   		int k; // 属于main域。
   		for(k = 0; k < 10; k++){
   
   		}
   		// 能否继续访问k呢？
   		System.out.println(k);
   	}
   
   	// 这个方法怎么定义先不用管，后面会学习。
   	public static void x(){
   		// 在这个位置上能访问i吗？
   		// 错误: 找不到符号
   		// System.out.println(i); // i是无法访问的。
   
   		// 可以定义一个变量起名i吗？
   		// 这个i的有效范围是x方法。
   		// 局部变量
   		int i = 200; // 所以这个i和main方法中的i不在同一个域当中。不冲突。
   	}
   }
   ```



## 3、数据类型

八个 ==基本数据类型== 及其占用空间大小

| 类型    | 存储空间 | 范围                  |
| ------- | -------- | --------------------- |
| byte    | 1字节    | -128 ~ 127            |
| short   | 2字节    | -(-2^15^) ~ (2^15^-1) |
| int     | 4字节    | -(2^31^) ~ (2^31^-1)  |
| long    | 8字节    | -(2^63^) ~ (2^63^-1)  |
| float   | 4字节    |                       |
| double  | 8字节    |                       |
| boolean | 1字节    |                       |
| char    | 2字节    | 0 ~ （2^16^ - 1）     |

#### 3.1 整数型字面量四种表现形式：

```java
// 十进制
int a = 10; 
System.out.println(a); // 10

// 八进制
int b = 010;
System.out.println(b); // 8

// 十六进制
int c = 0x10;
System.out.println(c); // 16

int x = 16; //十进制方式
System.out.println(x);// 16

// 二进制（JDK8的新特性，低版本不支持。）
int d = 0b10;
System.out.println(d); // 2
```



#### 3.2 数据类型转换：

* 在 java 中有一条非常重要的结论，必须记住：==在任何情况下，整数型的“字面量/数据”默认被当做 int 类型处理==。（记住就行）
  如果希望该“整数型字面量”被当做 long 类型来处理，需要在“字面量”后面添加 L / l 建议使用大写 L，因为小写 l 和 1 傻傻分不清。

* 小容量可以直接赋值给大容量，称为**自动类型转换**。
* 大容量不能直接赋值给小容量，**需要使用强制类型转换符进行强转**。但需要注意的是：加强制类型转换符之后，虽然编译通过了，但是运行的时候可能会损失精度。
* **但是：java 中有一个语法规则：当这个整数型字面量没有超出 byte（或 short）的取值范围，那么这个整数型字面量可以直接赋值给 byte（或 short）类型的变量。**

```java
public class IntTest04 {
	public static void main(String[] args) {
		// 分析：以下代码编译可以通过吗？
		// 300 被默认当做int类型
		// b变量是byte类型
		// 大容量转换成小容量，要想编译通过，必须使用强制类型转换符
		// 错误: 不兼容的类型: 从int转换到byte可能会有损失
		byte b = 300;

		// 要想让以上的程序编译通过，必须加强制类型转换符
		// 虽然编译通过了，但是可能精度损失。
		// 300这个int类型对应的二进制：00000000 00000000 00000001 00101100
		// byte占用1个字节，砍掉前3个字节，结果是：00101100 (44)
		byte b = (byte)300;
		System.out.println(b); // 44
        
        // 这样是都不会报错的
        byte x = 1;
		byte y = 127;
        short s = 1;
		short s1 = 32767;
        
        // 但这样就会报错了
        byte x = 128;
        short x = 32768;
	}
}
```

* byte、char、short 做混合运算的时候，各自先转换成 int 再做运算

```java
public class IntTest06{
	public static void main(String[] args){

		char c1 = 'a';
		byte b = 1;

		// 注意：这里的"+"是负责求和的
		System.out.println(c1 + b); // 98

		// 错误: 不兼容的类型: 从int转换到short可能会有损失
		//short s = c1 + b; // 编译器不知道这个加法最后的结果是多少。只知道是int类型。

		// 这样修改行吗？
		// 错误: 不兼容的类型: 从int转换到short可能会有损失
		// short s = (short)c1 + b;

		short s = (short)(c1 + b);

		// short k = 98;

		int a = 1;
		// 错误: 不兼容的类型: 从int转换到short可能会有损失
		// short x = 1; 可以
		short x = a; // 不可以，编译器只知道a是int类型，不知道a中存储的是哪个值。
		System.out.println(x);
	}
}
```

* 多种数据类型做混合运算的时候，最终的结果类型是“最大容量”对应的类型。(char+short+byte 这个除外，原因如上)

```java
long a = 10L;
char c = 'a';
short s = 100;
int i = 30;

long sum = a + c + s + i;

// 会出现：错误: 不兼容的类型: 从long转换到int可能会有损失
// int sum = a + c + s + i;

// 求和
System.out.println(sum); //237
```

* 练习

```java
public class TypeTransferTest{
	public static void main(String[] args){
		// 编译报错，因为1000已经超出范围了。
        // 错误: 不兼容的类型: 从int转换到byte可能会有损失
		byte b1 = 1000;
		// 可以
		byte b2 = 20;
		// 可以
		short s = 1000;
		// 可以
		int c = 1000;
		// 可以
		long d = c;
		// 编译报错
        // 错误: 不兼容的类型: 从long转换到int可能会有损失
		int e = d;
		// 可以
		int f = 10 / 3;
		// 可以
		long g = 10;
		// 编译报错
        // 错误: 不兼容的类型: 从long转换到int可能会有损失
		int h = g / 3;
		// 可以
		long m = g / 3;
		// 编译报错
        // 错误: 不兼容的类型: 从int转换到byte可能会有损失
		byte x = (byte)g / 3;
		// 可以
		short y = (short)(g / 3);
		// 可以
		short i = 10;
		// 可以
		byte j = 5;
		// 编译报错
        // 错误: 不兼容的类型: 从int转换到short可能会有损失
		short k = i + j;
		// 可以
		int n = i + j;
		// 可以
		char cc = 'a';
		System.out.println(cc); // a
		System.out.println((byte)cc); // 97
		// cc 会先自动转换成int类型，再做运算
		int o = cc + 100;
		System.out.println(o); // 197
	}
}
```



#### 3.3 原码 反码 补码

* 计算机在底层存储数据的时候，一律存储的是“==**二进制的补码形式**==”
* **对于一个正数来说：二进制原码、反码、补码是同一个，完全相同**
* 对于一个负数来说：二进制原码、反码、补码是什么关系：

```java
byte i = -1;
// 对应的二进制原码：10000001
// 对应的二进制反码（符号位不变，其它位取反）：11111110
// 对应的二进制补码（反码+1）：11111111
```

#### 3.4 关于java语言中的浮点型数据

**float是单精度**
**double是双精度**

* float 和 double 存储数据的时候都是存储的近似值
* 注意：任意一个浮点型都比整数型空间大。float 容量 > long 容量。
* **java 中规定，任何一个浮点型数据默认被当做 double 来处理，如果想让这个浮点型字面量被当做 float 类型来处理，那么请在字面量后面添加 F / f 。**	

```java
// 错误
float a = 3.14;
// 正确
float a = 3.14f;
// 正确
double a = 3.14;
```

#### 3.5 关于字符型：char

* char占用2个字节。
* char的取值范围：[0-65535]
* char采用 **unicode** 编码方式。
* char类型的字面量使用单引号括起来。

* char可以存储一个汉字。

```java
char c1 = '中';
System.out.println(c1);

char c2 = 'a';
System.out.println(c2);

// 0如果加上单引号的话，0就不是数字0了，就是文字0，它是1个字符。
char c3 = '0';
System.out.println(c3);

// 以下就会出现错误
// 错误: 不兼容的类型: String无法转换为char
char c4 = "a";

// 错误: 未结束的字符文字
char c5 = 'ab';

// 错误: 未结束的字符文字
char c6 = '1.08';
```

* 当一个整数赋值给 char 类型变量的时候，会自动转换成 char 字符型，最终的结果是一个字符

```java
char a = 97;
System.out.println(a); // a
```

* 当一个整数没有超出 byte  short  char 的取值范围的时候，这个整数可以直接赋值给 byte  short  char类型的变量。



#### 3.6 关于java中的转义字符

```java
// \t : 一个制表位
System.out.println("北京\t天津\t上海");
// \n : 换行符
System.out.println("jack\nsmith\nmary");
// \\ : 一个 \
System.out.println("C:\\\\Windows\\\\System32\\\\cmd.exe");// 输出 //
// \" : 一个 "
System.out.println("老韩说：\"要好好学习 Java\"");
// \r : 一个回车
System.out.println("韩顺平教育\r北京");
```



#### 3.7 关于 boolean 类型

* 在 java 语言中 boolean 类型只有两个值，没有其他值：true 和 false。不像 C 或者 C++，C 语言中 1 和 0 也可以表示布尔类型。
* boolean 类型在实际开发中使用在**逻辑判断当中**，通常放到**条件的位置上**（充当条件）



## 4、运算符

### 4.1 算术运算符

**\+	求和**
**\-	 相减**
**\*    乘积**
**/     商**
**%   求余数（求模）**
**++  自加1**
**--    自减1**

#### 4.1.1 关于 ++ 和 --

* 写在变量后 ---> 先赋值在自增

```java
int b = 0;
b = a++;
System.out.println("b = " + b);// b = 1
System.out.println("a = " + a);// a = 2
```

* 写在变量前 ---> 先自增再赋值

```java
int a = 1;
int b = 0;
b = ++a;
System.out.println("b = " + b);// b = 2
System.out.println("a = " + a);// a = 2
```



### 4.2 关系运算符

**\>		大于**
**\>=	 大于等于**
**\<		小于**
**\<=	 小于等于**
**\==	 关系运算符，判断是否相等**
**\!=      关系运算符，判读是否不相等**

**所有的关系运算符的运算结果都是布尔类型，不是true就是false，不可能是其他值。**



### 4.3 逻辑运算符

**&		逻辑与（可以翻译成并且）**
**|		 逻辑或（可以翻译成或者）**
**!		  逻辑非（取反）**
**&&	  短路与**
**||	   短路或**

**逻辑运算符两边要求都是布尔类型，并且最终的运算结果也是布尔类型。这是逻辑运算符的特点。**

#### 4.3.1 关于短路与 &&，短路或 ||

* 短路与&& 和 逻辑与 &有什么区别：
  * 首先这两个运算符的运算结果没有任何区别，完全相同。
  * 只不过“短路与&&”会发生短路现象。
* 什么是短路现象呢？
  * 右边表达式不执行，这种现象叫做短路现象。
* 什么时候使用&&，什么时候使用& ？
  * 从效率方面来说，&&比&的效率高一些。因为逻辑与&不管第一个表达式结果是什么，第二个表达式一定会执行。
  * 以后的开发中，短路与&&和逻辑与还是需要同时并存的。大部分情况下都建议使用短路与&&
    只有当既需要左边表达式执行，又需要右边表达式执行的时候，才会选择逻辑与&。

* 什么时候发生短路或现象？
  * 当左边的表达式结果是true的时候，右边的表达式不需要执行，此时会短路。



### 4.4 赋值运算符

赋值运算符包括“基本赋值运算符”和“扩展赋值运算符”：基本的、扩展的。

基本赋值运算符：=

扩展赋值运算符：

+=

*=
/=
%=

```java
int a = 10;
a += 10;
// 类似于
a = a + 10;
```



### 4.5 条件运算符：（三目运算符）

* 语法格式:
  * 布尔表达式 ? 表达式1 : 表达式2
* 执行原理是什么：
  * 布尔表达式的结果为true时，表达式1的执行结果作为整个表达式的结果。
  * 布尔表达式的结果为false时，表达式2的执行结果作为整个表达式的结果。

```java
boolean sex = true;
char x = sex ? '男' : '女';
System.out.println(x);// 男
```



### 4.6 + 运算符

* 运算符在java语言中有两个作用:
  1. 求和
  2. 字符串拼接
* 什么时候求和？什么时候进行字符串的拼接呢？
  * 当 + 运算符**两边都是数字类型**的时候，**求和**。
  * 当 + 运算符两边的“**任意一边”是字符串类型**，那么这个+会进行字符串**拼接**操作。
* 字符串拼接完之后的结果还是一个字符串

```java
public class A {
	public static void main(String[] args){
		int a = 100;
		int b = 200;
		int c = a + b;
		System.out.println("a = " + a);// 字符串："a  = 100"
		System.out.println(a + b);// 数字：300
		System.out.println(a + b + "110"); // 字符串："300110"
		System.out.println(a + (b + "110"));// 字符串："100200110"
		System.out.println("100+200=300");// 字符串："100+200=300"
		System.out.println(a + "+" + b + "=" + c);// 字符串："100+200=300"
		System.out.println(a + "+" + b + "=" + a + b);// 字符串："100+200=100200"
		System.out.println(a + "+" + b + "=" + (a + b));// 字符串："100+200=300"
	}
}
```



### 4.7 在java中接收键盘的输入

```java
// 创建一个键盘扫描器对象,对象名为 s
java.util.Scanner s = new java.util.Scanner(System.in);
// 接受一个整数
// 代码执行到这里的时候，会暂停下来等待用户的输入，用户可以从键盘上输入一个整数，然后回车，回车之
// 后,num就被赋上值了
int num = s.nextInt();
// 接受一个字符串
String str = s.next();
```



### 4.8 有一个问题要提出

```java
int i = 10;
i = i++;
System.out.println("i = " + i);
```

以上代码输出结果为：`i =  10`

原因是：`i = i++` 对应如下代码

```java
int tmep = k;
k++;
k = temp;
```





## 5、控制语句

### 5.1 if语句

**if 语句是分支语句，也可以叫做条件语句。**

* 语法格式

  * 第一种

  ```java
  if(布尔表达式){
      java语句;
      java语句;
  }
  ```

  * 第二种

  ```java
  if(布尔表达式){  // 分支1
      java语句;     
  }else{            // 分支2
      java语句;
  }
  ```

  * 第三种

  ```java
  if(布尔表达式1){ // 分支1
      java语句;
  }else if(布尔表达式2){ // 分支2
      java语句;
  }else if(布尔表达式3){
      java语句;
  }else if(布尔表达式4){
      java语句;
  }....
  ```

  * 第四种

  ```java
  if(布尔表达式1){ // 分支1
      java语句;
  }else if(布尔表达式2){ // 分支2
      java语句;
  }else if(布尔表达式3){
      java语句;
  }else if(布尔表达式4){
      java语句;
  }else{
      java语句; // 以上条件没有一个成立的。这个else就执行了。
  }
  ```

* 对于 if 语句来说，在任何情况下只能有 1 个分支执行，不可能存在 2 个或者更多个分支执行。if 语句中只要有 1 个分支执行了，整个 if 语句就结束了。（对于 1 个完整的if语句来说的。）

* 以上 4 种语法机制中，凡是带有 else 分支的，一定可以保证会有一个分支执行。以上 4 种当中，第一种和第三种没有 else 分支，这样的语句可能会导致最后一个分支都不执行。第二种和第四种肯定会有 1个分支执行。

* 当分支当中“java语句;”只有1条，那么大括号{}可以省略，但为了可读性，最好不要省略。

* 控制语句和控制语句之间是可以嵌套的，但是嵌套的时候大家最好一个语句一个语句进行分析，不要冗杂在一起分析。

* 一个例子

```java
import java.util.Scanner;

public class A {
	public static void main(String[] args){
	/*
	业务要求：
		1、从键盘上接收一个人的年龄。
		2、年龄要求为[0-150]，其它值表示非法，需要提示非法信息。
		3、根据人的年龄来动态的判断这个人属于生命的哪个阶段？
			[0-5] 婴幼儿
			[6-10] 少儿
			[11-18] 少年
			[19-35] 青年
			[36-55] 中年
			[56-150] 老年
		4、请使用if语句完成以上的业务逻辑。
	*/
	String str = "老年"; // 字符串变量默认值是“老年”
		if(age < 0 || age > 150){
			System.out.println("对不起，年龄值不合法");
			// 既然不合法，你就别让程序往下继续执行了，怎么终止程序执行
			//return;
		} else if(age <= 5){
			str = "婴幼儿";
		} else if(age <= 10){
			str = "少儿";
		} else if(age <= 18){
			str = "少年";
		} else if(age <= 35){
			str = "青年";
		} else if(age <= 55){
			str = "中年";
		} 
		System.out.println(str);	
}
```



### 5.2 switch语句

**switch语句也是选择语句，也可以叫做分支语句**

* 语法格式: 

```java
switch(值){
    case 值1:
        java语句;
        java语句;...
        break;
    case 值2:
        java语句;
        java语句;...
        break;
    case 值3:
        java语句;
        java语句;...
        break;
    default:
        java语句;
}
```

其中：break;语句不是必须的。default分支也不是必须的

* switch语句支持的值有哪些:
  * 支持 int 类型以及 String 类型
  * 在 JDK8 之前不支持 String 类型
  * byte , short , char 也可以使用在 switch 语句当中，因为 byte  short  char 可以进行自动类型转换
* switch 语句执行原理：
  * 拿“值”与“值1”进行比较，如果相同，则执行该分支中的 java 语句，然后遇到 "break;" 语句，switch语句就结束了。
  * 如果“值”与“值1”不相等，会继续拿“值”与“值2”进行比较，如果相同，则执行该分支中的 java 语句，然后遇到 "break;" 语句，switch 结束。
  * **注意：如果分支执行了，但是分支最后没有 “break;”，此时会发生[case 穿透现象](https://www.bilibili.com/video/BV1Rx411876f?p=286) 视频09:36处。**
  * 所有的 case 都没有匹配成功，那么最后 default 分支会执行。

### 5.3 for循环

* 语法机制：

```java
for(初始化表达式; 条件表达式; 更新表达式){
    循环体; // 循环体由java语句构成
    java语句;
    java语句;
    java语句;
    java语句;
    ....
}
```

* 执行原理:
  1. 先执行初始化表达式，并且初始化表达式只执行1次。
  2. 然后判断条件表达式的结果，如果条件表达式结果为true，则执行循环体。
  3. 循环体结束之后，执行更新表达式。
  4. 更新完之后，再判断条件表达式的结果，如果还是true，继续执行循环体。
  5. 直到更新表达式执行结束之后，再次判断条件时，条件为false，for循环终止。
* 更新表达式的作用是：控制循环的次数。

* 最简练的for循环怎么写?

```java
for(;;){
    System.out.println("死循环");
}
```

这就是个死循环

* 输出 0 - 9

```java
for(int i = 0;i < 10;i++){
    System.out.println("i = " + i); // 0 1 2 3....9
}
```

* 使用for循环，实现1~100所有奇数求和

```java
int sum = 0;
for (int i = 1; i <= 100; i += 2) {
    sum += i;
}
System.out.println("sum = " + sum);// sum = 2500
```

* 九九乘法表

```java
public class A {
	public static void main(String[] args){
		for (int i = 1; i <= 9; i++) {// 纵向循环
			for (int j = 1; j <= i; j++) {// 横向循环，j的范围受i的影响
				System.out.print(i +"*"+j +"="+(i*j)+"\t");
			}
			System.out.println();
		}
	}	
}
```



### 5.4 while循环

* 语法机制：

```java
while(布尔表达式){
    循环体;
    更新表达式;
}
```

* 执行原理：

  1. 判断布尔表达式的结果，如果为true就执行循环体，更新表达式

  2. 再次判断布尔表达式的结果，如果还是true，继续执行循环体，直到布尔表达式结果为false，while循环结束。

* **while循环的循环次数是：0~n次**



### 5.5 do..while循环

* 语法机制

```java
do {
    循环体;
}while(布尔表达式);
```

* 执行原理：
  1. 先执行循环体当中的代码，执行一次循环体之后，判断布尔表达式的结果
  2. 如果为true，则继续执行循环体，如果为false循环结束
* **对于do..while循环来说循环体执行次数是：1~n次。**



### 5.6 break;语句

* break;语句可以用在哪里呢
  1. switch 语句当中，用来终止 switch 语句的执行。用在 switch 语句当中，防止 case 穿透现象，用来**==终止 switch==**。
  2. break;语句用在循环语句当中，**==用来终止离它最近的那个循环语句==**。
* 一种特殊的语法（不怎么用）

```java
a:for(int k = 0; k < 2; k++){ 
    b:for(int i = 0; i < 10; i++){
        if(i == 5){
            break a; // 终止指定的循环，即整个大循环。
        }
        System.out.println("i ===> " + i); 
    }
}
```



### 5.7 continue;语句

* continue语句的作用是：**==终止当前"本次"循环，直接进入下一次循环继续执行。==**





## 6、方法与递归

**对于一个java程序来说，如果没有“方法”，代码无法得到复用。**

* 方法怎么定义，语法机制是什么

```java
[修饰符列表] 返回值类型 方法名(形式参数列表){
    方法体; 
}
// 如
public static int add (int a, int b) {
    return a + b;
}

public static 是修饰符列表，不是必须的，是可选的
int 是返回值类型
add 是方法名
int a, int b 是形式参数
return a + b； 是方法体，是Java语句
```

* 返回值：
  * 返回值类型可以是任何类型，只要是 Java 中合法的数据类型就行，数据类型包括**==基本数据类型==**和**==引用数据类型==**
  * 返回值一般指的是一个方法执行结束之后的结果。结果通常是一个数据，所以被称为“值”，而且还叫“返回值”。
  * 当一个方法执行结束不返回任何值的时候，返回值类型也不能空白，必须写上 **void关键字**
  * 当返回值类型不是 void 的的时候，在方法体结束时一定要写 return 值; 
  * **只要有 “return” 关键字的语句执行，当前方法必然结束**。return 只要执行，当前所在的方法结束，记住：不是整个程序结束。

* 方法名：方法名要见名知意。（驼峰命名方式）
* 形式参数列表：形式参数列表中的每一个参数都是“局部变量”，方法结束之后内存释放。形参的个数是：0~N个。

* 方法定义之后怎么调用（目前是 static 修饰的静态方法）：

```java
类名.方法名(实际参数列表);
```



### 6.1 return; 和 break; 和 continue; 的区别

* return：用来终止离它最近的一个方法
* break：用来终止switch和离它最近的循环
* continue：终止当前"本次"循环，直接进入下一次循环继续执行



### 6.2 一个错误

* 11: 错误: 缺少返回语句

```java
public class A {
	public static void main(String[] args){
		int x = m1(true);
		System.out.println(x);
	} 

	public static int m1(boolean flag) {
		if (flag) {
			return 1;
		}
        // 以下语句也得写上
        return 0；
	}
}
```



### 6.3 JVM中三块主要的内存

分别是 **==栈内存、堆内存、方法区==**

* 方法区：存放代码片段。存放class字节码（最先有文件的）
* 堆内存：[后面讲](####8.2.6 创建对象对应的 JVM 内存结构)
* 栈内存：方法调用的时候，该方法需要的内存空间在栈中分配。
  * 方法调用叫做：压栈（push）。分配空间
  * 方法结束叫做：弹栈（pop）。释放空间
  * **栈中存储什么：方法运行过程中需要的内存，以及栈中会存储方法的局部变量**

![image-20210204161426273](https://img-blog.csdnimg.cn/20210204162557342.png)

* 方法执行时内存的变化，[视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=350)

```java
public class MethodTest08{
	//主方法，入口
	public static void main(String[] args){
		System.out.println("main begin");
		int x = 100;
		m1(x);
		System.out.println("main over");
	}
	public static void m1(int i){ // i是局部变量
		System.out.println("m1 begin");
		m2(i);
		System.out.println("m1 over");
	}
	public static void m2(int i){
		System.out.println("m2 begin");
		m3(i);
		System.out.println("m2 over");
	
	}
	public static void m3(int i){
		System.out.println("m3 begin");
		System.out.println(i);
		System.out.println("m3 over");
	}
}
```

![image-20210204163942945](https://img-blog.csdnimg.cn/20210204164036207.png)



### 6.3 方法重载（Overload）

* 什么时候需要考虑使用方法重载：
  * 在同一个类当中，**如果“功能1”和“功能2”它们的功能是相似的**，那么可以考虑将它们的方法名一致，这样代码既美观，又便于后期的代码编写（容易记忆，方便使用）
  * 方法重载overload不能随便使用，如果两个功能压根不相干，不相似，根本没关系，此时两个方法使用重载机制的话，会导致编码更麻烦。无法进行方法功能的区分。

* 什么时候代码会发生方法重载：

  * 条件1：在同一个类当中
  * 条件2：方法名相同
  * 条件3：参数列表不同
    * ==参数的个数==不同算不同
    * ==参数的类型==不同算不同
    * ==参数的顺序==不同算不同

  * ==方法重载和方法的 “返回值类型” 和 “修饰符列表” 无关==

```java
public static int a() {
    
}
public static int a(int a, int b) {
    
}
public static int a(int a, long b) {
    
}
// 这样构成方法重载
```

```java
public static int m() {
    
}
public static double m() {
    
}
// 这样不构成方法重载
```



### 6.4 方法递归

**方法自己调用自己，这就是方法递归**

**当递归时程序没有结束条件，一定会发生：==栈内存溢出错误：StackOverflowError==**

**==所以：递归必须要有结束条件==**

* 递归执行是栈内存中的变化

```java
public class A {
	// 入口
	public static void main(String[] args){
		doSome(5);
		System.out.println("doSome over");
	}

	public static void doSome(int num){
		System.out.println("doSome "+"["+num+"]"+ "begin");
		// 结束条件
		if (num == 0) {
			return;
		}
		doSome(--num);
		System.out.println("doSome "+"["+(num+1)+"]"+ "over");
	}
}
```

![20210205114536800.png](https://img-blog.csdnimg.cn/20210205114536800.png)

* 使用递归实现计算 1+2+3+...+100 

```java
public class A {
	public static void main(String[] args){
		/*
		使用递归实现计算 1+2+3+...+100 
		 */
		System.out.println(sum(100));
	}

	public static int sum(int num) {
		if (num == 1) {
			return 1;
		}
		return num + sum(--num);
	}
}

```





## 8、认识面向对象

### 8.1 面向对象和面向过程 

* [视频详解](https://www.bilibili.com/video/BV1Rx411876f?p=373)

* 使用面向对象编程思想开发系统，在现代开发中会将面向对象贯穿整个过程，一般包括：
  * OOA：面向对象分析（Object-Oriented Analysis） 
  * OOD：面向对象设计（Object-Oriented Design）
  * OOP：面向对象编程（Object-Oriented Programming）
* **面向对象三大特征**
  * 封装（Encapsulation） 
  * 继承（Inheritance） 
  * 多态（Polymorphism）



### 8.2 类和对象的概念(很枯燥但很重要)

[视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=379)

#### 8.2.1 什么是类

* 类实际上在现实世界当中是==不存在的，是一个抽象的概念==。是一个模板。是我们人类大脑进行“思考、总结、抽象”的一个结果。
* 类本质上是现实世界当中某些事物具有共同特征，将这些共同特征提取出来形成的概念就是一个“类”，==“类”就是一个模板==。

#### 8.2.2 什么是对象

* ==对象是实际存在的个体==
* 在java语言中，要想得到“对象”，必须先定义“类”，**“对象”是通过“类”这个模板创造出来的**。

#### 8.2.3 术语

* 类：不存在的，人类大脑思考中总结的一个模板
* 对象：实际存在的个体，通过 “类” 创造出来
* 实例：对象的另一个名字
* 实例化：通过类这个模板将对象创建出来的过程叫做实例化
* 抽象：多个对象具有的共同特征，进行思考总结抽取共同特征的过程
* ==类 ---> 【实例化】 ---> 对象（实例）==
* ==对象 ---> 【抽象】 ---> 类==

#### 8.2.4 类的定义

```java
[修饰符] class 类名 {
 	// 类体 = 属性 + 方法
    // 属性在代码上以“变量”的形式存在
    // 方法描述动作或行为
}
```

定义一个学生类

```java
public class Student {
    // 以下四个变量即为 属性
    int sno;// 学号
    String name;// 姓名
    boolean gender;// 性别（true表示男，false表示女）
    String address;// 住址
    
    // 以下是一个方法
    public void print() {
        System.out.println(name + "的学号是：" + sno + "，性别是：" + (gender ? "男" : "女") + "，住在：" + address);
    }
}
```

#### 8.2.5 对象创建

```java
类名 变量名 = new 类名();// 这样就完成了对象的创建
// 如
Student student = new Student();
```

* 什么是实例变量：对象又被称为实例变量，实例变量在实际上就是：对象级别的变量
* 不能通过类名来直接访问实例变量，需要new对象后，通过 **“对象名.实例变量”** 才能访问实例变量

```java
// 如People类中的name变量就是实例变量
public class Person {
    String name;
}
```

#### 8.2.6 创建对象对应的 JVM 内存结构

[视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=385)

以下是一个学生类

```java
public class Student{
	// 属性（描述状态），在java程序中以“成员变量”的形式存在。
	// 学号
	// 一个对象一份。
	int no; // 这种成员变量又被称为“实例变量”。
	// 姓名
	String name;
	// 年龄
	int age;
	// 性别
	boolean sex;
	// 住址
	String addr;
}
```

以下main方法中使用学生类

```java
public class StudentTest {
    public static void main(String[] args) {
        Student s1 = new Student();
    }
}
```

![image-20210206110147553](https://img-blog.csdnimg.cn/20210206110351783.png)

#### 8.2.7 对象和引用的区别

* 对象是 new 出来的，在堆内存中存储
* 是一个变量，这个变量中储存了一个内存地址，指向了对象在堆内存中的地址

#### 8.2.8 系统默认值

对于成员变量来说，没有手动赋值时，系统默认赋值

| 数据类型     | 缺省默认值 |
| ------------ | ---------- |
| byte         | 0          |
| short        | 0          |
| int          | 0          |
| long         | 0L         |
| float        | 0.0f       |
| double       | 0.0        |
| boolean      | false      |
| cher         | '\u0000'   |
| 引用数据类型 | null       |

#### 8.2.9 画以下程序的内存图

```java
public class T{
	A o1; 
	public static void main(String[] args){
		D d = new D();
		C c = new C();
		B b = new B();
		A a = new A();
		T t = new T();

		c.o4 = d;
		b.o3 = c;
		a.o2 = b;
		t.o1 = a;

		System.out.println(t.o1.o2.o3.o4.i);
	}
}
class A{
	B o2;
}
class B{
	C o3;
}
class C{
	D o4;
}
class D{
	int i;
}
```

![内存图](https://img-blog.csdnimg.cn/20210206114813124.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTYwMTA0MA==,size_16,color_FFFFFF,t_70#pic_center)

#### 8.2.10 空指针异常（NullPointerException）

**==导致空指针异常最本质的原因是：空引用访问 “实例相关的数据”（包括实例变量 + 实例方法），会出现空指针异常==**

观察以下程序：

```java
/*
	空指针异常。（NullPointerException）

	关于垃圾回收器：GC
		在java语言中，垃圾回收器主要针对的是堆内存。
		当一个java对象没有任何引用指向该对象的时候，
		GC会考虑将该垃圾数据释放回收掉。
	
	出现空指针异常的前提条件是？
		"空引用"访问实例【对象相关】相关的数据时，都会出现空指针异常。
*/
public class NullPointerTest{
	public static void main(String[] args){
		// 创建客户对象
		Customer c = new Customer();
		// 访问这个客户的id
		System.out.println(c.id); // 0

		// 重新给id赋值
		c.id = 9521; // 终身代号
		System.out.println("客户的id是=" + c.id);

		c = null;
		// NullPointerException
		// 编译器没问题，因为编译器只检查语法，编译器发现c是Customer类型，
		// Customer类型中有id属性，所以可以：c.id。语法过了。
		// 但是运行的时候需要对象的存在，但是对象没了，尴尬了，就只能出现一个异常。
		System.out.println(c.id);
	}
}

class Customer{
	// 客户id
	int id; // 成员变量中的实例变量，应该先创建对象，然后通过“引用.”的方式访问。
}
```



![image-20210206122203931](https://img-blog.csdnimg.cn/20210206122223128.png)

#### 8.2.11 方法调用时的参数传递

* 参数传递的时候，和类型无关，不管是基本数据类型还是引用数据类型统一都是将变量中保存的那个“值”复制一份，传递下去，这个值可能是一个数字、字符串、可能是一个内存地址。



### 8.3 构造方法

>  **构造方法使用来创建对象的，并且给对象当中的实例变量赋值。**
>  
> **当一个类中没有提供任何构造方法，系统默认提供一个无参数的构造方法。这个==无参数的构造方法叫做缺省构造器==。**
>
> **当一个类中手动提供了构造方法，那么系统将不在提供默认的无参构造方法。**

* 构造方法的语法结构
  * 构造方法名和类名必须一致
  * 构造方法不需要指定返回值类型，也不能写void
  * 通常在构造方法体当中给属性赋值，完成属性的初始化

```java
[修饰符列表] 构造方法名(形式参数列表){
    构造方法体;
}
```

* 调用构造方法怎么调用呢
  * 使用new运算符来调用构造方法
  * 语法格式：

```java
new 构造方法名(实际参数列表);
```

* 构造方法支持方法重载：
  * 构造方法是支持方法重载的
  * 在一个类当中构造方法可以有多个
  * 并且所有的构造方法名字都是一样的

* 对于实例变量来说，==只要你在构造方法中没有手动给它赋值，统一都会默认赋值==。默认赋系统值。如：

```java
public class Vip{
	// 会员号
	long no;
	// 会员姓名
	String name;
	// 生日
	String birth;
	// 性别
	boolean sex;
	//无参数构造方法
	public Vip(){
		// 实际上这里还有两行代码（没有手动赋值，系统都会默认赋值。）
        // no = 0L;
        // name = null;
        // birth = null;
        // sex = false;
	}

	//有参数构造方法
	public Vip(long huiYuanHao, String xingMing){
		// 给实例变量赋值【初始化实例变量，初始化属性】
		no = huiYuanHao;
		name = xingMing;
		// 实际上这里还有两行代码（没有手动赋值，系统都会默认赋值。）
		//birth = null;
		//sex = false;
	}

	//有参数构造方法
	public Vip(long huiYuanHao,String xingMing, String shengRi){
		no = huiYuanHao;
		name = xingMing;
		birth = shengRi;
		// 实际上这里有一行默认的代码
		//sex = false;
	}

	//有参数的构造方法
	public Vip(long huiYuanHao,String xingMing,String shengRi,boolean xingBie){
		no = huiYuanHao;
		name = xingMing;
		birth = shengRi;
		sex = xingBie;
	}
}
```



## 9、封装

### 9.1 面向对象的三大特征

* **封装**
* **继承**
* **多态**

**有了封装，才有继承；有了继承，才有多态。**



### 9.2 什么是封装

* 封装的作用：
  * 第一个作用：保证内部结构的安全
  * 第二个作用：屏蔽复杂，暴露简单



### 9.3 实例方法

* 带有 static 的方法和不带有 static 的方法的调用
  * 带有 static：通过类名直接调用（类级别的方法）
  * 不带有 static：创建对象，通过对象来调用（对象级别的方法）

```java
public class MethodTest{
	public static void main(String[] args){
        // 以下是调用的静态方法（就是带 static 修饰的）
		MethodTest.doSome();
		//类名. 可以省略（在同一个类中。）
		doSome();
        
        // 以下是调用实例方法（就是不带 staitc 修饰的）
		// 尝试使用“类名.”的方式访问“实例方法”
		// 错误的
		//MethodTest.doOther();
		
		// 创建对象
		MethodTest mt = new MethodTest();
		// 通过"引用."的方式访问实例方法。
		mt.doOther();

	}	

	// 带有static
	public static void doSome(){
		System.out.println("do some!");
	}

	//这个方法没有static，这样的方法被称为：实例方法。（对象方法，对象级别的方法）
	public void doOther(){
		System.out.println("do other 
	}

}
```

* **注意：只要是方法，不管是静态方法、实例方法还是构造方法，它们在运行的时候都需要压栈。**

### 9.4 怎么进行封装，代码怎么实现

* 第一步：属性私有化（使用private关键字进行修饰。）
  * private 表示私有的，被这个关键词修饰之后，该数据只能在本类中访问。
* 第二步：对外提供简单的操作入口。
  * 对外提供公开的set方法和get方法作为操作入口，并且都不带static，都是实例方法。
  * **java开发规范中有要求，set方法和get方法要满足以下格式**

```java
get方法的要求：
    public 返回值类型 get+属性名首字母大写(无参){
    	return xxx;
	}
set方法的要求：
    public void set+属性名首字母大写(有1个参数){
	    xxx = 参数;
	}
```

通过一个程序演示 get 方法和 set 方法

```java
public class Person {
    // 实例变量
    private int age;
    
    // get方法
    public int getAge() {
        return age;
    }
    
    // set方法
    public void setAge(int newAge) {
        // 可以在这里设置“关卡”来过滤掉一些不合法数据
        if (newAge < 0 || newAge > 150) {
            System.out.println("您输入的数据不合法，请重新输入！");
            return;// 直接退出方法
        }
        age = newAge;
    }
    
}
```





## 10、static和this关键字

### 10.1 static

#### 10.1.1 static介绍

* static翻译为“静态”
* 所有static关键字修饰的都是类相关的，类级别的。
* 所有static修饰的，都是采用“类名.”的方式访问。
* static修饰的变量：静态变量
* static修饰的方法：静态方法

#### 10.1.2 变量的分类

* 根据声明的位置进行划分：
  * 在方法体当中声明的变量叫做：局部变量
  * 在方法体之外声明的变量叫做：成员变量
* 成员变量又可以分为：
  * 实例变量
  * 静态变量
* 三种变量分别存储在不同的内存中：
  * 局部变量：存储在栈内存中
  * 实例变量：存储在堆内存中（对象级别的）
  * 静态变量：存储在方法区中（是最先初始化的）（类级别的）

```java
class VarTest{

	// 以下实例的，都是对象相关的，访问时采用“引用.”的方式访问。需要先new对象。
	// 实例相关的，必须先有对象，才能访问，可能会出现空指针异常。
	// 成员变量中的实例变量
	int i;

	// 实例方法
	public void m2(){
		// 局部变量
		int x = 200;
	}

	// 以下静态的，都是类相关的，访问时采用“类名.”的方式访问。不需要new对象。
	// 不需要对象的参与即可访问。没有空指针异常的发生。
	// 成员变量中的静态变量
	static int k;

	// 静态方法
	public static void m1(){
		// 局部变量
		int m = 100;
	}
	
}
```



#### 10.1.3 什么时候使用静态变量 

* **如果这个类型的所有对象的某个属性值都是一样的**，不建议定义为实例变量，浪费内存空间
* 建议定义为类级别特征，**定义为静态变量，在 ==方法区== 中只保留一份**，节省内存开销。
* **一个对象一份的是实例变量。**
* **所有对象一份的是静态变量**
* ==划重点：静态变量会在类加载的时候初始化，并且存储在方法区中。==

```java
// 定义一个类表示中国人
public class Chinese {
    // 身份证
    // 每个人的身份证都不一样，用实例变量表示
    String idCard;
    // 姓名
    // 一个人对应一个名字，用实例变量表示
    String name;
    // 国籍
    // 每个人的国籍都一样，属于整个类的特征，使用静态变量表示
    static String country;
}
```

#### 10.1.4 实例变量和静态变量访问方法的区别

* 实例变量：一定需要使用 “引用.” 来访问
* 静态变量：建议使用 “类名.” 来访问，也可以使用 “引用.” 来访问，但是不推荐，这样会产生歧义
* **当 “空引用” 访问 “实例” 相关（实例变量，实例方法）的时候，会出现空指针异常；**
* **当 “空引用” 访问 “类” 相关（静态变量，静态方法）的时候，不会出现空指针异常。**

#### 10.1.5 什么时候定义为实例方法？什么时候定义为静态方法？

* 一个方法一般描述了一个行为，如果说该行为必须由对象去触发，那么该方法定义为实例方法。
* 当这个方法体当中，**==直接访问了实例变量==**，这个方法一定是实例方法。
* 我们以后开发中，大部分情况下，如果是工具类的话，**工具类当中的方法一般都是静态的**。(静态方法有一个优点，是不需要new对象，直接采用类名调用，极其方便。工具类就是为了方便，所以工具类中的方法一般都是static的。)

#### 10.1.6 静态代码块

使用 static 关键字可以定义静态代码块

* 语法：

```java
static {
    java语句;
    java语句;
}
```

* 静态代码块在什么时候执行：
  * ==类加载时执行==（早于 main 方法执行）
  * 并且只执行一次
* 一个程序可以写多个静态代码块
* 静态代码块一般是按照自上而下的顺序执行
* 静态代码块有啥作用，有什么用
  * 静态代码块不是那么常用（不是在每一个类中都要写）
  * 静态代码块这种语法机制实际上是SUN公司给我们java程序员的==一个特殊的时刻/时机==。这个时机叫做：==类加载时机==。如：**记录类加载的日志信息**

```java
public class StaticTest {
    // 静态代码块
    static {
        System.out.println("我是第一个静态代码块");
    }
    
    // 静态代码块
    static {
        System.out.println("我是第二个静态代码块");
    }
    
    // main方法
    public static void main(String[] args) {
        System.out.println("我是main方法");
    }
    // 静态代码块
    static {
        System.out.println("我是第三个静态代码块");
    }
}

/*
输出：
    我是第一个静态代码块
    我是第二个静态代码块
    我是第三个静态代码块
    我是main方法
*/
```

#### 10.1.7 JVM中的三块内存

* 方法只要执行，会压栈。（局部变量）
* new出来的对象都在堆中。垃圾回收器主要针对。（实例变量）
* 类的信息，字节码信息，代码片段。（静态变量）
* **静态方法的代码片段放在方法区，但是方法执行过程当中需要的内存在栈中。**

#### 10.1.8 目前为止，在 Java 程序中有顺序要求的

1. 对于一个方法来说，方法体中的代码执行是有顺序的，遵循自上而下的顺序执行
2. 静态代码块一和静态代码块二的执行是有先后顺序的
3.  静态代码块和静态变量在类加载时是有先后顺序的

#### 10.1.9 实例代码块

* 语法

```java
{
    java语句;
    java语句;
    java语句;
}
```

* 实例语句块在什么时候执行
  * 实例语句在类加载是**并没有执行**
  * 只要是构造方法执行，必然在构造方法执行之前，自动执行“实例语句块”中的代码。（==在构造方法前执行==）
  * 实际上这也是SUN公司为java程序员准备一个特殊的时机，叫做==对象构建时机==。

```java
public class InstanceCode{

	//入口
	public static void main(String[] args){
		System.out.println("main begin");
		new InstanceCode();// 调用无参构造
		new InstanceCode();
		new InstanceCode("abc");// 调用有参构造
		new InstanceCode("xyz");
	}
    
	//实例语句块
	{
		System.out.println("实例语句块执行！");	
	}

	// Constructor
	public InstanceCode(){
		System.out.println("无参数构造方法");
	}

	// Constructor
	public InstanceCode(String name){
		System.out.println("有参数的构造方法");
	}
}

/*
输出：
    main begin
    实例语句块执行！
    无参数构造方法
    实例语句块执行！
    无参数构造方法
    实例语句块执行！
    有参数的构造方法
    实例语句块执行！
    有参数的构造方法
*/
```





### 10.2 this

#### 10.2.1 this介绍

* this是一个关键字，全部小写。
* 一个对象一个this
* this是一个变量，是一个引用，==this保存当前对象的内存地址，指向自身==，严格意义上来说，this代表的就是“当前对象”
* ==this存储在堆内存当中对象的内部==

#### 10.2.2 this的内存结构

```java
public class ThisTest01{
	public static void main(String[] args){

		Customer c1 = new Customer("张三");
		Customer c2 = new Customer("李四");
	}
}

// 顾客类
class Customer{

	// 实例变量
	String name;   

	//构造方法
	public Customer(){
	
	}
	public Customer(String s){
		name = s;
	}
}
```

![image-20210206205256696](https://img-blog.csdnimg.cn/20210206205315532.png)

#### 10.2.3 this的使用

* ==this只能使用在实例方法中==。谁调用这个实例方法，this就是谁。所以this代表的是：当前对象。
* “this.”大部分情况下是可以省略的
* 为什么this不能使用在静态方法中
  * this代表当前对象，静态方法中不存在当前对象

#### 10.2.4 this. 什么时候不能省略

* 在实例方法中，或者构造方法中，==为了区分局部变量和实例变量==，这种情况下：this. 是不能省略的。

#### 10.2.5 this()

**this除了可以使用在实例方法中，还可以用在构造方法中**

* 通过当前的构造方法去调用另一个本类的构造方法，可以使用以下语法格式

```java
this(实际参数列表);
```

* 通过一个构造方法1去调用构造方法2，可以做到**代码复用**。但需要注意的是：“构造方法1”和“构造方法2” 都是在同一个类当中。

* ==注意：对于this()的调用只能出现在构造方法的第一行==

```java
public class Date {
    int year;
    int month;
    int day;
    
    // 调用无参构造方法是，显示 1970年1月1日
    public Date() {
        this(1970, 1, 1);
    }
    
    // 有参构造
    public Date(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }
}
```





## 11、继承（extends）

### 11.1 继承的作用

* 基本作用：子类继承父类，代码可以得到复用
* 重要作用：因为有了继承关系，才有了后期的 **方法覆盖 和 多态机制**

### 11.2 继承的相关特性

* B 类继承 A 类，则称 A 类为超类（superclass）、父类、基类，B 类则称为子类（subclass）、派生类、扩展类
* Java 中只支持单继承，不支持多继承，如 class A extends B,C{} ，这样是错误的
* 虽然Java中不支持多继承，但有时候会产生间接继承效果，如class A extends B{}   class B extends C{}，其实A就是间接继承于C的
* Java中规定，==子类继承父类，除构造方法不能继承外，剩下都可以继承。但是私有的属性无法在子类中直接访问==。（即父类中 private 修饰的不能在子类中直接访问，可以通过间接的手段）
* Java 中的类没有显示继承任何类，==则默认继承 Object 类==，Object 类是 Java 语言提供的根类（老祖宗类）， 也就是说，==一个对象与生俱来就有Object类型中所有的特征==。
* 继承也存在一些缺点，例如A类继承B类会导致它们之间耦合度非常高，B类发生改变后会马上影响A类。

### 11.3 继承的使用

* 本质上，子类继承父类之后，**是将父类继承过来的方法归为自己所有**。实际上调用的也不是父类的方法，是他子类自己的方法（因为已经继承过来了就属于自己的。）。

* 在实际开发中，满足什么条件的时候，我可以使用继承呢：
  * 凡是采用 **“is a/an”** 能描述的，都可以继承

```java
例如：
    Cat is an Animal：猫是一个动物
    Dog is an Animal：狗是一个动物
    CreditAccount is an Account：信用卡账户是一个银行账户
    ....
```

### 11.4 看看 Object 类的源码

```java
public class Object {
	 
	 // 注意：当源码当中一个方法以“;”结尾，并且修饰符列表中有“native”关键字
	 // 表示底层调用C++写的dll程序（dll动态链接库文件）
    private static native void registerNatives();

	 // 静态代码块
    static {
		  // 调用registerNatives()方法。
        registerNatives();
    }

	 // 无参数构造方法
    @HotSpotIntrinsicCandidate// 注解
    public Object() {}

	 // 底层也是调用C++
    @HotSpotIntrinsicCandidate
    public final native Class<?> getClass();

	 // 底层也是调用C++
    @HotSpotIntrinsicCandidate
    public native int hashCode();

	 // equals方法你应该能看懂。
	 // public是公开的
	 // boolean 是方法的返回值类型
	 // equals 是一个方法名：相等
	 // (Object obj) 形参
	 // 只不过目前还不知道这个方法存在的意义。
    public boolean equals(Object obj) {
		 //方法体
       return (this == obj);
    }
    
	 // 已有对象a，想创建一个和a一模一样的对象，你可以调用这个克隆方法。
	 // 底层也是调用C++
    @HotSpotIntrinsicCandidate
    protected native Object clone() throws CloneNotSupportedException;

	 // 一会我们可以测试一下toString()方法。
	 // public表示公共的
	 // String 是返回值类型，toString()方法执行结束之后返回一个字符串。
	 // toString 这是方法名。
	 // () 表示形参个数为0
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }

    @HotSpotIntrinsicCandidate
    public final native void notify();

    @HotSpotIntrinsicCandidate
    public final native void notifyAll();

    public final void wait() throws InterruptedException {
        wait(0L);
    }

    public final native void wait(long timeoutMillis) throws InterruptedException;

    public final void wait(long timeoutMillis, int nanos) throws InterruptedException {
        if (timeoutMillis < 0) {
            throw new IllegalArgumentException("timeoutMillis value is negative");
        }

        if (nanos < 0 || nanos > 999999) {
            throw new IllegalArgumentException(
                                "nanosecond timeout value out of range");
        }

        if (nanos > 0 && timeoutMillis < Long.MAX_VALUE) {
            timeoutMillis++;
        }

        wait(timeoutMillis);
    }
    @Deprecated(since="9")
    protected void finalize() throws Throwable { }
}
```

* 当直接输出一个**“引用”的时候，println() 方法会先自动调用 “引用.toString()”** ，然后输出 toString() 方法的执行结果。



## 12、方法覆盖（Override）

### 12.1 什么时候考虑使用方法覆盖

* 子类继承父类之后，**当继承过来的方法无法满足当前子类的业务需求时**，子类有权利对这个方法进行重新编写，有必要进行“方法的覆盖”。

* [回顾方法重载](###6.3 方法重载（Overload）)

### 12.2 怎样才能构成方法覆盖

* **两个类必须要有继承关系。**
* **重写之后的方法和之前的方法具有：**
  * **相同的返回值类型**
  * **相同的方法名**
  * **相同的形式参数列表**
* **访问权限不能更低，可以更高。**
* **重写之后的方法不能比之前的方法抛出更多的异常，可以更少。**

### 12.3 方法覆盖的使用

* 当子类对父类继承过来的方法进行“方法覆盖”之后，子类对象调用该方法的时候，一定执行覆盖之后的方法。
* **注意事项：**
  * **方法覆盖只是针对于方法，和属性无关。**
  * **私有方法无法覆盖。**
  * **构造方法不能被继承，所以构造方法也不能被覆盖。**
  * **方法覆盖只是针对于“实例方法”，“静态方法覆盖”没有意义。**

```java
public class Test{
    public static void main(String[] args) {
        Animal animal = new Animal();
        animal.move();
        Cat cat = new Cat();
        cat.move();
        Bird bird = new Bird();
        bird.move();
    }
}

class Animal {
    public void move() {
        System.out.println("动物在移动");
    }
}

class Cat extends Animal {
    // 以下是方法覆盖
    public void move() {
        System.out.println("猫在走猫步");
    }
}

class Bird extends Animal {
    // 以下是方法覆盖
    public void move() {
        System.out.println("鸟儿在飞翔");
    }
}

/*
输出：
	动物在移动
    猫在走猫步
    鸟儿在飞翔
*/
```

### 12.4 重载 toString() 方法

**调用一个 java 对象的 toString() 方法就可以将该java对象转换成字符串的表示形式。**

```java
public class Test {
    public static void main(String[] args) {
        Date date = new Date(2008, 8, 8);
        System.out.println(date);// 输出：2008年8月8日
    }
}

class Date {
    private int year;
    private int month;
    private int day;
    
    public Date() {
        this(1970, 1, 1);
    }
    public Date(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }
    
    public int getYear() {
        return year;
    }
    public void setYear(int year) {
        this.year = year;
    }
    public int getMonth() {
        return month;
    }
    public void setMonth(int month) {
        this.month = month;
    }
    public int getDay() {
        return day;
    }
    public void setDay(int day) {
        this.day = day;
    }
    
    // 重写toString()方法，输出格式为 xx年xx月xx日
    public String toString() {
        return getYear() +"年"+ getMonth() +"月"+ getDay() + "日";
    }
}
```





## 13、多态

### 13.1 向上转型和向下转型的概念

* 向上转型（**父类型引用指向子类型对象**）（子 ---转成---> 父）
  * 自动类型转换
* 向下转型（父 ---转成---> 子）
  * 强制类型转换，需要加强制类型转换符
* 注意：
  * java中允许向上转型，也允许向下转型
  * ==无论是向上转型，还是向下转型，两种类型之间必须有继承关系，没有继承关系编译器报错。==
  * 自动类型转换和强制类型转换是使用在基本数据类型上的，这里这么说只是为了好理解，在引用数据类型这里，只有向上转型和向下转型

### 13.2 对多态的理解

* **多态表示多种形态：**
  * **编译的时候一种形态。**
  * **运行的时候另一种形态。**
* 分析 第四行代码：a.move();
  * 先来分析编译阶段：
    * 对于编译器来说，编译器只知道 a 的类型是 Animal，所以编译器在检查语法的时候，会去 Animal.class 字节码文件中找 move() 方法，找到了，绑定上 move() 方法，编译通过，静态绑定成功。（==编译阶段属于静态绑定。==）
  * 再来分析运行阶段：
    * 运行阶段的时候，实际上在堆内存中创建的 java 对象是 Cat 对象，所以 move 的时候，真正参与 move 的对象是 Cat类型，所以运行阶段会动态执行 Cat 对象的 move() 方法。这个过程属于运行阶段绑定。（==运行阶段绑定属于动态绑定。==）
* 分析 a.catchMouse() 
  * 分析程序一定要**分析编译阶段的静态绑定和运行阶段的动态绑定**。只有编译通过的代码才能运行。没有编译，根本轮不到运行。
  * 在编译阶段，编译器只知道 a 是 Animal 类型，因此就去 Animal.class  文件中找 catchMouse()  方法，结果没找到，就报错了：**错误: 找不到符号**

```java
public class Test{
    public static void main(String[] args) {
       	Animal a = new Cat();// 向上转型，父类引用执行子类对象
        a.move();// 输出：猫在走猫步
        a.catchMouse();// 编译阶段报错：错误: 找不到符号
    }
}

// 父类
class Animal {
    public void move() {
        System.out.println("动物在移动");
    }
}

// 子类
class Cat extends Animal {
    // 以下是方法覆盖
    public void move() {
        System.out.println("猫在走猫步");
    }
    
    // Cat类中特有的方法
    public void catchMouse() {
    	System.out.println("猫在抓老鼠");
    }
}
```



### 13.3 什么时候必须使用“向下转型”

* **当你需要访问的是子类对象中“特有”的方法。此时必须进行向下转型。**

* **使用强制类型转换会有风险**



### 13.4 类型转换异常（ClassCastException）

* 向下转型，这样是没有毛病的

```java
Animal a = new Cat();
Cat cat = (Cat) a;
a.catchMouse();
```

* 但这样就会有问题了，会出现类转换异常（ClassCastException）

```java
Animal a = new Bird();
Cat cat = (Cat) a;
a.catchMouse();
```

分析：

* 编译时：编译器检测到 a 这个引用是 Animal 类型，而 Animal 和 Cat 之间存在继承关系，所以可以向下转型。编译没毛病。
* 运行时：堆内存实际创建的对象是：Bird 对象。在实际运行过程中，拿着 Bird 对象转换成 Cat 对象就不行了。因为 Bird 和 Cat 之间没有继承关系

```java
// 父类
class Animal {
    public void move() {
        System.out.println("动物在移动");
    }
}

// 子类
class Cat extends Animal {
    // 以下是方法覆盖
    public void move() {
        System.out.println("猫在走猫步");
    }
    
    // Cat类中特有的方法
    public void catchMouse() {
    	System.out.println("猫在抓老鼠");
    }
}

// 子类
class Bird extends Animal {
    // 以下是方法覆盖
    public void move() {
        System.out.println("鸟儿在飞翔");
    }
    
   	// Bird类中特有的方法
    public void sing() {
        System.out.println("鸟儿在唱歌");
    }
}
```



### 13.5 使用 instanceof 运算符 来避免类型转换异常

* ==instanceof 可以在运行阶段动态判断引用指向的对象的类型。==
* instanceof的语法：
  * (引用 instanceof 类型)
  * 如：`a instanceof Cat`

* instanceof 运算符的**运算结果只能是：true/false**
* c是一个引用，c变量保存了内存地址指向了堆中的对象。

```java
if (c instanceof Cat) {
    代表：c引用指向的堆内存中的java对象是一个Cat。
} else {
    代表：c引用指向的堆内存中的java对象不是一个Cat。
}
```

* 任何时候，任何地点，对类型进行向下转型时，一定要使用 instanceof  运算符进行判断。（java规范中要求的）这样可以很好的避免：ClassCastException
* 使用 [视频](https://www.bilibili.com/video/BV1Rx411876f?p=455)

```java
public class Test {
    public static void main(String[] args) {
        AnimalTest a = new AnimalTest();
        a.print(new Cat());// 输出：猫在抓老鼠
        a.print(new Bird());// 输出：鸟儿在唱歌
    }
}

class AnimalTest {
    // 一个实例方法
    public void print(Animal a) {
        // 因为我们不知道方法调用的时候回传进来哪个动物
        // 所以需要使用 instanceof 来判断类型
        if(a instanceof Cat){// 如果是 Cat类型，就向下转型成 Cat类型
			Cat c = (Cat)a;
			c.catchMouse();
		}else if(a instanceof Bird){// 如果是 Bird类型，就向下转型成 Bird类型
			Bird b = (Bird)a;
			b.sing();
		}
    }
}
```



### 13.6 多态在开发中有什么作用

* [视频](https://www.bilibili.com/video/BV1Rx411876f?p=455)

* **降低程序的耦合度，提高程序的扩展力**
* 面向抽象编程，不面向具体编程 



### 13.7 解释一些问题

#### 13.7.1  静态方法不存在方法覆盖

* 方法覆盖需要和多态机制联合起来使用才有意义
* 多态和对象有关系，而静态方法的执行不需要对象。所以，一般情况下，我们会说静态方法“不存在”方法覆盖。不探讨静态方法的覆盖。
* 如：

```java
public class Test{
	public static void main(String[] args){
		// 静态方法可以使用“引用.”来调用吗？可以
		// 虽然使用“引用.”来调用，但是和对象无关。
		Animal a = new Cat(); //多态
        
		// 静态方法和对象无关。
		// 虽然使用“引用.”来调用。但是实际运行的时候还是：Animal.doSome()
		a.doSome();// 输出：Animal的doSome方法执行！
		Animal.doSome();// 输出：Animal的doSome方法执行！
		Cat.doSome();// 输出：Cat的doSome方法执行！
	}
}

class Animal{
	// 父类的静态方法
	public static void doSome(){
		System.out.println("Animal的doSome方法执行！");
	}
}

class Cat extends Animal{
	// 尝试在子类当中对父类的静态方法进行重写
	public static void doSome(){
		System.out.println("Cat的doSome方法执行！");
	}
}
```

#### 13.7.2 私有方法不能覆盖

```java
// 经过测试，你记住就行。
// 私有方法不能覆盖。
public class OverrideTest06{

	// 私有方法
	private void doSome(){
		System.out.println("OverrideTest06's private method doSome execute!");
	}

	// 入口
	public static void main(String[] args){
		// 多态
		OverrideTest06 ot = new T();
		ot.doSome(); //OverrideTest06's private method doSome execute!
	}
}

/*
// 在外部类中无法访问私有的。
class MyMain{
	public static void main(String[] args){
		OverrideTest06 ot = new T();
		//错误: doSome() 在 OverrideTest06 中是 private 访问控制
		//ot.doSome();
	}
}
*/

// 子类
class T extends OverrideTest06{
	// 尝试重写父类中的doSome()方法
	// 访问权限不能更低，可以更高。
	public void doSome(){
		System.out.println("T's public doSome method execute!");
	}
}
```





## 14、super关键字

### 14.1 super介绍

1. **super能出现在实例方法和构造方法中。**
2. **super的语法是：“super.”、“super()”**
3. **super不能使用在静态方法中。**
4. **super. 大部分情况下是可以省略的。**
5. **[super.什么时候不能省略呢](###14.4 super. 什么时候不能省略)**
6. ==super() 只能出现在构造方法第一行，通过当前的构造方法去调用“父类”中的构造方法，目的是：创建子类对象的时候，先初始化父类型特征。==
7. super 不是引用。super也不保存内存地址，super也不指向任何对象。==super 只是代表当前对象内部的那一块父类型的特征==。

* 重要的结论：

  * ==当一个构造方法第一行：既没有this()又没有super()的话，默认会有一个super()==; 表示通过当前子类的构造方法调用父类的无参数构造方法。**所以必须保证父类的无参数构造方法是存在的。**

  * **this()和super() 不能共存，它们都是只能出现在构造方法第一行。**

```java
public class A {
    public static void main(String[] args) {
        C c = new C();
        /*
        	输出：
        		B类的有参数构造方法！
				C类的无参数构造方法！
        */
    }
}

// 父类
class B {
	String name;
	public B() {
		System.out.println("B类的无参数构造方法！");
	}
	public B(String name) {
		System.out.println("B类的有参数构造方法！");
	}
}

// 子类
class C extends B {
    /*
	public C() {
		// 其实在这里还有一句 super()，调用了B类的无参构造方法
		System.out.println("C类的无参数构造方法！");
	}
	*/
    
    public C() {
		// 也可以自己写 super("abc"); 表示调用了B类的有参构造方法
        super("abc");
		System.out.println("C类的无参数构造方法！");
	}
}
```

* this 和 super 混合

```java
public class A {
    public static void main(String[] args) {
        new C();
        /*
        	输出：
        		B类的无参数构造方法！
        		C类的有参数构造方法！
        		C类的无参数构造方法！
         */
    }
}

// 父类
class B {
	String name;
	public B() {
		System.out.println("B类的无参数构造方法！");
	}
	public B(String name) {
		System.out.println("B类的有参数构造方法！");
	}
}

// 子类
class C extends B {
	public C() {
        // 因为this和super不能同时出现，这里有了this，super()就没有了，也不能自己写上super()
        this("abc");
		System.out.println("C类的无参数构造方法！");
	}

	public C(String name) {
        // 这里其实还有个 super()，来调用父类的无参构造方法
		System.out.println("C类的有参数构造方法！");
	}
}
```



### 14.2 super(实参) 的用法

* **当在子类的构造方法中需要给从父类继承下来的属性赋值时，由于属性私有化，子类不能直接访问该属性，此时可以通过 super(实参) 来调用父类的构造方法，给属性赋值。**
* ==super(实参) 的作用是：初始化当前对象的父类型特征==。并不是创建新对象。实际上对象只创建了1个。
* ==super 关键字代表的就是“当前对象”的那部分父类型特征==

如：以下程序中 64行代码 就可以通过 `super(actno, balance)` 调用父类构造方法给父类中的属性赋值

```java
public class SuperTest03{
	public static void main(String[] args){

		CreditAccount ca1 = new CreditAccount();
		System.out.println(ca1.getActno() + "," + ca1.getBalance() + "," + ca1.getCredit());

		CreditAccount ca2 = new CreditAccount("1111", 10000.0, 0.999);
		System.out.println(ca2.getActno() + "," + ca2.getBalance() + "," + ca2.getCredit());

	}
}

// 账户类，父类
class Account extends Object{
	// 属性
	private String actno;
	private double balance;

	// 构造方法
	public Account(){
		//super();
		//this.actno = null;
		//this.balance = 0.0;
	}
	public Account(String actno, double balance){
		// super();
		this.actno = actno;
		this.balance = balance;
	}

	// setter and getter
	public void setActno(String actno){
		this.actno = actno;
	}
	public String getActno(){
		return actno;
	}
	public void setBalance(double balance){
		this.balance = balance;
	}
	public double getBalance(){
		return balance;
	}
}

// 信用账户
class CreditAccount extends Account{

	// 属性：信誉度（诚信值）
	// 子类特有的一个特征，父类没有。
	private double credit;

	// 构造方法
	public CreditAccount(String actno, double balance, double credit){

		// 私有的属性，只能在本类中访问。
		/*
		this.actno = actno;
		this.balance = balance;
		*/

		// 以上两行代码在恰当的位置，正好可以使用：super(actno, balance);
		// 通过子类的构造方法调用父类的构造方法。
		super(actno, balance);
		this.credit = credit;
	}

	// 提供无参数的构造方法
	public CreditAccount(){
		//super();
		//this.credit = 0.0;
	}

	// setter and getter方法
	public void setCredit(double credit){
		this.credit = credit;
	}
	public double getCredit(){
		return credit;
	}	
}
```



### 14.3 内存图描述 super

![image-20210207194723069](https://img-blog.csdnimg.cn/20210207194752129.png)



### 14.4 super. 什么时候不能省略

* 如果父类和子类中有同名的特征（属性和方法），并且想要在子类中访问父类的特征（属性和方法），super. 就不能省略；
* [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=472)



### 14.5 super总结

* **super.属性名    【访问父类的属性】**
* **super.方法名(实参) 【访问父类的方法】**
* **super(实参)  【调用父类的构造方法】**
* ==通过 super. 访问属性或方法的时候：==
  * ==如果在子类中没有和父类同名的属性或方法，效果同 this. 相同，可以省略 super. ；==
  * ==如果有同名的属性或方法，此时不能省略super. ，效果与 this. 不同==



## 15、面向对象

### 15.1 final关键字

* **final修饰的类无法继承**

* **final修饰的方法无法覆盖**

* **final修饰的变量只能赋一次值**

* **final修饰的引用一旦指向某个对象，则不能再重新指向其它对象，但该引用指向的对象内部的数据是可以修改的**（数组对象就是一个引用，可以对数组中的元素进行更改，但是当前对象不能指向另一个数组）

* **final修饰的实例变量必须手动初始化，不能采用系统默认值**

* **final修饰的实例变量一般和static联合使用，称为常量。**

  **如：`public static final double PI = 3.1415926;`**



### 15.2 抽象类

#### 15.2.1 对抽象类的理解

![image-20210207224810832.png](https://img-blog.csdnimg.cn/20210207224845179.png)

* 抽象类也是一种 “引用数据类型” 。编译之后也是一个 class 字节码文件。
* **类和类之间具有共同特征，将这些共同特征提取出来，形成的就是抽象类**。
* 类本身是不存在的，所以抽象类无法创建对象（即无法实例化）
* ==抽象类本身是无法实例化的，无法创建对象，所以抽象类就是用来被子类继承的。==

#### 15.2.2 抽象类的基础语法及抽象方法

* 语法

```java
[修饰符列表] abstract class 类名{
    类体;
}
```

* final 和 abstract不能联合使用，因为 final 修饰的类无法被继承，但是抽象类就是要用来被子类继承的。
* 抽象类的子类可以是抽象类。也可以是非抽象类。
* 抽象类虽然无法实例化，但是抽象类有构造方法，这个构造方法是供子类使用的。
* 抽象方法：
  * ==抽象方法表示没有实现的方法，没有方法体的方法==，如：`public abstract void doSome();`
  * 抽象方法特点是:
    * **没有方法体，以分号结尾**。
    * **前面修饰符列表中有abstract关键字。**
  * 抽象类中不一定有抽象方法，抽象方法必须出现在抽象类中
* **==一个非抽象类继承了抽象类，一定要将抽象类中的抽象方法全部实现了（即方法覆盖，但是要去掉 abstract 关键字），这是java语法上强行规定的，必须的，不然编译器就报错了。==**
  * 分析原因：因为之前有这样一个结论：**抽象方法必须出现在抽象类中**，当一个非抽象的类继承了抽象类，此时，这个非抽象类中就存在了一个抽象方法，如果实现这个抽象方法，抽象方法存在于非抽象类中，就与之前的结论相悖了。 

* 面试题（判断题）：java语言中凡是没有方法体的方法都是抽象方法：不对，错误的

  * Object类中就有很多方法都没有方法体，都是以“;”结尾的，但他们都不是抽象方法，例如：`public native int hashCode();`

  * 这个方法底层调用了C++写的动态链接库程序。
  * 前面修饰符列表中没有：abstract，有一个native，表示调用JVM本地程序。

#### 15.2.3 抽象类的作用

**降低接口实现类实现过程中的难度，将接口中不需要使用的抽象方法交给抽象类进行完成，这样接口实现类只需要将需要的方法进行重写。**

### 15.3 接口

#### 15.3.1 接口的基础语法

* 接口也是一种 “**引用数据类型**” 。编译之后也是一个 class 字节码文件。
* 接口是**完全抽象**的（**抽象类是半抽象**），或者也可以说接口是特殊的抽象类。
* 接口怎么定义，语法是什么：

```java
[修饰符列表] interface 接口名{}
```

* 接口支持多继承，一个接口可以继承多个接口。
* 接口中只包含两部分内容，**一部分是：常量，一部分是：抽象方法**。接口中没有其它内容了。只有以上两部分。
* 接口中所有的元素都是 public 修饰的。（都是公开的）
  * 接口中的抽象方法定义时：public abstract修饰符可以省略。
  * 接口中的常量的public static final可以省略。
* 接口中的方法都是抽象方法，所以接口中的方法不能有方法体。
* 类和类之间叫做继承，类和接口之间叫做实现。
  * 实现使用 implements 关键字完成
* 类和类之间叫做继承，类和接口之间叫做实现。
  * 继承使用 extends 关键字完成
* ==当一个非抽象的类实现接口的话，必须将接口中所有的抽象方法全部实现（覆盖、重写）==



#### 15.3.2 一个类可以实现多个接口

```java
public class Test {
    public static void main(String[] args) {
        ClassImpl c = new ClassImpl();
        c.methodA();// 输出：methodA
        c.methodB();// 输出：methodB
        c.methodC();// 输出：methodC
    }
}

interface A {
    void methodA();
}
interface B {
    void methodB();
}
interface C {
    void methodC();
}

// 这里实现了多个接口
class ClassImpl implements A, B, C {
    // 实现接口 A中的抽象方法
    public void methodA(){
        System.out.println("methodA");
    }
    // 实现接口 B中的抽象方法
    public void methodB(){
        System.out.println("methodB");
    }
    // 实现接口 C中的抽象方法
    public void methodC(){
        System.out.println("methodC");
    }
}
```

#### 15.3.3 当多个接口之间有同一个实现类的时候，这些接口之间也就存在了联系，可以相互转换

```java
public class Test {
    public static void main(String[] args) {
        A a = new ClassImpl();
        if (a instanceof B) {// 判断条件成立，可以将 A类型转换为 B类型
            B b = (B) a;
            b.methodB();    
        }
        if (a instanceof C) {// 因为 C接口和 A就扣没有同一个实现类，所以判断条件不成立
            C c = (C) a;
            c.methodC();
        }
        
    }
}

interface A {
    void methodA();
}
interface B {
    void methodB();
}
interface C {
    void methodC();
}

// 当前类实现了 A和 B接口，没有实现 C接口
class ClassImpl implements A, B{
    public void methodA(){
        System.out.println("methodA");
    }
    public void methodB(){
        System.out.println("methodB");
    }
}
```

#### 15.3.4 接口在开发中的作用

* **接口在开发中的作用，类似于多态在开发中的作用。**

* **多态的作用：面向抽象编程，不要面向具体编程，降低程序耦合度，提高程序扩展力。**

* **接口的使用离不开多态机制，接口 + 多态才可以降低程序耦合度**

* ==任何一个接口都有调用者和实现者，接口可以将调用者和实现者解耦合，调用者面向接口编程，实现者面向接口编写实现。==

* [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=514)

* 示例程序：通过菜单接口将厨师和顾客分离开来，降低程序耦合度

接口：FoodMenu

```java
public interface FoodMenu {
    // 西红柿炒鸡蛋
    void xihongshichaojidan();
    // 鱼香肉丝
    void yuxiangrousi();
}
```

接口实现类：Chef1、Chef2

```java
public class Chef1 implements FoodMenu{
    @Override
    public void xihongshichaojidan() {
        System.out.println("中餐师傅做的西红柿炒鸡蛋！");
    }

    @Override
    public void yuxiangrousi() {
        System.out.println("中餐师傅做的鱼香肉丝！");
    }
}
```

```java
public class Chef2 implements FoodMenu{
    @Override
    public void xihongshichaojidan() {
        System.out.println("西餐师傅做的西红柿炒鸡蛋！");
    }

    @Override
    public void yuxiangrousi() {
        System.out.println("西餐师傅做的鱼香肉丝！");
    }
}
```

接口调用类：Customer

```java
public class Customer {

    // 顾客手里有一个菜单
    private FoodMenu foodMenu;

    // 无参构造
    public Customer() {
	}

    // 有参构造
    public Customer(FoodMenu foodMenu) {
        this.foodMenu = foodMenu;
    }

    // getter and setter
    public FoodMenu getFoodMenu() {
        return foodMenu;
    }

    public void setFoodMenu(FoodMenu foodMenu) {
        this.foodMenu = foodMenu;
    }

    // 点菜方法
    public void order(int n) {
        FoodMenu foodMenu = this.getFoodMenu();
        if (n == 1) {
            foodMenu.xihongshichaojidan();
        } else if (n == 2) {
            foodMenu.yuxiangrousi();
        } else {
            System.out.println("请您重试！");
        }
    }
}
```

测试类：Test

```java
// 这个例子很经典！！！！！
// 1是西红柿炒鸡蛋， 2是鱼香肉丝
public class Test {
    public static void main(String[] args) {
        // 创建中餐厨师对象
        FoodMenu chef1 = new Chef1();
        // 创建顾客对象
        Customer customer = new Customer(chef1);
        // 顾客点菜
        customer.order(1);
        customer.order(2);
        System.out.println("----------------------------");
        // 创建中餐厨师对象
        FoodMenu chef2 = new Chef2();
        // 创建顾客对象
        Customer customer1 = new Customer(chef2);
        // 顾客点菜
        customer1.order(1);
    }
}
```

输出：

```java
中餐师傅做的西红柿炒鸡蛋！
中餐师傅做的鱼香肉丝！
----------------------------
西餐师傅做的西红柿炒鸡蛋！
```



#### 15.3.5 抽象类和接口之间的区别

1. **抽象类是半抽象的，接口是完全抽象的。**
2. **抽象类中有构造方法，接口中没有构造方法。**
3. **类和类之间只能单继承，接口和接口之间支持多继承。**
4. **一个类只能继承一个抽象类（单继承）， 一个类可以同时实现多个接口**
5. **接口中只允许出现常量和抽象方法**

6. **接口使用比抽象类多，一般抽象类使用的还是少。**
7. ==接口一般都是对“行为”的抽象。==





### 15.4 类和类之间的关系

**is a（继承）、has a（关联）、like a（实现）**

1. is a：

   Cat is an Animal（猫是一个动物）

   凡是能够满足is a的表示 ==“继承关系”==

   A extends B

2. has a：

   I has a Pen（我有一支笔）

   凡是能够满足has a关系的表示==“关联关系”==

   关联关系通常以“属性”的形式存在。

3. like a:

   Cooker like a FoodMenu（厨师像一个菜单一样）

   凡是能够满足like a关系的表示 ==“实现关系”==

   实现关系通常是：类实现接口。

   A implements B



### 15.5 package 和 import

#### 15.5.1 package

* [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=517)

#### 15.5.2 import

* [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=519)



### 15.6 访问控制权限修饰符

| 访问控制修饰符 |   本类   |    同包    |  异包子类  |  任意位置  |
| :------------: | :------: | :--------: | :--------: | :--------: |
|     public     | 可以访问 |  可以访问  |  可以访问  |  可以访问  |
|   protected    | 可以访问 |  可以访问  |  可以访问  | 不可以访问 |
|      默认      | 可以访问 |  可以访问  | 不可以访问 | 不可以访问 |
|    private     | 可以访问 | 不可以访问 | 不可以访问 | 不可以访问 |

* 访问控制权限修饰符可以修饰什么:
  * 属性（4个都能用）
  * 方法（4个都能用）
  * 类（public和默认能用，其它不行）
  * 接口（public和默认能用，其它不行）



### 15.7 JDK类库的根类：Object

#### 15.7.1 Object 类中的方法

* protected Object clone()  				// 负责对象克隆的。
* int hashCode()    							   // 获取对象哈希值的一个方法。

* boolean equals(Object obj)             // 判断两个对象是否相等

* String toString()                                 // 将对象转换成字符串形式

* protected void finalize()                   // 垃圾回收器负责调用的方法

#### 15.7.2 toString() 方法

* 源代码：

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

* 默认实现：类名@对象的内存地址转换为十六进制的形式

* 重写 toString() 方法

```java
public class Test {
    public static void main(String[] args) {
        Date date = new Date(2008, 8, 8);
        System.out.println(date);// 输出：2008年8月8日
    }
}

class Date {
    int year;
    int month;
    int day;

    public Date() {
    }

    public Date(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    @Override
    public String toString() {
        // 重写规则，越简单越明了就好
        return year + "年" + month + "月" + day + "日";
    }
}
```



#### 15.7.3 equals() 方法

* 源代码

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

* 设计目的
  * 通过equals方法来**判断两个对象是否相等**。
* 但是默认的 equals() 方法是通过 “==” 来判断两个对象的内存地址，我们需要的是判断的是对象中的内容是否相等， 因此默认 equals() 方法不够用，要重写。

* 重写 equals() 方法

```java
public class Test {
    public static void main(String[] args) {
        Date date = new Date(2008, 8, 8);
        Date date2 = new Date(2008, 8, 8);
        Date date3 = new Date(2008, 8, 9);
        System.out.println(date.equals(date2));
        System.out.println(date.equals(date3));
    }
}

class Date {
    int year;
    int month;
    int day;

    public Date() {
    }

    public Date(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    @Override
    public String toString() {
        return year + "年" + month + "月" + day + "日";
    }

    @Override
    public boolean equals(Object o) {
        // 首先判断连个对象是否是同一个对象，如果是就直接返回 true
        if (this == o) return true;
        // 如果 o是 null，或者 o的类型不是 Date类型，直接返回 false
        if (o == null || !(o instanceof Date)) return false;
        // 程序运行到这来表示：o不是 null并且是 Date类型的
        // 向下转型
        Date date = (Date) o;
        // 返回两个类的内容是否相等
        return this.year == date.year && this.month == date.month && this.day == date.day;
    }
}
```

* 结论：
  * java中什么类型的数据可以使用“==”判断：
    * java中基本数据类型比较是否相等，使用==
  * java中什么类型的数据需要使用equals判断：
    * java中所有的引用数据类型统一使用equals方法来判断是否相等。

* equals方法重写的时候要彻底，[视频](https://www.bilibili.com/video/BV1Rx411876f?p=537)



#### 15.7.4 finalize() 方法

* 源代码

```java
protected void finalize() throws Throwable { }
```

* 自从 JDK9 之后就已经过时了，了解一下就好。[视频](https://www.bilibili.com/video/BV1Rx411876f?p=538)



#### 15.7.5 hashCode() 方法

* 源代码

```java
public native int hashCode();
```

* 这个方法不是抽象方法，带有native关键字，底层调用C++程序。
* hashCode()方法返回的是哈希码：**实际上就是一个java对象的内存地址，经过哈希算法，得出的一个值。**

```java
public class Test{
    public static void main(String[] args) {
        Object obj = new Object();
        Date date = new Date();
        // 输出的值可以等同看做是 java对象的内存地址
        System.out.println(obj.hashCode());// 输出：460141958
        System.out.println(date.hashCode());// 输出：1163157884
    }
}

class Date {

}
```



### 15.8 匿名内部类

* 什么是内部类：
  * 在类的内部又定义了一个新的类，被称为内部类
* 内部类分类：
  * 静态内部类：类似于静态变量
  * 实例内部类：类似于实例变量
  * 局部内部类：类似于局部变量

```java
public class Test{
    // 该类在类的内部，所以称为内部类
    // 由于前面有static，所以称为“静态内部类”
    static class A {

    }
    // 该类在类的内部，所以称为内部类
    // 没有static叫做实例内部类。
    class B {

    }

    public void doSome() {
        // 该类在类的内部，所以称为内部类
        // 由于该类在方法中，叫做局部内部类。
        class C {

        }
    }
}
```

* 匿名内部类是局部内部类的一种，因为这个类没有名字而得名。

* 尝试使用匿名内部类

```java
public class Test {
    public static void main(String[] args) {
        MyMath myMath = new MyMath();
        // 使用匿名内部类，直接 new接口，在大括号中实现接口
        myMath.mySum(new Computer() {
            @Override
            public int sum(int a, int b) {
                return a + b;
            }
        }, 10, 100);
    }
}

// 负责计算的接口
interface Computer {
    // 抽象方法: 求和
    int sum(int a, int b);
}

// 数学类
class MyMath {
    // 数学求和方法
    public void mySum(Computer computer, int a, int b) {
        int retValue = computer.sum(a, b);
        System.out.println(a + "+" + b + "=" + retValue);
    }
}
```





## 16、数组

### 16.1 数组概要

* Java 语言中的数组是一种引用数据类型，不属于基本数据类型，数组的父类是 Object
* **数组实际上是一个容器**，可以同时容纳多个元素
* 数组中既可以存储基本数据类型数据，也可以存储引用数据类型数据
* 数组对象存储在堆内存中
* **数组当中如果存储的是 “引用数据类型”，实际上存储的是对象的 “引用” （对象的内存地址）**
* ==数组一旦创建，在 Java 中规定，数组长度不可变。==访问元素时，如果下标越界，会出现异常 ArrayIndexOutOfBoundsException（数组下标越界异常）
* 数组的内存结构

![image-20210208210831787](https://img-blog.csdnimg.cn/2021020821085041.png)

* ==所有数组对象都有一个 “length" 属性（Java自带的），用来获得数组中元素的个数。==

* 数组存储的元素类型统一。

* 数组中每一个元素存储的内存地址是连续的。

* ==将数组中第一个元素的内存地址作为整个数组对象的内存地址。==

* 数组元素的下标从 0 开始，最后一个元素的下标是： length- 1

* 数组这种数据结构的优点和缺点：

  * 优点：查询/检索某个下标的元素速度极快
    * 因为每一个元素的内存地址在空间存储上是连续的
    * 同时每一元素所占用的空间大小都是一样的
    * 指导了第一个元素的地址和要查询的元素的下标，就可以通过数学表达式计算出元素的地址，通过地址直接访问该元素。

  * 缺点：
    1. 为了保证数组中每个元素内存地址连续，所以在数组上删除元素的时候，要统一将后面的元素向前或向后位移，效率较低。
    2. 不能存储大数据量：因为很难找到一块特别大的连续的内存空间。

### 16.2 一维数组

#### 16.2.1 声明一维数组

```java
int[] array01;
double[] array02;
String[] array03;
boolean[] array04;
Object[] array05;
```

#### 16.2.2 初始化一维数组

* 静态初始化：

```java
int[] array = {1, 2, 3, 4, 5};
```

* 动态初始化：数组长度为 5，每个数组元素元素的值为 0

```java
int[] array = new int[5];// 初始化5个长度的int类型数组，每个元素默认值为0
String[] array2 = new String[6];// 初始哈6个长度的String类型数组，每个元素默认值null
```

* 什么时候静态初始化，什么时候动态初始化：

  * 当数组中的元素已经确定下来的时候，使用静态初始化。
  * 当数组中元素暂时不能确定下来的时候，动态初始化先把空间占了，之后在赋值。

* 方法的参数是数组

```java
public class Test {
    public static void main(String[] args) {
        String[] array = new String[5];
        String[] array02 = {"fff", "sss", "vvv"};
        // 向数组中传一个动态初始化的数组
        print(new String[6]);
        // 向数组中传一个静态初始化的数组
        print(new String[]{"12", "34", "56"});
    }

    public static void print(String[] array) {
        for (int i = 0; i <= array.length - 1; i++) {
            System.out.println(array[i]);
        }
    }
}
```



#### 16.2.3 mian方法中的String数组

JVM调用 mian 方法的时候，会自动传一个 String 类型的数组过来

**这个数组对象的长度是：0**

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("JVM传递过来的数组的长度是：" + args.length);// 输出：JVM传递过来的数组的长度是：0
    }
}
```

==**其实这个数组是留给用户的，用户可以在控制台上输入参数，这个参数自动会被转换为“String[] args”**==

如在 cmd 窗口输入` java Test abc def ghi`

JVM会自动将字符串 “abc def ghi” 按照空格分离，组成一个字符串

此时

```java
 System.out.println("JVM传递过来的数组的长度是：" + args.length);// 输出：JVM传递过来的数组的长度是：3
```

* 编历 args数组

```java
for (int i = 0; i <= args.length - 1 ;i++) {
    System.out.println("args[" + i + "] = " + args[i]);
}
/*
	输出：
		args[0] = abc
        args[1] = def
        args[2] = ghi
*/
```

* 使用 IDEA 给 args 数组传参数

![image-20210209110849937](https://img-blog.csdnimg.cn/20210209111158879.png) 

![image-20210209111435213](https://img-blog.csdnimg.cn/20210209111445177.png)



#### 16.2.4 数组扩容

**java中对数组的扩容是：先新建一个大容量的数组，然后将小容量数组中的数据一个一个拷贝到大数组当中。**

Java 的 **==System 类中有一个静态方法 arraycopy( )==** ，可以进行数组扩容。

```java
arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
```

* Object src：拷贝源
* int srcPos：源数组元素的起始位置
* Object dest：目标数组
* int destPos：目标数组元素的起始位置
* int length：拷贝到元素的个数

```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5};// 拷贝源
        int[] arr2 = new int[10];// 目标数组1
        int[] arr3 = new int[10];// 目标数组2
        // 将 arr数组中从下标为 2的元素开始，拷贝 3个元素到 arr2数组，从下标为 3的位置开始放
        System.arraycopy(arr, 2, arr2, 3, 3);
        // 将 arr数组中的所用元素拷贝到 arr3数组中
        System.arraycopy(arr, 0, arr3, 0, arr.length);
        for (int i = 0; i < arr2.length; i++) {
            System.out.println(arr2[i]);
        }
        for (int i = 0; i < arr3.length; i++) {
            System.out.println(arr3[i]);
        }
    }
}
```



### 16.3  二维数组

==**二维数组就是一个特殊的一维数组，每一个元素都是一个一维数组。**==

* 静态初始化

```java
int[][] array = {
    {1,2,3,4},
    {5,6,7},
    {9,10}
};
// 其中
System.out.println(array.length);// 3
System.out.println(array[0].length);// 4
System.out.println(array[1].length);// 3
System.out.println(array[2].length);// 2
// 取出第一个一维数组
int[] array01 = array[0];
// 	取出第一个一维数组中的第一个元素
int elem11 = array[0][0]; // elem11 = 1
```

* 动态初始化

```java
int[][] array2= new int[3][4];// 三个一维数组，每个一维数组中4个元素
```



### 16.4 冒泡排序算法

[视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=577)

* 冒泡排序的过程

```java
参与比较的数据：9 8 10 7 6 0 11

第1次循环：
8 9 10 7 6 0 11 (第1次比较：交换)
8 9 10 7 6 0 11 (第2次比较：不交换)
8 9 7 10 6 0 11 (第3次比较：交换)
8 9 7 6 10 0 11 (第4次比较：交换)
8 9 7 6 0 10 11 (第5次比较：交换)
8 9 7 6 0 10 11 (第6次比较：不交换)
最终冒出的最大数据在右边：11

参与比较的数据：8 9 7 6 0 10
第2次循环：
8 9 7 6 0 10（第1次比较：不交换）
8 7 9 6 0 10（第2次比较：交换）
8 7 6 9 0 10（第3次比较：交换）
8 7 6 0 9 10（第4次比较：交换）
8 7 6 0 9 10（第5次比较：不交换）

参与比较的数据：8 7 6 0 9
第3次循环：
7 8 6 0 9（第1次比较：交换）
7 6 8 0 9（第2次比较：交换）
7 6 0 8 9（第3次比较：交换）
7 6 0 8 9（第4次比较：不交换）

参与比较的数据：7 6 0 8
第4次循环：
6 7 0 8（第1次比较：交换）
6 0 7 8（第2次比较：交换）
6 0 7 8（第3次比较：不交换）

参与比较的数据：6 0 7
第5次循环：
0 6 7（第1次比较：交换）
0 6 7（第2次比较：不交换）

参与比较的数据：0 6
第6次循环：
0 6 （第1次比较：不交换）

```

* 自己写一个冒泡排序

```java
public class Test {
    public static void main(String[] args) {
        int[] array = {2, 56, 66, 1, 4, 3, 100};
        // 每次循环完后冒出最大的元素放最后
        for (int i = 1; i <= array.length-1; i++) {
            // 前后两个元素比较，大的往后移
            for (int j = 0; j <= array.length-(i+1); j++) {
                if (array[j] > array[j+1]) {
                    int temp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = temp;
                }
            }
        }

        // 另一种写法
        for (int i = array.length - 1; i >= 1; i--) {
            for (int j = 0; j < i; j++) {
                if (array[j] > array[j+1]) {
                    int temp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = temp;
                }
            }
        }
        
        
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }

    }
}
```



### 16.5 选择排序算法

* 原理：**每一次从这堆参与比较的数据中找出最小值，那这个最小值和最前面的元素交换位置。** 
* [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=579)
* 自己写的一个排序算法

```java
public class Test {
    public static void main(String[] args) {
        int[] array = {2, 56, 66, 1, 4, 3, 100};
        // 分析一下
        // 当前数组有7个元素
        // 第【1】次 循环找到1是最小的，放到第【1】个位置，剩下【6】个数比较
        // 第【2】次 循环找到2是最小的，放到第【2】个位置，剩下【5】个数比较
        // 第【3】次 循环找到3是最小的，放到第【3】个位置，剩下【4】个数比较
        // ......
        // 第【6】次 循环找到66是最小的，放到第【6】个位置，循环结束。

        for (int i = 0; i < array.length-1; i++) {
            // 先默认下标为 i的元素是最小的
            int minNumIndex = i;
            // 下标为 i的元素与其之后的元素一一比较
            for (int j = i + 1; j < array.length; j++) {
                // 如果最小元素大于之后的元素
                if (array[minNumIndex] > array[j]) {
                    // 就将更小的元素的下标赋给 minNumIndex
                    minNumIndex = j;
                }
            }
            // 如果 minNumIndex不等于默认的 i，就将第 i个元素和最小元素进行交换
            if (minNumIndex != i) {
                int temp = array[i];
                array[i] = array[minNumIndex];
                array[minNumIndex] = temp;
            }
        }

        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}
```



### 16.6 二分法查找

**二分查找算法是基于排序好的算法的。**

* 自己写的二分法查找

```java
/**
  * 从数组中查找目标元素的下标。
  * @param arr 被查找的数组（这个必须是已经排序的。）
  * @param dest 目标元素
  * @return -1表示该元素不存在，其它表示返回该元素的下标。
  */
public static int binarySearch(int[] arr, int dest) {
    // 开始下标
    int begin = 0;
    // 结束下标
    int end = arr.length - 1;
    // 开始元素的下标只要在结束元素下标的左边，就有机会继续循环。
    while(begin <= end) {
        // 中间元素下标
        int mid = (begin + end) / 2;
        if (arr[mid] == dest) {
            return mid;
        } else if (arr[mid] < dest) {
            // 目标在“中间”的右边
            // 开始元素下标需要发生变化（开始元素的下标需要重新赋值）
            begin = mid + 1; // 一直增
        } else {
            // arr[mid] > dest
            // 目标在“中间”的左边
            // 修改结束元素的下标
            end = mid - 1; // 一直减
        }
    }
    return -1;
}
```

* 综合以下先排序后查找

```java
package cn.yechen.java;

public class Test06 {
    public static void main(String[] args) {
        int[] array = {2, 56, 66, 1, 4, 3, 100};
        Num[] nums = new Num[7];
        for (int i = 0; i < nums.length; i++) {
            nums[i] = new Num(array[i], i);
        }

        print(nums);
        System.out.println("==========");
        selectSort(nums);
        print(nums);
        System.out.println("==========");
        int indexAfterSort = binarySearch(nums, 66);
        int index = nums[indexAfterSort].getIndex();
        System.out.println("66在排序之后的下标为：" + indexAfterSort);
        System.out.println("66原下标为：" + index);
    }

    // 选择排序算法
    public static void selectSort(Object[] array) {
        // 向下转型，这里就不用 instanceof 判断了
        Num[] arrays = (Num[]) array;
        for (int i = 0; i < arrays.length - 1; i++) {
            // 先默认下标为 i的元素是最小的
            int minNumIndex = i;
            // 下标为 i的元素与其之后的元素一一比较
            for (int j = i + 1; j < arrays.length; j++) {
                // 如果最小元素大于之后的元素
                if (arrays[minNumIndex].getNum() > arrays[j].getNum()) {
                    // 就将更小的元素的下标赋给 minNumIndex
                    minNumIndex = j;
                }
            }
            // 如果 minNumIndex不等于默认的 i，就将第 i个元素和最小元素进行交换
            if (minNumIndex != i) {
                /*int temp = arrays[i].getNum();
                arrays[i].setNum(arrays[minNumIndex].getNum());
                arrays[minNumIndex].setNum(temp);
                int tempIndex = arrays[i].getIndex();
                arrays[i].setIndex(arrays[minNumIndex].getIndex());
                arrays[minNumIndex].setIndex(tempIndex);*/
                Num tempNum = arrays[i];
                arrays[i] = arrays[minNumIndex];
                arrays[minNumIndex] = tempNum;
            }
        }
    }

    // 二分法查找
    public static int binarySearch(Object[] array, int dest) {
        // 向下转型
        Num[] arr = (Num[]) array;
        // 开始下标
        int begin = 0;
        // 结束下标
        int end = arr.length - 1;
        // 开始元素的下标只要在结束元素下标的左边，就有机会继续循环。
        while(begin <= end) {
            // 中间元素下标
            int mid = (begin + end) / 2;
            if (arr[mid].getNum() == dest) {
                return mid;
            } else if (arr[mid].getNum() < dest) {
                // 目标在“中间”的右边
                // 开始元素下标需要发生变化（开始元素的下标需要重新赋值）
                begin = mid + 1; // 一直增
            } else {
                // arr[mid] > dest
                // 目标在“中间”的左边
                // 修改结束元素的下标
                end = mid - 1; // 一直减
            }
        }
        return -1;
    }

    // 编历数组
    public static void print(Object[] arr) {
        // 向下转型
        Num[] nums = (Num[]) arr;
        for (int i = 0; i < nums.length; i++) {
            System.out.println(nums[i].getNum() +","+ nums[i].getIndex());
        }
    }
}


class Num {
    // 保存的值
    private int num;
    // 在数组中的下标
    private int index;

    public Num() {
    }

    public Num(int num, int index) {
        this.num = num;
        this.index = index;
    }

    public int getNum() {
        return num;
    }

    public void setNum(int num) {
        this.num = num;
    }

    public int getIndex() {
        return index;
    }

    public void setIndex(int index) {
        this.index = index;
    }
}

```

输出

```java
2,0
56,1
66,2
1,3
4,4
3,5
100,6
==========
1,3
2,0
3,5
4,4
56,1
66,2
100,6
==========
66在排序之后的下标为：5
66原下标为：2
```



### 16.7 Arrays工具类的使用（数组工具类）

**使用的时候查阅 API 文档即可。**

## 17、常用类

### 17.1 String

#### 17.1.1 String 概述

关于 java JDK 内置的一个类：java.lang.string

*  String 表示字符类型串，属于**引用数据类型**，不属于基本数据类型
* 在 java 中随便**使用双引号括起来的都是 String 对象**，例如“abc”，“def”，“hello world”，这是三个 String 对象
* java 中规定，双引号括起来的字符串，是不可变的。
* ==**在 JDK 中双引号括起来的字符串，都直接存储在“方法区”的“字符串常量池”当中。**==

#### 17.1.2 String 字符串的存储原理

```java
public class Test {
    public static void main(String[] args) {
        // 这两行代码表示底层创建了 3个字符串对象，都在字符串常量池中
        String s1 = "abcdef";
        String s2 = "abcdef" + "xy";
        
        // 凡是双引号括起来的都在字符串常量池中有一份
        // new对象的时候一定在堆内存中开辟空间
        String s3 = new String("xy");
    }
}
```

![String的内存图](https://img-blog.csdnimg.cn/20210210154121363.png)

```java
public class UserTest {
    public static void main(String[] args) {
        User user = new User(110, "张三");
    }
}

class User {
    private int id;
    private String name;

    public User() {

    }

    public User(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

![UserTest内存图](https://img-blog.csdnimg.cn/20210210155651495.png)

检验

```java
public class Test08 {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "abc";
        System.out.println(s1 == s2);// true

        String s3 = new String("abc");
        String s4 = new String("abc");
        System.out.println(s3 == s4);// false
        System.out.println(s3.equals(s4));// true
    }
}
```

#### 17.1.3 String类的构造方法

* 传一个字符串 

```java
// String()
String s1 = new String("abc");
System.out.println(s1);// 输出：abc
```

* 传一个 byte 数组

```java
// String(byte[] bytes)
// 将byte数组全部转为字符串
byte[] bytes = {97, 98, 99};// 97是a，98是b，99是c
String s2 = new String(bytes);
System.out.println(s2);// 输出：abc
```

```java
// String(byte[] bytes, int offset, int length)
// offset表示数组元素起始下标，length表示长度
// 将byte数组的一部分转换为字符串
byte[] bytes = {97, 98, 99, 100, 101};
String s2 = new String(bytes, 2, 3);
System.out.println(s2);// 输出：cde
```

* 传一个 char 数组

```java
// String(char[] value)
// 将char数组全部转为字符串
char[] chars = {'我', '是', '中', '国', '人'};
String s3 = new String(chars);
System.out.println(s3);// 输出：我是中国人
```

```java
// String(char[] value, int offset, int count)
// 将char数组的一部分转为字符串
char[] chars = {'我', '是', '中', '国', '人'};
String s3 = new String(chars, 2, 3);
System.out.println(s3);// 输出：中国人
```



#### 17.1.4 String类中的常用方法

##### 1. ` char charAt(int index)`

返回指定索引处的char值

`index` 表示索引

```java
char c = "abc".charAt(1);// 返回索引为1的元素
System.out.println(c);// 输出：b
```

##### 2. `int compareTo(String anotherString)`   

按字典顺序比较两个字符串的大小关系

逐个比较，有一个不一样就不比了，直接能输出结果

`anotherString` 表示另一个比较的字符串

```java
System.out.println("abc".compareTo("abc"));// 输出：0（前后一致）
System.out.println("abcd".compareTo("abce"));// 输出：-1（前小后大）
System.out.println("abce".compareTo("abcd"));// 输出：1（前大后小）
System.out.println("xyz".compareTo("yxz"));// 输出：-1（x小于y，前小后大，直接出结果，后面不比了）
```

##### 3. `boolean contains(CharSequence s)`

 判断前面的字符串中是否包含后面的字符串

`CharSequence` 是一个描述字符串结构的接口，在这个接口里面一般发现有三种常用的子类:`String` `StringBuffer` `StringBuilder`

```java
System.out.println("helloWorld.java".contains(".java"));// 输出：true
System.out.println("http://baidu.com".contains("https://"));// 输出：false
```

##### 4. `boolean startsWith(String prefix)`

判断某个字符串是否以某个字符串开始

```java
System.out.println("http://www.baidu.com".startsWith("http"));// 输出：true
System.out.println("http://www.baidu.com".startsWith("https"));// 输出：false
```

##### 5. `boolean endsWith(String suffix)`

判断某个字符串是否以某个字符串开始

```java
System.out.println("test.txt".endsWith(".java"));// 输出：false
System.out.println("test.txt".endsWith(".txt"));// 输出：true
```

##### 6. `boolean equalsIgnoreCase(String anotherString)`

判断两个字符串是否相等，并且忽略大小写

```java
System.out.println("ABC".equalsIgnoreCase("aBC"));// true
```

##### 7. `byte[] getBytes()`

将字符串对象转化为 byte 数组

```java
byte[] bytes = "abcde".getBytes();
for (int i = 0; i < bytes.length; i++) {
    System.out.println(bytes[i]);
}
/*
	输出：
		97
        98
        99
        100
        101
*/
```

##### 8. `char[] toCharArray()`

将字符串对象转换为 char 数组

```java
char[] chars = "我是中国人".toCharArray();
for (int i = 0; i < chars.length; i++) {
    System.out.println(chars[i]);
}
/*
	输出：
		我
        是
        中
        国
        人	
*/
```

##### 9. `int indexOf(String str)`

判断某个字符串在当前字符串中第一次出现处的索引

如果为这个当前字符串中没有该字符串，返回 -1

```java
System.out.println("abcdefghijklmn".indexOf("fgh"));// 输出：5
System.out.println("abcdefghijklmn".indexOf("fd"));// 输出：-1
```

##### 10. `int lastIndexOf(String str)`

判断某个字符串在当前字符串中最后一次出现处的索引

```java
System.out.println("abcdefgabc".lastIndexOf("abc"));// 输出：7
```

##### 11. `boolean isEmpty()`

判断当前字符串是否为空

```java
System.out.println("".isEmpty());// 输出：true
System.out.println("abc".isEmpty());// 输出：false
```

##### 12. `int length()` 

返回字符串长度

**注意：面试题**

```
判断数组长度和字符串长度不一样
判断数组长度是length属性，判断字符串长度是length()方法
```

```java
System.out.println("abcdefg".length());// 输出：7
```

##### 13. `String replace(CharSequence target, CharSequence replacement)`

将当前字符串中的 target替换为 replacement

```java
String newString = "http://www.baidu.com".replace("http", "https");
System.out.println(newString);// 输出：https://www.baidu.com
```

##### 14. `String[] split(String regex)` 

regex 为正则表达式

拆分字符串

```java
String[] newStrings = "name=zhangsan&password=123&age=20".split("&");
for (int i = 0; i < newString.length; i++) {
    System.out.println(newStrings[i]);
}
/*
	输出：
		name=zhangsan
        password=123
        age=20
*/
```

##### 15. `String substring(int beginIndex)`

从索引 `beginIndex` 处开始截取字符串

```java
System.out.println("http://www.baidu.com".substring(7));// 输出：www.baidu.com
```

`String substring(int beginIndex, int endIndex)`

`beginIndex`：起始索引（包括）
`endIndex`：结束索引（不包括）
左闭右开 [ `beginIndex`,` endIndex` )

```java
System.out.println("http://www.baidu.com".substring(11, 16));// 输出：baidu
```

##### 16. `String toLowerCase()`

将当前字符串转换为小写

```java
String newString = "ABCdeFg".toLowerCase();
System.out.println(newString);// 输出：abcdefg
```

##### 17. `String trim()`

将当前字符串 “前 后” 的空格去掉

```java
System.out.println("   abc   def    ".trim());// 输出：abc   def
```

##### 18. `static String valueOf(boolean b)`

将 “非字符串” 转化为 “字符串”

有好多重载的方法

```java
static String valueOf(boolean b)// 将 boolean 类型元素转换为字符串
static String valueOf(char c)// 将 char 类型元素转换为字符串
static String valueOf(char[] data)// 将 char 类型的数组元素转化为字符串
static String valueOf(char[] data, int offset, int count)// 将 char 类型的数组元素一部分转化为字符串，offset表示首元素索引，count表示长度
static String valueOf(double d)// 将 double 类型元素转化为字符串
static String valueOf(float f)// 将 float 类型元素转化为字符串
static String valueOf(int i)// 将 int 类型元素转化为字符串
static String valueOf(long l)// 将 long 类型元素怒转化为字符串
static String valueOf(Object obj)// 将引用数据类型转化为字符串，会自动调用该类的toStirng方法
```

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(String.valueOf(true));// 输出：true（String类型的）
        System.out.println(String.valueOf(100));// 输出：100（String类型的）
        System.out.println(String.valueOf(3.14159));// 输出：3.14159（String类型的）
        // 静态方法valueOf()方法，参数是一个对象的时候，会调用该对象的toString()方法
        // 没重写toString()方法，输出：javase.api.string.Customer@4fca772d（当前对象的默认			toStirng方法的输出结果）
        // 重写toString()方法，输出：toString()方法被调用了！
        System.out.println(String.valueOf(new Customer()));
    }
}

class Customer {
    @Override
    public String toString() {
        return "toString()方法被调用了！";
    }
}
```



### 17.2 StringBuffer

**因为在 Java 中字符串是不可变的，每一次的字符串拼接都会产生新的字符串，这样会占用大量的方法区内存，造成空间浪费。**

如果要进行大量的字符串的拼接操作，建议使用 JDK 中自带的：

​	`java.lang.StringBuffer`

​	`java.lang.StringBuilder`

**如何优化 StringBuffer 的性能**

* 在创建的时候尽可能给定一个初始化容量
* 最好减少底层数组的扩容次数，预估一下，给一个大一些初始化容量
* 关键点：给一个适合的初始化容量，可以提高程序的运行效率。

**`StringBuffer` 和 `StringBuilder` 的区别**

* `StringBuffer` 中的方法都有 `synchronized` 关键字修饰，表示在多线程环境下运行是安全的
* `StringBuilder` 是非线程安全的，但是效率高



### 17.3 基础类型对应的8个包装类

| 基础类型    | 包装类                  | 父类                 |
| ----------- | :---------------------- | -------------------- |
| **byte**    | **java.lang.Byte**      | **java.lang.Number** |
| **short**   | **java.lang.Short**     | **java.lang.Number** |
| **int**     | **java.lang.Integer**   | **java.lang.Number** |
| **long**    | **java.lang.Long**      | **java.lang.Number** |
| **float**   | **java.lang.Float**     | **java.lang.Number** |
| **double**  | **java.lang.Double**    | **java.lang.Number** |
| **boolean** | **java.lang.Boolean**   | **java.lang.Object** |
| **char**    | **java.lang.Character** | **java.lang.Object** |

#### 17.3.1 装箱和拆箱

```java
public class Test01 {
    public static void main(String[] args) {
        // 123这个基本数据类型，进行构造方法的包装达到了：基本数据类型向引用数据类型的转换
        // 基本数据类型 --（转换为）--> 引用数据类型 ：装箱
        Integer integer = new Integer(123);
        // 将引用数据类型 --（装换为）--> 基本数据类型 ： 拆箱
        float f = integer.floatValue();
        System.out.println(f);// 输出：123.0
    }
}
```

八种包装类中其中6个都是数字对应的包装类，他们的父类都是Number，可以先研究一下Number中公共的方法：
* Number是一个抽象类，无法实例化对象。
* Number类中有这样的方法：

```java
byte byteValue() // 以 byte 形式返回指定的数值。
abstract  double doubleValue() // 以 double 形式返回指定的数值。
abstract  float floatValue() // 以 float 形式返回指定的数值。
abstract  int intValue() // 以 int 形式返回指定的数值。
abstract  long longValue() // 以 long 形式返回指定的数值。
short shortValue() // 以 short 形式返回指定的数值。
// 这些方法其实所有的数字包装类的子类都有，这些方法是负责拆箱的。
```

#### 17.3.2 通过包装类中的常量来获取最大值和最小值

```java
// 通过包装类的常量来获取最大值和最小值
System.out.println(Integer.MAX_VALUE);// 2147483647
System.out.println(Integer.MIN_VALUE);// -2147483648
System.out.println(Double.MAX_VALUE);// 1.7976931348623157E308
```

#### 17.3.3 自从 JDK1.5 之后支持了自动装箱和自动拆箱

```java
// 自动装箱：基本数据类型自动转换为包装类
// int ---> Integer
Integer i = 100;
// 自动拆箱：包装类自动转换为基本数据类型
// Integer ---> int
int i1 = i;
```

#### 17.3.4 比较两个Integer是否相等

1. Integer是int的包装类，比较两个对象是否相等不能使用==，应该使用equals。
2. **java 中为了提高程序的执行效率，将 [-128. 127] 之间的所有包装对象提前创建好，放到了一个方法区的 “整数型常量池” 当中，目的是只要用这个区间的数据不需要在 new 对象了，直接从整数型常量中取出来就可以了。**
3. **-128至127（包括-128和127）范围内使用==比较，返回true，反之false**

```java
// i1 和 i2 中保存的内存地址是一样的，因为 127 保存在方法区的整数型常量池当中，不会在堆内存中 new 对象，直接取常量池当中的数据，所以内存地址相同。
Integer i1 = 127;
Integer i2 = 127;
// i3 和 i4 中保存的内存地址是不一样的，因为 128 不在[-128, 127] 内，不在整数型常量池当中，创建的时候要在堆内存中 new 对象，对象的内存地址是不同的。
Integer i3 = 128;
Integer i4 = 128;
SYstem.out.println(i1 == i2);// 输出：true
System.out.println(i3 == i4);// 输出：false
```

#### 17.3.5 cache缓存机制

```java
// 源码
// 这是 Integer 类中的内部类，在类加载的时候，会在整数型常量池中初始化 256 个对象。
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static final Integer cache[];

    static {
        // high value may be configured by property
        int h = 127;
        String integerCacheHighPropValue =
            sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
        if (integerCacheHighPropValue != null) {
            try {
                int i = parseInt(integerCacheHighPropValue);
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
            } catch( NumberFormatException nfe) {
                // If the property cannot be parsed into an int, ignore it.
            }
        }
        high = h;

        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);

        // range [-128, 127] must be interned (JLS7 5.1.7)
        assert IntegerCache.high >= 127;
    }

    private IntegerCache() {}
}
```

```java
// 源码
// 判断当前整数是否在 [-128, 127] 范文内，如果在，直接从常量池中区，如果不在，就 new 对象
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```

#### 17.3.6 NumberFormatException

当在 Integer 的构造方法中传入一个非整数型的字符串，会报异常（数字格式化异常）

```java
Integer i1 = new Integer("中文");
System.out.println(i1);
// Exception in thread "main" java.lang.NumberFormatException: For input string: "中文"
```

```java
// 总结已学过的经典异常
空指针异常：NullPointerException
类转换异常：ClassCastException
数组下标越界异常：ArrayIndexOutOfBoundsException
数字格式化异常：NumberFormatException
```

#### 17.3.7 常用方法

```java
static int	parseInt(String s)// 将字符串转换为int类型数字
    
static String	toBinaryString(int i)// 将十进制整数转换为二进制形式的字符串
    
static String	toHexString(int i)// 将十进制整数转换为十六进制的字符串
    
static String	toOctalString(int i)// 将十进制整数转换为八进制的字符串
```

#### 17.3.8 String    int    Integer 之间的相互转化

![image-20210216135247764](https://img-blog.csdnimg.cn/20210216135401651.png)



### 17.4 日期相关类

#### 17.4.1 获取系统的当前时间（精确到毫秒的系统当前时间）

```java
Date nowTime = new Date();
System.out.println(nowTime);// 输出：Tue Feb 16 14:05:06 CST 2021
```

#### 17.4.2 日期格式化

将日期类 Date，按照指定的格式进行转换：Date ---> 转换成为具有一定格式的日期字符串 ---> String

**`java.text.SimpleDateFormat` 是专门负责日期格式化的。**

```java
// Date --(转换为)--> String
Date nowTime = new Date();
/*
	yyyy 年(年是4位)
    MM 月（月是2位）
    dd 日
    HH 时
    mm 分
    ss 秒
    SSS 毫秒（毫秒3位，最高999。1000毫秒代表1秒）
    注意：在日期格式中，除了y M d H m s S这些字符不能随便写之外，剩下的符号格式自己随意组织。
    */
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
String time = sdf.format(nowTime);
System.out.println(time);// 输出：2021-02-16 14:13:22 984
```

```java
// String --(转换为)--> Date
String timeStr = "2008-08-08 08:08:08 888";
SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
try {
    Date time = simpleDateFormat.parse(timeStr);
    System.out.println(time);// 输出：Fri Aug 08 08:08:08 CST 2008
} catch (ParseException e) {
    e.printStackTrace();
}
```

#### 17.4.3 获取自1970年1月1日 00:00:00 000（GMT 格林尼治标准时间）到当前系统时间的总毫秒数。

```java
long nowTimeMillis = System.currentTimeMillis();
System.out.println(nowTimeMillis);// 输出：1613459089458
```

将获取到的毫秒数转化为日期格式（通过 Date 类的构造方法）

```java
public class Test02 {
    public static void main(String[] args) {
        Date time = new Date(1);
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-hh HH:mm:ss SSS");
        String timeStr = simpleDateFormat.format(time);
        System.out.println(timeStr);
    }
}
```



### 17.5 数字相关类

#### 17.5.1 数字格式化

`java.text.DecimalFormat` 专门负责数字格式化的

```java
//DecimalFormat df = new DecimalFormat("数字格式");
/*
	数字格式有哪些？
    # 代表任意数字
    , 代表千分位
    . 代表小数点
    0 代表不够时补0

	###,###.##
    表示：加入千分位，保留2个小数。
    */
DecimalFormat df = new DecimalFormat("###,###.##");
//String s = df.format(1234.56);
String s = df.format(1234.561232);
System.out.println(s); // "1,234.56"

DecimalFormat df2 = new DecimalFormat("###,###.0000"); //保留4个小数位，不够补上0
String s2 = df2.format(123456789.56);
System.out.println(s2); // "123,456,789.5600"
```

#### 17.5.2 java.math.DigDecimal

BigDecimal 属于大数据，精度极高。不属于基本数据类型，属于java对象（引用数据类型），这是SUN提供的一个类。专门用在财务软件当中。

```java
// 这个100不是普通的100，是精度极高的100
BigDecimal v1 = new BigDecimal(100);
// 精度极高的200
BigDecimal v2 = new BigDecimal(200);
// 求和
// v1 + v2; // 这样不行，v1和v2都是引用，不能直接使用+求和。
BigDecimal v3 = v1.add(v2); // 调用方法求和。
System.out.println(v3); //300

BigDecimal v4 = v2.divide(v1);
System.out.println(v4); // 2
```



### 17.6 Random随机数

#### 17.6.1 产生随机数

 ```java
// 创建随机数对象
Random random = new Random();

// 随机产生一个 int 类型范围内的数据
int num01 = random.nextInt();
System.out.println(num01);

// 随机产生一个 [0 , 101) 范围内的整数，不包括 101
int num02 = random.nextInt(101);
System.out.println(num02);
 ```

#### 17.6.2 测试

编写程序，生成5个不重复的随机数[0-4]。重复的话重新生成。最终生成的5个随机数放到数组中，要求数组中这5个随机数不重复。

* 自己的想法

```java
import java.util.Arrays;
import java.util.Random;

public class Test01 {
    public static void main(String[] args) {
        int[] arr = new int[5];
        Random random = new Random();
        // 给数组中的每一个数赋初值 -1
        Arrays.fill(arr, -1);

        // 赋值
        for (int i = 0; i < arr.length; i++) {
            int num = random.nextInt(5);
            if (check(num, arr)) {
                num = rebuild(num, arr);
            }
            arr[i] = num;
        }

        // 输出
        for (int num : arr) {
            System.out.println(num);
        }
    }

    /**
     * 使用递归重新生成一个数（没有出现过的）
     * @param num 需要被重新生成的数
     * @param arr 数组
     * @return 重新生成的 num
     */
    public static int rebuild(int num, int[] arr) {
        Random random = new Random();
        num = random.nextInt(5);
        if (check(num, arr)) {
            num = rebuild(num, arr);
        }
        return num;
    }

    /**
     * 判断 num 在 arr 数组中书否存在
     * @param num 被判断的数字
     * @param arr 数组
     * @return true表示存在， false表示不存在
     */
    public static boolean check(int num, int[] arr) {
        for (int j : arr) {
            if (num == j) return true;
        }
        return false;
        /*int[] array = new int[arr.length];
        // 数组拷贝
        System.arraycopy(arr, 0, array, 0, arr.length);
        // 数组排序
        Arrays.sort(array);
        // 二分法查找，找到的话返回的值会大于等于 0
        return Arrays.binarySearch(array, num) >= 0;*/
    }
}
```

* 老师的想法

```java
import java.util.Arrays;
import java.util.Random;

public class Test02 {
    public static void main(String[] args) {
        // 创建Random对象
        Random random = new Random();

        // 准备一个长度为5的一维数组。
        int[] arr = new int[5];
        Arrays.fill(arr, -1);// 数组元素赋值 -1

        // 循环，生成随机数
        int index = 0;
        while(index < arr.length){
            int num = random.nextInt(5);
            if(!check(num, arr)){
                arr[index++] = num;
            }
        }

        // 输出
        for (int num : arr) {
            System.out.println(num);
        }
    }

    /**
     * 判断 num 在 arr 数组中书否存在
     * @param num 被判断的数字
     * @param arr 数组
     * @return true表示存在， false表示不存在
     */
    public static boolean check(int num, int[] arr) {
        for (int j : arr) {
            if (num == j) return true;
        }
        return false;
    }
}
```



### 17.7 Enum枚举

枚举是一种**引用数据类型**

语法：

```java
enum 枚举类型名 {
    枚举值1, 枚举值2
}
```

结果只有两种情况的时候，建议使用 boolean 类型，

当结果超过两种并且还是可以一枚一枚列举 出来的，建议使用枚举类型。

```java
public class Test01 {
    public static void main(String[] args) {
        Result result = divide(10, 0);
        System.out.println(result == Result.SUCCESS ? "计算成功" : "计算失败");
    }

    /**
     * 计算两个int类型数据的商。
     * @param a int数据
     * @param b int数据
     * @return Result.SUCCESS表示成功，Result.FAIL表示失败！
     */
    public static Result divide(int a, int b){
        try {
            int c = a / b;
            return Result.SUCCESS;
        } catch (Exception e){
            return Result.FALSE;
        }
    }
}

enum Result {
    SUCCESS, FALSE
}
```



## 18、异常（Exception）

### 18.1 异常的基本概念

#### 18.1.1 异常信息

```java
public class Test01 {
    public static void main(String[] args) {
        int r = 10 / 0;
        System.out.println(r);
    }
}
```

以上程序运行后已出现异常

```java
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Test01.main(Test01.java:3)
```

**java 是一门很完善的语言，提供了异常的处理方式，当程序出现了不正常的情况，JVM 虚拟机就会把异常信息打印在控制台，供程序员参考，==增加程序的健壮性==**。



#### 18.1.2 异常以什么形式存在

**==异常在 java 中以类的形式存在，每一个异常类都可以创建异常对象。==** 

```java
NumberFormatException numberFormatException = new NumberFormatException("数字格式化异常");
System.out.println(numberFormatException);// 输出：java.lang.NumberFormatException: 数字格式化异常

ArrayIndexOutOfBoundsException arrayIndexOutOfBoundsException = new ArrayIndexOutOfBoundsException("数组下标越界异常");
System.out.println(arrayIndexOutOfBoundsException);// 输出：java.lang.ArrayIndexOutOfBoundsException: 数组下标越界异常
```

异常类对应现实生活：

**丢失钱包（是一个异常类）**

**2008年，8月8日，小明的钱包丢了（是一个异常对象）**

### 18.2 异常的分类

#### 18.2.1 异常的层次结构

![image-20210217153631429](https://img-blog.csdnimg.cn/20210217153729367.png)

**编译时异常（受检异常）：异常必须要在编译（编写）阶段预先处理，如果不处理，编译器会报错，发生的概率较高。**

```java
// 运行出错
public class Test01 {
    public static void main(String[] args) {
        // main方法中调用doSome()方法
        // 因为doSome()方法声明位置上有：throws ClassNotFoundException
        // 我们在调用doSome()方法的时候必须对这种异常进行预先的处理。
        // 如果不处理，编译器就报错。
        doSome();//编译器报错信息： Unhandled exception: java.lang.ClassNotFoundException
    }

    /**
     * doSome方法在方法声明的位置上使用了：throws ClassNotFoundException
     * 这个代码表示doSome()方法在执行过程中，有可能会出现ClassNotFoundException异常。
     * 叫做类没找到异常。这个异常直接父类是：Exception，所以ClassNotFoundException属于编译时异常。
     * @throws ClassNotFoundException
     */
    public static void doSome() throws ClassNotFoundException{
        System.out.println("doSome!!!!");
    }
}
```

**运行时异常（未受检异常）：在编译阶段可以不处理，发生的概率较低。**

```java
// 运行出错
public class Test01 {
    public static void main(String[] args) {
         /*
        程序执行到此处发生了ArithmeticException异常，底层new了一个ArithmeticException异常对象，
        然后抛出了，由于是main方法调用了100 / 0，所以这个异常ArithmeticException抛给了main方法，
        main方法没有处理，将这个异常自动抛给了JVM，JVM最终终止程序的执行。

        ArithmeticException 继承 RuntimeException，属于运行时异常。
        在编写程序阶段不需要对这种异常进行预先的处理。
         */
        System.out.println(100 / 0);

        // 这里的HelloWorld没有输出，没有执行。
        System.out.println("Hello World!");
    }
}
```

#### 18.2.1 处理异常的两种方式

==对于编译时异常，一定要在编译阶段就处理掉。==

**第一种方式：在方法声明的位置上，使用 `throws` 关键字，将异常抛给上一级。**（**谁调用我，我就抛给谁**）

> 但是异常上抛之后，方法调用者还是需要对这个异常进行处理，可以选择上抛或直接处理。

> 当异常一直上抛，最后抛给了 mian 方法，main 方法继续上抛，抛给了 jvm 虚拟机，jvm 知道这个异常发生，最后只能终止 java 程序的运行。

```java
public class Test01 {
    // 一般不建议在main方法上上抛异常，因为如果异常真正发生了，一定会抛给jvm虚拟机，jvm只有终止程序
    public static void main(String[] args) throws ClassNotFoundException {
        // 将异常上抛，如果没有出现异常，程序正常执行，出现问题，jvm 直接终止程序运行
        doSome();
    }

    public static void doSome() throws ClassNotFoundException{
        System.out.println("doSome!!!!");
    }
}
```

**第二种方式：在方法体内，使用 `try...catch` 语句进行异常的捕捉。**（**这件事情发生了，但我自己解决了，谁也不知道**）

```java
public class Test01 {
    public static void main(String[] args) {
        // 使用 try...catch 语句进行异常捕捉
        try {
            // 尝试调用方法，如果没有出现异常，不会进入 catch 语句块
            doSome();
        } catch (ClassNotFoundException e) {// 这里的引用 e 中保存的是之前 new 出来的异常对象的内存地址
            // 如果出现异常，进入 catch 语句块
            // 捕捉异常
            // 以下程序是打印异常堆栈追踪信息
            e.printStackTrace();
        }
    }

    // 如果出现异常，会在底层 new 一个 ClassNotFoundException 异常对象，并且上抛
    public static void doSome() throws ClassNotFoundException{
        System.out.println("doSome!!!!");
    }
}
```



### 18.3 异常的上抛和捕捉

#### 18.3.1 上抛

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class Test01 {
    // 一般不建议在main方法上上抛异常，因为如果异常真正发生了，一定会抛给jvm虚拟机，jvm只有终止程序
    public static void main(String[] args) {
        System.out.println("main begin");
        // 不建议在main方法上上抛异常，所以在这里捕捉异常
        try {
            m1();
        } catch (FileNotFoundException e) {
            System.out.println("文件不存在！");
        }
        System.out.println("main over");
    }

    // 继续上抛
    private static void m1() throws FileNotFoundException {
        System.out.println("m1 begin");
        m2();
        System.out.println("m1 over");
    }

    // 异常上抛，可以上抛具体异常，也可以上抛父类异常，如 FileNotFoundException 的父类就是 IOException
    // private static void m2() throws IOException {
    private static void m2() throws FileNotFoundException {
        System.out.println("m2 begin");
        // 会出现异常，选择上抛
        new FileInputStream("D:\\Code\\Kotlin\\Day01\\Kotlin01\\src\\com\\Person.kt");
        System.out.println("m2 over");
    }
}
```

* 如果异常没有发生：

```java
// 输出：
	main begin
    m1 begin
    m2 begin
    m2 over
    m1 over 
    main over
```

* 如果发生了异常：

```java
// 输出：
	main begin
    m1 begin
    m2 begin
    文件不存在！
    main over
```

#### 18.3.2 捕捉

> catch后面的小括号中的类型可以是具体的异常类型，也可以是该异常类型的父类型。
>
> catch可以写多个。建议catch的时候，精确的一个一个处理。这样有利于程序的调试。
>
> catch写多个的时候，从上到下，必须遵守从小到大。

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class Test01 {
    public static void main(String[] args) {
        // 使用 try...catch 语句来进行异常的捕捉
        try {
            //  会出现文件未发现异常
            FileInputStream fileInputStream = new FileInputStream("D:\\Code\\Kotlin\\Day01\\Kotlin01\\src\\com\\Person.kt");
            // 会出现计算异常
            System.out.println(100 / 0);
        } catch (FileNotFoundException | ArithmeticException e) {// 这里可以捕捉具体的异常，也可以捕捉父类异常
            // FileNotFoundException | ArithmeticException e 是 JDK8 新特性
            if (e instanceof FileNotFoundException) {
                System.out.println("文件没有找到");
            } else {
                System.out.println("除数不能为 0");
            }
        }
    }
}
```

#### 18.3.3 上抛和捕捉的选择

**==如果希望调用者来处理异常，就 throws 上报==，其他情况使用 try ... catch 捕捉**



### 18.4 异常对象的常用方法

1. **获取异常的简单描述信息：**`String msg = exception.getMessage();` 

```java
NullPointerException nullPointerException = new NullPointerException("空指针异常！");
// 获取异常的简单描述信息
String msg = nullPointerException.getMessage();
System.out.println(msg);// 输出：空指针异常！
```

2. **打印异常追踪的堆栈信息**：`exception.printStackTrace();`

```java
NullPointerException nullPointerException = new NullPointerException("空指针异常！");
// java 后台打印异常追踪信息的时候，采用了异步线程的方式打印
nullPointerException.printStackTrace();
```

**异常追踪信息怎么看：**

​	从上往下一行一行看，但是要注意的是，sun 公司写好的代码就不用看了，只要的问题是在自己编写的代码上。



### 18.5 关于try..catch中的finally子句

* **在finally子句中的代码是最后执行的，并且是一定会执行的**，即使try语句块中的代码出现了异常。
* finally子句必须和try一起出现，不能单独编写。
* finally语句通常使用在哪些情况下呢？
  * **通常在finally语句块中完成资源的释放/关闭**。（保证代码一定执行）

* try...finally （没有 catch）可以连用
* **finally 语句块中的代码会在 return 前执行**

```java
try {
    System.out.println("try...");
    return;
} finally {
    // finally中的语句会执行。能执行到。
    System.out.println("finally...");
}
/*
	输出：
		try...
        finally...
*/
```

* **如果退出 JVM，finally语句块中的代码不执行**

```java
try {
    System.out.println("try...");
    // 退出 JVM
    System.exit(0);
} finally {
    System.out.println("finally...");
}
/*
	输出：
		try...
*/
```

* ==面试题== : 最后的结果输出为 100

```java
public class Test01 {
    public static void main(String[] args) {
        int result = m();
        System.out.println(result);
    }

    public static int m() {
        int i = 100;
        try {
            // 这行代码出现在 i = 100 之后，所以最终的返回值必须是 100
            // 但是return 语句还必须保证是最后执行的，一旦执行，整个方法结束。
            // 可以从反编译的程序来看出执行顺序
            return i;
        } finally {
            i++;
        }
    }
}
```

```java
java语法规则（有一些规则是不能破坏的，一旦这么说了，就必须这么做！）：
    java中有一条这样的规则：
        方法体中的代码必须遵循自上而下顺序依次逐行执行（亘古不变的语法！）
    java中海油一条语法规则：
        return语句一旦执行，整个方法必须结束（亘古不变的语法！）
```

反编译结果：

```java
public class Test01 {
    public Test01() {
    }

    public static void main(String[] args) {
        int result = m();
        System.out.println(result);
    }

    public static int m() {
        byte i = 100;

        byte var1;
        try {
            var1 = i;
        } finally {
            int var5 = i + 1;
        }

        return var1;
    }
}
```



### 18.6 自定义异常

第一步：编写一个类继承 Exception 或者 RunTimeException。

第二步：提供两个构造方法，一个无参数，一个带有 String 参数的。

```java
public class MyException extends Exception {// 编译时异常
    // 无参构造方法
    public MyException() {
        // 默认有一个 super()
    }
    
    // 有参构造方法
    public MyException(String s) {
        super(s);
    }
}
```

```java
public class MyException extends RunTimeException {// 运行时异常
    // 无参构造方法
    public MyException() {
        // 默认有一个 super()
    }
    
    // 有参构造方法
    public MyException(String s) {
        super(s);
    }
}
```



###  18.7 方法覆盖与异常

**重写之后的方法不能比重写之前的方法抛出更多的异常**

==tips：父类方法不抛异常，子类可以抛RunTimeException==





## 19、集合

### 19.1 集合概述

#### 19.1.1 什么是集合

* 集合实际上就是一个**==容器==**。可以来容纳其它类型的数据。

* 集合不能直接存储基本数据类型，另外集合也不能直接存储java对象，

  **==集合当中存储的都是java对象的内存地址==**。（或者说集合中存储的是引用。）

* 集合在java中本身是一个容器，是一个**==对象==**

![001-集合中存储的是对象的内存地址](https://img-blog.csdnimg.cn/20210218120728216.png)

#### 19.1.2 在java中每一个不同的集合，底层会对应不同的数据结构

```java
new ArratList(); // 创建一个集合对象，底层是数组
new LinkList();// 创建一个集合对象，底层是链表
new TreeSet();// 创建一个集合对象，底层是二叉树
```

#### 19.1.3 集合继承结构

**java 中集合分为两类：**

* 一类是==单个方式==存储元素： 

单个方式存储元素，这一类集合中**超级父接口：java.util.Collection**;

 ![Collection集合继承结构图](https://img-blog.csdnimg.cn/20210218131441367.png)

* 一类是以==键值对儿的方式==存储元素 

  以键值对的方式存储元素，这一类集合中**超级父接口：java.util.Map**;

 ![Map集合的继承结构图](https://img-blog.csdnimg.cn/2021021813340813.png)

**总结：**

**实现类：**

> **[ArrayList](####19.3.1 ArrayList)：底层是数组；**
>
> **[LinkedList](####19.3.2 LinkList )：底层是双向链表；**
>
> **[Vector](####19.3.3 Vector（不常用）)：底层是数组，是线程安全的，效率较低，使用较少；**
>
> **[HashSet](####19.6.2 HashSet / HashMap )：底层使用的是 HashMap，放到 HashSet 中的元素等同于放到 HashMap 集合中的 key 部分了；**
>
> **[TreeSet](####19.6.5 TreeSet / TreeMap)：底层是 TreeMap，放到 TreeSet 集合中的元素等同于放到 TreeMap 集合中的 key 部分了；**
>
> **[HashMap](####19.6.2 HashSet / HashMap )：底层是哈希表；**
>
> **[HashTable](####19.6.3 HashTable)：底层是哈希表，只不过是线程安全的，效率较低，使用较少；**
>
> **[Properties](####19.6.4 Properties)：是 HashTable 的子类，是线程安全的，并且 key 和 value 只能存储字符串 String 类型；**
>
> **[TreeMap](####19.6.5 TreeSet / TreeMap)：底层是二叉树，TreeMap 集合的 key 可以自动按照大小顺序排序。**

**[List](####19.3.1 List 接口) 集合存储元素的特点：有序可重复**

> 有序：存进去的顺序和取出来的顺序相同，每一个元素都有下标。
>
> 可重复：可以存进去两个相同的元素，例如：存进去 1，可以再存进去 1。

**[Set（Map）](####19.6.1 Map 接口)集合存储元素的特点：无序不可重复**

> 无序：存进去的顺序和取出来的顺序不一定相同，另外 Set 集合中的元素没有下标。
>
> 不可重复：不可以存进去两个相同的元素。

**SortedSet（SortedMap）集合存储元素的特点：无序不可重复，元素可排序**

> 无序：存进去的顺序和取出来的顺序不一定相同，另外 Set 集合中的元素没有下标。
>
> 不可重复：不可以存进去两个相同的元素。
>
> 可排序：可以按照 Key 的大小顺序排序。

**Map集合中的Key，就是一个Set集合。**

**往Set集合中放数据，实际上放到了Map集合的Key部分。**



### 19.2 Collection 和 Iterator

#### 19.2.1 Collection集合

**Collection 中可以存放什么元素：**

>没有使用“泛型”之前，Collection中可以存储Object的所有子类型。
>
>使用了“泛型”之后，Collection中只能存储某个具体的类型。
>
>集合中不能直接存储基本数据类型，也不能存 java 对象，只是存储 java 对象的内存地址。

**Collection 中的常用方法：**

```java
boolean add(Object e) // 向集合中 末尾 添加元素
int size()  // 获取集合中元素的个数
void clear() // 清空集合
boolean contains(Object o) // 判断当前集合中是否包含元素o，包含返回true，不包含返回false
boolean remove(Object o) // 删除集合中的某个元素。
boolean isEmpty()  // 判断该集合中元素的个数是否为0
Object[] toArray()  // 调用这个方法可以把集合转换成数组。【作为了解，使用不多。】
```

**contains源码分析**

```java
// 测试程序
Collection collection = new ArrayList();

String s1 = new String("abc");
String s2 = new String("def");
String s3 = new String("abc");

collection.add(s1);
collection.add(s2);

boolean result = collection.contains(s3);
System.out.println(result);// 输出：true
```

![image-20210218153600561](https://img-blog.csdnimg.cn/2021021815361690.png)

```java
// 源码
public boolean contains(Object o) {
    // 如果indexOf方法返回的值大于等于 0，就返回 true，表示包含
    return indexOf(o) >= 0;
}

public int indexOf(Object o) {
    // 如果传进来的元素是 null
    if (o == null) {
        // 编历数组，存在 null值就返回下标
        for (int i = 0; i < size; i++)
            if (elementData[i]==null)
                return i;
    } else {
        // 编历数组
        for (int i = 0; i < size; i++)
            // 使用 equals() 来判断对象中的内容是否相同，不以内存地址为判断标准
            // 当然前提条件是当前类重写了 equals() 方法，否则比较的还是内存地址
            if (o.equals(elementData[i]))
                return i;
    }
    return -1;
}
```

**结论：contains方法中是使用 equals()  方法来判断两个对象是否相等的，所有存放在 集合中的对象一定要重写 equals() 方法。**

​			**remove方法底层也是调用 equals() 方法来判断两个对象是否相等的。**



#### **19.2.2 Iterator迭代器**

==Collection 接口继承 Iterable 接口，继承了 Iterator() 方法，会返回一个 Iterator 类型的迭代器，用于 Collection 的编历。（在 Map 中不能用）==

**迭代器 Iterator 中的方法：**

```java
boolean hasNext()// 如果仍有元素可以迭代，则返回 true。
Object next()// 返回迭代的下一个元素。
```

**迭代器执行过程：**

```java
// 创建集合
Collection collection = new ArrayList();
// 添加元素
collection.add(100);
collection.add(3.14);
collection.add("abc");
collection.add(new Object());
// 使用Iterator迭代器对集合编历
// 第一步：获取集合迭代器对象
Iterator iterator = collection.iterator();
// 第二步：通过迭代器对象开始编历集合
while (iterator.hasNext()) {
    Object obj = iterator.next();
    System.out.println(obj);
}
```



![image-20210218143857008](https://img-blog.csdnimg.cn/20210218143913522.png)

* **迭代集合过程中用 remove() 方法会出现异常，要使用迭代器的 remove 方法**

  在迭代集合元素的过程中，不能调用集合对象的 remove 方法，删除元素：`collection.remove(o)`; 迭代过程中不能这样。否则会出现：`java.util.ConcurrentModificationException` (**当集合的结构发生改变时，迭代器必须重新获取**)

  **在迭代元素的过程当中，一定要使用迭代器 Iterator 的 remove 方法，删除元素，不要使用集合自带的remove方法删除元素。**

  [视频讲解](https://www.bilibili.com/video/BV1Rx411876f?p=677)





### 19.3 List 接口及其实现类

#### 19.3.1 List 接口

**List 集合存储元素特点：有序可重复**

**List 接口特有的方法：**

```java
void add(int index, Object element)// 在列表指定位置（index）处插入元素（element），效率较低，使用较少
Object set(int index, Object element)// 修改指定位置（index）处元素为（element），返回被替换的元素
Object get(int index)// 根据下标（index）获取指定元素
int indexOf(Object o)// 获取指定对象（o）第一次出现处的索引
int lastIndexOf(Object o)// 获取指定对象（o）最后一次出现处的索引
Object remove(int index)// 删除指定位置（index）处的元素，返回删除的元素
```

**由于有下标，所以 List 集合有自己特有的编历方式**

```java
List list = new ArrayList();
list.add(100);
list.add(110);
list.add(120);

// 编历
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```



#### 19.3.1 ArrayList

==默认初始化容量为 10（底层先创建了一个长度为 0 的数组，当添加第一个元素的时候，初始哈容量 10）。==

ArrayList 底层是一个 **Object[] 数组**

```java
transient Object[] elementData;
```

**ArrayList 的无参构造方法会初始化一个长度为0的数组，在添加元素的时候会初始化容量。**

```java
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = 
//     
public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
```

**ArrayList 的有参构造需要传进去一个 int 类型的初始化容量（ininialCapacity）**

```java
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: "+
                                           initialCapacity);
    }
}
```

**数组每次扩容会扩大之前容量的 1.5 倍**

```java
private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);// 新容量是老容量的 1.5 倍
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}
```

==二进制位运算：==

\>> n ： ==表示二进制向右移动 n 位，计算成十进制就是 缩小为原来的  $ \frac{1}{2^n}$ 倍==

\<< n ： ==表示二进制向左移动 n 位，计算成十进制就是 扩大为原来的  2^n^ 倍==



#### 19.3.2 LinkList 

**链表的优点**

> 由于链表上的元素在空间存储上内存地址不连续。
>
> 所以随机增删元素的时候不会有大量元素位移，因此随机增删效率较高。
>
> 在以后的开发中，如果遇到随机增删集合中元素的业务比较多时，建议使用LinkedList。

**链表的缺点**

> 不能通过数学表达式计算被查找元素的内存地址，每一次查找都是从头
>
> 节点开始遍历，直到找到为止。所以LinkedList集合检索/查找的效率较低。



**单链表** 

> 节点（Node）是单链表中基本的单元，每一个节点都有两个属性
>
> 一个属性是存储数据的
>
> 一个属性是存储下一个节点的内存地址的

```java
// 节点
public class Node {
    // 存储数据
    Object data;
    // 下一个节点
    Node next;

    public Node(Object data, Node next) {
        this.data = data;
        this.next = next;
    }
}
```

```java
public class Link {
    // 头节点
    Node node;
    
    // 向链表末尾添加节点的方法
    public void add(Object data) {
        // 如果头节点为 null
        if (node == null) {
            // 新建一个头节点
            node = new Node(data, null);
        } else {// 头节点不是 null
            // 找到最后一个节点
            Node lastNode = findList(node);
            // 让尾节点的next执行新节点
            lastNode.next = new Node(data, null);
        }
    }

    private Node findList(Node node) {
        // 如果这个节点的next是null，表明这个节点就是尾结点了
        if (node.next == null) {
            return node;
        }
        // 使用递归
        return findList(node.next);
    }
}
```

**LinkedList（==双向链表==）**

add方法源码阅读

```java
public LinkedList() {
	Node<E> first = null;// 指向当前链表的第一个节点
    Node<E> last = null;// 指向当前链表的最后一个节点
}

public boolean add(E e) {
    linkLast(e);
    return true;
}

void linkLast(E e) {
    final Node<E> l = last;// 使 l 执行当前链表中的最后一个节点
    final Node<E> newNode = new Node<>(l, e, null);// 创建一个新的节点对象，prev 指向最后一个节点，next 指向 null
    last = newNode;// 使 last 指向新创建的节点（此时新节点就是链表中最后的一个节点了）
    if (l == null)// 这个 if 分支只会执行在当前链表中没有节点的时候
        first = newNode;// 使 first 指向新创建的第一个节点
    else
        l.next = newNode;// 使之前最后一个节点的 next 指向新建的节点
    size++;
    modCount++;
}
```



#### 19.3.3 Vector（不常用）

底层也是一个数组

初始化容量为 10

扩容后的容量是之前的 2 倍

Vector 中的所有方法都是线程同步的，都带有 syschronized 关键字，是线程安全的，效率比较低，使用较少了

怎样将一个线程不安全的 ArrayList 集合装换为线程安全的呢？
* 使用工具类 `java.util.Collections;`
* `Collections.synchronizedList(List<T> list)`



### 19.4 泛型机制

**JDK5.0之后推出的新特性：泛型**

泛型这种语法机制，只在程序编译阶段起作用，只是给编译器参考的。（运行阶段泛型没用！）

泛型好处：

1. 集合中存储的元素类型统一了。
2. 从集合中取出的元素类型是泛型指定的类型，不需要进行大量的“向下转型”！

泛型缺点：

1. 导致集合中存储的元素缺乏多样性；
2. 大多数业务中，集合中元素的类型还是统一的。所以这种泛型特性被大家所认可。

泛型实例：

```java
public class Test {
    public static void main(String[] args) {
        // 使用泛型
        // 使用泛型List<Animal>之后，表示List集合中只能存储Animal类型的数据
        // 用泛型来指定集合中存储的数据类型
        // 指定List集合中只能存储Animal类型数据，存储String类型数据编译就报错了
        // 这样使用了泛型后，集合中的元素的数据类型更加统一了
        List<Animal> myList = new ArrayList<Animal>();

        // 准备对象
        Cat cat = new Cat();
        Bird bird = new Bird();

        // 将对象添加到集合中去
        myList.add(cat);
        myList.add(bird);

        // 编历集合，取出Cat让它抓老鼠，取出Bird让它飞翔
        // 获取迭代器,表示迭代器迭代的是Animal类型
        Iterator<Animal> iterator = myList.iterator();
        while (iterator.hasNext()) {
            // 使用泛型后，每一次迭代返回的数据都是Animal类型
            Animal animal = iterator.next();
            // 这里就不需要进行强制类型转换了
            animal.move();
            // 但是如果要调用子类特有的方法，就需要向下转型（是一定要向下转型的）
            if (animal instanceof Cat) {
                ((Cat) animal).catchMouse();
            }
            if (animal instanceof Bird) {
                ((Bird) animal).catchChicken();
            }

        }
    }
}

class Animal {
    // 父类特有方法
    public void move() {
        System.out.println("动物在移动");
    }
}

class Cat extends Animal {
    @Override
    public void move() {
        System.out.println("猫在走猫步");
    }

    // 子类特有方法
    public void catchMouse() {
        System.out.println("猫在捉老鼠");
    }
}

class Bird extends Animal {
    @Override
    public void move() {
        System.out.println("鸟儿在飞翔");
    }

    // 子类特有方法
    public void catchChicken() {
        System.out.println("鸟儿在捉小鸡");
    }
}
```

自定义泛型：

```java
public class Test {
    public static void main(String[] args) {
       // 这是钻石表达式，前面指定了类型，后面就可以不指定了
       MyClass<String> MyClass01 = new MyClass<>();
        MyClass01.doSome("e");
        // 以下会报错
        // stringMyClass.doSome(123);

        MyClass<Integer> myClass02 = new MyClass<>();
        myClass02.doSome(123);// 自动装箱
        // 以下会报错
        // myClass.doSome(true);

        // 不使用泛型，默认类型为 Object
        MyClass myClass03 = new MyClass();
        myClass03.doSome(new Object());
    }
}

// 当前类使用了泛型
class MyClass<E> {
    // 方法内传进去的参数类型为 E，在 new 对象的时候可以规定下来，不使用泛型，就默认为 Object
    public void doSome(E e) {
        System.out.println(e);
    }
}
```



### 19.5 增强 for 循环（foreach）

**JDK5.0后推出了一个新特性：叫做增强for循环，或者叫做foreach**

**foreach有一个缺点：==没有下标。在需要使用下标的循环中，不建议使用增强for循环==**。

增强 for 循环编历数组：

```java
int[] array = {1,3,54,5657,34,4664,43};
for (int i : array) {
    System.out.println(i);
}
/*
	输出：
		1
        3
        54
        5657
        34
        4664
        43
*/
```

增强 for 循环编历集合：

```java
// 三种方式编历集合
// 创建集合
List<String> list = new ArrayList<>();
list.add("zhangsan");
list.add("lisi");
list.add("wangwu");
list.add("zhaoliu");

// 使用迭代器方式
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String next = iterator.next();
    System.out.println(next);
}

System.out.println("============");

// 使用普通 for 循环，通过下标方式
for (int i = 0; i < list.size(); i++) {
    String string = list.get(i);
    System.out.println(string);
}

System.out.println("============");

// 使用增强 for 循环
for (String s : list) {
    System.out.println(s);
}
```



### 19.6 Map 接口及其实现类

#### 19.6.1 Map 接口

Map和Collection没有继承关系

Map集合以==key 和 value==的方式存储数据：==键值对==

* key和value都是引用数据类型。
* key和value都是存储对象的内存地址。
* key起到主导的地位，value是key的一个附属品。

**Map接口中常用方法：**

```java
V put(K key, V value) // 向Map集合中添加键值对
V get(Object key) // 通过key获取value
void clear()    // 清空Map集合
boolean containsKey(Object key) // 判断Map中是否包含某个key
boolean containsValue(Object value) // 判断Map中是否包含某个value
boolean isEmpty()   // 判断Map集合中元素个数是否为0
V remove(Object key) // 通过key删除键值对
int size() // 获取Map集合中键值对的个数。
Collection<V> values() // 获取Map集合中所有的value，返回一个Collection
Set<K> keySet() // 获取Map集合所有的key（所有的键是一个set集合）
Set<Map.Entry<K,V>> entrySet() // 将Map集合转换成Set集合

 假设现在有一个Map集合，如下所示：
    map1集合对象
    key             value
    ----------------------------
    1               zhangsan
    2               lisi
    3               wangwu
    4               zhaoliu
    
    Set set = map1.entrySet();
	set集合对象：
    1=zhangsan 【Set集合中元素的类型是 Map.Entry<K,V>】
    2=lisi     【Map.Entry是静态内部类，是Map中的静态内部类】
    3=wangwu
    4=zhaoliu ---> 这个东西是个什么？Map.Entry
```

```java
// 创建 Map 集合
Map<Integer, String> map = new HashMap<>();

// V put(K key, V value)
map.put(1, "zhangsan");
map.put(2, "lisi");
map.put(3, "wangwu");
map.put(4, "zhaoliu");

// V get(Object key)
String value02 = map.get(2);
System.out.println("key为2的value是" + value02 );// key为2的value是lisi

// boolean containsKey(Object key)
// boolean containsValue(Object value)
// 底层都是使用 equals() 方法来进行判断的
System.out.println("map中是否包含key = 3，" + map.containsKey(3));// map中是否包含key = 3，true
System.out.println("map中是否包含key = 5，" + map.containsKey(5));// map中是否包含key = 5，false
System.out.println("map中是否包含value = zhangsan，" + map.containsValue("zhangsan"));// map中是否包含value = zhangsan，true

// V remove(Object key)
String remove = map.remove(1);
System.out.println("移除掉的value是：" + remove);// 移除掉的value是：zhangsan

// Collection<V> values()
Collection<String> values = map.values();
for (String s : values) {
    System.out.println(s);
}

// Set<K> keySet()
Set<Integer> keys = map.keySet();
for (Integer i : keys) {
    System.out.println(i);
}

// Set<Map.Entry<K,V>> entrySet()
Set<Map.Entry<Integer, String>> set = map.entrySet();
System.out.println(set);// [2=lisi, 3=wangwu, 4=zhaoliu]

// void clear()
map.clear();

// int size()
System.out.println(map.size());// 0
```

**Map集合的编历：**

```java
// 第一种：获取所有的Key，通过编历Key，来编历Value
// 效率较低，因为每次都要从 Map 集合中通过 key 去找 value
Set<Integer> keys = map.keySet();
for (Integer key : keys) {
    System.out.println(key + "=" + map.get(key));
}

// 第二种：Set<Map.Entry<K,V>> entrySet()
// 将 Map 转换为 Set，Set 中存储的数据的数据类型是 Map.Entry
Set<Map.Entry<Integer, String>> set = map.entrySet();
for (Map.Entry<Integer, String> node : set) {
    System.out.println(node.getKey() + "=" + node.getValue());
}

// 第三种：JDK8新特性
map.forEach((key, value) ->{
    System.out.println(key + "=" + value);
});
```



#### 19.6.2 HashSet / HashMap 

**HashMap集合底层是==哈希表/散列表==的数据结构**。

**哈希表是一个怎样的数据结构呢：**

* 哈希表是一个数组和单向链表的结合体。
* 数组：在查询方面效率很高，随机增删方面效率很低。
* 单向链表：在随机增删方面效率较高，在查询方面效率很低。
* 哈希表将以上的两种数据结构融合在一起，充分发挥它们各自的优点。(一维数组，这个数组中每一个元素是一个单向链表)

![008-哈希表或者散列表数据结构](https://img-blog.csdnimg.cn/20210222185835378.png)

**HashMap集合底层的源代码：**

```java
HashMap集合底层的源代码：
public class HashMap{
    // HashMap底层实际上就是一个数组。（一维数组）
    Node<K,V>[] table;
    // 静态的内部类HashMap.Node
    static class Node<K,V> {
        final int hash; // 哈希值（哈希值是key的hashCode()方法的执行结果。hash值通过哈希函数/算法，可以转换存储成数组的下标。）
        final K key; // 存储到Map集合中的那个key
        V value; // 存储到Map集合中的那个value
        Node<K,V> next; // 下一个节点的内存地址。
    }
}
```

**两个方法的实现原理：**

`map.put(k, v);`

第一步：**先将 k, v 封装到 Node 对象当中**

第二步：**底层会调用 k 的 hashCode() 方法得出 hash 值**

第三步：通过哈希函数 / 哈希算法将 hash 值转换为数组的下标，如果该下标位置上没有元素，那么就直接将 Node 对象放到这个位置上了，如果该下标上有元素，就会那着 **Node 节点上的 k 和链表中每个节点的 k 进行 equals** ，如果所有 equals 方法返回的都是 false，那么这个新节点将会被添加到链表的最后，如果其中有一个返回 true，**那么这个节点的 vlaue 值会被 Node 节点的 v 覆盖。**

`v = map.get(k);`

先调用 k 的 **hashCode 方法取得 hash 值**，然后通过**哈希算法将 hash 值转换为 数组的下标**，通过数组下标快速定位到某个位置，**如果这个位置上什么也没有，就返回 null**，如果这个位置上有单向链表，就拿着参数 k 和链表上各个节点的 k 进行 equals ，**如果 equals 方法返回的都是 false，那么方法返回 null**，只要其中有一个节点 equals **后返回 true，此时这个节点上的 value 就是我们要找的 value**，get 方法最终返回这个 value。

**HashMap集合的key部分特点：==无序，不可重复==**

* 无序：因为不一定挂到哪个单向链表上；
* 不可重复：equals 方法保证  HashMap 集合的 key 不可重复，如果 key 重复了，value 就会覆盖。

**==重点：放在HashMap集合key部分的元素，以及放在HashSet集合中的元素，需要同时重写hashCode和equals方法。==**

![image-20210222191852249](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210222191852249.png)



**HashMap 集合的==默认初始化容量是16，默认加载因子是0.75==**（这个默认加载因子是当HashMap集合底层数组的容量达到75%的时候，数组开始扩容。）

重点，**记住：HashMap集合初始化容量必须是2的倍数**，这也是官方推荐的，这是因为达到散列均匀，为了提高HashMap集合的存取效率，所必须的。

**对于哈希表数据结构来说：**

 *     如果o1和o2的hash值相同，一定是放到同一个单向链表上。
 *     当然如果o1和o2的hash值不同，但由于哈希算法执行结束之后转换的数组下标可能相同，此时会发生 **==“哈希碰撞”==**。

**HashMap集合key部分允许null吗：允许**

* 但是要注意：HashMap集合的key null值只能有一个。



#### 19.6.3 HashTable

Hashtable方法都带有synchronized：线程安全的。

Hashtable和HashMap一样，底层都是哈希表数据结构。

Hashtable的**初始化容量是11，默认加载因子是：0.75f**

**Hashtable的扩容是：原容量 * 2 + 1**

Hashtable的key和value都是不能为null的。（HashMap集合的key和value都是可以为null的。）



#### 19.6.4 Properties

**Properties是一个Map集合，继承Hashtable，Properties的==key和value都是String类型==。**

Properties被称为属性类对象

```java
// 创建一个Properties对象
Properties pro = new Properties();

// 两个方法，一个存，一个取
pro.setProperty("11", "AA");
pro.setProperty("22", "BB");
pro.setProperty("33", "CC");
pro.setProperty("44", "DD");
pro.setProperty("55", "EE");

// 通过key获取value
System.out.println(pro.getProperty("11"));
System.out.println(pro.getProperty("22"));
System.out.println(pro.getProperty("33"));
System.out.println(pro.getProperty("44"));
System.out.println(pro.getProperty("55"));
```



#### 19.6.5 TreeSet / TreeMap

**TreeSet集合存储元素特点：**

* 无序不可重复的，但是存储的元素可以自动按照大小顺序排序！
* 无序：这里的无序指的是存进去的顺序和取出来的顺序不同。并且没有下标。

```java
TreeSet<String> treeSet = new TreeSet<>();
treeSet.add("abd");
treeSet.add("aba");
treeSet.add("abc");
for (String s : treeSet) {
    System.out.println(s);
}
/*
	输出：
		aba
        abc
        abd
*/
```

**TreeSet集合底层实际上是一个TreeMap，TreeMap集合底层是一个二叉树。**

![010-自平衡二叉树](https://img-blog.csdnimg.cn/20210222213937898.png)

**放到TreeSet集合中的元素，等同于放到TreeMap集合key部分了。**

**对自定义的类型来说，TreeSet可以排序吗？**

* 以下程序中对于Person类型来说，无法排序。因为没有指定Person对象之间的比较规则。

 *     谁大谁小并没有说明啊。
 *     以下程序运行的时候出现了这个异常：
 *         `java.lang.ClassCastException:class com.bjpowernode.javase.collection.Personcannot be cast to class java.lang.Comparable`
 *     出现这个异常的原因是：Person类没有实现 `java.lang.Comparable `接口。

```java
public class Test {
    public static void main(String[] args) {
        TreeSet<Person> set = new TreeSet<>();
        set.add(new Person(20));
        set.add(new Person(12));
        set.add(new Person(8));
        for (Person person : set) {
            System.out.println(person);
        }
    }
}

class Person {
    int age;

    public Person(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                '}';
    }
}
```

**TreeSet集合中元素可排序的第一种方式：实现 `java.lang.Comparable` 接口，重写 `compareTo()` 方法**

```java
public class Test {
    public static void main(String[] args) {
        TreeSet<Person> set = new TreeSet<>();
        set.add(new Person(20, "zhangsan"));
        set.add(new Person(20, "zhangsi"));
        set.add(new Person(12, "lisi"));
        for (Person person : set) {
            System.out.println(person);
        }
        /*
        	输出：
        		Person{age=12, name='lisi'}
                Person{age=20, name='zhangsan'}
                Person{age=20, name='zhangsi'}
        */
    }
}

// 要比较的类实现 Comparable 接口
class Person implements Comparable<Person>{
    int age;
    String name;

    public Person(int age, String name) {
        this.age = age;
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }

    @Override
    // 先按照年龄升序，如果年龄一样的再按照姓名升序。
    // compareTo方法的返回值很重要：
    // 返回0表示相同，value会覆盖。
    // 返回>0，会继续在右子树上找。
    // 返回<0，会继续在左子树上找。
    public int compareTo(Person o) {
        return this.age > o.age ? (Integer.compare(this.age, o.age)) : (this.name.compareTo(o.name));
    }
}
```

**TreeSet集合中元素可排序的第二种方式：使用比较器的方式**。

* 可以写一个类实现比较器接口 `java.util.Comparator` ，重写 `compare()` 方法，将比较器作为参数放入 TreeSet 的构造方法中

```java
public class Test {
    public static void main(String[] args) {
        TreeSet<Person> set = new TreeSet<>(new PersonComparator());
        set.add(new Person(20, "zhangsan"));
        set.add(new Person(20, "zhangsi"));
        set.add(new Person(12, "lisi"));
        for (Person person : set) {
            System.out.println(person);
        }
        /*
        	输出：
        		Person{age=12, name='lisi'}
                Person{age=20, name='zhangsan'}
                Person{age=20, name='zhangsi'}
        */
    }
}


class PersonComparator implements Comparator<Person> {
    @Override
    public int compare(Person o1, Person o2) {
        return o1.age > o2.age ? (Integer.compare(o1.age, o2.age)) : (o1.name.compareTo(o2.name));
    }
}
```

* 可以使用匿名内部类写一个比较器

```java
TreeSet<Person> set = new TreeSet<>(new Comparator<Person>() {
    @Override
    public int compare(Person o1, Person o2) {
        return o1.age > o2.age ? (Integer.compare(o1.age, o2.age)) : (o1.name.compareTo(o2.name));
    }
});
set.add(new Person(20, "zhangsan"));
set.add(new Person(20, "zhangsi"));
set.add(new Person(12, "lisi"));
for (Person person : set) {
    System.out.println(person);
}
/*
输出：
	Person{age=12, name='lisi'}
    Person{age=20, name='zhangsan'}
    Person{age=20, name='zhangsi'}
 */
```

**Comparable 和 Comparator 怎么选择呢？**

* **当比较规则不会发生改变的时候**，或者说当比较规则只有1个的时候，建议实现Comparable接口。
* **如果比较规则有多个，并且需要多个比较规则之间频繁切换**，建议使用Comparator接口。（**Comparator接口的设计符合OCP原则。**）





## 20、IO 流

### 20.1 IO流概述

#### 20.1.1 什么是 IO 流

I : Input

O : Output

==**通过IO可以完成硬盘文件的读和写。**==

![001-什么是IO](https://img-blog.csdnimg.cn/20210222222354471.png)

#### 20.1.2 IO流的分类

**一种方式是按照流的方向进行分类：**

以内存作为参照物

* 往内存中去，叫做==输入(Input)==。或者叫做==读(Read)==
* 从内存中出来，叫做==输出(Output)==。或者叫做==写(Write)==



**另一种方式是按照读取数据方式不同进行分类：**

* 有的流是按照  **==字节==**  的方式读取数据，**一次读取1个字节byte**，等同于一次读取8个二进制位。

  **这种流是万能的，什么类型的文件都可以读取**。包括：文本文件，图片，声音文件，视频文件等....

  假设文件file1.txt，采用字节流的话是这样读的：

  ​	**a中国bc张三fe**

  ​	第一次读：一个字节，正好读到'a'

  ​	第二次读：一个字节，正好读到'中'字符的一半。（'a'字符在windows系统中占用1个字节。）

  ​	第三次读：一个字节，正好读到'中'字符的另外一半。（'中'字符在windows系统中占用2个字节。）

* 有的流是按照  ==**字符**==  的方式读取数据的，**一次读取一个字符**，这种流是为了**方便读取普通文本文件**而存在的，这种流不能读取：图片、声音、视频等文件。只能读取纯文本文件（不能读取 word 文件）

  假设文件file1.txt，采用字符流的话是这样读的：

  ​	**a中国bc张三fe**

  ​	第一次读：'a'字符（'a'字符在windows系统中占用1个字节。）

  ​	第二次读：'中'字符（'中'字符在windows系统中占用2个字节。）



#### 20.1.3 java IO流四大家族

**四大家族的首领（都是抽象类）：**

* java.io.InputStream（字节输入流）
* java.io.OutputStream（字节输出流）
* java.io.Reader（字符输入流）
* java.io.Writer（字符输出流）

**==所有的流==都实现了:**

* `java.io.Closeable` 接口：都是可关闭的，都有`close() `方法。

  流毕竟是一个管道，这个是内存和硬盘之间的通道，**用完之后一定要关闭，不然会耗费(占用)很多资源**。养成好习惯，用完流一定要关闭。

**所有的==输出流==都实现了：**

* `java.io.Flushable` 接口，都是可刷新的，都有`flush()` 方法。

  养成一个好习惯，输出流在最终输出之后，一定要记得 flush() 刷新一下。这个**刷新表示将通道/管道当中剩余未输出的数据强行输出完**（清空管道！）刷新的作用就是清空管道。

  **注意：如果没有flush()可能会导致丢失数据**。

**==注意：在java中只要“类名”以Stream结尾的都是字节流。以“Reader/Writer”结尾的都是字符流。==**



#### 20.1.4 java.io包下需要掌握的流有16个

**文件专属：**

* `java.io.FileInputStream`（掌握）
* `java.io.FileOutputStream`（掌握）
* `java.io.FileReader`
* `java.io.FileWriter`

**转换流：（将字节流转换成字符流）:**

* `java.io.InputStreamReader`
* `java.io.OutputStreamWriter`

**缓冲流专属：**

* `java.io.BufferedReader`

* `java.io.BufferedWriter`

* `java.io.BufferedInputStream`

* `java.io.BufferedOutputStream`

**数据流专属：** 

* `java.io.DataInputStream`

* `java.io.DataOutputStream`

**标准输出流：**

* `java.io.PrintWriter`

* `java.io.PrintStream`（掌握）

**对象专属流：**

* `java.io.ObjectInputStream（掌握）`

* `java.io.ObjectOutputStream（掌握）`



### 20.2 FileInputStream

#### 20.2.1 概述

* **文件字节输入流，万能的，任何类型的文件都可以采用这个流来读。**
* 字节的方式，完成输入的操作，完成读的操作（==硬盘---> 内存==）

#### 20.2.2 简单使用

* 构造方法中可以放文件的路径
* 当文件不在 IDEA 项目文件下时，要使用**绝对路径**
* 当文件在 IDEA 项目下是，可以使用相对路径，**默认路径是当前项目的根目录**
* **流使用完一定要在 finally 语句块中关闭**

```java
int	read()// 从输入流中读取一个字节的数据，返回值是读取到的字符的 ASCII 码，当数据被读完的时候会返回 -1
int	read(byte[] b)// 从输入流中读取最多b.length字节的数据到字节数组中，返回值是此次往 byte 数组中存放的字节个数，当数据读完的时候会返回 -1
int	read(byte[] b, int off, int len)// 从输入流中读取多达len字节的数据到一个字节数组中。
```

```java
FileInputStream fileInputStream = null;
try {
    // 构造方法中可以放文件的路径
    // 当文件不在 IDEA 项目文件下时，要使用绝对路径
    // 当文件在 IDEA 项目下是，可以使用相对路径，默认路径是当前项目的根目录
    fileInputStream = new FileInputStream("src//cn//yechen//myfile.txt");

    // 读文件，一次读取一个字节byte，这样内存和硬盘交互太频繁，基本上 时间/资源 都耗费在交互上面了
    int read = 0;
    while ((read = fileInputStream.read()) != -1) {
        System.out.println(read);// 这里输出的都是字符的 ASCII 码
    }

    // 一次读 byte.length 个字节
    byte[] bytes = new byte[10];
    int readCount = 0;
    StringBuffer buffer = new StringBuffer();
    while ((readCount = fileInputStream.read(bytes)) != -1) {
        // 使用 String 类的构造方法，将 byte 数组转变为字符串（起始下标为 0， 长度为 reedCount）
        String string = new String(bytes, 0, readCount);
        buffer.append(string);
    }
    System.out.println(buffer);

} catch (IOException e) {
    e.printStackTrace();
} finally {
    // 流使用完一定要记得关闭
    // 关闭流的前提是流不是空的，避免空指针异常
    if (fileInputStream != null) {
        try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 20.2.3 其他方法

`int available()` ：返回流当中剩余的没有读到的字节数量

**可以在读取小文件的时候将此方法的返回值作为 byte 数组的长度，一次直接读完方放到 byte 数组中。**

但是不适用于读取大文件，因为数组的内存空间是连续的，找不到一块很大的连续内存空间来存放 byte 数组。

```java
FileInputStream fileInputStream = new FileInputStream("src//cn//yechen//myfile.txt");

int available = fileInputStream.available();
System.out.println("还剩多少字节可以读：" + available);// 输出：还剩多少字节可以读：119

int read = fileInputStream.read();// 读了一个字节
System.out.println("还剩多少字节可以读：" + fileInputStream.available());// 输出：还剩多少字节可以读：118

myfile.txt ->
    public class Hello {
        public static void main(String[] args) {
            System.out.println("HelloWorld");
        }
    }
```

`long skip(long n)`： 跳过 n 个字节不读

```java
FileInputStream fileInputStream = new FileInputStream("src//cn//yechen//myfile02.txt");
System.out.println("第一次读到：" + fileInputStream.read());// 输出：第一次读到：97（a）

// 跳过三个字节（bcd）
fileInputStream.skip(3);

System.out.println("第二次读到：" + fileInputStream.read());// 输出：第二次读到：101（e）

myfile02.txt -> 
    abcdefg
```





### 20.3 FileOutputStream

文件字节输出流，负责写。

**从内存到硬盘。**

**输出流在写完之后一定要记得刷新。**

**简单使用：**

```java
FileOutputStream fileOutputStream = null;
try {
    // 这种方式谨慎使用，这种方式会先将原文件清空，然后重新写入。
    // fileOutputStream = new FileOutputStream("src//cn//yechen//myfile03.txt");
    // 以追加的方式在文件末尾写入。不会清空原文件内容。
    // 文件不存在的时候会自动创建
    fileOutputStream = new FileOutputStream("src//cn//yechen//myfile03.txt", true);

    byte[] bytes = {97,98,99,100,101,102};
    // 将 byte 数组写入文件
    fileOutputStream.write(bytes);

    String string = "我是中国人";
    // 将 string 字符串先转变为 byte 数组在写入文件
    byte[] bytes1 = string.getBytes();
    fileOutputStream.write(bytes1);

    // 使用完流记得刷新一下
    fileOutputStream.flush();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fileOutputStream != null) {
        try {
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

myfile03 ->
    abcdef我是中国人
```



### 20.4 FileReader / FileWriter

**文件字符输入流，只能读取普通文本。**

读取文本内容时，比较方便，快捷。

```java
FileReader reader = null;
try {
    // 创建字符输入流
    reader = new FileReader("src//cn//yechen//myfile.txt");

    char[] chars = new char[1024 * 512];// 一次读取 1 MB
    int readCount = 0;
    // 开始读
    while ((readCount = reader.read(chars)) != -1) {
        System.out.println(new String(chars, 0, readCount));
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



**文件字符输出流。只能输出普通文本。**

```java
FileWriter fileWriter = null;
try {
    // 创建字符输出流对象
    fileWriter = new FileWriter("src//cn//yechen//myfile02.txt");
    // 开始写
    char[] chars = {'我', '是', '中', '国', '人', '！'};
    // 可以传进char数组
    fileWriter.write(chars);
    // 可以传进字符串
    fileWriter.write("我是中国人！");
    // 刷新流
    fileWriter.flush();

} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fileWriter != null) {
        try {
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



### 20.5 BufferedReader / BufferWriter

**BufferedReader:**

* 带有缓冲区的字符输入流。
* 使用这个流的时候不需要自定义char数组，或者说不需要自定义byte数组。自带缓冲。

```java
FileReader fileReader = null;
BufferedReader bufferedReader = null;
try {
    fileReader = new FileReader("src\\io\\copy\\CopyTest01.java");
    // 当一个流的构造方法中需要一个流的时候，这个被传进来的流叫做：节点流。
    // 外部负责包装的这个流，叫做：包装流，还有一个名字叫做：处理流。
    // 像当前这个程序来说：FileReader就是一个节点流。BufferedReader就是包装流/处理流。
    bufferedReader = new BufferedReader(fileReader);
    String s;
    // bufferedReader.readLine()方法读取一个文本行，但不带换行符。
    while ((s = bufferedReader.readLine()) != null) {
        System.out.println(s);
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    // 只需要关闭最外层的包装流就行了
    if (bufferedReader != null) {
        try {
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**BufferWriter：**

* 带有缓冲的字符输出流

```java
BufferedWriter bufferedWriter = null;
try {
    bufferedWriter = new BufferedWriter(new FileWriter("src//cn//yechen//myfile02.txt"));
    // 可以写入一个字符串
    bufferedWriter.write("我是中国人");// 写入：“我是中国人”

    // 可以写入一个 char 数组的一部分
    char[] chars = {'我','是','中','国','人'};
    bufferedWriter.write(chars, 2, 3);// 写入：“中国人”

    // 刷新输出流
    bufferWriter.flush();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (bufferedWriter != null) {
        try {
            bufferedWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**节点流和包装流：**

当一个流的构造方法中需要一个流的时候，这个被传进来的流叫做：节点流。

 外部负责包装的这个流，叫做：包装流，还有一个名字叫做：处理流。

**关闭流的时候只需要关闭最外层的包装流即可。**

节点流和包装流是相对的。



### 20.6 InputStreamReader / OutputStreamWriter

**转换流**

`InputStreamReader` ： 将字节输入流转换为字符输入流。

```java
FileInputStream fileInputStream = new FileInputStream("");
InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream);
```

`OutputStreamWriter` ： 将字节输出流转换为字符输出流。

```java
FileOutputStream fileOutputStream = new FileOutputStream("");
OutputStreamWriter outputStreamWriter = new OutputStreamWriter(fileOutputStream);
```



### 20.7 DataOutputStream / DataInputStream

**DataOutputStream：**数据专属的流

这个流可以将数据连同数据的类型一并写入文件。

注意：这个文件不是普通文本文档。（这个文件使用记事本打不开。）

```java
DataOutputStream dataOutputStream = null;
try {
    dataOutputStream = new DataOutputStream(new FileOutputStream("data"));
    // 写数据
    byte b = 13;
    int i = 1000;
    double d = 222;
    boolean flag = true;
    char c = 'a';

    // 写
    dataOutputStream.writeByte(b);
    dataOutputStream.writeInt(i);
    dataOutputStream.writeDouble(d);
    dataOutputStream.writeBoolean(flag);
    dataOutputStream.writeChar(c);

    // 刷新数据流
    dataOutputStream.flush();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (dataOutputStream != null) {
        try {
            dataOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**DataInputStream：** 数据字节输入流

DataOutputStream 写的文件，只能使用 DataInputStream 去读。并且读的时候你需要提前知道写入的顺序。

读的顺序需要和写的顺序一致。才可以正常取出数据。

```java
DataInputStream dataInputStream = null;
try {
    dataInputStream = new DataInputStream(new FileInputStream("data"));
    // 开始读
    byte b = dataInputStream.readByte();
    int i = dataInputStream.readInt();
    double v = dataInputStream.readDouble();
    boolean b1 = dataInputStream.readBoolean();
    char c = dataInputStream.readChar();

    // 输出
    System.out.println(b);
    System.out.println(i);
    System.out.println(v);
    System.out.println(b1);
    System.out.println(c);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (dataInputStream != null) {
        try {
            dataInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



### 20.8 PrintStream

标准的字节输出流。**默认输出到控制台**。

标准输出流**不需要手动close()关闭**。

可以改变标准输出流的输出方向。

```java
// 记录标准输出流的默认输出方向（到控制台）
PrintStream printStream = System.out;
// 改变输出方向
System.setOut(new PrintStream(new FileOutputStream("log", true)));// 为了方便已经抛出异常
// 输出到指定路径
System.out.println("zhangsan");
System.out.println("lisi");
System.out.println("wangwu");
// 输出到控制台
printStream.println(1);
printStream.println(2);
printStream.println(3);

// log文件输出
zhangsan
lisi
wangwu
    
// 控制台输出
1
2
3
```

**可以写一个类来打印日志信息，日志信息存放在一个文件中**

```java
public class MyLog {
    public static void printLog(String msg) {
        try {
            // 改变标准输出流的输出方向
            System.setOut(new PrintStream(new FileOutputStream("log", true)));
            // 获取当前时间
            long nowTimeMillis = System.currentTimeMillis();
            Date date = new Date(nowTimeMillis);
            SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
            String nowTimeStr = simpleDateFormat.format(date);
            // 输出日志信息
            System.out.println(nowTimeStr + "：" + msg);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```



### 20.9 File

**File类和四大家族没有关系**，所以File类不能完成文件的读和写。

File对象代表：**文件和目录路径名的抽象表示形式。**

* 一个目录是一个 File 对象
* 一个文件也是一个 File 对象

**一个File对象有可能对应的是目录，也可能是文件。File只是一个路径名的抽象表示形式。**

#### File类中常用的方法：

1. 创建一个 File 对象

```java
File file = new File("D:\\Code\\Java");// 构造方法中跟目录路径或是文件路径，可以存在，也可以不存在
```

2. `boolean exists()` ：判断当前目录或文件**是否存在**

```java
boolean isExists = file.exists();
```

3. `boolean createNewFile()`：**当且仅当具有此名称的文件还不存在时**，才会自动创建一个以该抽象路径名命名的**新空文件**。

```java
// 如果当前路径 目录或文件不存在
if (!file.exists()) {
    // 以文件的形式创建出来
    file.createNewFile();
}
```

4. `boolean mkdir()`：创建以这个抽象路径名命名的**目录**。

```java
// 如果当前路径 目录或文件不存在
if (!file.exists()) {
    // 以目录的形式创建出来
    file.mkdir();
}
```

5. `boolean mkdirs()` ： 创建以这个抽象路径名命名的目录，**包括任何必要但不存在的父目录**。

```java
File file02 = new File("D:\\a\\b\\c");
if (!file02.exists()) {
    file02.mkdirs();
}
```

6. `String	getParent()` : **返回这个抽象路径名的父路径名字符串**，如果这个路径名没有指定父目录，则返回null。

```java
File file = new File("D:\\Code\\Java\\JavaLearning");
String parent = file.getParent();
System.out.println(parent);// D:\Code\Java
```

7. `File getParentFile()` ： **返回这个抽象路径名的父目录的抽象路径名**，如果这个路径名没有指定父目录，则返回null。
8. `String getPath()` ：将这个抽象的路径名转换为**一个路径名字符串**。
9. `String	getAbsolutePath()` ：返回这个抽象路径名的**绝对路径名字符串。**
10. `File getAbsoluteFile()` ：返回这个抽象路径名的**绝对形式**。

```java
File file = new File("src//cn//yechen");// 以 IDEA 根目录为默认路径的 目录
File parentFile = file.getParentFile();
System.out.println(parentFile.getPath());// src\cn
System.out.println(parentFile.getAbsolutePath());// C:\Users\30117\Desktop\Demo\src\cn
File absoluteFile = file.getAbsoluteFile();
System.out.println(absoluteFile.getPath());// C:\Users\30117\Desktop\Demo\src\cn\yechen
```

11. `String	getName()` ：返回由这个抽象路径名表示的**文件或目录的名称**。

```java
File file = new File("src//cn//yechen");// 以 IDEA 根目录为默认路径的 目录
System.out.println(file.getName());// Yechen
```

12. `boolean isDirectory()` ： 测试此抽象路径名表示的文件**是否为目录**。

13. `boolean isFile()` ：测试此抽象路径名表示的文件**是否为普通文件**。

```java
File file = new File("src//cn//yechen");// 以 IDEA 根目录为默认路径的 目录
System.out.println(file.isFile());// false
System.out.println(file.isDirectory());// true
```

14. `long lastModified()` ：返回这个抽象路径名所表示的文件**最后一次修改的时间。**

```java
File file = new File("D:\\Java基础知识篇.pdf");
long lastModified = file.lastModified();// 这个毫秒是从1970年到现在的总毫秒数。
Date date = new Date(lastModified);
SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
String timeStr = simpleDateFormat.format(date);
System.out.println(timeStr);// 2020-05-25 09:05:53 000
```

15. `long length()` ：返回由这个抽象路径名表示的**文件的长度（字节）**。

```java
File file = new File("D:\\Java基础知识篇.pdf");
System.out.println(file.length());// 2416894 
```

16. `File[]	listFiles()` ：返回一个**抽象路径名数组**，它表示由这个抽象路径名指定的**目录中的文件**。

```java
File file = new File("src//cn//yechen");
File[] files = file.listFiles();
// 编历 files
for (File file1 : files) {
    System.out.println(file1.getAbsolutePath());// 输出目录中文件的绝对路径
}
/*
	输出：
		C:\Users\30117\Desktop\Demo\src\cn\yechen\collection
        C:\Users\30117\Desktop\Demo\src\cn\yechen\Link
        C:\Users\30117\Desktop\Demo\src\cn\yechen\myfile.txt
        C:\Users\30117\Desktop\Demo\src\cn\yechen\myfile02.txt
        C:\Users\30117\Desktop\Demo\src\cn\yechen\myfile03.txt
        C:\Users\30117\Desktop\Demo\src\cn\yechen\MyLog.java
        C:\Users\30117\Desktop\Demo\src\cn\yechen\Test.java
        C:\Users\30117\Desktop\Demo\src\cn\yechen\Test01
*/
```



### 20.10 ObjectInputStream / ObjectOutputStream

#### 20.10.1 序列化和反序列化

* 序列化（Serialize）：将 java 对象从内存中存储到文件中，将 java 对象的状态保存下来的过程。
* 反序列化（DeSerialize）：将硬盘上的数据重新恢复到内存中，恢复成 java 对象。

![003-对象的序列化和反序列化](https://img-blog.csdnimg.cn/20210224160626327.png)

**==参与序列化的类型必须实现 `java.io.Serilizable` 接口（只是一个标志，不用重写方法==**）

起到标识的作用，标志的作用，java虚拟机看到这个类实现了这个接口，可能会对这个类进行特殊待遇。Serializable这个标志接口是给java虚拟机参考的，**java虚**

**拟机看到这个接口之后，会为该类自动生成一个序列化版本号。**



**序列化版本号有什么用呢：**

java虚拟机识别一个类的时候先通过类名，**如果类名一致，再通过序列化版本号**。不同的人编写了同一个类，但“这两个类确实不是同一个类”。这个时候序列化版本就起上区分的作用了。

但是对于一个类来说，使用自动序列化版本号之后如果要再次改动代码，重新编译后就会生成不同的序列化版本号，虚拟机就会认为是一个全新的类，就会出现问题。

**所以，凡是一个类实现了Serializable接口，建议给该类==提供一个固定不变的序列化版本号==。这样，以后这个类即使代码修改了，但是版本号不变，java虚拟机会认为是同一个类。**

**IDEA自动生成固定不变的序列化版本号：**

![image-20210224170751366](https://img-blog.csdnimg.cn/2021022417081334.png)

![image-20210224171032375](https://img-blog.csdnimg.cn/20210224171046816.png)



`transient` **修饰符修饰的属性不参与序列化，该类对象序列化后取出来属性赋类型默认值。**



#### 20.10.2 使用

**序列化 / 反序列化单个对象**

```java
// 先不管异常，直接抛出
// 使用自动序列化版本号

// 序列化
ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("student"));
objectOutputStream.writeObject(new Student("zhangsan", 20));
objectOutputStream.flush();
objectOutputStream.close();

// 反序列化
ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("student"));
Object o = objectInputStream.readObject();
System.out.println(o);// 输出：Student{name='zhangsan', age=20}
objectInputStream.close();
```

**序列化 / 反序列化多个对象（将对象放在集合中）**

```java
// 先不管异常，直接抛出
// 使用自动序列化版本号

// 序列化
ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("student"));
List<Student> list = new ArrayList<>();
list.add(new Student("zhangsan", 20));
list.add(new Student("lisi", 21));
list.add(new Student("wangwu", 22));
objectOutputStream.writeObject(list);
objectOutputStream.flush();
objectOutputStream.close();

// 反序列化
ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("student"));
Object o = objectInputStream.readObject();
if (o instanceof List) {
    List<Student> list = (List<Student>) o;
    for (Student student : list) {
        System.out.println(student);
    }
}
objectInputStream.close();

/*
	输出：
		Student{name='zhangsan', age=20}
        Student{name='lisi', age=21}
        Student{name='wangwu', age=22}
*/
```



#### 20.10.3 对序列化版本号的理解

当一个类实现了 Serializable 接口后，java 虚拟机会自动给这个类加上一个序列化版本号。

当该类对象进行序列化之后，之后如果要修改该类中的代码，然后直接对之前的文件进行反序列化，会出现异常

```java
Exception in thread "main" java.io.InvalidClassException: （无效的类异常）
cn.yechen.test.Student; 
local class incompatible: stream classdesc serialVersionUID = -8149392996694432981, 
local class serialVersionUID = 2278957827885088367
```

**这是由于类修改了之后，该类在重新编译之后，序列化版本号与文件中保存的版本号不同了，因此出现异常，不能反序列化。**

因此推荐自己给该类提供一个固定不变的序列化版本号，之后类发生改变，版本号还是一样的。

**反序列化得到的信息是与==当前类==中的特征是一样的，不是之前存了多少现在就拿出来多少，例如：如果属性多了，就会给多是属性赋上默认值，如果属性少了，就不会在出现了。**

```java
// 改动前
public class Student implements Serializable {

    private static final long serialVersionUID = -68497944707546340L;
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}

// 序列化 / 反序列化之后输出：
Student{name='zhangsan', age=20}

// 修改后，并且不在序列化
public class Student implements Serializable {

    private static final long serialVersionUID = -68497944707546340L;
    String name;
    int age;
    String address;

    public Student(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", address='" + address + '\'' +
                '}';
    }
}

// 反序列化之后，输出
Student{name='zhangsan', age=20, address='null'}
```



### 20.11 **文件复制**

#### 20.11.1 单个文件的复制粘贴

**使用 FileInputStream 和 FileOutputStream 一边读一边写**（先要将文件读到内存中，再从内从中将文件写到指定路径下）

如果程序没问题，但是复制不成功，出现异常

`java.io.FileNotFoundException: C:\Java基础知识篇.pdf (拒绝访问。)`

可以将 IDEA 或命令行工具使用**管理员身份**打开。

```java
// 将文件 D:\Java基础知识篇.pdf 拷贝到 C盘下
// 创建输入流
FileInputStream fileInputStream = null;
// 创建输出流
FileOutputStream fileOutputStream = null;

try {
    fileInputStream = new FileInputStream("D:\\Java基础知识篇.pdf");
    fileOutputStream = new FileOutputStream("C:\\Java基础知识篇.pdf" );

    // 记录开始时间
    long begin = System.currentTimeMillis();

    // 核心部分：一边读，一边写
    byte[] bytes = new byte[1024 * 1024];// 一次读 1 MB
    int readCount = 0;
    // 一边读
    while ((readCount = fileInputStream.read(bytes)) != -1) {
        // 一边写
        fileOutputStream.write(bytes, 0, readCount);
    }

    // 输出流刷新
    fileOutputStream.flush();

    // 记录结束时间
    long end = System.currentTimeMillis();
    System.out.println("复制总共花费：" + (end - begin) + " 毫秒");
} catch (IOException e) {
    e.printStackTrace();
} finally {
    // 两个异常要分开解决，如果一起 try 的话，一个流出现异常，另一个流就关闭不了了
    if (fileInputStream != null) {
        try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    if (fileOutputStream != null) {
        try {
            fileOutputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 20.11.2 目录 + 文件的复制粘贴

```java
import java.io.*;

// 拷贝目录 + 文件
public class Test {
    public static void main(String[] args) {
        // 复制源
        File srcFile = new File("D:\\temp");
        // 复制目标
        File destFile = new File("D:\\temp02");
        // 复制方法
        copy(srcFile, destFile);
    }

    /**
     * 复制目录方法
     * @param srcFile 复制源
     * @param destFile 复制目标
     */
    public static void copy(File srcFile, File destFile) {
        // 如果源文件是一个文件（不是目录），就进行文件的复制粘贴
        if (srcFile.isFile()) {
            // 拼接目标路径（目标路径 + "\\" + 当前文件路径减掉前面 3 个字符（即盘符 D:\））
            String newFilePath = destFile.getAbsolutePath() + "\\" + srcFile.getAbsolutePath().substring(3);
            // 将目标路径封装成 file 对象，传入文件拷贝方法
            File file = new File(newFilePath);
            copyFile(srcFile, file);
            // 直接退出当前方法
            return;
        }

        // 程序走到了代表当前文件是一个目录
        // 获取子目录
        File[] files = srcFile.listFiles();
        for (File file : files) {
            // 如果字目录是一个目录
            if (file.isDirectory()) {
                // 拼接目标路径（目标路径 + "\\" + 当前文件路径减掉前面 3 个字符（即盘符 D:\））
                String newFilePath = destFile.getAbsolutePath() + "\\" + file.getAbsolutePath().substring(3);
                // 将目标路径封装成 file 对象
                File file1 = new File(newFilePath);
                // 以目录形式创建
                if (!file1.exists()) {
                    file1.mkdirs();// 这里一定啊要注意，是创建多层目录！！！！！！
                }
            }
            // 进行递归，将当前目录和目标目录传进去
            copy(file, destFile);
        }
     }
     
    /**
     * 文件拷贝方法
     * @param srcFile 复制源
     * @param destFile 复制目标
     */
    public static void copyFile(File srcFile, File destFile) {
        FileInputStream fileInputStream = null;
        FileOutputStream fileOutputStream = null;
        try {
            fileInputStream = new FileInputStream(srcFile);
            fileOutputStream = new FileOutputStream(destFile);
            // 一边写一边读
            byte[] bytes = new byte[1024 * 1024];// 一次读 1 MB
            int readCount = 0;
            while ((readCount = fileInputStream.read(bytes)) != -1) {
                fileOutputStream.write(bytes, 0, readCount);
            }
            // 刷新输出流
            fileOutputStream.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fileInputStream != null) {
                try {
                    fileInputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fileOutputStream != null) {
                try {
                    fileOutputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



### 20.12 IO+Properties的联合应用

IO流：文件的读和写。

Properties:是一个Map集合，key和value都是String类型。

**以后经常改变的数据，可以单独写到一个文件中，使用程序动态读取**。 将来只需要修改这个文件的内容，java代码不需要改动，不需要重新编译，服务器也不需要重启。就可以拿到动态的信息。**类似于以上机制的这种文件被称为==配置文件==。**

当配置文件中的内容格式是：

key1=value1

key2=value2

...

时，我们把这种配置文件叫做**==属性配置文件==**。

java规范中有要求：**属性配置文件建议以 `.properties` 结尾**，但这不是必须的。

`Properties`  类就是专门存放属性配置文件内容的一个类。

```java
FileInputStream fileInputStream = null;
try {
    // 新建一个输入流对象
    fileInputStream = new FileInputStream("src\\userinfo.properties");
    // 新建一个 Map 集合
    Properties properties = new Properties();
    // 调用 Properties 对象的 load 方法将文件中的数据加载到 Map 集合中。
    // 文件中的数据顺着管道加载到Map集合中，其中等号左边做 key，右边做 value
    properties.load(fileInputStream);

    // 通过 key 获取 value
    System.out.println(properties.getProperty("username"));
    System.out.println(properties.getProperty("password"));
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fileInputStream != null) {
        try {
            fileInputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```







## 21、多线程

### 21.1 多线程概述

**什么是进程？什么是线程？**

* 进程是一个**应用程序**（1个进程是一个软件）
* 线程是一个进程中的**执行场景/执行单元**。
* 一个进程可以启动多个线程。

* 对于java程序来说，当在DOS命令窗口中输入：java HelloWorld 回车之后，会先启动JVM，**而JVM就是一个进程**。JVM再启动一个主线程调用main方法。

  同时再启动一个垃圾回收线程负责看护，回收垃圾。最起码，**现在的java程序中至少有两个线程并发，一个是垃圾回收线程，一个是执行main方法的主线程。**

**==进程A和进程B的内存独立不共享==。**

**==线程A和线程B，堆内存和方法区内存共享。但是栈内存独立，一个线程一个栈==。**

* 假设启动10个线程，会有10个栈空间，每个栈和每个栈之间，互不干扰，各自执行各自的，这就是多线程并发。
* java中之所以有多线程机制，目的就是为了**提高程序的处理效率。**



### 21.2 线程的创建和启动

**有两种方法创建线程对象**

#### 21.2.1 编写一个类，直接继承java.lang.Thread，重写run方法

```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("分支线程--->" + i);
        }
    }
}
```

**==注意：==**  run 方法中的方法不能 throws，只能 try ... catch

**因为 run() 方法在父类中没有抛出任何异常，子类不能比父类抛出更多的异常。**



**使用时**

怎么创建线程对象？ new就行了。

怎么启动线程呢？ 调用线程对象的start()方法。

* start()方法的作用是：**启动一个分支线程，在JVM中开辟一个新的栈空间，这段代码任务完成之后，瞬间就结束了。**
* 这段代码的任务只是为了开启一个新的栈空间，只要新的栈空间开出来，start()方法就结束了。**线程就启动成功了。**
* **启动成功的线程会自动调用run方法**，并且run方法在分支栈的栈底部（压栈）。（**类似于一个程序的main函数，是一个入口**）

```java
public class Test {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        // 启动线程
        myThread.start();
        // 这是在主线程中运行的
        for (int i = 0; i < 1000; i++) {
            System.out.println("主线程--->" + i);
        }
    }
}
```

**直接使用 `myThread.run()` 和 使用 `myThread.start()` 的区别：**

使用 `myThread.run()` 后不会开辟一个新的栈空间，即 run 方法中的内容还是运行在主线程中的

![002-线程的run](https://img-blog.csdnimg.cn/20210224210144175.png)

使用 `myThread.start()` 后会开辟一个新的栈空间，开启一个线程，之后这个线程会自动调用 run 方法，主线程和分支线程并发执行。、

![003-线程的start](https://img-blog.csdnimg.cn/20210224210637630.png)

#### 21.2.2 编写一个类，实现java.lang.Runnable接口，实现run方法

```java
// 这并不是一个线程类，是一个可运行的类。它还不是一个线程。
class MyThread implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("分支线程--->" + i);
        }
    }
}
```

**使用**

```java
public class Test {
    public static void main(String[] args) {
        // 创建一个可运行的对象
        MyThread myThread = new MyThread();
        // 将可运行的对象封装成线程对象
        Thread thread01 = new Thread(myThread);

        // 使用匿名内部类的方式创建线程对象
        Thread thread02 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 10; i++) {
                    System.out.println("分支线程02--->" + i);
                }
            }
        });
        //启动线程
        thread01.start();
        thread02.start();

        // 这是在主线程中运行的
        for (int i = 0; i < 10; i++) {
            System.out.println("主线程--->" + i);
        }
    }
}

```

**第二种方式实现接口比较常用，因为一个类实现了接口，它还可以去继承其它的类，更灵活。**



### 21.3 线程的生命周期

![image-20210224225338862](https://img-blog.csdnimg.cn/20210224225353959.png)

* **新建状态**：刚 new 出来的线程对象，可以通过调用 start 方法进入就绪状态。

* **就绪状态**：调用 start 方法之后，此时的线程状态又可称为**可运行状态**，当前状态下该线程具有**抢夺 CPU 时间片的权利**，如果抢到了 CPU 时间片，就会进入运行状态。

* **运行状态**：抢占到 CPU 时间片的线程会进入运行状态，**此时会开始执行 run 方法**，当抢夺到的 CPU 时间片用完之后，通过 JVM 的调度，该线程会再次进入就绪状态抢夺 CPU 时间片，如果抢到了，就会再进入运行状态，**接着上一次的代码继续执行 run 方法**，**线程会在就绪状态和运行状态之间来回循环**，直到 run 方法执行完毕，进入死亡状态。

* **阻塞状态**：**当一个线程在运行状态下遇到了阻塞事件**，例如接受用户的键盘输入，或者 sleep 方法等，都会使该线程进入阻塞状态，**进入阻塞状态的线程会放弃之前占有的 CPU 时间片**。当阻塞解除之后，该线程会**回到就绪状态继续抢夺 CPU 时间片**。

* **死亡状态**：**线程 run 方法执行结束**标志着这个线程进入死亡状态。



### 21.4 获取线程的名称

获取线程对象的名字：`String name = 线程对象.getName();`

修改线程对象的名字：`线程对象.setName();`

怎么获取当前线程对象：`Thread thread = Thread.currentThread();`

当线程没有设置名字的时候，默认的名字有什么规律：

```
Thread-0
Thread-1
Thread-2
Thread-3
.....
```

```java
public static void main(String[] args) {
    Thread thread01 = new Thread(new Runnable() {
        @Override
        public void run() {
            for (int i = 0; i < 10; i++) {
                doSome(i);
            }
        }
    });
    // 更改线程名称
    thread01.setName("线程1");

    Thread thread02 = new Thread(new Runnable() {
        @Override
        public void run() {
            for (int i = 0; i < 10; i++) {
                doSome(i);
            }
        }
    });
    // 更改线程名称
    thread02.setName("线程2");

    // 启动线程
    thread01.start();
    thread02.start();

    // 主线程调用方法
    for (int i = 0; i < 10; i++) {
        doSome(i);
    }
}

public static void doSome(int i) {
    Thread thread = Thread.currentThread();
    // 打印当前调用该方法的线程名称
    System.out.println("【" + thread.getName() + "】正在调用 doSome 方法，输出：" + i);
}
```



### 21.5 线程的调度与控制

#### 21.5.1 Thread.sleep()

**关于线程的sleep方法：**`static void sleep(long millis)`

* 静态方法，通过类名 Thread 来调用。
* 参数是  ==毫秒==：使当前线程休眠 1 秒：`Thread.sleep(1000);`
* 作用：**让==当前线程==进入休眠，进入“阻塞状态”，放弃占有CPU时间片，让给其它线程使用。**
* Thread.sleep()方法，可以做到这种效果：**间隔特定的时间，去执行一段特定的代码，每隔多久执行一次。**

```java
public static void main(String[] args) {
    // 每间隔 1 秒输出
    for (int i = 0; i < 10; i++) {
        System.out.println(Thread.currentThread().getName() + "--->" + i);
        // 休眠 1 秒
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

**面试题**：

```java
public class Test {
    public static void main(String[] args) {
        // 创建线程对象
        Thread t = new MyThread3();
        t.setName("t");
        t.start();

        // 调用sleep方法
        try {
            // 问题：这行代码会让线程t进入休眠状态吗？
            t.sleep(1000 * 5); // 在执行的时候还是会转换成：Thread.sleep(1000 * 5);
                                     // 这行代码的作用是：让当前线程进入休眠，也就是说main线程进入休眠。
                                     // 这样代码出现在main方法中，main线程睡眠。
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 5秒之后这里才会执行。
        System.out.println("hello World!");
    }
}


class MyThread3 extends Thread {
    public void run(){
        for(int i = 0; i < 10000; i++){
            System.out.println(Thread.currentThread().getName() + "--->" + i);
        }
    }
}
```



#### 21.5.2 终止线程的睡眠

`void interrupt()` : 中断线程睡眠

```java
public class Test {
    public static void main(String[] args) {
        // 创建线程对象
        Thread t = new MyThread3();
        t.setName("t");
        t.start();

        // 使主线程睡眠 5 秒，模拟一段时间
        try {
            MyThread3.sleep(1000 * 5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 5秒之后这里才会执行。
        // 终断t线程的睡眠（这种终断睡眠的方式依靠了java的异常处理机制。）
        t.interrupt();
    }
}

class MyThread3 extends Thread {
    public void run(){
        System.out.println(Thread.currentThread().getName() + "---> begin");
        try {
            // 睡眠1年
            Thread.sleep(1000 * 60 * 60 * 24 * 365);
        } catch (InterruptedException e) {
            // 打印异常信息
            e.printStackTrace();
        }
        //没有干预的话要 1 年之后才会执行这里
        System.out.println(Thread.currentThread().getName() + "---> end");
    }
}

// 输出：
t---> begin
java.lang.InterruptedException: sleep interrupted
	at java.lang.Thread.sleep(Native Method)
	at cn.yechen.MyThread3.run(Test.java:30)
t---> end（这是 5 秒后输出的）
```



#### 21.5.3 终止一个线程的执行

**第一种方法**：使用 `stop` 方法（这种方式存在很大的缺点：**容易丢失数据**。因为这种方式是直接将线程杀死了，线程没有保存的数据将会丢失。不建议使用。）

**第二种方法**：**在线程类中打一个布尔标记**，使用这个布尔标记来决定线程的运行和终止。

```java
public class Test {
    public static void main(String[] args) {
        MyThread3 myThread3 = new MyThread3();
        myThread3.setName("t");
        myThread3.start();

        // 模拟 5 秒
        try {
            Thread.sleep(1000 * 5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 终止 t 线程
        myThread3.run = false;
    }
}

class MyThread3 extends Thread {
    boolean run = true;
    public void run(){
        for (int i = 0; i < 10; i++) {
            if (run) {
                System.out.println(Thread.currentThread().getName() + "--->" + i);
                // 睡 1 秒
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            } else {
                // 可以在线程结束前在这里执行数据保存
                return;
            }
        }
    }
}
```



#### 21.5.4 线程的调度

##### 常见的线程调度模型有哪些：

1. 抢占式调度模型：那个线程的**优先级比较高**，抢到的**CPU时间片的概率就高一些/多一些**。java采用的就是抢占式调度模型。

2. 均分式调度模型：**平均分配CPU时间片**。每个线程占有的CPU时间片时间长度一样。平均分配，一切平等。有一些编程语言，线程调度模型采用的是这种方式。

##### java中提供了哪些方法是和线程调度有关系的呢：

1. 关于线程的优先级：

   * `void setPriority(int newPriority)`   设置线程的优先级

   * `int getPriority()`   获取线程优先级

   * 优先级比较高的获取CPU时间片可能会多一些。（但也不完全是，大概率是多的。）

```java
System.out.println("最高优先级：" + Thread.MAX_PRIORITY);// 最高优先级：10
System.out.println("默认优先级：" + Thread.NORM_PRIORITY);// 最高优先级：5
System.out.println("最小优先级：" + Thread.MIN_PRIORITY);// 最高优先级：1
```

2.  让位方法
   * `static void yield()`  让位方法
   * **暂停当前正在执行的线程对象，回到就绪状态，让给其它线程。**
   * yield()方法不是阻塞方法。让当前线程让位，让给其它线程使用。
   * yield()方法的执行会**让当前线程从“运行状态”回到“就绪状态”**。（注意：在回到就绪之后，有可能还会再次抢到。）

```java
 public static void main(String[] args) {
     Thread thread = new Thread(new Runnable() {
         @Override
         public void run() {
             for (int i = 1; i <= 1000; i++) {
                 // 当 i 是 10 的倍数的时候，t 线程让位给其他线程
                 if (i % 10 == 0) {
                     Thread.yield();
                 }
                 System.out.println(Thread.currentThread().getName() + "--->" + i);
             }
         }
     });
     thread.setName("t");
     thread.start();

     for (int i = 1; i <= 1000; i++) {
         // 当 i 是 100 的倍数的时候，main 线程让位给其他线程
         if (i % 100 == 0) {
             Thread.yield();
         }
         System.out.println(Thread.currentThread().getName() + "--->" + i);
     }
 }
```

3. 合并线程
   * `void join()`   合并线程

```java
public static void main(String[] args) {
    // main begin 最先输出
    System.out.println("main begin");
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            for (int i = 1; i <= 1000; i++) {
                System.out.println(Thread.currentThread().getName() + "--->" + i);
            }
        }
    });
    thread.setName("t");
    thread.start();

    try {
        // t 线程合并到 当前（main）线程中，当前线程受阻塞，直到 t 线程执行完成，当前线程才会继续执行
        // 相当于 t 线程插了一个队，走到了当前线程前面，还死活不让当前线程执行，要自己执行完后才让当前线程继续执行
        thread.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }

    // main over 最后输出
    System.out.println("main over");
}
```



### 21.6 线程安全

以后在开发中，我们的项目都是运行在服务器当中，而服务器已经将线程的定义，线程对象的创建，线程的启动等，都已经实现完了。这些代码我们都不需要

编写。

**最重要的是：你要知道，你编写的程序需要放到一个多线程的环境下运行，你更需要关注的是这些数据在多线程并发的环境下是否是安全的。**

**什么时候数据在多线程并发的环境下会存在安全问题呢？**

* 条件1：多线程并发
* 条件2：有共享数据
* 条件3：共享数据有修改的行为

**怎么解决线程安全问题呢？**

* 用排队执行解决线程安全问题。

* 这种机制被称为：**==线程同步机制==**。

* 专业术语叫做：线程同步，**实际上就是线程不能并发了，线程必须排队执行。线程排队了，==就会牺牲一部分的效率==，但是没有办法，数据安全最重要。**

  * **异步编程模型**：线程 t1 和线程 t2，各自执行各自的，t1 不管 t2，t2 不管 t1，谁也不需要等谁，这种编程模型叫做：异步编程模型。其实就是：**多线程并发（效率较高。）**

  * **同步编程模型**：线程t1和线程t2，在线程t1执行的时候，必须等待t2线程执行结束，或者说在t2线程执行的时候，必须等待t1线程执行结束，两个线程之间发生了等待关系，这就是同步编程模型。**效率较低。线程排队执行。**



#### 21.6.1 使用银行账户取钱的例子模拟多线程并发下的数据安全问题：

1. 定义一个银行账户类 Account，有账户名和余额属性，还有一个取钱的方法

```java
class Account {
    private String accountName;
    private double balance;

    public Account() {
    }

    public Account(String accountName, double balance) {
        this.accountName = accountName;
        this.balance = balance;
    }

    public String getAccountName() {
        return accountName;
    }

    public void setAccountName(String accountName) {
        this.accountName = accountName;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    // 取钱方法
    public void withdraw(double money) {
        // 取之前的余额
        double before = getBalance();
        // 取之后的余额
        double after = before - money;
        // 模拟网路延迟
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 更新余额
        setBalance(after);
    }
}
```

2. 定义一个线程类，是一个 Account 类型的属性，使用构造方法是两个线程访问同一个账户对象

```java
class MyThread extends Thread {
    Account account;

    public MyThread(Account account) {
        this.account = account;
    }

    @Override
    public void run() {
        // 执行取款方法
        double money = 5000;
        account.withdraw(money);
        System.out.println(Thread.currentThread().getName() + "对账户[" + account.getAccountName() + "]取款成功，余额为：" + account.getBalance());
    }
}
```

3. 编写测试类模拟两个人同时对一个账户取钱

```java
public class Test {
    public static void main(String[] args) {
        Account account = new Account("act-001", 10000);
        MyThread myThread01 = new MyThread(account);
        MyThread myThread02 = new MyThread(account);
        myThread01.setName("t1");
        myThread02.setName("t2");
        myThread01.start();
        myThread02.start();
    }
}

/*
输出：
	t2对账户[act-001]取款成功，余额为：5000.0
	t1对账户[act-001]取款成功，余额为：5000.0
*/
```

**这样线程并发就造成了数据的不安全。**



#### 21.6.2 synchronized 关键字

Java中有三大变量？【重要的内容。】

* **实例变量：在堆中。**

* **静态变量：在方法区。**

* **局部变量：在栈中。**

以上三大变量中：

* **局部变量永远都不会存在线程安全问题。**因为局部变量不共享。（一个线程一个栈。）局部变量在栈中。所以局部变量永远都不会共享。

* 实例变量在堆中，堆只有1个。静态变量在方法区中，方法区只有1个。**堆和方法区都是多线程共享的，所以可能存在线程安全问题。**

 结论：

* 局部变量+常量：不会有线程安全问题。 

* 成员变量：可能会有线程安全问题。

 

**有三种写法：**

**==同步代码块==**

```java
synchronized(线程共享对象) {
    同步代码块
}
```

synchronized 后面小括号中传的这个“数据”是相当关键的。**这个数据必须是多线程共享的数据**。才能达到多线程排队。

在java语言中，**==任何一个对象都有“一把锁==**，其实这把锁就是标记。（只是把它叫做锁。） 100个对象，100把锁。1个对象1把锁。

当 t1 线程执行过程中遇到了 sychronized 关键字，就会自动找括号内这个对象的 “ 对象锁 ” ，找到之后，就会占有这把锁，然后执行同步代码块中的语句，执行过程中如果另一个线程 t2 也要也遇到了 sychronized 关键字，也会找对象的 “ 对象锁 ” ，但是此时 “ 对象锁 “ 还被 t1 占有，t2 只能在同步代码块之外等待 t1 执行完成归还 “ 对象锁 ”，t1 执行完同步代码块后归还 “ 对象锁 ”，然后 t2 占有这把锁之后，进入同步代码块执行程序。

**修改银行账户取钱例子中的取钱方法：**此时线程在执行是会排队，保障数据安全。

```java
public void withdraw(double money) {
	// 当前对象是线程的共享对象，所以括号内添 this
    synchronized (this) {
        // 取之前的余额
        double before = getBalance();
        // 取之后的余额
        double after = before - money;
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 更新余额
        setBalance(after);
    }
}
```



**==在实例方法上使用 synchronized==**

**表示共享对象一定是this并且同步代码块是整个方法体。对象锁，一个对象一把。**

修饰了整个实例方法，表示整个方法体都需要同步，**可能会无故扩大同步的范围，导致程序的执行效率降低**。所以这种方式不常用。

如果共享的对象就是this，并且需要同步的代码块是整个方法体，建议使用这种方式。



**==在静态方法上使用 synchronized==**

表示找**类锁**。**一个类的类锁永远只有1把**。就算创建了100个对象，那类锁也只有一把。



[面试题01](.\sychronized面试题\面试题01)

[面试题02](.\sychronized面试题\面试题02)

[面试题03](.\sychronized面试题\面试题03)

[面试题04](.\sychronized面试题\面试题04)



#### 21.6.3 死锁

![image-20210225204323069](https://img-blog.csdnimg.cn/20210225204416480.png)

```java
// 程序不会执行完成，也不会出现异常，也不会出现错误
public class Test {
    public static void main(String[] args) {
        Object o1 = new Object();
        Object o2 = new Object();
        MyThread01 myThread01 = new MyThread01(o1, o2);
        MyThread02 myThread02 = new MyThread02(o1, o2);
        myThread01.start();
        myThread02.start();
    }
}

class MyThread01 extends Thread {
    Object o1;
    Object o2;

    public MyThread01(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o1) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o2){

            }
        }
    }
}

class MyThread02 extends Thread {
    Object o1;
    Object o2;

    public MyThread02(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o2) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o1){

            }
        }
    }
}
```



#### 21.6.4 开发过程中如何解决线程安全问题

**第一种方案**：尽量使用**局部变量**代替“实例变量和静态变量”。

**第二种方案**：如果必须是实例变量，那么可以考虑**创建多个对象**，这样实例变量的内存就不共享了。（一个线程对应1个对象，100个线程对应100个对象，

对象不共享，就没有数据安全问题了。）

**第三种方案**：如果不能使用局部变量，对象也不能创建多个，这个时候就只能**选择synchronized了。线程同步机制。**



### 21.7 守护线程

**java语言中线程分为两大类：**

* 一类是：**用户线程**
  * 主线程main方法是一个用户线程。
* 一类是：**守护线程**（后台线程）
  * 其中具有代表性的就是：垃圾回收线程（守护线程）。

**守护线程的特点**：

* 一般守护线程是一个**死循环**，但当所有的用户线程结束，守护线程就会自动结束。

**守护线程用在什么地方呢？**

例如：

> 每天00:00的时候系统数据自动备份。
>
> 这个需要使用到定时器，并且我们可以将定时器设置为守护线程。
>
> 一直在那里看着，每到00:00的时候就备份一次。
>
> 所有的用户线程如果结束了，守护线程自动退出，没有必要进行数据备份了。

```java
public class Test {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.setName("t");
        // 将 t 线程设置为守护线程
        myThread.setDaemon(true);
        myThread.start();

        // 主线程是一个用户线程
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + "--->" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class MyThread extends Thread {

    @Override
    public void run() {
        int i = 0;
        // 由于该线程是一个守护线程，即使是死循环，当时当用户线程结束的时候，守护线程也要结束
        while (true) {
            System.out.println(Thread.currentThread().getName() + "--->" + (i++));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```



### 20.8 定时器

定时器的作用：

* **间隔特定的时间，执行特定的程序。**

那么在java中其实可以采用多种方式实现：

* **可以使用sleep方法**，睡眠，设置睡眠时间，没到这个时间点醒来，执行任务。这种方式是最原始的定时器。（比较low）

* 在java的类库中已经写好了一个**定时器**：`java.util.Timer`，可以直接拿来用。不过，这种方式在目前的开发中也很少用，因为现在有很多高级框架都是支持

  定时任务的。

* 在实际的开发中，目前使用较多的是**Spring框架中提供的SpringTask框架**，这个框架只要进行简单的配置，就可以完成定时器的任务。（但是底层还是 Timer）

```java
public class Test {
    public static void main(String[] args) {
        Timer timer = new Timer();
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        Date date = null;
        try {
            date = simpleDateFormat.parse("2021-02-25 21:30:00 000");
        } catch (ParseException e) {
            e.printStackTrace();
        }
        // timer.schedule(定时任务, 第一次执行时间, 间隔多久执行一次);
        // 从 2021-02-25 21:30:00 000 这个时间开始，每 5 秒执行一次 MyTimer 中的定时任务
        timer.schedule(new MyTimer(), date, 1000 * 5);
    }
}

class MyTimer extends TimerTask {
    @Override
    public void run() {
        // 编写你需要执行的任务就行了。
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        String time = simpleDateFormat.format(new Date());
        System.out.println(time + "执行了一次数据备份！");
    }
}
```



### 20.9 创建线程的第三种方法（JDK8 新特性）

实现线程的第三种方式：**实现Callable接口**。（JDK8新特性。）

这种方式实现的线程**可以获取线程的返回值**。

* 这种方式的优点：可以获取到线程的执行结果。
* 这种方式的缺点：**效率比较低，在获取t线程执行结果的时候，当前线程受阻塞，效率较低**。

```java
public class Test {
    public static void main(String[] args) {
        // 匿名内部类方式
        FutureTask futureTask = new FutureTask(new Callable() {
            @Override
            public Object call() throws Exception {
                // 线程执行一个任务，执行之后可能会有一个执行结果
                // 模拟执行
                System.out.println("call method begin");
                Thread.sleep(1000 * 10);
                System.out.println("call method end!");
                int a = 100;
                int b = 200;
                return a + b; //自动装箱(300结果变成Integer)
            }
        });
        // 创建线程对象
        Thread thread = new Thread(futureTask);
        // 启动线程
        thread.start();

        try {
            // 这里是main方法，这是在主线程中。
            // 在主线程中，怎么获取t线程的返回结果？
            // get()方法的执行会导致 “当前线程阻塞”
            Object o = futureTask.get();
            System.out.println("线程执行结果：" + o);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```



### 20.10 关于Object类中的wait和notify方法。（生产者和消费者模式）

wait 和 notify 方法不是线程对象的方法，是java中任何一个java对象都有的方法，因为这两个方式是Object类中自带的。

wait方法和notify方法不是通过线程对象调用，是通过对象调用的。

**wait()方法作用：**

```java
Object o = new Object();
o.wait();
```

表示：

* **让正在 o 对象上活动的线程进入等待状态**，无期限等待，直到被唤醒为止。

* o.wait();方法的调用，会让 “当前线程（正在o对象上活动的线程）” 进入等待状态。

 **notify()方法作用：**

```java
Object o = new Object();
o.notify();
```

表示：

* 唤醒正在o对象上等待的线程。
* 还有一个notifyAll()方法：这个方法是唤醒o对象上处于等待的所有线程。

 **生产者和消费者模式：**

![007-生产者和消费者模式](https://img-blog.csdnimg.cn/20210225223605145.png)

程序实现：

```java
public class Test {
    public static void main(String[] args) {
        // 创建1个仓库对象，共享的。
        List list = new ArrayList();
        // 创建两个线程对象
        // 生产者线程
        Thread t1 = new Thread(new Producer(list));
        // 消费者线程
        Thread t2 = new Thread(new Consumer(list));

        t1.setName("生产者线程");
        t2.setName("消费者线程");

        t1.start();
        t2.start();
    }
}

// 生产线程
class Producer implements Runnable {
    // 仓库
    private List list;

    public Producer(List list) {
        this.list = list;
    }
    @Override
    public void run() {
        // 一直生产（使用死循环来模拟一直生产）
        while(true){
            // 给仓库对象list加锁。
            synchronized (list){
                if(list.size() > 0){ // 大于0，说明仓库中已经有1个元素了。
                    try {
                        // 当前线程进入等待状态，并且释放Producer之前占有的list集合的锁。
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                // 程序能够执行到这里说明仓库是空的，可以生产
                Object obj = new Object();
                list.add(obj);
                System.out.println(Thread.currentThread().getName() + "--->" + obj);
                // 唤醒消费者进行消费
                list.notifyAll();
            }
        }
    }
}

// 消费线程
class Consumer implements Runnable {
    // 仓库
    private List list;

    public Consumer(List list) {
        this.list = list;
    }

    @Override
    public void run() {
        // 一直消费
        while(true){
            synchronized (list) {
                if(list.size() == 0){
                    try {
                        // 仓库已经空了。
                        // 消费者线程等待，释放掉list集合的锁
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                // 程序能够执行到此处说明仓库中有数据，进行消费。
                Object obj = list.remove(0);
                System.out.println(Thread.currentThread().getName() + "--->" + obj);
                // 唤醒生产者生产。
                list.notifyAll();
            }
        }
    }
}
```





## 22 反射（Reflect）

### 22.1 反射的基本概念

**反射机制有什么用：**

* 通过java语言中的反射机制可以**操作字节码文件**。
* 优点类似于黑客。（可以读和修改字节码文件。）
* 通过反射机制可以**操作代码片段**。（class文件。）

**反射机制的相关类在哪个包下：**

* `java.lang.reflect.*`;

**反射机制相关的重要的类有哪些：**

* `java.lang.Class`：代表整个字节码，代表一个类型，代表**整个类**。
* `java.lang.reflect.Method`：代表字节码中的方法字节码。代表**类中的方法**。
* `java.lang.reflect.Constructor`：代表字节码中的构造方法字节码。代表**类中的构造方法**。
* `java.lang.reflect.Field`：代表字节码中的属性字节码。代表类中的**成员变量（静态变量+实例变量）**。

例如：

```java
java.lang.Class：
    public class User{
        
        // Field
        int no;

        // Constructor
        public User(){

        }
        public User(int no){
            this.no = no;
        }

        // Method
        public void setNo(int no){
            this.no = no;
        }
        public int getNo(){
            return no;
        }
    }
```



### 22.2 对 class 的反射

#### 22.2.1 获取 Class 的三种方式

第一种：**Class c = Class.forName("完整类名带包名");**

```java
Class c = null;
try {
    c = Class.forName("java.lang.String");
} catch (ClassNotFoundException e) {
    e.printStackTrace();
}
System.out.println(c);// 输出：class java.lang.String
```

**Class.forName() 方法的执行会进行类加载**，

* 所以当只想要执行类中的静态代码块，不想执行其他代码的时候，使用 Class.forName()  方法即可，这个方法的执行会导致类加载，类加载是静态代码块会执行 ，其他代码不执行即可，不需要获取字节码文件。 

第二种：**Class c = 对象（引用）.getClass();**（java中任何一个对象都有一个方法：getClass()，获取当前对象的类型的 Class 对象）

```java
// s 是一个引用指向 String 类型的对象
String s = "abc";
// c 代表 String.class 字节码文件，c 代表 String 类型。
Class c = s.getClass();
System.out.println(c);// class java.lang.String
```

第三种：**Class c = 任何类型.class;**（任何类型，包括基本数据类型，包括自定义的类，都有一个 class 属性）

```java
Class c1 = Integer.class;
Class c2 = Date.class;
System.out.println(c1);// class java.lang.Integer
System.out.println(c2);// class java.util.Date
```



```java
Class c1 = null;
try {
    c1 = Class.forName("java.lang.String");
} catch (ClassNotFoundException e) {
    e.printStackTrace();
}
Class c2 = "abc".getClass();
System.out.println(c1 == c2);// true
```

**c1 和 c2 两个变量中保存的内存地址是相同的，都执行方法区中的 String.class 字节码文件**

![001-字节码内存图](https://img-blog.csdnimg.cn/20210226133802243.png)

#### 22.2.2 通过反射实例化对象

`T	newInstance()` ： 创建由这个类对象表示的类的新实例。

**注意**：newInstance()方法内部实际上调用了**无参数构造方法**，**必须保证无参构造存在才可以**。

```java
public class Test {
	public static void main(String[] args) throws Exception{
		Class c = Class.forName("User");
        // 通过Class的newInstance()方法来实例化对象。
		c.newInstance();
	}
}

class User {
	public User() {
		System.out.println("无参构造方法被调用！");
	}
}
```



**通过反射来实例化对象的优点**

* java代码写一遍，再不改变java源代码的基础之上，**可以做到不同对象的实例化**。
  非常之灵活。（**符合OCP开闭原则：对扩展开放，对修改关闭。**）

**如：通过读取属性配置文件来实例化对象**（可以通过修改配置文件来实例化不同的对象）

```java
public class Test {
    public static void main(String[] args) throws Exception{
        // 通过IO流读取classinfo.properties文件
        Properties properties = new Properties();
        // 创建字节输入
        FileInputStream fileInputStream = new FileInputStream("src\\cn\\yechen\\student.properties");
        // 加载
        properties.load(fileInputStream);
        // 关闭流
        fileInputStream.close();
        // 通过 key 获取 value
        String className = properties.getProperty ("className");

        // 动态获取 class
        Class c = Class.forName(className);
        // 实例化对象
        Object o = c.newInstance();
        System.out.println(o);// Fri Feb 26 14:23:25 CST 2021

    }
}
```

properties 文件

```
className=java.util.Date
```

#### 22.2.3 Class 类中的方法

* `static Class<?> forName(String className)`：返回指定类名（className）的字节码文件（class文件）
* `String	getName()` ：获取完整类名
* `String	getSimpleName()`：获取简单类名
* `Field[] getFields()` ：以 Field 类型的数组返回当前类中的**所有公共属性（public修饰的）**封装成的 Field 对象
* `Field[] getDeclaredFields()` ：以 Field 类型的数组返回当前类中的**所有属性**封装成的 Field 对象
* `Field getDeclaredField(String name)` ：通过属性名 “name” 来获取属性对象。
* `Method[] getDeclaredMethods()` ：以数组的形式获得所有 方法对象。
* `Method	getDeclaredMethod(String name, Class<?>... parameterTypes)` ：通过方法名 “name” 和 参数列表【0 - N个】获得方法对象。
* `Constructor<?>[] getDeclaredConstructors()`：以数组的形式获得所有 构造方法对象
* `Constructor<T>	getDeclaredConstructor(Class<?>... parameterTypes)`：通过 参数列表【0 - N个】获得构造方法对象。





### 22.3 获取文件的绝对路径（通用的）

之前可以在 IDEA 中使用相对路径来定位文件，但是当程序离开了 IDEA 环境，程序就不能执行了。

同时由于之后的项目会运行在不同的操作系统中，文件路径是不同是，所以直接写上绝对路径也是有局限性的。

**通过以下方式可以针对不同的系统动态获取去文件的绝对路径。**

**但有一个使用条件：文件需要在类路径（src目录是类路径的根路径）下。才能用这种方式。**

例如：`db.properties` 文件的路径为 `src/cn/yechen/db.properties`

```java
String path = Thread.currentThread().getContextClassLoader()
    .getResource("cn/yechen/db.properties").getPath();
System.out.println(path);
// 输出：/C:/Users/30117/Desktop/Demo/out/production/Demo/cn/yechen/db.properties
```

其中：

`Thread.currentThread()` ：返回当前**线程对象**

`getContextClassLoader()`： 是线程对象的方法，可以获取到当前线程的**类加载器对象**。

`getResource()`：【获取资源】这是类加载器对象的方法，当前线程的类加载器默认从类的根路径下**加载资源**。

**作用举例：在 IO 流的使用中使路径更通用**

```java
String path = Thread.currentThread().getContextClassLoader()
    .getResource("cn/yechen/db.properties").getPath();
FileReader fileReader = new FileReader(path);
```

还可以简化：直接以流的形式返回

```java
InputStream inputStream = Thread.currentThread().getContextClassLoader()
    .getResourceAsStream("cn/yechen/db.properties");
```

`Thread.currentThread().getContextClassLoader().getResourceAsStream("cn/yechen/db.properties");` 会返回一个 `InputStream`



### 22.4 资源绑定器（ResourceBundle）

**资源绑定器，只能绑定xxx.properties文件。并且这个文件必须在类路径下。文件扩展名也必须是properties**

并且在写路径的时候，**路径后面的扩展名不能写**。

```java
ResourceBundle resourceBundle = ResourceBundle.getBundle("cn/yechen/student");
String className = resourceBundle.getString("className");
System.out.println(className);// 输出：java.util.Date
```

properties 文件

```
className=java.util.Date
```



### 22.5 JDK中自带的类加载器

**什么是类加载器？**

* 专门负责加载类的命令/工具。（ClassLoader）

**JDK中自带了3个类加载器：**

* ==启动类加载器==（ rt.jar）
* ==扩展类加载器==（ext/*.jar）
* ==应用类加载器==（classpath）

**类加载过程：**

例如代码：String string  = "abc";

代码在开始执行之前，会将所需要类全部加载到 JVM 当中。通过类加载器加载，看到以上代码类加载器会找String.class文件，找到就加载，那么是怎么进行加载的呢？

* **首先通过“启动类加载器”加载**。注意：启动类加载器专门加载：`D:\Environmental\JDK8.0\jre\lib\rt.jar` 下的 class 文件，这都是JDK最核心的类库。

* **如果通过“启动类加载器”加载不到的时候，会通过"扩展类加载器"加载。**注意：扩展类加载器专门加载：`D:\Environmental\JDK8.0\jre\lib\ext\*.jar` 中的 class 文件

* **如果“扩展类加载器”没有加载到，那么会通过“应用类加载器”加载。**注意：应用类加载器专门加载：classpath中的类。

**双亲委派机制：**

java中为了保证类加载的安全，使用了双亲委派机制。

**优先从启动类加载器中加载**，这个称为“父”，“父”无法加载到，

**再从扩展类加载器中加载**，这个称为“母”。

双亲委派。如果都加载不到，**才会考虑从应用类加载器中加载**。直到加载到为止。



### 22.6 通过反射机制访问对象的某个属性（Filed）

**在反射中，一个类的每一个属性都会被封装成一个 Filed**

```java
public class Student {
    // Field翻译为字段，其实就是属性/成员
    // 4个Field，分别采用了不同的访问控制权限修饰符
    private String name; // Field对象
    protected int age; // Field对象
    boolean sex;
    public int no;
    public static final double MATH_PI = 3.1415926;
}
```



### 22.6 反射 Field

**在反射中，一个类的每一个属性都会被封装成一个 Field**

```java
public class Student {
    // Field翻译为字段，其实就是属性/成员
    // 4个Field，分别采用了不同的访问控制权限修饰符
    private String name; // Field对象
    protected int age; // Field对象
    boolean sex;
    public int no;
    public static final double MATH_PI = 3.1415926;
}
```

**Field对象的常用方法：**

* `Object get(Object obj)` ：返回 obj 对象上的 当前属性（Field对象）的**属性值**
* `void set(Object obj, Object value)`：给 obj 对象的当前属性（Field对象）赋值为 value

* `int getModifiers()` ：以整数形式返回当前属性（Field对象）的 Java 语言**修饰符**。这个返回值是不同修饰符组合的代号。
  * 可以通过 `Modifier` 类中的静态方法 `toString` 将 返回值转换成 字符串形式的修饰符。
* `Class<?> getType()` ： 返回**当前属性的类型**，返回值类型是 Class，可以通过 Class 的 getSimpleName 方法获得类名（不带包名）
*  `String getName()` ： 返回当前属性（Field对象）的**属性名**。
* `void setAccessible(boolean flag)` ：将这个反射对象的可访问标志设置为指定的布尔值。（**设置为 true后可以给私有属性赋值和取值**）

```java
// 通过反射机制将 Student 类中的所有属性（包括修饰符列表、类型、属性名、属性值）获取到
public class Test {
    public static void main(String[] args) throws Exception{
        Class c = Class.forName("cn.yechen.Student");
        // 实例化对象，调用 Student 类的无参构造方法
        Object obj = c.newInstance();
        // 通过 StringBuilder 累加字符串
        StringBuilder stringBuilder = new StringBuilder();
        /*// 获取所有public修饰的属性 Field
        Field[] fields = c.getFields();
        System.out.println(fields.length);// 2*/
        // 获取所有属性
        Field[] declaredFields = c.getDeclaredFields();
        for (Field field : declaredFields) {
            // 获取属性的修饰修饰符列表
            stringBuilder.append(Modifier.toString(field.getModifiers()));
            stringBuilder.append(" ");
            // 获取属性的类型名
            stringBuilder.append(field.getType().getSimpleName());
            stringBuilder.append(" ");
            // 获取属性的属性名
            stringBuilder.append(field.getName());
            stringBuilder.append(" = ");
            // 获取属性的属性值，一般情况下 private 修饰的属性是取不到的，会报异常，但是可以通过如下方法，打破封装
            field.setAccessible(true);
            Object o = field.get(obj);
            stringBuilder.append(o);
            // 换行
            stringBuilder.append("\n");
        }
        System.out.println(stringBuilder);
    }
}

class Student {
    private String name; // Field对象
    protected int age; // Field对象
    boolean sex;// Field对象
    public int no;// Field对象
    public static final double MATH_PI = 3.1415926;// Field对象
}
```



### 22.7 可变长度参数

**int... args 这就是可变长度参数**

语法是：类型...  （注意：一定是3个点。）

注意：

* 可变长度参数要求的**参数个数是：0~N个**。
* **可变长度参数在参数列表中必须在最后一个位置上**，而且可变长度参数**只能有1个**。
* 可变长度参数可以当做**一个数组来看待**。

```java
public class Test {
    public static void main(String[] args) {
        m1(1,2,3,4,5);
        m1(new int[]{1,2,3,4,5});
        m1();
    }

    public static void m1(int... args) {
        for (int i : args) {
            System.out.println(i);
        }
    }
}
```



### 22.8 反射 Method

**Method 对象的常用方法：**

* `int getModifiers()` ：以整数形式返回当前方法（Method 对象）的 Java 语言**修饰符**。这个返回值是不同修饰符组合的代号。
  * 可以通过 `Modifier` 类中的静态方法 `toString` 将 返回值转换成 字符串形式的修饰符。

* `Class<?> getReturnType()` ： 获取方法的返回值类型。
* `String	getName()` ：获取方法名。
* `Class<?>[]	getParameterTypes()` ：获取方法的参数列表的类型。
* `Object	invoke(Object obj, Object... args)`：调用对象的方法，obj 为对象，args 为实际参数。

```java
// 获取方法的修饰符列表，返回值类型，方法名，形式参数列表
public class Test {
    public static void main(String[] args) {
        Class c = null;
        try {
            c = Class.forName("java.lang.String");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        StringBuilder stringBuilder = new StringBuilder();
        // 获得所有方法对象
        Method[] declaredMethods = c.getDeclaredMethods();
        // 编历方法
        for (Method method : declaredMethods) {
            // 获取方法的修饰符列表
            stringBuilder.append(Modifier.toString(method.getModifiers()));
            stringBuilder.append(" ");
            // 获取返回值类型
            stringBuilder.append(method.getReturnType().getSimpleName());
            stringBuilder.append(" ");
            // 获取方法名
            stringBuilder.append(method.getName());
            stringBuilder.append(" (");
            // 获取形式参数列表的类型
            Class<?>[] parameterTypes = method.getParameterTypes();
            for (int i = 0; i < parameterTypes.length; i++) {
                if (i == parameterTypes.length - 1) {
                    stringBuilder.append(parameterTypes[i].getSimpleName());
                    break;
                }
                stringBuilder.append(parameterTypes[i].getSimpleName());
                stringBuilder.append(", ");
            }
            stringBuilder.append(") {}");
            stringBuilder.append("\n");
        }
        System.out.println(stringBuilder);
    }
}
```

**通过反射机制怎么调用一个对象的方法**

```java
// 通过反射机制调用对象方法
public class Test {
    public static void main(String[] args) {
        try {
            Class<?> c = Class.forName("cn.yechen.MyClass");
            // 创建对象
            Object obj = c.newInstance();
            // 获取方法对象
            Method method = c.getDeclaredMethod("login", String.class, String.class);
            // 调用方法
            /*
            四要素：
            method 方法
            obj 对象
            "admin","123" 实参
            retrunValue 返回值
             */
            Object retrunValue = method.invoke(obj, "admin", "123456");
            System.out.println(retrunValue);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyClass {
    public boolean login(String admin, String password) {
        if ("admin".equals(admin) && "123456".equals(password)) {
            return true;
        }
        return false;
    }
}
```



### 22.9 反射 Constructors

* `Class<?>[]	getParameterTypes()` ：获取构造方法方法的参数列表的类型。
* `T newInstance(Object... initargs)` ：执行有参构造方法。

```java
// 通过反射机制调用有参数的构造方法
public class Test {
    public static void main(String[] args) {
        try {
            Class<?> c = Class.forName("cn.yechen.MyClass");
            // 调用无参构造方法
            Object obj = c.newInstance();// 输出：执行了无参构造方法！
            // 调用两个参数的方法创建对象
            Constructor<?> declaredConstructor = c.getDeclaredConstructor(int.class, String.class);
            declaredConstructor.newInstance(123, "abc");// 输出：执行了两个参数的构造方法
            // 调用四个参数的方法创建对象
            Constructor<?> declaredConstructor1 = c.getDeclaredConstructor(int.class, String.class, double.class, boolean.class);
            declaredConstructor1.newInstance(123, "abc", 123, true);// 输出：执行了四个参数的构造方法
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyClass {
    int a;
    String b;
    double c;
    boolean d;

    public MyClass() {
        System.out.println("执行了无参构造方法！");
    }

    public MyClass(int a) {
        System.out.println("执行了一个参数的构造方法！");
    }

    public MyClass(int a, String b) {
        System.out.println("执行了两个参数的构造方法！");
    }

    public MyClass(int a, String b, double c, boolean d) {
        System.out.println("执行了四个参数的构造方法！");
    }
}
```



### 22.10 获取父类和实现的接口

获取父类：`Class<? super T>	getSuperclass()`

获取实现的接口：`Class<?>[]	getInterfaces()`

```java
public class Test {
    public static void main(String[] args) {
        try {
            Class<?> c = Class.forName("java.lang.String");
            // 获取父类
            Class<?> superClass = c.getSuperclass();
            System.out.println(c.getName() + "的父类是：" + superClass.getName());
            // 获取实现的接口
            Class<?>[] interfaces = c.getInterfaces();
            System.out.println(c.getName() + "实现的接口有：");
            for (Class inter : interfaces) {
                System.out.println(inter.getName());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
/*
输出：
java.lang.String的父类是：java.lang.Object
java.lang.String实现的接口有：
java.io.Serializable
java.lang.Comparable
java.lang.CharSequence
*/
```





## 23、注解（Annotation）

### 23.1 注解概述

注解，或者叫做注释类型，英文单词是：Annotation

注解Annotation是一种引用数据类型。编译之后也是生成xxx.class文件。

**怎么自定义注解呢？语法格式？**

```java
[修饰符列表] @interface 注解类型名{

}
```

**注解怎么使用，用在什么地方？**

* 注解使用时的语法格式是：**@注解类型名**

* 注解可以出现在**类上、属性上、方法上、变量上**等....注解还可以出现在**注解类型**上。

**java.lang包下的注释类型：**

`Deprecated`：用 @Deprecated 注释的程序元素，不鼓励程序员使用这样的元素，通常是因为它很危险或存在更好的选择。 

`Override` ：表示一个方法声明打算重写超类中的另一个方法声明。

```java
// 标识性注解，给编译器做参考的。
// 编译器看到方法上有这个注解的时候，编译器会自动检查该方法是否重写了父类的方法。如果没有重写，报错。
// 这个注解只是在编译阶段起作用，和运行期无关！
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {
}
```

**元注解：**用来标注“注解类型”的“注解”，称为元注解。

`Target`：这是一个元注解，这个Target注解用来**标注“被标注的注解”**可以出现在**哪些位置**上。

* `@Target(ElementType.METHOD)`：表示“被标注的注解”只能出现在方法上。

* `@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, MODULE, PARAMETER, TYPE})`

  表示该注解可以出现在：构造方法上、字段上、局部变量上、方法上、...、类上...。

`Retention`：这是一个元注解，这个Retention注解用来**标注“被标注的注解”最终保存在哪里**。

* `@Retention(RetentionPolicy.SOURCE)`：表示该注解只被保留在**java源文件**中。

* `@Retention(RetentionPolicy.CLASS)`：表示该注解被保存在**class文件**中。

* `@Retention(RetentionPolicy.RUNTIME)`：表示该注解被保存在class文件中，并且**可以被反射机制所读取**。



### 23.2 注解的使用

**自定义注解：**

*  注解当中的属性可以是哪一种类型？
  * `byte` `short` `int` `long` `float` `double` `boolean` `char` `String` `Class` `枚举类型`以及以上每一种的**数组**形式。

```java
public @interface MyAnnotation01 {
    /**
     * 我们通常在注解当中可以定义属性，以下这个是MyAnnotation的name属性。
     * 看着像1个方法，但实际上我们称之为属性name。
     * @return
     */
    String name();

    /*
    颜色属性
     */
    String color();

    /*
    年龄属性
     */
    int age() default 25; //属性指定默认值
}
```

```java
public @interface MyAnnotation02 {
    
    String value();
}
```

**使用注解：**

* 如果一个注解当中有属性，那么必须给属性赋值。（**除非该属性使用default指定了默认值**。）
* 格式为：`@MyAnnotation(属性名=属性值,属性名=属性值,属性名=属性值...)`

```java
@MyAnnotation01(name = "abc", color = "红色")
public class Test {
    
}
```

```java
// 如果一个注解的属性的名字是value，并且只有这一个属性需要赋值（其他属性都指定了默认值）的话，在使用的时候，该属性名可以省略。
@MyAnnotation02(“value”)
public class Test {
    
}
```

**通过反射机制获取类中方法的注解：（同样的方式也可以获得类上、属性上的注解）**

```java
public class Test {
    public static void main(String[] args) {
        try {
            Class<?> myClass = Class.forName("cn.yechen.MyClass");
            Method doSomeMethon = myClass.getDeclaredMethod("doSome");
            if (doSomeMethon.isAnnotationPresent(MyAnnotation.class)) {
                MyAnnotation annotation = doSomeMethon.getAnnotation(MyAnnotation.class);
                System.out.println(annotation.username());
                System.out.println(annotation.passworld());
            }
        } catch (ClassNotFoundException | NoSuchMethodException e) {
            e.printStackTrace();
        }
    }
}


class MyClass {
    @MyAnnotation(username = "root", passworld = "123456")
    public void doSome() {

    }

}

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation {
    String username();
    String passworld();
}
```

### 23.3 使用注解实现一个业务要求，体会注解的作用

业务要求：通过一个注解来判断一个类中是否有 `id` 属性，如果有就正常执行，没有就抛出异常。

1. 定义注解

```java
@Target(ElementType.TYPE)// 该注解执行注解在类上
@Retention(RetentionPolicy.RUNTIME)//给注解可以被反射机制读取到
public @interface MustHasIdPropertyAnnotation {
}
```

2. 定义一个异常类

```java
public class HasNotIdPropertyException extends RuntimeException{
    public HasNotIdPropertyException() {
    }

    public HasNotIdPropertyException(String message) {
        super(message);
    }
}
```

3. 定义一个（被注解）被检查的类

```java
@MustHasIdPropertyAnnotation
public class User {
    int id;
    String name;
}
```

4. 测试

```java
public class Test {
    public static void main(String[] args) {
        try {
            Class<?> userClass = Class.forName("cn.yechen.annotation.User");
            boolean isOK = false;// 是否合法的标记
            if (userClass.isAnnotationPresent(MustHasIdPropertyAnnotation.class)) {
                // 获取 userClass 的全部属性，检查是否存在 int 类型的 id 属性
                Field[] declaredFields = userClass.getDeclaredFields();
                for (Field field : declaredFields) {
                    if ("id".equals(field.getName()) && "int".equals(field.getType().getSimpleName())) {
                        // 合法
                        isOK = true;
                        break;
                    }
                }

            }
            if (isOK) {
                System.out.println("该类中存在 int 类型的 id 属性！");
            } else {
                // 不合法就抛出异常
                throw new HasNotIdPropertyException("该类中一定要有一个 int 类型的 id 属性！");
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

当 User 类中存在 int 类型的 id 属性时，就会输出`该类中存在 int 类型的 id 属性！`

当 User 类中不存在 int 类型的 id 属性时，就会输出异常信息。 
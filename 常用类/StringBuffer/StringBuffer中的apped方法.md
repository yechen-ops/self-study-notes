# StringBuffer中的appead()方法

测试程序

```java
public class Test01 {
    public static void main(String[] args) {
        StringBuffer stringBuffer = new StringBuffer();
        stringBuffer.append("abc");
        System.out.println(stringBuffer);
    }
}
```



首先通过无参构造方法调用了父类 `AbstractStringBuilder` 中的构造方法

```java
public StringBuffer() {
    super(16);
}

AbstractStringBuilder(int capacity) {
    value = new char[capacity];
}
```

创建了一个长度为 `16` 的 **char** 类型数组，数组名为 ==**value**==



此时 

`str = "abc"`

 `toStringCache` ~~表示返回最后一次toString的缓存值，一旦StringBuffer被修改就清除这个缓存值~~

```java
public synchronized StringBuffer append(String str) {
    toStringCache = null;
    super.append(str);
    return this;
}
```

调用父类 `AbstractStringBuilder` 的 `append(String str)` 方法

```java
public AbstractStringBuilder append(String str) {
    if (str == null)// 当 str 是 null 的时候，
        return appendNull();// 在 value 数组中添加四个元素 'n''u''l''l'
    int len = str.length();// 计算当前字符串的长度，目前是 3
    ensureCapacityInternal(count + len);// 确保当前容量是否够用，如果不够用回进行数组扩容
    str.getChars(0, len, value, count);
    count += len;
    return this;
}
```

`str.getChars(0, len, value, count);` 将当前字符串变成 char 数组，通过数组拷贝赋值给 之前的 ==value== 数组

`count` 表示当前总的字符串的长度


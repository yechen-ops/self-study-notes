## IDEA 配置数据库

### 一、关联方式

![image-20210314212328031](C:%5CUsers%5C30117%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210314212328031.png)

![image-20210314212718758](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314212718758.png)

![image-20210314213116830](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314213116830.png)

![image-20210314213219332](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314213219332.png)

>表面上很多人认为配置 Database 就是为了有一个 GUI 管理数据库功能，但是这并不是 IntelliJ IDEA 的 Database 最重要特性。数据库的 GUI 工具有很多，IntelliJ IDEA 的 Database 也没有太明显的优势。IntelliJ IDEA 的 Database 最大特性就是对于 Java Web 项目来讲，常使用的 ORM 框架，如 Hibernate、Mybatis 有很好的支持，比如配置好了 Database 之后，IntelliJ IDEA 会自动识别 domain 对象与数据表的关系，也可以通过 Database 的数据表直接生成 domain 对象等等。



### 二、常用操作

![image-20210314213623507](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314213623507.png)

>**图标 1：**同步当前的数据库连接。这个是最重要的操作。配置好连接以后或通过其他工具操作数据库以后，需要及时同步。
>
>**图标 2：**配置当前的连接。 
>
>**图标 3：**断开当前的连接。
>
>**图标 4：**显示相应数据库对象的数据
>
>**图标 5：**编辑修改当前数据库对象

![image-20210314213755087](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314213755087.png)

![image-20210314213926646](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/image-20210314213926646.png)
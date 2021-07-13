## MyBatis

### 一、三层架构

> 界面层（视图层）

完成和用户的交互，接受请求，显示请求的处理结果。

使用 `SpringMVC` 框架来实现。

> 业务逻辑层

计算数据，处理业务逻辑。

使用 `Spring` 框架来实现。

> 数据访问层（持久层）

对数据库进行操作。

使用 `MyBatis` 进行操作。



### 二、概述

#### 1. MyBatis 是什么，有什么特点？

它是一款半自动的 `ORM` 持久层框架，具有较高的 SQL 灵活性，支持高级映射 (一对一，一对多)，动态 SQL，延迟加载和缓存等特性，但它的数据库无关性较低。

* 什么是 `ORM`：

  `Object Relation Mapping`，对象关系映射。**对象指的是 Java 对象，关系指的是数据库中的关系模型**，对象关系映射，指的就是在 **Java 对象和数据库的关系模型之间建立一种对应关系**，比如用一个Java的Student类，去对应数据库中的一张 student 表，类中的属性和表中的列一一对应。Student类就对应student表，一个Student对象就对应student表中的一行数据。

* 为什么 mybatis 是半自动的 ORM 框架：

  **用 mybatis 进行开发，需要手动编写 SQL 语句**。而全自动的 ORM 框架，如 `hibernate`，则不需要编写 SQL 语句。用 hibernate 开发，只需要定义好 ORM 映射关系，就可以直接进行 CRUD 操作了。由于 mybatis 需要手写SQL 语句，**所以它有较高的灵活性，可以根据需要，自由地对 SQL 进行定制**，也因为要手写 SQL，**当要切换数据库时，SQL 语句可能就要重写，因为不同的数据库有不同的方言 (Dialect)，所以 mybatis 的数据库无关性低**。虽然 mybatis 需要手写 SQL，但相比 JDBC，它提供了输入映射和输出映射，可以很方便地进行 SQL 参数设置，以及结果集封装。并且还提供了关联查询和动态 SQL 等功能，极大地提升了开发的效率。并且它的学习成本也比 hibernate 低很多。

#### 2. 简单使用 MyBatis

1. 创建数据库和数据表

   ```sql
   CREATE DATABASE springdb;
   use springdb;
   
   CREATE TABLE `student` (
    `id` int(11) NOT NULL ,
    `name` varchar(255) DEFAULT NULL,
    `email` varchar(255) DEFAULT NULL,
    `age` int(11) DEFAULT NULL,
     PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

2. 加入 maven 依赖

   `pom.xml`

   ```xml
   <!-- 单元测试依赖 -->
   <dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>4.11</version>
       <scope>test</scope>
   </dependency>
   <!-- mybatis 依赖 -->
   <dependency>
       <groupId>org.mybatis</groupId>
       <artifactId>mybatis</artifactId>
       <version>3.5.6</version>
   </dependency>
   <!-- mysql 驱动 -->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>5.1.23</version>
   </dependency>
   ```

3. 创建 dao 接口，定义操作数据库的方法

   `cn.yechen.dao.Studentdao.java`

   ```java
   package cn.yechen.dao;
   
   import cn.yechen.entity.Student;
   
   import java.util.List;
   
   public interface StudentDao {
       /**
        * 获取 Student 表中的所有数据
        * @return Student 表中所有数据
        */
       List<Student> selectStudents();
   
   
       /**
        * 添加学生的方法
        * @param student 新增学生对象
        * @return 影响数据库的行数
        */
       int insertStudent(Student student);
   }
   ```

4. 创建 mapper（sql 映射文件），写和接口中方法对应的 sql 语句

   `cn.yechen.dao.StudentDao.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <!--
   	以上语句是指定约束文件的，格式是固定的，mybatis-3-mapper.dtd 文件就是约束文件
       约束文件是用来检查文件中出现的标签、属性必须符合 mybatis 的要求
   -->
   <mapper namespace="cn.yechen.dao.StudentDao">
   	
       <!-- 查询操作 -->
       <select id="selectStudents" resultType="cn.yechen.entity.Student">
           select id,name,email,age from Student
       </select>
   
       <!-- 插入操作 -->
       <insert id="insertStudent">
           insert into student (id, name, email, age) values (#{id}, #{name}, #{email}, #{age})
       </insert>
   </mapper>
   ```

   `<mapper>` ：是当前文件的根标签，必须存在的

   * namespace：叫做命名空间，值是唯一的，可以是自定义的字符串，要求你使用 dao 接口的全限定名称。

   `<select>` ： 表示执行查询

   `<insert>` ： 表示插入数据操作

   `<update>` ： 表示更新数据库操作

   `<delete>` ： 表示删除操作

   * **id**：是你要执行的 sql 语句的唯一标识，mybatis 会使用这个 id 的值来找到要执行的 sql 语句，id 值可以自定义，但是推荐使用接口中的方法名。
   * **resultType**：表示执行 sql 语句执行后得到的 resultSet，编历后得到的 java 对象的类型，值写的是返回值类型的全限定名称。

   

5. 创建 mybatis 主配置文件

   `resources/mybatis-config.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <!--
   	以上语句是指定约束文件的，格式是固定的，mybatis-3-mapper.dtd 文件就是约束文件
       约束文件是用来检查文件中出现的标签、属性必须符合 mybatis 的要求
   -->
   <configuration>
   
       <!-- settings：控制 mybatis 的全局行为 -->
       <settings>
           <!-- 设置 mybatis 输出日志 --> 
           <setting name="logImpl" value="STDOUT_LOGGING"/>
       </settings>
   
       <!-- 环境配置：数据库的连接信息
            default：必须和 其中一个 environment 标签中的 id 值一致，
                     告诉 mybatis 使用的是哪个数据库的连接信息，也就是访问哪个数据库。
       -->
       <environments default="development">
           <!-- 数据库信息的配置，是一个环境
                id：一个自定义的唯一值，表示环境的名称
            -->
           <environment id="development">
               <!-- 表示 mybatis 的事务类型
                    type：使用 JDBC（表示使用 jdbc 中的 Connection 对象的 commit 和 rollback 做事务处理）
                -->
               <transactionManager type="JDBC"/>
               <!-- 表示数据源，用来连接数据库
                    type：表示数据源类型，POOLED 表示使用连接池
                -->
               <dataSource type="POOLED">
                   <property name="driver" value="com.mysql.jdbc.Driver"/>
                   <property name="url" value="jdbc:mysql://localhost:3306/springdb"/>
                   <property name="username" value="root"/>
                   <property name="password" value="ruanlitao2000"/>
               </dataSource>
           </environment>
       </environments>
   
       <!--执行所有的 sql 映射文件的位置-->
       <mappers>
           <!-- 一个 mapper 标签指定一个 sql 映射文件的位置，从类路径（target/classes classes 就表示类路径）开始表示文件位置 -->
           <mapper resource="cn/yechen/dao/StudentDao.xml"/>
       </mappers>
   </configuration>
   
   <!--
       是 mybatis 的只要配置文件，主要定义了数据库的配置信息和 sql 映射文件的位置
       1. <!DOCTYPE configuration
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-config.dtd">
           是指定约束文件的，格式是固定的，mybatis-3-config.dtd 文件就是约束文件
           约束文件是用来检查文件中出现的标签、属性必须符合 mybatis 的要求
   
       2. <configuration> 表示根标签
   
   -->
   ```

   `<configuration>`：表示根标签。

   `<settings>`：控制 mybatis 的全局行为。

   `<environments>`：环境配置，数据库的连接信息。

   * **default**：必须和其中一个 environment 标签中的 id 值一致，告诉 mybatis 使用的是哪个数据库的连接信息，也就是访问哪个数据库。

   `<environment>`：数据库信息的配置，是一个环境。一个 <environments> 中可以写多个。

   * **id**：一个自定义的唯一值，表示环境的名称，当要使用这个环境的时候，就可以将 <environments> 标签中的 default 属性与 id 属性一致。

   `<dataSource>`：表示数据源，用来连接数据库。

   * **type**：表示数据源类型，POOLED 表示使用连接池。

   `<property>`：表示连接数据库的核心信息，驱动，url，user，password。

   

6. 使用 mybatis 中的对象 `SqlSession` 来执行 sql 语句

   `Test/java/cn.yechen.TestMyBatis`

   ```java
   public class TestMybatis {
   
       // 测试查询操作
       @Test
       public void testSelectStudents() {
           // 访问 mybatis，读取 Student 数据
           // 1. 定义 mybatis 主配置文件的名称，从类路径开始
           String resource = "mybatis-config.xml";
   
           // 2. 读取主配置文件
           InputStream inputStream = null;
           try {
               inputStream = Resources.getResourceAsStream(resource);
           } catch (IOException e) {
               e.printStackTrace();
           }
   
           // 3. 通过 SqlSessionFactoryBuilder 对象的 build() 方法创建 SqlSessionFactory 对象
           SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
   
           // 4. 从 SqlSessionFactory 对象中获取 SqlSession 独享
           SqlSession sqlSession = sqlSessionFactory.openSession();
   
           // 5。 指定要执行的 sql 语句的标识
           String sqlId = "cn.yechen.dao.StudentDao.selectStudents";
   
           // 6。 通过 sqlId 执行 sql
           List<Student> list = sqlSession.selectList(sqlId);
   
           // 7. 输出结果
           for (Student student : list) {
               System.out.println(student);
           }
   
           // 8. 关闭 SqlSession 对象
           sqlSession.close();
       }
   
       // 测试插入操作
       @Test
       public void testInsertStudent() {
           String resource = "mybatis-config.xml";
           InputStream inputStream = null;
           try {
               inputStream = Resources.getResourceAsStream(resource);
           } catch (IOException e) {
               e.printStackTrace();
           }
           SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
           SqlSession sqlSession = sqlSessionFactory.openSession();
   
           String sqlId = "cn.yechen.dao.StudentDao.insertStudent";
           int result = sqlSession.insert(sqlId, new Student(8, "zhangsan", "123456789", 15));
           // 注意：mybatis 默认不是自动提交事务的，所以在 insert，update，delete 之后要手工提交事务
           sqlSession.commit();
   
           System.out.println(result);
           sqlSession.close();
       }
   }
   ```

   查询语句执行结果：

   ![image-20210421221004673](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image-20210421221004673.5ax3k2x4fk40.png)

### 三、主要类介绍

`Resources`：mybatis 中的一个类，**负责读取主配置文件**。

```java
InputStream inputStream = Resources.getResourceAsStream("mybatis-config.xml");
```

`SqlSessionFactoryBuilder`：只有一个功能：**用于创建 SqlSessionFactory 对象**。

```java
SqlSessionFactory factory = new SqlSessionFactoryBuilder.build(inputStream);
```

`SqlSessionFactory（接口）`：重量级对象，该对象在创建时耗时长、使用资源多，在整个项目中，有一个就够用了。作用：**获取 SqlSession 对象**。

```java
SqlSession sqlSession = factory.openSession();
```

* SqlSessionFactory 的默认实现类是 DefaultSqlSessionFactory
* 方法 `openSession`：
  * openSession() 无参：获取的是**非自动提交事务**的 SqlSession 对象。
  * openSession(boolean autoCommit)：**自己设置是否自动提交事务（true 表示自动提交）**，并获得对应的 SqlSession 对象

`SqlSession（接口）`：定义了操作数据库的方法，增删改查，事务提交，事务回滚。

* SqlSession 的默认实现类是 DefaultSqlSession
* SqlSession 对象**不是线程安全的**，在执行完 sql 语句后，要使用 **.close() 方法关闭**它。



### 四、使用 mybatis 的动态代理

#### 1. 什么是动态代理

mybatis 通过 SqlSession 的方法动态帮你创建 dao 接口的实现类，通过实现类来执行 sql。

#### 2. 使用动态代理

1. 封装工具类，通过工具类获取 SqlSession 对象。

   `cn.yechen.util.MyBatisUtils.java`

   ```java
   public class MyBatisUtils {
   
       private static SqlSessionFactory factory;
   
       // SqlSessionFactory 对象在程序中只需要一个，因此将创建的代码写在静态代码块中，只在类加载的时候创建一次
       static {
           // 读取主配置文件
           String rescourse = "mybatis-config.xml";
           InputStream inputStream = null;
           try {
               inputStream = Resources.getResourceAsStream(rescourse);
           } catch (IOException e) {
               e.printStackTrace();
           }
           // 创建 SqlSessionFactory 对象
           factory = new SqlSessionFactoryBuilder().build(inputStream);
       }
       
       /**
        * 获取 SqlSession 对象
        * @return SqlSession 对象
        */
       public static SqlSession getSqlSession() {
           SqlSession sqlSession = null;
           if (factory != null) {
               sqlSession = factory.openSession();
           }
           return sqlSession;
       }
   }
   ```

2. 使用动态代理查询所有学生

   ```java
   public class AppTest {
       @Test
       public void testSelectStudent() {
           // 获取 SqlSession 对象
           SqlSession sqlSession = MyBatisUtils.getSqlSession();
   
           // 使用 mybatis 的动态代理生成的接口实现类
           StudentDao mapper = sqlSession.getMapper(StudentDao.class);
   		System.out.println(studentDao.getClass().getName());
           
           List<Student> studentList = mapper.selectStudents();
           for (Student student : studentList) {
               System.out.println(student);
           }
           sqlSession.close();
       }
   }
   ```

   执行结果：

   ![image-20210421221211689](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image-20210421221211689.26u54jt4qhzw.png)

#### 3. 使用动态代理的要求

1. dao 接口和 mapper 文件放在一个目录下。
2. dao 接口和 mapper 文件名称一致。
3. mapper 文件中的 namespace 的值要和 dao 接口的全限定名称一致。
4. mapper 文件中的 <select><insert><update><delete> 标签的 id 值与接口中的方法一致。
5. dao 接口中不要使用重载方法，保证 mapper 文件中的 id 值是唯一的。



### 五、sql 中的参数传递

#### 一个参数时

在 sql 语句中使用 `#{任意字符}` 来传值。

例如：

```xml
<select id="selectStudentById" resultType="cn.yechen.entity.Student" parameterType="java.lang.Integer">
    select id,name,email,age from student where id=#{id}
</select>
```

其中：

`<paramterType>`：表示 dao 接口中方法参数的数据类型，值是 java 类型的全限定名称，或者是 MyBatis 中已经设置好的别名。**这个属性是可选的**，因为 MyBatis 可以通过**类型处理器（TypeHandler）推断出具体传入语句的参数**，默认值为未设置（unset）。

**MyBatis  如何执行对数据库的操作：**

1. mybatis 会创建 Connection、PreparedStatement 对象。

2. 获取 sql 语句，将 #{} 使用占位符 ? 代替。

   ```java
   String sql = "select id,name,email,age from student where id=?";
   ```

3. 对 PreparedStatement 对象赋值，预编译 sql。

   ```java
   preparedStatement = connection.prepareStatement(sql);
   ```

4. 向 sql 语句中赋值。

   ```java
   preparedStatement.setInt(1, id);
   ```

5. 执行 sql，获取结果集。

   ```java
   ResultSet resultSet = preparedStatement.executeQuery();
   ```

6. 将查询结果封住为 resultType 属性的执行的类型，返回给对象。

   ```java
   Student student = null;
   while(resultSet.next()) {
       student = new Student();
       student.setInt(resultSet.getInt("id"));
       student.setName(resultSet.getString("name"));
       student.setEmail(resultSet.getString("email"));
       student.setAge(resultSet.getInt("age"));
   }
   return student;
   ```

#### 多个参数时

##### 方法一 

在接口中的方法参数使用 `@Param("自定义名称")` 命名，mapper 中使用 `#{自定义名称}`。

```java
// dao 接口
List<Student> selectMultiParam(@Param("studentName") String name, @Param("studentAge") Integer age);
```

```xml
<!-- mapper 文件 -->
<select id="selectMultiParam" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where name=#{studentName} or age=#{studentAge}
</select>
```



##### 方法二

在接口中的方法==参数使用 java 对象==，在 mapper 中使用==java 对象的属性值作为 sql 参数的实际值==，这个 java 对象可以是使用时封装的 java 对象，也可以直接使用数据库对象类（po 类），mapper 中使用 #{java 对象属性名}。

* **最完整的语法格式**：#{属性名，javaType=java对象中属性的类型，jdbcType=字段在数据库中的数据类型}  这种方法很少用。
*  **使用简化的方式**：#{属性名} 常用，javaType 和 jdbcType 的值 mybatis 可以通过反射获取

```java
// dao 接口
List<Student> selectMultiObject(QueryParam queryParam);

// 自定义查询参数类
public class QueryParam {
    private String queryName;
    private Integer queryAge;


    public String getQueryName() {
        return queryName;
    }

    public void setQueryName(String queryName) {
        this.queryName = queryName;
    }

    public Integer getQueryAge() {
        return queryAge;
    }

    public void setQueryAge(Integer queryAge) {
        this.queryAge = queryAge;
    }
}
```

```xml
<!-- mapper 文件 -->
<select id="selectMultiObject" resultType="cn.yechen.entity.Student">
    select id, name, email, age from student where name=#{queryName} or age=#{queryAge}
</select>
```



##### 方法三

**多个简单类型**的参数通过`参数的位置`来传值。

* mybatis 3.4 之前，使用 #{0}，#{1}... 来传值
* mybatis 3.4 之后，使用 `#{arg0}，#{arg1}...` 来传值。

```java
// dao 接口
List<Student> selectMultiPosition(String name, Integer age);
```

```xml
<!-- mapper 文件 -->
<select id="selectMultiPosition" resultType="cn.yechen.entity.Student">
    select id, name, email, age from student where name=#{arg0} or age=#{arg1}
</select>
```



##### 方法四

在接口中的方法==参数使用 Map 类型对象==，mapper 中使用 ==#{map对象的 key}==

```java
// dao 接口
List<Student> selectMultiMap(Map<String, Object> map);

// 测试方法
@Test
public void testSelectMultiMap() {

    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);

    Map<String, Object> map = new HashMap<>();
    // key 为 “stuName”
    map.put("stuName", "李四");
    // key 为 "stuAge"
    map.put("stuAge", 15);
    List<Student> studentList = mapper.selectMultiMap(map);

    for (Student s : studentList) {
        System.out.println(s);
    }
    sqlSession.close();
}
```

```xml
<!-- mapper 文件 -->
<select id="selectMultiMap" resultType="cn.yechen.entity.Student">
    select id, name, email, age from student where name=#{stuName} or age=#{stuAge}
</select>
```



#### 参数传递时 # 和 $ 的区别

`#`：是 mybatis 中的占位符，告诉 mybatis 使用实际的参数值代替。并==使用 PrepareStatement 对象执行 sql 语句, #{…}代替 sql 语句的 “?”==。这样做更安全(可以避免 sql 注入)，更迅速，通常也是首选做法。

`$`：是 mybatis 中的占位符，表示字符串替换，告诉 mybatis 使用 `$` 包含的“字符串”替换所在位置。==使用 Statement 把 sql 语句和 ${...} 的内容连接起来==。主要用在替换表名，列名，不同列排序等操作。会有 sql 注入等安全风险。



### 六、sql 的返回结果

#### 1、resultType 属性

`resultType`：属性指定的是结果类型，sql 语句执行完成之后，mybatis 调用指定的 java 类的无参构造方法，创建对应的对象。使用时要保证指定 java 类中的属性和数据库字段的名称要一致，并存在属性对应的 get 和 set 方法，mybatis 会将 ResultSet 对象中的指定列值赋给同名的属性。

`resultType 属性值`可以是：

* 类型的全限定名称，比如类 Integer 就要写成 java.lang.Integer。
* 由 mybatis 官方文档中指定的常用类型的别名，如 java。lang.Integer 的别名就是 int。

##### 当返回值是 `Map` 类型的时候

==执行完 sql 后，会将列名赋给 map 的 key，列值赋给 map 的 value。==

```java
// dao 接口
Map<Object, Object> selectMapById(Integer id);
```

```xml
<!-- mapper 文件 -->
<select id="selectMapById" resultType="java.util.Map">
    select id,name,email from student where id=#{id};
</select>
```

```java
// 测试类
@Test
public void testSelectMapById() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    Map<Object, Object> objectObjectMap = mapper.selectMapById(3);
    System.out.println(objectObjectMap);
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.4u997xac6aa0.png)

#### 2、定义自定义类型别名

##### 第一种方式

在 mybatis 主配置文件中的 `<typeAliases>` 标签中定义，使用 `<typeAlias>` 标签自定义别名。

```xml
<!-- mybatis-config.xml -->
<typeAliases>
    <typeAlias type="cn.yechen.dao.Student" alias="student"/>
</typeAliases>
```

* type 属性：表示类型的全限定名称
* alias 属性：表示自定义别名

##### 第二种方式

在 mybatis 主配置文件中的 `<typeAliases>` 标签中定义，使用 `<package>` 标签指定包名，该包下的所有类名就是别名了。

```xml
<!-- mybatis-config.xml -->
<typeAliases>
    <package name="cn.yechen.dao"/>
</typeAliases>
```

* name 属性：表示指定的包名，包中的所有类名就是别名。

==使用时隐患==：当使用 `<package>` 标签定义了两个包，此时在两个包中存在同名的类，此时 mybatis 就不能区分出两个类，程序就会抛出异常。

#### 3、当列名和属性名不一致的时候的解决方法

##### 第一种方法

使用 `<resultMap>` 标签：表示**结果映射**，指定 SQL 语句中的列名和 java 对象中的属性的对应关系，你可以自定义哪个列赋给哪个属性。**resultMap 和 resultType 不能一起用，二选其一**。

使用步骤：

1. 先定义一个 resultMap，自其中写上类名和属性一一对应的关系。

   ```java
   // cn.yechen.vo.SelectStudent
   @NoArgsConstructor
   @AllArgsConstructor
   @Getter
   @Setter
   @ToString
   public class SelectStudent {
       private Integer studentId;
       private String studentName;
       private String studentEmail;
       private Integer studentAge;
   }
   ```

   ```xml
   <!-- mapper 文件 -->
   <!-- id 属性值就是待会儿使用时 resultMap 属性的属性值 -->
   <resultMap id="studentMap" type="cn.yechen.vo.SelectStudent">
       <!--
           对于主键列，使用 <id> 标签
           column：数据库中的列名
           property：java 类型的属性名
       -->
       <id column="id" property="studentId" />
   
       <!--
           对于非主键类，使用 <result> 标签
           column：数据库中的列名
           property：java 类型的属性名
       -->
       <result column="name" property="studentName"/>
       <result column="email" property="studentEmail"/>
       <result column="age" property="studentAge"/>
   </resultMap>
   ```

2. 在 select 标签中使用 resultMap，值是定义时设定的 id 值。

   ```xml
   <!-- mapper 文件 -->
   <select id="selectAllStudent" resultMap="studentMap">
       select id,name,email,age from student
   </select>
   ```



##### 第二种方法

使用 resultType 指定要使用的 java 类的全限定名称，但在写 sql 语句的时候为每一列指定一个别名（==使用 sql 中的语法 as，给列名重命名==），这个别名和 java 类中的属性相一致。

```xml
<!-- mapper 文件 -->
<select id="selectAllStudent2" resultType="cn.yechen.vo.SelectStudent">
    select id as studentId,name as studentName,email as studentEmail,age as studentAge from student
</select>
```



#### 4、模糊查询

##### 第一种方法

在 java 代码中将 like 之后的值全部传过来。

```java
// dao 接口类
List<Student> selectLikeOne(String name);
```

```xml
<!-- mapper 文件 -->
<select id="selectLikeOne" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where name like #{name}
</select>
```

```java
// 测试方法
@Test
public void testSelectLikeOne() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    // 传递的值就是 like 之后的全部值
    List<Student> studentList = mapper.selectLikeOne("%李%");
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.3azw0mmj5we0.png)



##### 第二种方式

在 mapper 文件中拼接 like 的内容。

```java
// dao 接口
List<Student> selectLikeTwo(String name);
```

```xml
<!-- mapper 文件 -->
<select id="selectLikeTwo" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where name like "%" #{name} "%"
</select>
```

```java
// 测试方法
@Test
public void testSelectLikeTwo() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    List<Student> studentList = mapper.selectLikeTwo("李");
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.2d8jqff3hp1c.png)

### 七、动态 sql

**动态sql**: sql 的内容是变化的，==可以根据条件获取到不同的 sql 语句==。主要是 where 部分发生变化。

#### if  标签

```xml
<!-- 语法 -->
<if test="java 对象中的属性满足的条件">
    满足条件下拼接上去的 sql
</if>
<!-- 比如：当 name 属性不为 null 且不为空时拼接 sql -->
<if test="name != null and name != ''">
    name = #{name}
</if>
```

==不足==：当 if 中的条件不全满足的时候，拼接后的 sql 语法可能有问题。会存在 and 或 or 的多出或者缺少，导致 sql语法错误，如：

```java
// dao 接口
List<Student> selectStudentIf(Student student);
```

```xml
<!-- mapper 文件 -->
<select id="selectStudentIf" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where
    <if test="name != null and name != ''">
        name = #{name}
    </if>
    <if test="age > 0">
        or age > #{age}
    </if>
</select>
```

```java
// 测试方法
@Test
public void testSelectStudentIf() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    List<Student> studentList = mapper.selectStudentIf(new Student(0, null, null, 14));
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

错误：

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.6o2zm4yirwo0.png)



#### where  标签

标签中包含多个 <if> 标签，当 if 标签中有一个及以上的条件成立时，mybatis 会在 sql 语句后加一个 where 关键字并去掉（添加）条件成立的 if 标签 sql 语句中多余（需要）的 and 或者 or。

```java
// dao 接口
List<Student> selectStudentWhere(Student student);
```

```xml
<!-- mapper 文件 -->
<select id="selectStudentWhere" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student
    <where>
        <if test="name != null and name != ''">
            and name = #{name}
        </if>
        <if test="age > 0">
            or age > #{age}
        </if>
    </where>
</select>
<!--
1. 当两个 if 都不成立时，sql 语句为：select id,name,email,age from student;
2. 当只有第一个 if 成立时，sql 语句为：select id,name,email,age from student where name=?;
3. 当只有第二个 if 成立时，sql 语句为：select id,name,email,age from student where age>?;
4. 当两个 if 都成立时，sql 语句为：select id,name,email,age from student where name=? or age=?;
-->
```

```java
// 测试方法
@Test
public void testSelectStudentWhere() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    List<Student> studentList = mapper.selectStudentWhere(new Student(0, "李四", null, 0));
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.7j49dfbyg9o0.png)



#### foreach  标签

==用来循环 java 中的数组、list 集合的，主要用在 sql 语句的 in 语句中。==

##### 使用一：list 中保存的是基本数据类型

```xml
<foreach collection="" item="" open="" close="" separator="">
    #{item中自定义的用来编历的变量}
</foreach>
<!--
1. collection：表示接口中方法参数的类型，如果是数组，属性值就是 “array”，如果是集合，属性值就是 “list”
2. item：自定义的，代表数组或集合成员中的一个变量。
3. open：循环开始时的字符。
4. close：循环结束时的字符。
5. separator：集合成员之间的分隔符。
-->
```

如：

```java
// dao 接口
List<Student> selectForeachOne(List<Integer> idList);
```

```xml
<!-- mapper 文件 -->
<select id="selectForeachOne" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where id in
    <foreach collection="list" item="stuId" open="(" close=")" separator=",">
        #{stuId}
    </foreach>
</select>
```

```java
// 测试方法
 @Test
public void testSelectForeachOne() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    List<Integer> list = new ArrayList<>();
    list.add(1);
    list.add(2);
    list.add(3);
    list.add(4);
    List<Student> studentList = mapper.selectForeachOne(list);
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.6y86x7qfwk80.png)



##### 使用二：list 中保存的是引用数据类型

```xml
<foreach collection="" item="" open="" close="" separator="">
    #{item中自定义的编历对象.对应的属性值}
</foreach>
<!--
1. collection：表示接口中方法参数的类型，如果是数组，属性值就是 “array”，如果是集合，属性值就是 “list”
2. item：自定义的，代表数组或集合成员中的一个变量。
3. open：循环开始时的字符。
4. close：循环结束时的字符。
5. separator：集合成员之间的分隔符。
-->
```

如：

```java
// dao 接口
List<Student> selectForeachTwo(List<Student> stuList);
```

```xml
<!-- mapper 文件 -->
<select id="selectForeachTwo" resultType="cn.yechen.entity.Student">
    select id,name,email,age from student where id in
    <foreach collection="list" item="stu" open="(" close=")" separator=",">
        #{stu.id}
    </foreach>
</select>
```

```java
// 测试方法
@Test
public void testSelectForeachTwo() {
    SqlSession sqlSession = MyBatisUtils.getSqlSession();
    StudentDao mapper = sqlSession.getMapper(StudentDao.class);
    List<Student> list = new ArrayList<>();
    list.add(new Student(1, null, null, null));
    list.add(new Student(2, null, null, null));
    List<Student> studentList = mapper.selectForeachTwo(list);
    for (Student student : studentList) {
        System.out.println(student);
    }
    sqlSession.close();
}
```

![image](https://cdn.jsdelivr.net/gh/yechen-ops/image-hosting@master/20210423/image.qo1fthw2cgg.png)



#### sql  标签

==将高复用的 sql 语句放在 <sql> 标签中，实现 sql 的复用。==

使用步骤：

1. 先定义

   ```xml
   <sql id="自定义的唯一名称，代表当前 sql">
       sql 语句
   </sql>
   ```

2. 在 <select><insert> 等标签中使用 sql 语句

   ```xml
   <select>
   	<include refid="sql 标签中 id 的值">
   </select>
   ```

   

### 八、mybatis 主配置文件

全局配置文件中，各个标签要按照如下顺序进行配置，因为mybatis加载配置文件的源码中是按照这个顺序进行解析的

```xml
<configuration>
	<!-- 配置顺序如下
     properties  

     settings

     typeAliases

     typeHandlers

     objectFactory

     plugins

     environments
        environment
            transactionManager
            dataSource

     mappers
     -->
    <mappers>
    	<!-- 一个 mapper 标签指定一个 sql 映射文件的位置，从类路径（target/classes classes 就表示类路径）开始表示文件位置 -->
        <mapper resource="cn/yechen/dao/StudentDao.xml"/>
        
        <!-- 也可以使用 class 属性，值是 dao 接口的全限定名称 -->
        <mapper class="cn.yechen.dao.StudentDao">
        
        <!-- 批量注册，name 属性指向 dao 层的包，表示在该 dao 包下，所有的 mapper 映射文件全部自动注册 -->
        <package name="cn.yechen.dao">
    </mappers>
</configuration>
```



[参考官方文档](https://mybatis.org/mybatis-3/zh/configuration.html)



### 九、mybatis 逆向工程

https://www.cnblogs.com/zzjlxy-225223/p/12458344.html



### 十、参考文档

[mybatis看这一篇就够了，简单全面一发入魂](https://blog.csdn.net/vcj1009784814/article/details/106391982)

[官方文档](https://mybatis.org/mybatis-3/zh/index.html)
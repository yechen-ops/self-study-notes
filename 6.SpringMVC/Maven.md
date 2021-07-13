## Maven

### 一、Maven 简介

#### 1. 概述

**介绍：**

* Maven 是 Apache 软件基金会组织维护的一款自动化构建工具，专注服务于 Java 平台的项目构建和

  依赖管理。Maven 这个单词的本意是：专家，内行。读音是['meɪv(ə)n]或['mevn]。

* Maven 是目前最流行的自动化构建工具，对于生产环境下多框架、多模块整合开发有重要作用，Maven 是一

  款在大型项目开发过程中不可或缺的重要工具。

* Maven 可以整合多个项目之间的引用关系，我们可以根据业务和分层需要任意拆分一个项目。

* Maven 提供规范的管理各个常用 jar 包及其各个版本，并且可以自动下载和引入项目中。

* Maven 可以根据指定版本自动解决 jar 包版本兼容问题。

* Maven 可以把 jar 包所依赖的其它 jar 包自动下载并引入项目。

**Maven 支持对 Java 项目进行构建，构建过程的几个主要过程：**

* `清理`：删除以前的编译结果，为重新编译做好准备。

* `编译`：将Java源程序编译为字节码文件。

* `测试`：针对项目中的关键点进行测试，确保项目在迭代开发过程中关键点的正确性。

* `报告`：在每一次测试后以标准的格式记录和展示测试结果。

* `打包`：将一个包含诸多文件的工程封装为一个压缩文件用于安装或部署。Java 工程对应 jar 包，Web

  工程对应war包。

* `安装`：在Maven环境下特指将打包的结果——jar包或war包安装到本地仓库中。

* `部署`：将打包的结果部署到远程仓库或将war包部署到服务器上运行.

#### 2. 核心概念

Maven能够实现自动化构建是和它的内部原理分不开的，这里我们从 Maven 的`九个核心概念`入手，

看看Maven是如何实现自动化构建的

* [约定的目录结构](####1. 约定的目录结构)
* [POM 文件](####2. pom 文件)
* [坐标](####3. 坐标)
* [依赖管理](####4. 依赖管理)
* [仓库管理](####5. 仓库)
* [生命周期](####6. 生命周期)
* [插件和目标](####7. 插件)
* 继承
* 聚合

#### 3. Maven 的安装

##### 下载安装 Maven

[Maven官网](https://maven.apache.org/)

![image-20210201204538495](https://i.loli.net/2021/02/01/ZqSmxKpRQ8UHaod.png)

##### 配置环境变量

配置如下：

* `M2_HOME`：maven 目录下的 bin 目录
* `MAVEN_HOME`：maven 的目录
* 在系统的 `path` 中配置 `%MAVEN_HOME%\bin`

确保配置成功

![image-20210201212204477](https://i.loli.net/2021/02/01/rfiYc8XJzEPuk1A.png)

##### 阿里云镜像

* 镜像（mirrors）：
  * 作用：加速我们的下载速度
* 国内建议使用阿里云的镜像，在 **conf/setting.xml** 文件下的 **mirrors **标签下配置

```xml
<mirror>
		<id>aliyunmaven</id>
		<mirrorOf>central</mirrorOf>
		<name>aliyun maven</name>
		<url>https://maven.aliyun.com/repository/public </url>
</mirror>
或者是（其实都一样）
<mirror> 
    <id>nexus-aliyun</id> 
    <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf> 
    <name>Nexus aliyun</name> 
    <url>http://maven.aliyun.com/nexus/content/groups/public</url> 
</mirror>
```

##### 本地仓库

**建立一个本地仓库**（LocalRepository）

![image-20210201213820943](https://i.loli.net/2021/02/01/2xLRIT7Bia4smMX.png)

在 **conf/setting.xml** 文件下配置

```xml
<localRepository>D:\Environmental\Maven\apache-maven-3.6.3\maven-repo</localRepository>
```



### 二、Maven 的核心概念

#### 1. 约定的目录结构

```shell
└─src
    ├─main
    │   ├─java
    │   └─resource
    └─test
    │   ├─java
    │   └─resource
    └─pom.xml     
```

src：源代码

main：主程序

java：主程序的 java 源码

resources：主程序的配置文件

test：测试程序

java：测试程序的 java 源码

resources：测试程序的配置文件

pom.xml：Maven 工程的核心配置文件



Maven的核心思想：**约定大于配置**，有约束，不要去违反

Maven会规定好你该如何去编写我们的 Java 代码，必须要按照这个规范来



#### 2. pom 文件

Project Object Model 项目对象模型。Maven 把一个项目的结构和内容抽象成一个模型，在 xml 文件中

进行声明，以方便进行构建和描述，pom.xml 是 Maven 的灵魂。所以，maven 环境搭建好之后，所有的学习和

操作都是关于 pom.xml 的。

**常用标签**

* 基本信息：
  * `modelVersion`：Maven 模型的版本，对于 Maven2 和 Maven3 来说，它只能是 4.0.0。
  * `groupId`：组织 id，一般是公司域名的倒写。
  * `artifactId `：项目名称，也是模块名称，对应 groupId 中 项目中的子项目。
  * `version`：项目的版本号。
  * `packaging `：项目打包的类型，可以使 jar、war、rar、ear、pom，默认是 jar。
* 依赖：
  * `dependencies 和 dependency`：在 Maven 中，项目需要使用到的 jar 包就被称为依赖，使用标签 dependency 来配置。而这种依赖的配置正是通过坐标（groupId，artifactId 和 version 作为定位标）来定位的。

* 配置属性：
  * `properties`：properties 是 用 来 定 义 一 些 配 置 属 性 的 ， 例 如 project.build.sourceEncoding（项目构建源码编码方式），可以设置为 UTF-8，防止中文乱码，也可定义相关构建版本号，便于日后统一升级。
* 构建：
  * `build`：build 表示与构建相关的配置，例如设置编译插件的 jdk 版本。

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!-- Maven 模型的版本 -->  
  <modelVersion>4.0.0</modelVersion>

  <!-- 组织 Id -->  
  <groupId>cn.yechen</groupId>
  <!-- 项目名称 -->
  <artifactId>smbms</artifactId>
  <!-- 项目版本 -->  
  <version>1.0-SNAPSHOT</version>
  <!-- 项目打包类型 -->
  <packaging>war</packaging>

  <!-- 配置属性 --> 
  <properties>
    <!-- 使用 UTF-8 进行编码 -->  
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!-- 编译使用的 JDK 版本 -->  
    <maven.compiler.source>1.8</maven.compiler.source>
    <!-- 运行使用的 JDK 版本 -->  
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <!-- 依赖 -->  
  <dependencies>
    <!-- servlet依赖 -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <!-- 构建 -->  
  <build>
    <finalName>smbms</finalName>
    <pluginManagement>
      <!-- 插件 -->  
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

#### 3. 坐标

#### 4. 依赖管理

#### 5. 仓库

#### 6. 生命周期

#### 7. 插件

### 三、Maven 在 IDEA 中应用

##### 创建一个 MavenWeb（使用模板的） 项目

![image-20210201214810205](https://i.loli.net/2021/02/01/VTo4xOESeiwUuNL.png)

![image-20210201215025855](https://i.loli.net/2021/02/01/RGDgMYQBr4VouXE.png)

![image-20210201215634720](https://i.loli.net/2021/02/01/Thk1Kv8LHOYn9dr.png)

![image-20210201215854686](https://i.loli.net/2021/02/01/pU5dXJsaKCQFjTV.png)

最后设置完点 finish

![image-20210201220028700](https://i.loli.net/2021/02/01/VGHRqLf1ID8ZWlE.png)

等待项目构建成功

![image-20210201220512686](https://i.loli.net/2021/02/01/3bcaLPsJtNhMGde.png)

观察 Maven仓库中多了那些东西

IDEA中的 Maven 设置

**注意：IDEA项目创建成功之后，看一眼 Maven 的配置**

![image-20210201221514502](https://i.loli.net/2021/02/01/xozmckFMIfnuGR6.png)

![image-20210201221836454](https://i.loli.net/2021/02/01/246tMWUFkYBimbC.png)

到这里，Maven 在 IDEA 中的配置就基本 OK 了！



##### 创建一个普通的 Maven 项目（不勾模板）

![image-20210201222451893](https://i.loli.net/2021/02/01/FfMi48Zsmaur1xL.png)

**这是干净的 Maven 项目**

![image-20210201225642870](https://i.loli.net/2021/02/01/7yYhXMZpEJUQb42.png)

这个只有在 Web 应用下才会有！

![image-20210201225857449](https://i.loli.net/2021/02/01/x7e623hbl9pw8uX.png)



##### 标记文件夹功能

**第一种**

![20210201232103845.png](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/20210201232103845.png)

![20210201232103900.png](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/20210201232103900.png)

第二种

![20210201232407953.png](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/20210201232407953.png)

![20210201232821875.png](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/20210201232821875.png)



##### IDEA的骚操作（查看依赖jar包关系图）

![image-20210202145756356](C:/Users/30117/AppData/Roaming/Typora/typora-user-images/20210202145820296.png)

### 四、Maven 的依赖管理

### 五、Maven 的常用设置
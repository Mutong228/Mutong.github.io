---
title: Maven
date: 
tags:
	- Maven
categories:
	- [Maven]
---

# Maven学习笔记

## Maven基础

**概念**

Maven是一个项目管理工具，它包含了一个项目对象模型（POM：Project Object Model），一组标准集合，一个项目生命瘦子（Project Lifecycle），一个依赖管理系统（Dependency Management System），和用来运行定义在生命周期阶段（phase）中插件（plugin）目标（goal）的逻辑。

**功能**

帮助程序员构建工程，管理jar报，编译代码，自动运行单元测试，打包，生成报表，以及部署项目，生成Web站点。

Maven本地仓库介绍：

- 本地仓库：

  用来存储从远程仓库或中央仓库下载的插件和jar包，项目使用一些插件或jar包，优先从本地仓库查找

- 远程仓库：

  如果本地需要插件或jar包，本地仓库没有，默认是从远程仓库下载。远程仓库可以在互联网内，也可以子啊局域网内。

- 中央仓库：

  在maven软件中内置一个远程仓库地址：`http://repo1.maven.org/maven2`，它是中央仓库，服务与整个互联网，它是由Maven团队自己维护，里面存储了非常全的jar包，它包含了世界上大部分流行的开源项目构件。但是由于在国外，下载速度慢，不利于使用，可改为使用国内公司架设的远程仓库。

**Maven目录结构：**

- src 源码
  - main：主工程代码
    - java：主工程代码
    - resources：需要使用的配置文件
    - webapp：web项目的资源目录（jap/html/WEB-INF），有web项目时存在
  - test：测试目录
    - java：测试代码
    - resources：测试需要使用的配置文件
- pom.xml：项目和核心配置文件

**常用命令：**

- compile：编译，将 src/main/java 下的文件编译为 class 文件输出到 target 目录下
- clean：清理，执行 clean会删除 target 目录及内容
- package：打包，对于 java 工程执行package打成 jar 包，对于web工程打成war 包
- install：安装，执行 install 将maven打成 jar 包或war 包发布到本地仓库
- 注意：当后面的命令执行时，前面的操作过程也都会自动执行

**Maven的生命周期**

- Clean：在进行真正的构建之前进行一些清理工作
- 核心构建：编译、测试、打包、部署等等
- 站点发布

**Maven坐标**
概念：被Maven管理的资源的唯一标识

- groupid：组织名称
- artifactid：模块名称
- version：版本号

坐标搜索：[Maven Repository](https://mvnrepository.com/)

**依赖的范围**

项目依赖某个包，需要在pom.xml中添加包的坐标，而且要指定依赖范围`<scope></scope>`

| **依赖范围** | **对编译有效** | **对测试有效** | **对运行时有效** |        **示例**         |
| :----------: | :------------: | :------------: | :--------------: | :---------------------: |
|   compile    |       ✔️        |       ✔️        |        ✔️         |       spring-core       |
|     test     |       -        |       ✔️        |        -         |          Junit          |
|   provided   |       ✔️        |       ✔️        |        -         |       servlet-api       |
|   runtime    |       -        |       ✔️        |        ✔️         |        JDBC驱动         |
|    system    |       ✔️        |       ✔️        |        -         | 本地Maven仓库之外的类库 |

依赖范围由强到弱的顺序是：compile > provided > runtime > test

使用方式：

- 默认引入 的 jar 包 ------- compile 【默认范围 可以不写】（编译、测试、运行都有效 ）
- servlet-api 、jsp-api ------- provided （编译、测试有效， 运行时无效防止和 tomcat 下 jar 包冲突）
- jdbc 驱动 jar 包 ---- runtime （测试、运行 有效 ）
- junit ----- test （测试有效）

## Maven进阶

### 1、分模块开发与设计

**意义：**
使得各个模块中仅包含当前模块对应的功能与配置文件，满足不同模块之间的共享的需求

**步骤**
	1、使用install指令将当前模块发布到本地仓库

​	2、需要依赖当前模块的模块通过导入当前模块的坐标进行使用

### 2、依赖管理

#### 1.依赖传递

依赖具有传递性，模块1依赖模块2，而模块2依赖模块3、4、5等模块，此时1抹开均可以使用这些依赖

- 直接依赖：在当前项目中通过依赖配置建立的依赖关系
- 简介依赖：被依赖的资源如果依赖其他资源，则当前项目间接依赖其他资源

**依赖传递冲突问题：**

- 路径优先：当依赖中出现了相同的资源时，层级越深，优先级越低，层级越浅，优先级越高
- 声明优先：当资源在相同层级被依赖时，配置顺序考前的覆盖配置顺序靠后的
- 特殊优先：当同级配置了相同资源的不同版本，后配置的覆盖先配置的，即后配置的优先级高

#### 2.可选依赖

可选依赖是隐藏当前工程所依赖的资源，隐藏后对应的资源不具有依赖传递性，即对外隐藏当前依赖的资源（不透明）

在对应资源的坐标中添加，true表示隐藏，false表示不隐藏

```xml
<optional>true</optional>
```

#### 3.排序依赖

排除依赖是指在当前引用的资源中将其中的某些依赖排除。在某些资源不可通过可选依赖进行隐藏时，可使用排除依赖，即主动断开依赖的资源，被排除的资源无需指定版本（不需要）

```xml
<exclusions>
    <exclusion>
        <groupId></groupId>
        <artifactId></artifactId>
    </exclusion>
</exclusions>

```

### 3、聚合

- 聚合：将多个模块组织成一个整体，同时对整个项目进行构建的过程称为聚合
- 聚合工程：通常是一个不具有业务功能的空工程（有且仅有一个pom文件）
- 作用：使用聚合工程可以将多个工程编组，通过对聚合工程进行构建，实现对所包含的模块进行同步构建
  - 当工程中的莫格模块更新时，必须保障工程中与已更新模块关联的模块同步更新，使用聚合工程可以解决批量模块同步构建的问题

**步骤**

​	1、创建聚合工程

​	2、指定聚合工程的打包方式

```xml
<packaging>pom</packaging>
```

​	3、设置所管理的模块名称

```xml
<modules>
    <!--配置各个模块的路径即可 如 ../maven-xxx -->
    <module></module>
</modules>
```

### 4、继承

**概念**
继承描述的是两个工程之间的关系，与Java中的继承类似，子工程可以继承父工程的配置信息，常见与依赖关系的继承

**作用**

- 简化配置
- 减少版本冲突

**配置**
在子工程中配置所继承的父工程

```xml
<parent>
	<groupId></groupId>
    <artifactId></artifactId>
    <version></version>
    <relativePath></relativePath><!--(可选配置)通过相对路径可以快速找到父工程 如：../maven-parent/pom.xml-->
</parent>

```



在父工程中配置可选的依赖

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
        	<groupId></groupId>
            <artifactId></artifactId>
            <version></version>
        </dependency>
    </dependencies>
</dependencyManagement>

```



在子工程中根据需要配置上述的可选依赖

```xml
<dependency>
    <groupId></groupId>
    <artifactId></artifactId>
</dependency>

```

**聚合与继承的区别**

- 作用：
  - 聚合用于快速构建项目
  - 继承用于快速配置
- 相同点
  - 打包方式均为pom
  - 均属于设计型模块，无实际模块内容
- 不同点
  - 聚合在当前模块中配置关系，可以感知参与聚合的模块有哪些
  - 继承在子模块中配置关系，父模块无法感知哪些子模块继承了自己

### 5、属性

通过配置属性对版本进行统一管理

```xml
<properties>
	<!--定义变量-->
    <spring.version>5.1.9.RELEASE</spring.version>
</properties>
<dependency>
    <groupId></groupId>
    <artifactId></artifactId>
    <version>${spring.version}</version>
</dependency>

```

**配置文件加载pom中的属性**
	1、自定义属性：

```xml
<properties>
    <jdbc.url>jdbc:mysql//.....</jdbc.url>
</properties>

```

​	2、配置文件中引用属性

```xml
jdbc.url=${jdbc.url}
```

​	3、开启资源文件目录加载属性的过滤器

```xml
<build>
    <resources>
        <resource>
            <!--使用内置属性${project.baseject}进行统一配置-->
            <directory>${project.basedir}/src/main/resources</directory>
            <!--开启-->
            <filter>true</filter>
        </resource>
    </resources>
</build>

```

​	4、配置maven打包war包时，可以使用以下配置忽略web.xml配置检查

```xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-war-plugin</artifactId>
    <version>3.2.3</version>
    <configuration>
        <failOnMissingWebXml>false</failOnMissingWebXml>
    </configuration>
</plugin>

```

**属性分类**
	1、自定义属性

​	2、内置属性：`${basedir}`、`${vesrsion}`等

​	3、Setting属性：`${settings.localRepository}`等

​	4、Java系统属性：`${user.home}`等

​	5、环境变量属性：`${env.JAVA_HOME}`等

### 6、版本管理

- 工程版本
  - SNAPSHOT(快照版本)
    - 项目开发工程中临时输出的版本，称为快照版本
    - 快照版本随着开发的进展不断更新
  - RELEASE(发布版本)
    - 项目开发到阶段里程碑后，向外部发布较为稳定的版本。此时版本所对应的构件文件相对稳定，即
    - 进行功能的后续开发，也不会改变当前发布版本内容，称为发布版本
- 发布版本
  - alpha版
  - beta版
  - 数字版

### 7、多环境开发配置

实际开发环境中，存在多种不同的环境如测试环境、生成环境等等，而maven提供配置多种环境的设定，帮助开发者使用工程中快速切换环境

```xml
<!--配置多环境-->
<profiles>
    <!--开发环境-->
    <profile>
        <id>env_dep</id>
        <properties>
            <jdbc.url>jdbc:mysql//.....1</jdbc.url>
        </properties>
        <!--设置为默认环境-->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--生产环境-->
     <profile>
        <id>env_pro</id>
        <properties>
            <jdbc.url>jdbc:mysql//.....2</jdbc.url>
        </properties>
    </profile>
    <!--测试环境-->
    <profile>
        <id>env_test</id>
        <properties>
            <jdbc.url>jdbc:mysql//.....3</jdbc.url>
        </properties>
    </profile>
</profiles>

```

**指定环境**

```xml
mvn install(生命周期指令) -P id(环境id)
```

### 8、跳过测试

在存在开发功能更新中且未开发完毕或者需要快速打包等等情况下，常常需要跳过测试。

**使用**
	1、点击闪电按钮开启全局跳过

​	2、细粒度控制跳过测试，使用和指定包含和排除

```xml
<build>
    <plugins>
        <plugin>
            <!--测试插件-->
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.xxxx</version>
            <configuration>
                <!--整体跳过-->
                <skipTest>true</skipTest>
                <!-- 配置排除部分不参与测试的内容
				整体不跳过:
				<skipTest>false</skipTest>
				排除内容:
				<excludes>
					<exclude>**/xxxTest.java</exclude>
				</excludes>
-->
            </configuration>
        </plugin>
    </plugins>
</build>
```

3、使用指定

```xml
mvn package(生命周期指令) -D skipTests
```

### 9、私服

#### 1.简介

私服是一台独立的服务器，用于解决团队内部的资源共享和资源同步问题。

Nexus，一款maven私服产品，下载：https://help.sonatype.com/repomanager3/product-information/download

**安装与启动**

- 启动服务器（命令行启动）：nexus.exe /run nexus
- 访问服务器（默认端口：8081）：http://localhost:8081
- 修改基础配置信息
  - etc/nexus-default.properties 文件中保存nexus的基础配置信息，包括默认端口
- 修改服务器运行配置信息
  - bin/nexus.vmoptions 文件中保存nexus服务器启动对应的配置信息，如默认占用内存空间

#### 2.仓库分类

| **仓库类别** | **英文** |        **功能**         | **关联操作** |
| :----------: | :------: | :---------------------: | :----------: |
|   宿主仓库   |  hosted  | 保存自主研发+第三方资源 |     上传     |
|   代理仓库   |  proxy   |    代理连接中央仓库     |     下载     |
|    仓库组    |  group   | 为仓库编组简化下载操作  |     下载     |

- 宿主仓库：保存无法从中央仓库获取的资源
  - 自主研发资源
  - 第三方非开源资源
- 代理仓库：代理远程仓库，通过nexus访问其他公共仓库
- 仓库组：将若干仓库设计成一个组，简化配置
  - 不用于保存资料，属于设计型仓库

#### 3.资源上传与下载

**配置**

- 配置本地仓库访问私服权限

```xml
<!--私服的访问权限-->
<server>
  <id>zyl-snapshot</id>
  <username>admin</username>
  <password>admin</password>
</server>
<server>
  <id>zyl-release</id>
  <username>admin</username>
  <password>admin</password>
</server>
```

- 配置本地仓库访问私服的路径

```xml
<!--私服的访问路径-->
<mirror>
  <id>maven-public</id>
  <mirrorOf>*</mirrorOf>
  <url>http://localhost:8081/repository/maven-public/</url>
</mirror>
```



- 在pom.xml配置当前项目访问私服上次资源的保存位置

```xml
<distributionManagement> 
    <repository> 
        <id>zyl-release</id> 
        <url>http://localhost:8081/repository/zyl-release/</url>      
 	</repository> 
    <snapshotRepository> 
        <id>zyl-snapshot</id> 
        <url>http://localhost:8081/repository/zyl-snapshot/</url>
	</snapshotRepository>
</distributionManagement>
```

- 资源上传 ：deploy指定

（注：本文参考https://blog.csdn.net/L1ghtn1nggggg/article/details/124437648）

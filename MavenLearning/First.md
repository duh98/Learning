# Maven简介及快速入门

## 一、*Maven*的介绍
    Maven就是一个软件，需要掌握软件安装、配置、以及基本功能（项目构建、依赖管理 ）使用。
## 二、依赖管理
    Maven 可以管理项目的依赖，包括自动下载所需依赖库、自动下载依赖需要的依赖并且保证版本没有冲突、依赖版本管理等。通过 Maven，我们可以方便地维护项目所依赖的外部库，而我们仅仅需要编写POM文件进行配置。
## 三、构建管理
    项目构建是指将源代码、配置文件、资源文件等转化为能够运行或部署的应用程序或库的过程。Maven 可以管理项目的编译、测试、打包、部署等构建过程。通过实现标准的构建生命周期，Maven 可以确保每一个构建过程都遵循同样的规则和最佳实践。同时，Maven 的插件机制也使得开发者可以对构建过程进行扩展和定制。主动触发构建，只需要简单的命令操作即可。
![Maven的构建过程\生命周期](/MavenLearning/img/image.png)
## 四、*Maven*的配置

- 配置文件
    - maven/conf/settings.xml，主要修改的有三个配置：1.依赖本地缓存位置（本地仓库位置）2.maven下载镜像3.maven选用编译项目的jdk版本。
- 配置本地仓库地址
---
    <!-- localRepository
     The path to the local repository maven will use to store artifacts.
    
     Default: ${user.home}/.m2/repository
    <localRepository>/path/to/local/repo</localRepository>
    -->
    <!-- conf/settings.xml 55行 -->
    <localRepository>D:\repository(自己的仓库地址)</localRepository>
---
- 配置国内阿里镜像
---
    <!--在mirrors节点(标签)下添加中央仓库镜像 160行附近-->
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
---
- 配置jdk版本项目构建
---
        <!--在profiles节点(标签)下添加jdk编译版本 268行附近-->
    <profile>
        <id>jdk-17</id>
        <activation>
        <activeByDefault>true</activeByDefault>
        <jdk>17</jdk>
        </activation>
        <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <maven.compiler.compilerVersion>17</maven.compiler.compilerVersion>
        </properties>
    </profile>
---

- 编译器配置本地maven

![Maven的构建过程\生命周期](/MavenLearning/img/maven配置.png)

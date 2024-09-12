# 基于IDEA的Maven工程创建

## *Maven*的GAVP属性介绍

- GroupID 格式
    
    com.{公司/BU }.业务线.[子业务线]，最多 4 级。

- ArtifactID 格式

    产品线名-模块名。语义不重复不遗漏。

- Version版本号格式推荐

    - 主版本号：当做了不兼容的 API 修改，或者增加了能改、改变产品方向的新功能。
    - 次版本号：当做了向下兼容的功能性新增（新增类、接口等）。
    - 修订号：修复 bug，没有修改方法签名的功能加强，保持 API 兼容性。
    - 例如： 初始→1.0.0  修改bug → 1.0.1  功能调整 → 1.1.1等

- Packaging定义规则

    ***指示将项目打包为什么类型的文件，idea根据packaging值，识别maven项目类型！***
    
    packaging 属性为 *jar*（默认值），代表普通的Java工程，打包以后是.jar结尾的文件。
    
    packaging 属性为 *war*，代表Java的web工程，打包以后.war结尾的文件。

    packaging 属性为 *pom*，代表不会打包，用来做继承的父工程。

- *Maven*工程结构

    ![Maven结构图](/MavenLearning/img/maven工程结构.png)

    - pom.xml：Maven 项目管理文件，用于描述项目的依赖和构建配置等信息。
    - src/main/java：存放项目的 Java 源代码。
    - src/main/resources：存放项目的资源文件，如配置文件、静态资源等。
    - src/main/webapp/WEB-INF：存放 Web 应用的配置文件。
    - src/main/webapp/index.html：Web 应用的入口页面。
    - src/test/java：存放项目的测试代码。
    - src/test/resources：存放测试相关的资源文件，如测试配置文件等。


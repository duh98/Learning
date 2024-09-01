# Maven的核心功能

## 依赖管理
    Maven 依赖管理是 Maven 软件中最重要的功能之一。Maven 的依赖管理能够帮助开发人员自动解决软件包依赖问题，使得开发人员能够轻松地将其他开发人员开发的模块或第三方框架集成到自己的应用程序或模块中，避免出现版本冲突和依赖缺失等问题。
  
***重点: 编写pom.xml文件!***    
### pom文件的配置
- 项目基础信息属性的配置
    ---
        <!-- 模型版本 -->
        <modelVersion>4.0.0</modelVersion>
        <!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成， 如com.companyname.project-group，maven会将该项目打成的jar包放本地路径：/com/companyname/project-group -->
        <groupId>com.companyname.project-group</groupId>
        <!-- 项目的唯一ID，一个groupId下面可能多个项目，就是靠artifactId来区分的 -->
        <artifactId>project</artifactId>
        <!-- 版本号 -->
        <version>1.0.0</version>

        <!--打包方式
            默认：jar
            jar指的是普通的java项目打包方式！ 项目打成jar包！
            war指的是web项目打包方式！项目打成war包！
            pom不会讲项目打包！这个项目作为父工程，被其他工程聚合或者继承！后面会讲解两个概念
        -->
        <packaging>jar/pom/war</packaging>
    ---
- 依赖管理和添加
    ---
            <!-- 
        通过编写依赖jar包的gav必要属性，引入第三方依赖！
        scope属性是可选的，可以指定依赖生效范围！
        依赖信息查询方式：
            1. maven仓库信息官网 https://mvnrepository.com/
            2. mavensearch插件搜索
        -->
        <dependencies>
            <!-- 引入具体的依赖包 -->
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.17</version>
                <!--
                    生效范围
                    - compile ：main目录 test目录  打包打包 [默认]
                    - provided：main目录 test目录  Servlet
                    - runtime： 打包运行           MySQL
                    - test:    test目录           junit
                -->
                <scope>runtime</scope>
            </dependency>

        </dependencies>
    ---
    
- 依赖管理和添加
    ---
        <!--声明版本-->
        <properties>
        <!--命名随便,内部制定版本号即可！-->
        <junit.version>4.11</junit.version>
        <!-- 也可以通过 maven规定的固定的key，配置maven的参数！如下配置编码格式！-->
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        </properties>

        <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <!--引用properties声明版本 -->
            <version>${junit.version}</version>
        </dependency>
        </dependencies>
    ---
### 依赖传递和冲突
- 减少重复依赖：当多个项目依赖同一个库时，Maven 可以自动下载并且只下载一次该库。这样可以减少项目的构建时间和磁盘空间。
- 自动管理依赖: Maven 可以自动管理依赖项，使用依赖传递，简化了依赖项的管理，使项目构建更加可靠和一致。
- 确保依赖版本正确性：通过依赖传递的依赖，之间都不会存在版本兼容性问题，确实依赖的版本正确性！

### 解决依赖冲突（如何选择重复依赖）方式
- 短路优先原则（第一原则）
- 依赖路径长度相同情况下，则“先声明优先”

### 依赖导入失败解决方案
- 检查网络连接和 Maven 仓库服务器状态。
- 确保依赖项的版本号与项目对应的版本号匹配，并检查 POM 文件中的依赖项是否正确。
- 清除本地 Maven 仓库缓存（lastUpdated 文件），因为只要存在lastupdated缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的gav属性依次向下查找文件夹，最终删除内部的文件，刷新重新下载即可！

### 删除脚本
---
    使用记事本打开
    set REPOSITORY_PATH=D:\repository  改成你本地仓库地址即可！
    点击运行脚本，即可自动清理本地错误缓存文件！！
---

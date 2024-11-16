# Spring核心之控制反转

## 基础点
---
- Spring框架管理这些Bean的创建工作，即由用户管理Bean转变为框架管理Bean，这个就叫控制反转 - Inversion of Control (IoC)Spring 框架托管创建的Bean放在哪里呢？ 这便是IoC Container;Spring 
- 框架为了更好让用户配置Bean，必然会引入不同方式来配置Bean？ 这便是xml配置，Java配置，注解配置等支持Spring 
- 框架既然接管了Bean的生成，必然需要管理整个Bean的生命周期等；
- 应用程序代码从Ioc Container中获取依赖的Bean，注入到应用程序中，这个过程叫 依赖注入(Dependency Injection，DI) ； 所以说控制反转是通过依赖注入实现的，其实它们是同一个概念的不同角度描述。通俗来说就是IoC是设计思想，DI是实现方式
- 在依赖注入时，有哪些方式呢？这就是构造器方式，@Autowired, @Resource, @Qualifier... 同时Bean之间存在依赖（可能存在先后顺序问题，以及循环依赖问题等）
---
## Spring Bean是什么

    Spring里面的bean就类似是定义的一个组件，而这个组件的作用就是实现某个功能的，这里所定义的bean就相当于给了你一个更为简便的方法来调用这个组件去实现你要完成的功能。

## Ioc是什么
    Ioc是一种设计思想，不是具体技术。在Java开发中，Ioc意味着将你设计好的对象交给容器控制，而不是传统的在你的对象内部直接控制。

![原始调用](/spring/img/spring-framework-ioc-1.png)
![ioc调用](/spring/img/spring-framework-ioc-2.png)

## IOC配置的三种方式

### xml配置
    将bean的信息配置.xml文件里，通过Spring加载文件为我们创建bean。
    - 优点： 可以使用于任何场景，结构清晰，通俗易懂
    - 缺点： 配置繁琐，不易维护，枯燥无味，扩展性差

![xml配置](/Spring/img/img006.webp)
---
    <!-- 实验一 [重要]创建bean -->
    <bean id="happyComponent" class="com.atguigu.ioc.HappyComponent"/>
---
    - bean标签：通过配置bean标签告诉IOC容器需要创建对象的组件信息
    - id属性：bean的唯一标识,方便后期获取Bean！
    - class属性：组件类的全限定符！
    - 注意：要求当前组件类必须包含无参数构造函数！

#### 构造函数注入
---
    <!-- 场景1: 多参数，可以按照相应构造函数的顺序注入数据 -->
    <beans>
    <bean id="userService" class="x.y.UserService">
        <!-- value直接注入基本类型值 -->
        <constructor-arg  value="18"/>
        <constructor-arg  value="赵伟风"/>
        
        <constructor-arg  ref="userDao"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
    </beans>


    <!-- 场景2: 多参数，可以按照相应构造函数的名称注入数据 -->
    <beans>
    <bean id="userService" class="x.y.UserService">
        <!-- value直接注入基本类型值 -->
        <constructor-arg name="name" value="赵伟风"/>
        <constructor-arg name="userDao" ref="userDao"/>
        <constructor-arg name="age"  value="18"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
    </beans>

    <!-- 场景2: 多参数，可以按照相应构造函数的角标注入数据 
            index从0开始 构造函数(0,1,2....)
    -->
    <beans>
        <bean id="userService" class="x.y.UserService">
        <!-- value直接注入基本类型值 -->
        <constructor-arg index="1" value="赵伟风"/>
        <constructor-arg index="2" ref="userDao"/>
        <constructor-arg index="0"  value="18"/>
    </bean>
    <!-- 被引用类bean声明 -->
    <bean id="userDao" class="x.y.UserDao"/>
    </beans>
---
#### Setter方法注入
---
    <bean id="simpleMovieLister" class="examples.SimpleMovieLister">
    <!-- setter方法，注入movieFinder对象的标识id
        name = 属性名  ref = 引用bean的id值
    -->
    <property name="movieFinder" ref="movieFinder" />

    <!-- setter方法，注入基本数据类型movieName
        name = 属性名 value= 基本类型值
    -->
    <property name="movieName" value="消失的她"/>
    </bean>

    <bean id="movieFinder" class="examples.MovieFinder"/>

---

### 注解配置
|注解|作用|
|-|-|
|@Component|该注解用于描述 Spring 中的 Bean，它是一个泛化的概念，仅仅表示容器中的一个组件（Bean），并且可以作用在应用的任何层次，例如 Service 层、Dao 层等。 使用时只需将该注解标注在相应类上即可。|
|@Repository|该注解用于将数据访问层（Dao 层）的类标识为 Spring 中的 Bean，其功能与 @Component 相同。|
|@Service|该注解通常作用在业务层（Service 层），用于将业务层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。|
|@Controller|该注解通常作用在控制层（如SpringMVC 的 Controller），用于将控制层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。|

#### 注解方式使用步骤

- 1.基本扫描配置

    ---
        <!-- 配置自动扫描的包 -->
        <!-- 1.包要精准,提高性能!
            2.会扫描指定的包和子包内容
            3.多个包可以使用,分割 例如: com.atguigu.controller,com.atguigu.service等
        -->
        <context:component-scan base-package="com.atguigu.components"/>
    ---
- 2.为bean组件设置id
    ---
        //类名首字母小写就是 bean 的 id。例如：SoldierController 类对应的 bean 的 id 就是 soldierController。也可以指定。
        @Controller(value = "soldierController")
        public class SoldierController {
        }
    ---


## Ioc和DI的关系
    控制反转是通过依赖注入实现的，其实它们是同一个概念的不同角度描述。通俗来说就是IoC是设计思想，DI是实现方式。

# DI的三种方式
    常用的注入方式主要有三种：构造方法注入（Construct注入），setter注入，基于注解的注入（接口注入）

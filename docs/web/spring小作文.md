spring小作文

# 1.总：

Spring是一个轻量级的**控制反转(IoC)**和**面向切面(AOP)**的**容器**（bean容、框架）。

Spring负责：

- 管理bean的**生命周期**（负责创建和销毁这些bean）
- 负责调度bean来提供服务
- 维护和管理多个bean之间的关系

# 2.分：

## 特性：IOC（DI）和AOP

#### "控制反转"IOC：

就是对组件对象`控制权的转移`，从程序代码本⾝转移到了外部容器，由`spring容器`来创建 对象并管理对象之间的依赖关系。

`DI`是对IoC更准确的描述，即组件之间的依赖关系由容器在运⾏期决定，形象的来说，即由容器动态 的将`某种依赖关系`注⼊到`组件`之中。

#### DI的**实现方式**

可以通过setter⽅法注⼊（设值注⼊）、构造器注⼊和接⼝注⼊三种⽅式来实现

#### AOP

```xml
 <!--配置事务管理器：由于MyBatisPlus是基于JDBC来管理事务的，因此Spring已经提供了一个现成的实现类-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="ds"/>
    </bean>
 <!--配置切面：切点(where) + 执行什么样的切面逻辑(do what)-->
    <aop:config>
        <!--配置通知者-->
        <aop:advisor advice-ref="advice1" pointcut="execution(* com.example.service..*Service.*(..))"/>
    </aop:config>

    <!--开启事务注解-->
    <tx:annotation-driven transaction-manager="transactionManager"/>
```

1.Aop是什么，有什么作用

通过切面的方式实现对功能的扩展（模板方法），支持将一些通用的任务进行集中式的管理，例如:安全，事务，日志等，从而使代码能更好的复用。

2.你如何理解AOP中的连接点(Joinpoint)、切点(Pointcut)、增强(Advice)、引介(Introduction一种特殊的增强)、织入(Weaving) 、切面(Aspect（切点和增强组成的）)这些概念?

切点(Pointcut):如果连接点相当于数据中的记录，那么切点相当于查询条件

增强可以是前置增强、后置增强、返回后增强、抛异常时增强和包围型增强。

**3.实现AOP的技术**，主要分为两大类:（代理模式）
静态代理–指使用AOP框架提供的命令进行编译，从而在编译阶段就可生成AOP代理类，因此也称为编译时增强;
动态代理–在运行时在内存中“临时"生成AOP动态代理类，因此也被称为运行时增强。JDK动态代理、CGLIB

## 其他

1.事务

常使用的是声明式事务管理:事务管理与业务代码分离。仅使用注解或基于XML的配置来管理事务。

Spring的事务传播行为：
PROPAGATION(蔓延、传播、传输)

如果当前没有事务，就新建一个事务，如果已经存在一个事务
PROPAGATION_REQUIRED
中，加入到这个事务中。这是默认的事务传播行为
PROPAGATION_SUPPORTS
支持当前事务，如果当前没有事务，就以非事务方式执行。

bean 的⽣命周期主要有以下⼏个阶段

1、Spring容器根据配置中的 bean定义中实例化 bean。
2、Spring使用依赖注入填充所有属性，如 bean中所定义的配置。
3、如果bean实现BeanNameAware接口，则工厂通过传递bean 的 ID来调用setBeanName()。
4、如果bean实现 BeanFactoryAware接口，工厂通过传递自身的实例来调用setBeanFactory()。
5、如果存在与 bean关联的任何 BeanPostProcessors,则调用preProcessBeforelnitialization()方法。
6、如果为 bean指定了init方法 ( <bean>的init-method 属性），那么将调用它。
7、最后，如果存在与 bean关联的任何 BeanPostProcessors ，则将调用postProcessAfterInitialization()方法。
8、如果 bean实现 DisposableBean接口，当spring容器关闭时，会调用destory()。
9、如果为 bean指定了destroy方法 ( <bean>的 destroy-method 属性），那么将调用它。

SpringMVC工作流程：
1、用户发送请求至前端控制器DispatcherServlet
2、DispatcherServlet收到请求调用HandlerMapping 处理器映射器。
3、处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果则生成)一并返回给DispatcherServlet。
4、DispatcherServlet通过HandlerAdapter 处理器适配器调用处理器5、执行处理器(Controller，也叫后端控制器)。
6、Controller执行完成返回ModelAndView
7、HandlerAdapter将controller执行结果 ModeIAndview返回给DispatcherServlet8、DispatcherServlet 将 ModelAndView传给ViewReslover视图解析器
9、ViewReslover解析后返回具体View
10、DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）。11、DispatcherServlet响应用户



Spring的重要注解：
@Controller- 用于Spring MVC项目中的控制器类。service -用于服务类。
RequestMapping -用于在控制器处理程序方法中配置URI映射。
@ResponseBody-用于发送Object作为响应,通常用于发送XML或JSON数据作为响应。PathVariable -用于将动态值从 URI映射到处理程序方法参数。
Autowired-用于在 spring bean中自动装配依赖项。

@Qualifier-使用@Autowired 注解，以避免在存在多个bean类型实例时出现混淆。@Scope-用于配置spring bean的范围。
@Configuration，@ComponentScan和 @Bean -用于基于java 的配置。@Aspect，@Before，@After，@Around，@Pointcut-用于切面编程（AOP）。

Spring 的事务隔离级别

底层其实是**基于数据库**的，Spring 并没有⾃⼰的⼀套隔离级别。DEFAULT：使⽤数据库的默认隔离级别。 

READ_UNCOMMITTED：读未提交，最低的隔离级别，会读取到其他事务还未提交的内容，存在脏 

读。

READ_COMMITTED：读已提交，读取到的内容都是已经提交的，可以解决脏读，但是存在不可重复 

读。

REPEATABLE_READ：可重复读，在⼀个事务中多次读取时看到相同的内容，可以解决不可重复读， 

但是存在幻读。 

SERIALIZABLE：串⾏化，最⾼的隔离级别，对于同⼀⾏记录，写会加写锁，读会加读锁。在这种情 

况下，只有读读能并发执⾏，其他并⾏的读写、写读、写写操作都是冲突的，需要串⾏执⾏。可以防 

⽌脏读、不可重复度、幻读，没有并发事务问题。 
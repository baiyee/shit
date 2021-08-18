
## Spring总结

### 0.什么是Spring？
Spring是java企业级应用的开源开发框架。主要用来开发Java应用，Web应用。主要宗旨用于简化Java企业级开发，通过POJO为基础的编程模型促进良好编程习惯。

### 1.为什么要使用 Spring？Spring的好处在哪里？
• 轻量：Spring是轻量级，基本版本大约2MB左右大小。
• 非侵入：基于Spring框架开发应用中的对象，可以不依赖Spring Api。
• 控制反转：Spring通过IoC控制反转实现了控制反转，交给容器去进行创建对象，不需要关心对象的创建过程。
• 依赖注入：DI Dependency Injection 创建对象中依赖的对象不需要手动的方法去设置，而是通过配置赋值。
• 面向切面编程：AOP Aspect Oriented Program 把核心业务和周边业务区分开，独立开发，通过动态代理进行耦合，实现了真正面向接口编程。
• Web MVC框架：Spring Web框架能够很好的实现业务的解耦
• 事务处理：Spring提供了一个持续的事务管理接口，可以扩展至上至本地事务，下至全局事务(JTA)
• 异常处理：Spring提供方便的API把具体技术相关的异常(JDBC,Hibernate,JDO抛出异常)转化为一致的uncheck非检查异常。

### 2.AOP是什么？
AOP是Aspect Oriented Program 面吐切面编程，首先在面向切面编程思想中，把功能分为核心业务功能和周边业务功能，分别独立开发。
核心业务功能：添加数据，修改数据，登录注册。周边业务功能：性能统计、日志、事务管理。周边业务功能在Spring AOP思想中被定义成切面。
把切面和核心业务功能编制在一起叫做AOP。

### 3.IoC是什么？
IoC是Inversion of Control 控制反转。核心思想是利用工厂模式，设置一个对象的容器，把对象的创建，依赖的管理，生命周期的管理交给容器来完成。
当我们需要一个对象A a时，通过容器Factory.get("A")的方式，从容器中拿A对象，至于在创建过程中还需要什么对象就不用我们操心。
使用接口时，我们只需要把接口的实现类放入到容器中，通过@Service @Controller等注解把类交给Spring容器管理。使用时通过@Autowired或其他注入方式，
从容器中注入接口对应的实现，这样就能实现真正的解耦，真正的面向接口编程。

### 4.Spring 有哪些主要模块？
• Core module
• Bean module
• Context module
• JDBC module
• ORM module
• Expression Language module
• OXM module
• Java Messaging Service(JMS) module
• Transaction module
• Web module
• Web-Servlet module
• Web-Struts module
• Web-Portlet module 

### 4.1Spring核心容器(应用上下文)模块
基于Bean的模块，提供核心功能，BeanFactory是Spring为基础的应用的核心。Spring框架建立在此模块之上，使Spring成为一个容器。

### 4.2BeanFactory实现举例
BeanFactory 是工厂模式的一种实现，提供了控制反转，应用配置和依赖从代码中隔离，最常见的实现是XmlBeanFactory类

### 4.3XmlBeanFactory类  
最常用的就是 org.springframework.beans.factory.xml.XmlBeanFactory，XmlBeanFactory是根据XML中定义的Beans，
该容器从XML文件中读取解析配置文件，并用它去创建一个完全配置的系统或应用。

### 4.4解释JDBC module 和 ORM module
通过JDBC模块和DAO模块保证数据库代码的简洁，避免数据库资源错误关闭导致的问题，它在各种不同的数据库错误信息之上，提供了统一的异常访问层。
利用Spring AOP和Spring 应用中的对象提供事务管理。

###4.5解释ORM module 
Spring通过提供ORM module，可以让我们在JDBC之上使用一个对象/关系映射(ORM)工具，比如集成Hibernate，JPA，Mybatis，SQL Maps

###4.6解析Web module 
Spring Web 是构建在application context模块基础之上的，提供一个适合web应用的上下文。

###4.7ApplicationContext常见的实现是什么？
• FileSystemXmlApplicationContext：容器从XML加载Bean，XML配置文件加载bean类需要配置全路径，并且构造方法不能私有化。
• ClassPathXmlApplicationContext：容器从XML加载Beans，Beans类路径需要配置全路径，不然bean加载时会找不到这个类。
• WebXmlApplicationContext：容器加载一个定义了Web应用的所有Bean。

###4.8 BeanFactory和ApplicationContext有什么区别？
BeanFactory和ApplicationContext都是Spring内的两大核心接口，都可以作为Spring容器。ApplicationContext是BeanFactory的子类。
BeanFactory：Spring最底层接口，包含各种bean定义，读取bean配置文件，bean加载实例化，控制bean的生命周期，维护bean直接的依赖关系。
ApplicationContext：bean的派生类，除了有bean的具有的功能外，还提供了更完整地框架功能：

###5.如何给 Spring 容器提供配置元数据?
1.基于XML配置，注解配置，java配置。

###6.怎么定义类的作用域？
Spring中 通过定义bean时的scope属性来定义bean的作用域，主要有singleton返回一个单例bean，protoType返回多例bean

###6.1Spring支持的几种bean作用域？
• singleton：bean在Spring IoC容器中只有一个实例（线程不安全的，可使用ThreadLocal来保证线程安全）
• protoType：一个bean可以有多个实例
• request：每次Http请求创建一个bean，bean的作用域仅在当前http请求内有效，请求结束，bean实例销毁。
• session：一次http session内有效，相同session请求 返回同一bean实例，不同session返回不同bean实例。相同Http请求 每次返回不同bean实例。
不同实例直接不共享属性，仅在请求内有效，请求结束，实例被销毁。
• global Session：全局HttpSession中，仅返回同一Bean实例，仅在portletContext 下有效

###6.2Spring 框架中的单例 bean 是线程安全的吗?
不是，因为多线程下，拿Controller举例。没有设置scope 默认singleton， 当其中有个变量 int a； a++；多线程访问这段代码每次都是不一样的， 
那么肯定会出现变量值错误的问题，可通过设置scope 为 prototype（中文 原型），但是这种情况也不一定线程安全，当int a 加上 static 修饰时，每次请求
返回值也会不同。

###7.解释Spring的生命周期？
• 实例化bean Instantiation 
• 属性赋值 Populate
• 初始化 initialization
• 销毁 Destruction
主要逻辑都在doCreate()方法中，1.createBeanInstance()实例化，2.populateBean()属性赋值，3.initializeBean()初始化 
4.销毁在容器关闭时调用详见ConfigurableApplicationContext#close()
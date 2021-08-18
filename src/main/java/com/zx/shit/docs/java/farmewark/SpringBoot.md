
## SpringBoot总结

### 1.什么是SpringBoot？
SpringBoot是建立在Spring框架之上，基于Spring启动，避免样板代码和配置。减少工作量的框架。

### 2.SpringBoot的核心配置文件是什么？
• bootstrap (.yml或.properties) 由父ApplicationContext加载，bootstrap优先加载
• application(. yml 或者 . properties)用于SpringBoot项目的自动化配置.

### 3.SpringBoot有哪些优点？
减少大量开发时间并提高生产力，避免编写大量样板代码，注释，和XML配置。SpringBoot应用程序与Spring生态系统
(Spring JDBC，Spring JPA，Spring ORM，Spring Data，Spring security)集成非常容易。
• 使用 Spring 项目引导页面可以在几秒构建一个项目方便对外输出各种形式的服务，如 REST API、WebSocket、Web、Streaming、Tasks
• 非常简洁的安全策略集成
• 支持关系数据库和非关系数据库
• 支持运行期内嵌容器，如 Tomcat、Jetty强大的开发包
• 支持热启动
• 自动管理依赖
• 自带应用监控
• 支持各种 IED，如 IntelliJ IDEA 、NetBeans
• 缺点是集成度过高，不太容易了解底层。
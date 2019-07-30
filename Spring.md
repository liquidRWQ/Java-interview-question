# Spring



## 说一说Spring的AOP



面向切面编程，在目标类的方法中动态加功能，就是以动态代理的思想实现类与类之间的解耦。 目标对象如果实现了接口，Spring就使用jdk的动态代理来生产代理类，如果目标对象继承了类，Spring就使用cglib的来生成代理类。

jdk的动态代理是用InvocationHandler的实现类来生成代理对象进行代理。反射获取代理类。

cglib的动态代理是用MethodInterceptor 的实现类来生成代理对象。调用getClass方法获取代理类







## 说一说Spring的IOC



控制反转，就是把程序需要的对象注入到一个容器中管理，从而实现类之间的解耦。



IOC的创建过程是

1. 创建BeanFactory Bean工厂对象
2. 使用Resouce对象读取配置类或xml配置文件中
3. 解析配置中的bean
4. 将bean注册到BeanFactory工厂中，以beanName为键，beanDefinition为值放到HashMap中（beanDefinitionMap）
5. 初始化bean。



Spring中bean的作用域有哪些？



1. singleton 单例

2. prototype 原型（多例）

3. requset 一次请求一个bean

4. session  一次会话一个bean

   





## Spring 中的单例 bean 的线程安全问题了解吗





使用ThreadLocal解决单例成员变量的线程安全问题

使用线程安全类





## Spring 中的 bean 生命周期



1. Ioc注册bean
2. ioc初始化bean，调用set方法
3. 如果bean'实现了Aware接口就调用相应的方法。
4. 调用前置处理方法
5. 调用bean的自定义初始化方法
6. 调用后置处理器方法。
7. ioc关闭，调用bean的销毁方法。



## 说一说SpringMVC的工作流程





1. 客户端发送请求到dispaterServlet
2. dispaterServlet调用HandlerMapping的方法解析url并找到指定了Handler
3. dispaterServlet调用HandlerAdapter区执行相应的Handler方法。
4. 方法处理完后返回一个ModelAndView对象
5. 再由视图解析器ViewResolver进行解析
6. 返回View视图对象给前端。





## SpringMVC用了哪些设计模式



工厂模式，  比如BeanFactory

代理模式  ，  AOP功能

单例模式      单例bean的创建

模板方法模式  Redis的模板操作类 RedisTemplate

适配器模式  HandlerAdapater

装饰者模式




### AOP基本概念

----

* 什么是AOP，AOP英语全名就是Aspect oriented programming，字面意思就是**面向切面编程** 

*  面向切面的编程是对面向对象编程的补充，面向对象的编程核心模块是类，然而在**AOP中核心模块是切面**。切面实现了多种类型和对象的模块化管理，比如事物的管理
*  **AOP是OOP的延续**，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。**利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率** 

#### 作用及优势

- 作用：
  在程序运行期间，不修改源码对已有方法进行增强。
- 优势
  减少重复代码
  提高开发效率
  维护方便

---

举例：那么现在我们有一个需求，想记录发送http请求的客户端IP以及请求接口信息，最简单的方法就是我们在每一个controller方法中调用一个打印相关信息的函数，这样会存在一个问题，有多少接口，我们就会调用多少次日志打印函数。那么有没有一种简单的方法可以实现日志的记录呢，有当然有，我们可以通过**Filter**或者**Interceptor**实现请求拦截功能，记录日志信息。那么该有人问什么是Filter、Interceptor，那它们和我们将要说的AOP有什么区别？

AOP使用的主要是**动态代理** ， 过滤器使用的主要是**函数回调**；拦截器使用是**反射机制** 。一个请求过来，先进行过滤器处理，看程序是否受理该请求 。 过滤器放过后 ， 程序中的拦截器进行处理 ，处理完后进入被 AOP动态代理重新编译过的主要业务类进行处理 

- Filter：和框架无关，过滤器拦截的是URL，可以控制最初的http请求，但是更细一点的类和方法控制不了
- Interceptor ：拦截器拦截的也是URL，拦截器有三个方法，相对于过滤器更加细致，有被拦截逻辑执行前、后进行操作等
- AOP : 面向切面拦截的是**类的元数据（包、类、方法名、参数等**） 相对于拦截器更加细致，而且非常灵活，拦截器只能针对URL做拦截，而**AOP针对具体的代码，能够实现更加复杂的业务逻辑**

 三者功能类似，但各有优势，从过滤器 -> 拦截器 -> 切面，拦截规则越来越细致，执行顺序依次是过滤器、拦截器、切面 

---

传统OOP流程图：

![1601381902774](C:\Users\14396\AppData\Roaming\Typora\typora-user-images\1601381902774.png)

运用AOP后：

![1601382148419](C:\Users\14396\AppData\Roaming\Typora\typora-user-images\1601382148419.png)



---

来看一下Spring官方提供的一些有关AOP的基本概念：

1. **通知（Advice）**: AOP 框架中的**增强处理**。通知描述了切面何时执行以及如何执行增强处理；通知类型，主要有以下几种：

- Before ：前置通知，在连接点方法前调用；对应Spring中@Before注解
- After ：后置通知，在连接点方法后调用；对应Spring中的@After注解
- AfterReturning：返回通知，在连接点方法执行并正常返回后调用，要求连接点方法在执行过程中没有发生异常；对应Spring中的@AfterReturning注解
- AfterThrowing：异常通知，当连接点方法异常时调用；对应Spring中的@AfterThrowing注解
- Around：环绕通知，它将覆盖原有方法，但是允许你通过反射调用原有方法；对应Spring中的@Around注解；

2. 连接点（Join Point）: 连接点表示应用执行过程中能够插入切面的一个点，这个点可以是方法的调用、异常的抛出。在 Spring AOP 中，连接点总是方法的调用，可以说目标对象中的方法就是一个连接点；

3. 切点（Pointcut）: 就是连接点的集合；对应Spring中的@Pointcut注解；

4. 切面（Aspect）: 切面是通知和切点的结合；对应Spring中的注解@Aspect修饰的一个类；

5. 目标对象（Target object）：即被代理的对象；

6. 代理对象（AOP proxy）：包含了目标对象的代码和增强后的代码的那个对象；

---


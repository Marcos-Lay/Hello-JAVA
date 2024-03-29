# SpringIOC:5.1.7RELEASE 源码解读
> 本文将带领你一行行的解读SpringIOC的源码，由于SpringIOC的代码非常庞大，因此想要快速的了解某个知识点，本文可能不适合。但是如果要深入了解SpirngIOC的内部原理，这篇文章就是以此目的而生的，由于作者也是一个JAVA初入者，本文可能讲解思想不是特别严谨，但是作为一个JAVA小白来阅读本篇文章，我相信我所讲解的过程将会是最符合JAVA初学者的学习步骤。
## 依赖
如果启动一个Spring容器，请使用 maven 的小伙伴直接在 dependencies 中加上以下依赖即可
<img src="https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Spring/spring-context.png">
## 配置加载入口
Spring源码如此庞大，从哪里作为突破口开始研究是非常重要的，很多人由于盲目的阅读导致效率不高，知识点不能得到有效的学习，因此找到合适的突破点对于学习SpringIOC有着事半功倍的作用。
<img src="https://github.com/Marcos-Lay/Hello-JAVA/blob/master/Docs/Spring/配置加载入口.png">
- A.ClassPathXmlApplicationContext 编译入口
```java
/**
 * @program: demo
 * @description:
 * @author: Marcos-Lay
 * @create: 2019-07-08 10:17
 **/
@RunWith(SpringJUnit4ClassRunner.class)
public class TestSpring {
    //加载单个配置文件
    @Test
    public void test1(){
        ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext1.xml");
    }
    //加载多个配置文件
    @Test
    public void test2(){
        ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("application.xml","application1.xml");
    }
    //加载配置文件，并指定是否加载上下文
    @Test
    public void test3(){
        String[] a = {"application.xml","application1.xml"};
        ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext(a,true);
    }
}
```
- B.FileSystemXmlApplication 文件系统的路径
```java
/**
 * @program: spring
 * @description: 测试FileSystemXmlApplicationContext
 * @author: Marcos-Lay
 * @create: 2019-08-01 15:27
 **/
@RunWith(SpringJUnit4ClassRunner.class)
public class TestFileSystemXmlApplicationContext {
    //使用了classpath作为前缀，这样FileSystemXmlApplicationContext就可以读到classpath的配置文件
    @Test
    public void test1(){
        FileSystemXmlApplicationContext fileSystemXmlApplicationContext = new FileSystemXmlApplicationContext("classpath：applicationContext.xml");
    }
    //加载多个配置文件,多个配置文件以逗号隔开
    @Test
    public void test2(){
        FileSystemXmlApplicationContext fileSystemXmlApplicationContext = new FileSystemXmlApplicationContext("classPath:application.xml","classPath:application1.xml");
    }
    //以String数组形式加载多个配置文件，并指定refresh
    @Test
    public void test3(){
        String[] a = {"",""};
        FileSystemXmlApplicationContext fileSystemXmlApplicationContext = new FileSystemXmlApplicationContext(a,false);
    }
}
```
- C.AnnotationConfigApplicationContext 通过注解配置入口
    - @Configuration,@Bean
## 对于WEB项目，Spring如何去寻找配置文件
> 这里有一个疑问，咱们这里以手动的方式去加载配置，那么Spring容器自身是怎么知道哪些是Spring的配置文件呢？

首先，对于一个Web项目来说，Spring不会去寻找Spring配置文件的，在Web项目中，自动加载的只有web.xml文件，如果想要加载其他的配置文件，需要在web.xml里去指定
```java
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>
        classpath:spring.xml,classpath:spring-mybatis.xml
    </param-value>
</context-param>

<listener>
    <listener-class>
        org.springframework.web.context.ContextLoaderListener
    </listener-class>
</listener>
```
由于context-param是可选项，因此如果没有指定对应配置文件的话，会默认加载名称叫做applicationContext.xml的文件，同时param-value中还可以指定别的配置文件，多个配置文件中间使用逗号分隔就可以了
## 介绍BeanFactory和ApplicationContext
在学习SpringIOC之前，先来介绍一下Spring中的几个重要的类，在接下来的学习当中都是围绕着这几个累进性的，因此在现在要着重介绍一下，有一个大致的印象。你也许听说过，Spring其实是作为一个容器，支持各种各样的组件来配合。而Spring的IOC是一个工厂（容器）来管理Bean，所以Spring的IOC中最重要的有两点，一个是创建 Bean 容器，一个是初始化 Bean。
- 创建Bean容器
最重要的类就是BeanFactory
- 初始化Bean
最重要的类就是ApplicationContext
## 实例化ApplicationContext
本文通过ClassPathXmlApplicationContext来作为入口实例化ApplicationContext，首先来写一个简单的例子，通过断点来对源码进行跟踪解读。
- 定义一个接口
```java
public interface TestMassage {

    String getMassage();
}
```
- 定义接口实现类
```java
/**
 * @program: spring
 * @description:
 * @author: Marcos-Lay
 * @create: 2019-08-01 15:53
 **/
public class TestMassageImpl implements TestMassage{

    public String getMassage() {
        return "hello SpringIOC";
    }
}
```
- 创建applicationContext配置文件，把接口装配成bean交给Spring管理
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    <bean id="testMassage" class="com.malei.TestMassageImpl"></bean>
    
</beans>
```
- 通过ClassPathXmlApplicationContext来启动ApplicationContext
```java
/**
 * @program: spring
 * @description: 启动ApplicationContext
 * @author: Marcos-Lay
 * @create: 2019-08-01 15:55
 **/
public class StartApplicationContext {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext classPathXmlApplicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        TestMassage bean = classPathXmlApplicationContext.getBean(TestMassage.class);
        System.out.println(bean.getMassage());
        //输出结果hello SpringIOC
    }
}
```
接下来我们通过断点调试来查看Spring如何通过ClassPathXmlApplicationContext来实例化ApplicationContext,这就是SpringIOC的核心


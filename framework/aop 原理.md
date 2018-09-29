# Spring AOP实现原理

## 1 AOP

AOP（Aspect Orient Programming），面向切面编程，作为面向对象编程的一种补充，用于处理系统中分布于各个模块的横切关注点，比如事务管理、日志、缓存等等。AOP实现的关键在于AOP框架自动创建的AOP代理，AOP代理主要分为静态代理和动态代理，静态代理的代表为AspectJ，动态代理则以Spring AOP为代表。

## 2 Spring AOP

Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理。JDK动态代理通过反射来接收被代理的类，并且要求被代理的类必须实现一个接口。JDK动态代理的核心是InvocationHandler接口和Proxy类。

如果目标类没有实现接口，那么Spring AOP会选择使用CGLIB来动态代理目标类。CGLIB（Code Generation Library）是一个代码生成的类库，可以在运行时动态生成某个类的子类，CGLIB是通过继承的方式做的动态代理，因此如果某个类被标记为final，那么它是无法使用CGLIB做动态代理的。

### 2.1 JDK动态代理

定义一个接口类：

```java
package org.java.base.springaop;

public interface Service {
    public void add();
    
    public void update();
}
```

实现接口类：

```java
package org.java.base.springaop

public class ServiceImpl implements Service {
    public void add() {
    	System.out.println("service add...");
    }
    
    public void update() {
    	System.out.println("service update...");
    }
}
```

实现动态代理类MyInvocationHandler，实现InvocationHandler接口：

```java
package org.java.base.springaop

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

public class MyInvocationHandler implements InvocationHandler {
    private Object target;
    
    MyInvocationHandler(Object target) {
        super();
        this.target = target;
    }
    
    public object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 程序执行前加入逻辑，MethodBeforeAdviceInterceptor
        System.out.println("before-----------------");
        // 程序执行
        Object result = method.invoke(target, args);
        // 程序执行后加入逻辑，MethodAfterAdviceInterceptor
        System.out.println("after------------------");
        return result;
    }
}
```

测试类：

```java
package org.java.base.springaop

import java.lang.reflect.Proxy;

public class Test {
    public static void main(String[] args) {
        Service aService = new ServiceImpl();
        MyInvocationHandler handler = new MyInvocationHandler(aService);
        // Proxy为InvocationHandler实现类动态创建一个符合某一接口的代理实例
        Service aServiceProxy = (Service) Proxy.newProxyInstance(aService.getClass().getClassLoader(), aService.getClass().getInterfaces(), handler);
        // 由动态生成的代理对象aServiceProxy代理执行程序，其中aServiceProxy符合Service接口
        aServiceProxy.add();
        System.out.println();
        aServiceProxy.update();
    }
}

// 输出
before-----------------
service add...
after------------------
    
before-----------------
service update...
after------------------
```

### 2.2 CGLIB动态代理

目标类，CGLIB不需要定义目标类的统一接口：

```java
package org.java.base.springaop

public class Base {
	System.out.println("add-----------");
}
```

实现动态代理类CglibProxy，需要实现MethodInterceptor接口，实现Intercept方法。该代理中在add方法前后加入了自定义的切面逻辑，目标类add方法执行语句为proxy.invokeSuper(object, args)。

```java
package org.java.base.springaop

import java.lang.reflect.Method
import org.springframework.cglib.proxy.MethodInterceptor;
import org.springframework.cglib.proxy.MethodProxy;

public class CglibProxy implements MethodInterceptor {
    public Object intercept(Object object, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        // 添加切面逻辑(advice)，此处是在目标类代码执行之前，即为MethodBeforeAdviceInterceptor
        System.out.println("before------------");
        // 执行目标类add方法
        proxy.invokeSuper(object, args);
        // 添加切面逻辑(advice)，此处是在目标类代码执行之后，即为MethodAfterAdviceInterceptor
        System.out.println("after-------------");
        return null;
    }
}
```

获取增强的目标类的工厂Factory，其中增强的方法类对象是由Enhancer来实现的：

```java
package org.java.base.springaop

import org.springframework.cglib.proxy.Enhancer;

public class Factory {
    public static Base getInstance(CglibProxy proxy) {
        Enhancer enhancer = new Enhancer();
        enhancer.setSuperclass(Base.class);
        // 回调方法的参数为代理类对象CglibProxy，最后增强目标类调用的是代理类对象CglibProxy中的Intercept方法
        enhancer.setCallback(proxy);
        // 此刻，base不是单纯的目标类，而是增强过的目标类
        Base base = (Base)enhancer.create();
        return base;
    }
}
```

测试类：

```java
package org.java.base.springaop;

public class Testcglib {
    public static void main(String[] args) {
        CglibProxy proxy = new CglibProxy();
        // base为生成的增强过的目标类
        Base base = Factory.getInstance(proxy);
        base.add();
    }
}

// 输出
before------------
add-----------
after-------------
```



## 3 总结

#### JDK动态代理（Dynamic Proxy）

基于标准JDK的动态代理功能

只针对实现了接口的业务对象

#### CGLIB

通过动态地对目标对象进行子类化来实现AOP代理

需要指定`@EnableAspectJAutoProxy(proxyTargetClass = true)`来强制使用

当业务对象没有实现任何接口的时候默认会选择CGLIB



##### 参考

1. [Spring AOP实现原理](https://juejin.im/post/5af3bd6f518825673954bf22#heading-4)
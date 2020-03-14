# 代理模式

代理模式分为：
静态代理
动态代理

### 真实类接口

```java
package demo02;

public interface UserService {
    void add();
    void update();
    void delete();
    void query();
}
```

### 真实类实现

```java
package demo02;

public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("Impl 调用 add（）");
    }

    public void update() {
        System.out.println("Impl 调用 update（）");
    }

    public void delete() {
        System.out.println("Impl 调用 delete（）");
    }

    public void query() {
        System.out.println("Impl 调用 query（）");
    }
}
```

### 静态代理

```java
package demo02;

public class StaticProxy implements UserService {

    // 这里写死了类型 UserService， 导致一个真实类必须要有一个静态代理类
    private UserService userService;

    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    public void add() {
        otherBusiness();
        this.userService.add();
    }

    public void update() {
        otherBusiness();
        this.userService.update();
    }

    public void delete() {
        otherBusiness();
        this.userService.delete();
    }

    public void query() {
        otherBusiness();
        this.userService.query();
    }

    // 代理做的其他事情
    private void otherBusiness() {
        System.out.println("静态代理做一些其他事情. ");
    }
}
```

### 动态代理

```java
package demo02;


import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class DynamicProxy implements InvocationHandler {

    // 这里因为不涉及具体的方法调用，所以类型可以是 Object，就可以接收多种类型的真实类接口，就改进了静态代理的一对一限制
    private Object proxyInstance;

    public void setProxyInstance(Object proxyInstance) {
        this.proxyInstance = proxyInstance;
    }

    public Object getProxy() {
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),
                this.proxyInstance.getClass().getInterfaces(),this);
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        otherBusiness();
        Object result = method.invoke(this.proxyInstance, args);
        return result;
    }

    // 动态代理可以做的其他操作
    private void otherBusiness() {
        System.out.println("动态代理中做的其他操作");
    }
}
```

### 客户端调用

```java
package demo02;

public class Client {
    public static void main(String[] args) {
        // ----------- 静态代理方法 -----------
        /*
        // 生成一个真实类实例
        UserServiceImpl userService = new UserServiceImpl();
        // 生成一个代理类实例
        StaticProxy staticProxy = new StaticProxy();
        // 把真实实例交给代理实例
        staticProxy.setUserService(userService);
        // 通过代理实例调用方法
        staticProxy.add();
        staticProxy.update();
        staticProxy.delete();
        staticProxy.query();
         */

        // ----------- 动态代理方法 -----------
        // 生成一个真实类实例
        UserServiceImpl userService = new UserServiceImpl();
        // 生成一个动态代理管理类实例
        DynamicProxy dynamicProxy = new DynamicProxy();
        // 把真实实例交给动态代理管理类实例
        dynamicProxy.setProxyInstance(userService);
        // 获得代理实例，类型转换为当前匹配的真实类类型 ** 这里，把类型限制放到了客户端，改进了静态代理的一对一限制 **
        UserService proxy = (UserService) dynamicProxy.getProxy();
        // 通过代理实例调用方法
        proxy.add();
        proxy.delete();
        proxy.update();
        proxy.query();
    }
}
```


# 抽象工厂模式

和工厂方法模式一摸一样，区别在于：

工厂方法模式，一个工厂生产一个产品。

抽象工厂模式，一个工厂，生产同一个产品族（同一个公司）的所有产品。

***

产品接口 Phone：

```java
public interface PhoneInterface {
    void start();
    void call();
    void shutdown();
}
```

Phone 实现：

```java
public class HuaweiPhone implements PhoneInterface {
    @Override
    public void start() {
        System.out.println("华为开机");
    }

    @Override
    public void call() {
        System.out.println("华为打电话");
    }

    @Override
    public void shutdown() {
        System.out.println("华为关机");
    }
}
```

```java
public class XiaomiPhone implements PhoneInterface {
    @Override
    public void start() {
        System.out.println("小米开机");
    }

    @Override
    public void call() {
        System.out.println("小米打电话");
    }

    @Override
    public void shutdown() {
        System.out.println("小米关机");
    }
}
```

产品接口 Router：

```java
public interface RouterInterface {
    void linkStart();
    void linkOver();
}
```

Router 实现：

```java
public class HuaweiRouter implements RouterInterface {
    @Override
    public void linkStart() {
        System.out.println("华为路由器连接");
    }

    @Override
    public void linkOver() {
        System.out.println("华为路由器断开");
    }
}
```

```java
public class XiaomiRouter implements RouterInterface {
    @Override
    public void linkStart() {
        System.out.println("小米路由器连接");
    }

    @Override
    public void linkOver() {
        System.out.println("小米路由器断开");
    }
}
```

工厂接口：

```java
public interface abstractFactory {
    PhoneInterface getPhone();
    RouterInterface getRouter();
}
```

工厂实现：

```java
// 华为工厂
public class HuaweiFactory implements abstractFactory {
    @Override
    public PhoneInterface getPhone() {
        return new HuaweiPhone();
    }

    @Override
    public RouterInterface getRouter() {
        return new HuaweiRouter();
    }
}

```

```java
// 小米工厂
public class XiaomiFactory implements abstractFactory {
    @Override
    public PhoneInterface getPhone() {
        return new XiaomiPhone();
    }

    @Override
    public RouterInterface getRouter() {
        return new XiaomiRouter();
    }
}
```

测试：

```java
class Test{
    public static void main(String[] args) {
        PhoneInterface phone;
        RouterInterface router;

        String s = "xiaomi";
        if (s.equals("xiaomi")) {
            System.out.println("========= 使用小米产品 =========");
            XiaomiFactory xiaomiFactory = new XiaomiFactory();

            phone = xiaomiFactory.getPhone();
            router = xiaomiFactory.getRouter();
        } else {
            System.out.println("========= 使用华为产品 =========");
            HuaweiFactory huaweiFactory = new HuaweiFactory();

            phone = huaweiFactory.getPhone();
            router = huaweiFactory.getRouter();
        }

        phone.call();

        router.linkStart();

    }
}
```


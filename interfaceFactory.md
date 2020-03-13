# 工厂方法模式

改进：实现了开闭原则，设置了工厂的接口，每一个 Car 接口的实现类，对应一种工厂接口的实现类。

抽象接口 Car：

```java
public interface Car {
    void getName();
}
```

接口实现类 Wulin 和 Tesla：

```java
public class Wulin implements Car {
    @Override
    public void getName() {
        System.out.println("五菱");
    }
}
```

```java
public class Tesla implements Car {
    @Override
    public void getName() {
        System.out.println("特斯拉");
    }
}
```

工厂接口：

```java
public interface CarFactory {
    Car getName();
}
```

工厂接口实现类：

```java
public class WulinFactory implements CarFactory {
    @Override
    public Car getName() {
        return new Wulin();
    }
}
```

```java
public class TeslaFactory implements CarFactory {
    @Override
    public Car getName() {
        return new Tesla();
    }
}
```


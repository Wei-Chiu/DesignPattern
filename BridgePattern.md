# 桥接模式

![屏幕快照 2020-03-14 下午9.57.54](/Users/apple/Desktop/java/DesignPattern/屏幕快照 2020-03-14 下午9.57.54.png)

![屏幕快照 2020-03-14 下午11.02.10](/Users/apple/Desktop/java/DesignPattern/屏幕快照 2020-03-14 下午11.02.10.png)

桥接模式，就是使用组合，例如在 Computer 抽象类中，组合 Brand。

### 品牌接口

```java
package BridgePattern;

public interface Brand {
    void info();
}
```

### 品牌的两个实现

```java
package BridgePattern;

public class Lenovo implements Brand {

    @Override
    public void info() {
        System.out.print("联想的");
    }
}
```

```java
package BridgePattern;

public class Dell implements Brand {

    @Override
    public void info() {
        System.out.print("戴尔的");
    }
}
```

### 电脑抽象类，因为需要组合，所以使用抽象类而不是接口

```java
package BridgePattern;

public abstract class Computer {
    // 吧品牌组合进来，实现桥接
    Brand brand;

    public Computer(Brand brand) {
        this.brand = brand;
    }

    // 输出电脑品牌
    void info() {
        brand.info();
    }
}
```

### 电脑的两个实现类

```java
package BridgePattern;

public class Laptop extends Computer{
    public Laptop(Brand brand) {
        super(brand);
    }

    @Override
    void info() {
        super.info();
        // 输出电脑类型：笔记本
        System.out.println("笔记本");
    }
}
```

```java
package BridgePattern;

public class Pad extends Computer {
    public Pad(Brand brand) {
        super(brand);
    }

    @Override
    void info() {
        super.info();
        // 输出电脑类型：平板
        System.out.println("平板");
    }
}
```

### 测试

```java
package BridgePattern;

public class Test {
    public static void main(String[] args) {
        Computer computer1 = new Laptop(new Lenovo());
        computer1.info();

        Computer computer2 = new Pad(new Dell());
        computer2.info();
    }

}
```


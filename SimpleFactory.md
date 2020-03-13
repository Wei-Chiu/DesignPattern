# 简单工厂模式

有点：不用关注创建实例时候的参数，不用关注参数等具体内容。

缺陷：难以实现开闭原则，即新增接口实现类，需要对工厂的代码进行修改。

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

工厂：

```java
public class SimpleFactory {
    // 方式一
    public static Car getCar(String name) {
        if (name == "Wulin") {
            return new Wulin();
        } else if (name == "Tesla") {
            return new Tesla();
        }
        return null;
    }

    // 方式二
    public static Wulin getWuLin() {
        return new Wulin();
    }
    public static Tesla getTesla() {
        return new Tesla();
    }
}

```


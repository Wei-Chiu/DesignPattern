# 单例模式(懒汉恶汉改进)

```java
// 饿汉式，线程安全，调用效率高，不能延时加载
public class SingletonDemo {
    private SingletonDemo() {

    }

    private static SingletonDemo singletonDemo = new SingletonDemo();

    public static SingletonDemo getSingletonDemo() {
        return singletonDemo;
    }
}

// 懒汉式，线程安全，调用效率低，可以延迟加载
class SingletonDemo02{
    private SingletonDemo02() {

    }

    private static SingletonDemo02 SingletonDemo02;

    public synchronized static SingletonDemo02 getSingletonDemo02() {
        if (SingletonDemo02 == null) {
            SingletonDemo02 = new SingletonDemo02();
        }
        return SingletonDemo02;
    }
}

// DCL 懒汉式，由于懒汉式的 get 方法，一次只能有一个线程进入，效率不高。
// 因此该用双重检测锁，使用  关键字，防止一个线程在创建对象的过程中，另一个线程获得了不为 null 但是不完整的对象。
class SingletonDemo03{
    private SingletonDemo03(){

    }

    private volatile static SingletonDemo03 singletonDemo03;

    public static SingletonDemo03 getSingletonDemo03() {
        if (singletonDemo03 == null) {
            synchronized (SingletonDemo03.class) {
                singletonDemo03 = new SingletonDemo03();
            }
        }
        return singletonDemo03;
    }
}

// 饿汉式改进，使用静态内部类实现，线程安全，可以延时加载
class SingletonDemo04{
    private SingletonDemo04(){}

    private static class InnerClass{
        private static final SingletonDemo04 instance = new SingletonDemo04();
    }

    public static SingletonDemo04 getInstance() {
        return InnerClass.instance;
    }
}
```


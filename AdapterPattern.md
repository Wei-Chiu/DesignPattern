# 适配器模式

将一个类的接口，转换成客户希望的另外一个接口。Adapter 模式使得原本由于接口不兼容而不能一起工作的类，可以在一起工作。

电脑，网线，适配器。电脑不能直接插网线，需要通过适配器来实现上网。

角色对应：
适配者：网线。
适配器：适配器实现。
期望接口：USB。

### 网线

```java
package AdapterPattern;

public class NetworkLine {
    public void connectIn() {
        System.out.println("网络接入成功。");
    }
}
```



### 适配器接口



```java
package AdapterPattern;

// 被适配的类：网线
public interface AdapterInterface {
    // 处理适配
    void handlerAdapt();
}
```



### 适配器实现

```java
package AdapterPattern;

public class AdapterImpl implements AdapterInterface {

    private NetworkLine networkLine;

    public AdapterImpl(NetworkLine networkLine) {
        this.networkLine = networkLine;
    }

    @Override
    public void handlerAdapt() {
        networkLine.connectIn();
    }
}
```

### 电脑

```java
package AdapterPattern;

public class Computer {
    public void openSafari(AdapterInterface adapter) {
        adapter.handlerAdapt();
    }
}
```

### 测试

```java
package AdapterPattern;

public class Test {
    public static void main(String[] args) {
        Computer computer = new Computer();
        NetworkLine networkLine = new NetworkLine();
        AdapterInterface adapter = new AdapterImpl(networkLine);

        computer.openSafari(adapter);
    }
}
```


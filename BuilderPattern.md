# 建造者模式

描述：由指挥，工人和产品三个要素。指挥负责指挥构建一个工程，由她决定如何构建，具体构建由工人完成。

应用场景：产品具有复杂的内部结构，但是这些产品具有共同特性。

优点：实现了产品建造和表示分离，实现了解耦。可以使客户端不需要知道产品内部组成细节。因为只需要创建 director 和 worker ，具体 director 怎么指挥 worker，不需要知道。

缺点：只能创建相似的产品，因为抽象的 Builder 在一定程度上，限制了 Worker 能做的事情。

### 产品

```java
package BuildPattern;

// 产品
public class Product {
    String propertyA = "可乐";
    String propertyB = "鸡翅";
    String propertyC = "汉堡";

    public String getPropertyA() {
        return propertyA;
    }

    public void setPropertyA(String propertyA) {
        this.propertyA = propertyA;
    }

    public String getPropertyB() {
        return propertyB;
    }

    public void setPropertyB(String propertyB) {
        this.propertyB = propertyB;
    }

    public String getPropertyC() {
        return propertyC;
    }

    public void setPropertyC(String propertyC) {
        this.propertyC = propertyC;
    }

    @Override
    public String toString() {
        return "Product{" +
                "propertyA='" + propertyA + '\'' +
                ", propertyB='" + propertyB + '\'' +
                ", propertyC='" + propertyC + '\'' +
                '}';
    }
}
```

### 抽象建造者

```java
package BuildPattern;

// 抽象的建造者，每个步骤可以有不同的实现，对应不同的工人
public abstract class Builder {
    abstract void buildA();
    abstract void buildB();
    abstract void buildC();

    abstract Product getProduct();
}
```

### 建造者具体实现

```java
package BuildPattern;

// 具体的工人，实现具体的建造过程
public class Worker extends Builder {

    Product product;

    public Worker() {
        this.product = new Product();
    }

    @Override
    void buildA() {
        product.setPropertyA("自选A");
    }

    @Override
    void buildB() {
        product.setPropertyA("自选B");
    }

    @Override
    void buildC() {
        product.setPropertyA("自选C");
    }

    @Override
    Product getProduct() {
        return product;
    }
}
```



### 指挥

```java
package BuildPattern;

// 指挥：核心，负责指挥构建一个工程，由她决定如何构建
public class Director {
    public Product build(Builder builder) {
        // 指挥来觉点建造顺序
        builder.buildA();
        builder.buildC();
        builder.buildB();

        return builder.getProduct();
    }
}
```



### 测试

```java
package BuildPattern;

public class Test {
    public static void main(String[] args) {
        // 指挥
        Director director = new Director();
        // 工人
        Worker worker = new Worker();
        // 指挥工人完成
        Product build = director.build(worker);
        // 输出
        System.out.println(build.toString());
    }
}
```




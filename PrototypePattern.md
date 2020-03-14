# 原型模式

原型模式就是不通过 new 来创建对象，而通过 clone 创建新的对象。

默认的 Object 的 clone 方法，是浅拷贝，只是值复制。

需要实现 Cloneable 接口，自己实现一个深拷贝。

ps.通常和工厂方法一起使用，如果对象较为复杂，则选择 clone。

### 重写 Cloneable 接口的对象

```java
package PrototypePattern;

import java.util.Date;

public class Video implements Cloneable {
    String name;
    Date datetime;

    @Override
    protected Object clone() throws CloneNotSupportedException {
        Video cloneVideo = (Video) super.clone();
        cloneVideo.datetime = (Date) this.datetime.clone();
        return cloneVideo;
    }

    public Video() {
    }

    public Video(String name, Date datetime) {
        this.name = name;
        this.datetime = datetime;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Date getDatetime() {
        return datetime;
    }

    public void setDatetime(Date datetime) {
        this.datetime = datetime;
    }

    @Override
    public String toString() {
        return "Video{" +
                "name='" + name + '\'' +
                ", datetime=" + datetime +
                '}';
    }
}
```

### 测试

```java
package PrototypePattern;

import java.util.Date;

public class Test {
    public static void main(String[] args) throws CloneNotSupportedException {
        // 创建 v1
        Date date = new Date();
        Video v1 = new Video("狂胜说", date);
        // 克隆
        Video v2 = (Video) v1.clone();
        // 输出对象
        System.out.println(v1.toString());
        System.out.println(v2.toString());
        // 输出 hash code
        System.out.println("Hash Code: " + v1.hashCode());
        System.out.println("Hash Code: " + v2.hashCode());
        // 分割线
        System.out.println("===============");
        // 修改日期，深拷贝验证
        date.setTime(123123);
        System.out.println(v1.toString());
        System.out.println(v2.toString());
    }
}
```


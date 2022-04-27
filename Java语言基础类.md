### Java语言基础类

#### Java基础类库

```java
java.lang //Java语言的核心类库 自动导入java.lang.*
java.util //实用工具
java.io //标准输入/输出类库
java.awt //javax.swing 图形用户界面（GUI）的类库
java.net //网络功能的类库
java.sql //数据库访问的类库
```

#### 阅读JDK API文档

* 在线查阅

  []: https://tool.oschina.net/apidocs/apidoc?api=jdk_7u4

#### 阅读JDK源码

* JDK的源代码
  * 安装JDK后即有 src.zip

#### Object类

* Object类是所有类的直接或间接父类
* 让所有的类有了一致性

#### equals()

* 简单地说， == 是引用是否相等，equals是内容相等
* 如果覆盖**equals()**方法，一般也要覆盖**hashCode()**方法

#### getClass()

* getClas()方法是final方法，它不能被重载
* 它返回一个对象在运行时所对应的类的表示

```java
void PrintClassName(Object obj){
    System.out.println("The object's class is " + obj.getClass().getName());
}

Object creatNewInstanceOf(object obj){
    return obj.get.Class().newInstance();
}
```

#### toString()

* toString()方法用来返回对象的字符串表示

* 常用于显示s

  `System.out.println(person);`

* 另外，用于字符串的加号

  `"current person is" + person`

* 通过重载toString()方法，可以适当地显示对象的信息以进行调试

#### 基本数据类型的包装类

* Java的基本数据类型用于定义简单的变量和属性将十分方便，但为了面向对象的环境一致，Java中提供了基本数据类型的包装类（wrapper）,它们是这些基本类型的面向对象的代表

* 与8种基本数据类型相对应，基本数据类型的包装类也有8种，分别是

  `Charactor,Byte,Short,Integer,Long,Float,Double,Boolean`

#### 包装类的特点

* 这些类都提供了一些常数

  `Integer.MAX_VALUE(整数最大值)， Double.NaN(非数字)， Double.POSITIVE_INFINITY(正无穷)`

* 提供了**valueOf(String)，toString()**

  * 用于从字符串转换及或转换成字符串

* 通过 **Value()**方法可以得到所包装的值

  * Integer对象的**intValue()**方法

* 对象中所包装的值是不可改变的（**immutable**）

  * 要改变对象中的值只有重新生成新的对象（稳定性）

* **toString(), equals()** 等方法进行了覆盖

> Double类提供了parseDouble(), max, min方法等

#### 包装与拆包

* JDK1.5以上，有**包装（boxing）**及**拆包（unboxing）**

  ```java
  //Integer I = 5;
  I = Integer.valueOf(5);
  //int i = I;
  I = I.intValue();
  ```

#### Math类

```java
System.out.println(Math.abs(-1));
System.out.println(Math.floor(100.99));
System.out.println(Math.ceil(100.00001));
System.out.println(Math.round(20.4));
System.out.println(Math.max(99, 98));
System.out.println(Math.pow(2, 10));
System.out.println((int)(Math.random()*10));//随机的 1-10
System.out.println(Math.sqrt(9));
System.out.println((-5-Math.sqrt(Math.pow(5, 2)-4*2*2))/2);
System.out.println("x=");
```

#### System类

* 在Java中，系统属性可以通过环境变量来获得

  * `System.getProperty(String name)`方法获得特定的系统属性值
  * `System.getProperties()`方法获得一个**Properties类**，其中包含了所有可用的系统属性信息

* 在命令行运行Java程序时可使用 ++-D 选项++添加新的系统属性

  `java -D var = value Myprog`

```java
import java.util.*
class SystemProperties{
	public static void main(String[] args){
        Properties props = System.getProperties();
        Enumeration keys = props.propertyNames();
        while(keys.hashMoreElements()){
            String key = (String) key.nextElement();
            System.out.println(key + " = " + props.getProperty(key));
        }
    }
}
```


















































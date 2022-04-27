### Java程序的核心基础

#### Java的特点

* 简单易学
* 面向对象
* 跨平台性
* 安全性
* 支持多线程

#### Java三种核心机制

* Java虚拟机

* 代码安全性检测

* 垃圾回收机制


#### Java程序的编译与运行

![image-20200520191600592](C:\Users\Tao\AppData\Roaming\Typora\typora-user-images\image-20200520191600592.png)

#### Java的面向对象

对象具有两方面的含义：

* 现实生活中：
  * 是客观世界中的一个实体

* 计算机世界中：
  * 是一个可标识的存储区域 

#### Java的类

* 类：具有共同属性和行为的对象集合
  * 属性：变量（字段 field）
  * 行为：函数（方法 method）
* 类与对象的关系
  * 类是对象的抽象（模板）
  * 对象是类的**实例**

*注：类和对象有时都统称“对象”，为了明确起见，后者称为“对象实例”

![image-20200520193255558](C:\Users\Tao\AppData\Roaming\Typora\typora-user-images\image-20200520193255558.png)

#### Java的封装

* 模块化：将属性和行为封装在类中，程序定义很多类
* 信息隐蔽：将类的细节部分隐藏起来（用户只通过受保护的接口访问某个类）

![image-20200520193826334](C:\Users\Tao\AppData\Roaming\Typora\typora-user-images\image-20200520193826334.png)

#### Java的继承

* 继承性
  * 父类和子类之间共享数据和方法

![image-20200520194016573](C:\Users\Tao\AppData\Roaming\Typora\typora-user-images\image-20200520194016573.png)

* 继承的好处
  * 更好地进行抽象与分类
  * 增强代码的重用率
  * 提高可维护性

#### Java的多态性

* 多态
  * 不同的对象收到同一个消息（调用方法）可产生完全不用的效果
  * 实现的细节则由接收对象自行决定

```java
foo(Person p){
    p.sayHello();
}
foo(new Student());
foo(new Teacher());
```

#### 面向对象设计思想的要点

* 认为客观世界由各种对象组成
* 程序的分析和设计都围绕着
  * 有哪些对象类
  * 每个类有哪些属性、哪些方法
  * 类之间的关系（继承、关联等）
  * 对象之间发送消息（调用方法）

### Java程序的类型与基本构成

#### Application和Applet程序的区别

* 结构和运行环境不同
* 前者是独立的程序，需要执行器（调用虚拟机）来运行
* 后者是嵌在HTML网页中的非独立的程序
  * 由专门的appletViewer来运行
  * 或者由Web浏览器（调用Java虚拟机）来运行

#### Application程序

* HelloWorldApp.java

* 要点
  * class是主体
  * public类名与文件同名
  * main()的写法是固定的
  * System.out.print 及 println 及 printf

```java
public class HelloWorldApp{
    public static void main(String args[]){
        System.out.println("Hello World");
    }
}
```

#### Applet程序

* HelloWorldApplet.java
  * import表示导入
  * extends JApplet表示继承
    * Applet或JApplet都可以
  * 有paint()方法，表示如何绘制
  * 没有main()方法

```java
import java.awt.*;
import java.applet.*;
import javax.swing.*;
public class HelloWorldApplet extends JApplet{
    public void paint(Graphics g){
        g.drawString("Hello World!",20,20);
    }
}
```

* HelloWorldApplet.html

```html
<HTML>
    <HEAD><TITLE> An Applet </TITLE></HEAD>
    <BODY>
        <applet code="HelloWorldApplet.class" width=200 height=40 background=white>
        </applet>
    </BODY>
</HTML>
```

#### Java程序的基本构成

* HelloDate.java
  * package 语句（ 0或1句 ）
  * import 语句 （ 0或多句 ）
    * 导入其他类的类库
  * 类定义——class（ 1或多个 ）
    * 一个文件只能有一个public类（ 与文件同名 ）

```java
package edu.pku.tds.ch02;
import java.util.*;
public class HelloDate {
    
}
```



* 类 = 类头 + 类体
* 类成员 = 字段（ field ）+ 方法（ method ）  
  * 字段（ field，属性，变量 ） 方法（ method，函数 ）
* 方法 = 方法头 + 方法体

```java
class Person{
    int age;
    String name;
    public void sayHello(){
        
    }
};
```

### 开发Java程序的基本步骤

#### 程序的编辑、编译与运行

* 源程序编辑
  * 可用任一文本编辑器
* 程序编译
  * 使用JDK中的 **javac** 工具
* 程序运行
  * 使用 java 工具

#### JAVA工具包JDK

* Java编程的基础工具是JDK
* JDK安装后的文件夹
  * Bin 该目录存放工具文件
  * Jre 该目录存放与 java 运行环境相关的文件
  * Demo 该目录存放一些示例文件
  * Include 该目录存放与 C 相关的头文件
  * Lib 该目录存放程序库
  * Db 数据库相关文件

#### Application的编辑、编译与运行

* 程序编辑：编辑器——文件名要与 public class 的类名一致
  * 区分大小写
* 程序编译——转换为字节码 （ bytecode ）文件，扩展名 .class
  * （ .class 文件中包含 java 虚拟机的指令 ）
  * 编译可以使用JDK工具 javac.exe
  * 如 javac Hello.java
* 程序的运行——执行 .class 文件中的指令的过程
  * 如 java Hello

*注：不要写成 java Hello.class ，因为这里需要的是类名 ，不是文件名

#### Applet的编辑、编译与运行

* Java Applet 程序必须嵌入到HTML中，并由负责解释HTML文件的WWW浏览器充当解释器，解释执行程序
* Java Applet 在WWW中引入了动态交互的内容

1. 源程序的编辑和编译
2. 在HTML文件中嵌入Applet
   * 使用<applet>标签：

```html
<applet code="HelloWorldApplet.class" width=200 height=40 background=white></applet>
```

#### 其他几个工具

* 主要的工具
  * javac  编译
  * java  运行（ 控制台及图形界面程序 ）
  * javaw  运行图形界面程序
  * appletViewer  运行applet程序
* 另外常用的几个工具
  * jar  打包工具
  * javadoc  生成文档
  * javap  查看类信息及反汇编
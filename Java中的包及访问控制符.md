### Java中的包及访问控制符

#### package

* package pkg1[.pkg2[.pkg3...]];
* 包及子包的定义，实际上是为了解决**名字空间、名字冲突**
  * 它与类的继承没有关系，事实上，一个子类与其父类可以位于不同的包中。
* 包有两方面的含义
  * 一是名字空间、存储路径（文件夹）
  * 一是可访问性（同一包中的各个类，**默认情况下可互相访问**）

#### package语句

* 包层次的根目录是由环境变量CLASSPATH来确定的

* 在简单情况下，没有package语句，这时称为无名包（unnamed package）

  * 在Eclipse中，也叫（default package）

* Java的JDK提供了很多包

  java.applet,java.awt,java.awt.image,java.awt.peer,java.io,java.lang,java.net,java.util,javax.swing,等

#### import语句

* 为了能使用Java中已提供的类，需要用import语句来导入所需要的类

* import语句的格式为：   

  `import package1[.package2...].(classname|*);`

  ```java
  import java.util.Data; //这样，程序中java.util.Date可以简写为Date
  import java.awt.*;
  import java.awt.event.*;
  ```

  > 注意：使用星号（*）只能表示本层次的所有类，不包括子层次下的类

* Java编译器自动导入包java.lang.*

* Eclipse等IDE可以方便地生成import语句

#### 修饰符

* 修饰符（modifiers）分为两类

  * 访问修饰符（access modifiers）

    ==public、private==

  * 其他修饰符

    ==abstract==

* 可以修饰类、也可以修饰类的成员（字段、方法）

#### 成员的访问控制符（权限修饰符）

|                  | 同一个类中 | 同一个包中 | 不同包中的子类 | 不同包中的非子类 |
| :--------------: | :--------: | :--------: | :------------: | :--------------: |
|     private      |    Yes     |            |                |                  |
| 默认（包可访问） |    Yes     |    Yes     |                |                  |
|    protected     |    Yes     |    Yes     |      Yes       |                  |
|      public      |    Yes     |    Yes     |      Yes       |       Yes        |

#### 类的访问控制符

* 在定义类时，也可以用访问控制符

* 类的访问控制符或者为public，或者默认

  ```java
  // 若使用public，其格式为
  public class 类名{
      ...
  }
  ```

* 如果类用public修饰，则该类可以被其他类所访问；

* 若类默认访问控制符，则该类只能被同包中的类访问

#### setter与getter

* 将字段用private修饰，从而更好地将信息进行封装和隐藏
* 用set()和get()方法对类地属性进行存取、分别称为setter与getter
* 这种方法有以下优点
  * 属性用private更好地封装和隐藏，外部类不能随意存取和修改
  * 提供方法来存取对象的属性，在方法中可以对给定的参数的合法性进行检验
  * 方法可以用来给出计算后的值
  * 方法可以完成其他必要的工作（如清理资源、设定状态）
  * 只提供get()方法，而不提供set()方法，可以保证属性是只读的

```java
class Person2{
    private int age;
    public void setAge(int age){
        if(age > 0 && age < 200)
            this.age = age;
    }
    public int getAge(){
        return age;
    }
}
```

#### 非访问控制符

|          | 基本含义               | 修饰类         | 修饰成员 | 修饰局部变量 |
| -------- | ---------------------- | -------------- | -------- | ------------ |
| static   | 静态的、非实例的、类的 | 可以修饰内部类 | Yes      |              |
| final    | 最终的、不可改变的     | Yes            | Yes      | Yes          |
| abstract | 抽象的、不可实例化的   | Yes            | Yes      |              |

#### static字段

* 静态字段最本质的特点是：

  * 它们是类的字段，**不属于任何一个对象实例**

* 它不保存在某个对象实例的内存区间中，而是保存在类的内存区域的公共存储单元

* 类变量可以通过类名直接访问，也可以通过实例对象来访问，两种方法的**结果是相同的**

* 如System类的in和out对象，就是属于类的域，直接用类名来访问，即System.in和System.out

  ```java
  // 在类Person中可以定义一个类域为totalNum
  class Person{
      static long totalNum;
      int age;
      String Name;
  }
  // totalNum代表人类的总人数，它与具体对象实例无关。可以有两种方法来访问：Person.totalNum和p.totalNum（假定p是Person对象）
  ```

> 在一定意义上，可以用来表示全局变量

#### static方法

* 用static修饰符修饰的方法仅属于类的静态方法，又称为类方法
* 与此相对，不用static修饰的方法，则为实例方法
* 类方法的本质是该方法是属于整个类的，**不是属于某个实例的**
* 声明一个方法为static有以下几重含义
  * 非static的方法是属于某个对象的方法，在这个对象创建时，对象的方法在内存中拥有自己专用的代码段。而static的方法是属于整个类的，它在内存中的代码段将随着类的定义而进行分配和装载，不被任何一个对象专有
  * 由于static方法是属于整个类的，所以它不能操纵和处理属于某个对象的成员变量，而只能处理属于整个类的成员变量，即static方法只能处理本类中的static域或调用static方法
  * static方法中，不能访问实例变量，不能使用this或super
  * 调用这个方法时，应该使用类名直接调用，也可以用某一个具体的对象名
    * 例如：Math.random(),Integer.parseInt()等就是类方法，直接用类名进行访问

#### import static

```java
// 导入静态System
import static java.lang.System.*
//可以使用out.println();表示System.out.println();
```

#### final

* final 类

  如果一个类被 final 修饰符所修饰和限定，说明这个类**不能被继承**，即不可能有子类

* final方法

  final 修饰符所修饰的方法，是不能被子类所覆盖的方法

* final 字段及final局部变量（方法中的变量）
  * 它们的值**一旦给定，就不能更改**
  * 是**只读量**，它们**能且只能被赋值一次**，而不能被赋值多次

* 一个字段被**static final**两个修饰符所限定时，**它可以表示常量**
  
  * 如Integer.MAX_VALUE（表示最大整数）、Math.PI（表示圆周率）就是这种常量
* 关于赋值
  * 在定义static final域时，若不给定初始值，则按默认值进行初始化（数值为0，boolean型为false，引用型为null）
  * 在定义final字段时，若不是static的域，则必须且只能赋值一次，不能缺省
    * 这种域的赋值方法有两种：**一是在定义变量时赋值初始值，二是在每一个构造函数中进行赋值**
  * 在定义final局部变量时，也必须且只能赋值一次，它的值可能不是常量，但它的取值在变量存在期间不会改变

#### abstract

* abstract类

  * 凡是用abstract修饰符修饰的类被称为**抽象类**
  * 抽象类不能被实例化

* abstract方法

  * 被abstract所修饰的方法叫**抽象方法**，抽象方法的作用在为所有子类定义一个统一的接口。对抽象方法只需声明，而不需实现，**即用分号（；）而不是用{}**

    `abstract return Type abstractMethod([paramlist]);`

  * 抽象类中可以包含抽象方法，也可以不包含abstract方法，但是，一旦某个类中包含了abstract方法，则这个类必须声明为abstract类

  * 抽象方法在子类中必须被实现，否则子类仍然是abstract的
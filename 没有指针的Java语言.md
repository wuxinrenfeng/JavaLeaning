### 没有指针的Java语言

#### 引用与指针

* 引用（reference）实质就是指针（pointer）
* 受控的、安全的

* 特点
  * 会检查空指引
  * 没有指针运算 *（p+5）
  * 不能访问没有引用到的内存
  * 自动回收垃圾

#### C语言指针在Java中的体现

* 传地址 → 对象
  * 引用类型，引用本身就相当于指针（可以用来修改对象的属性，调用对象的方法）
  * 基本类型：没有对应的

```java
//交换两个整数
void swap(int x, int y){
    int t = x;
    x = y;
    y = t;
}
int a = 8, b = 9;
swap(a,b);
//一种变通的方法 ：传出一个有两个分量x,y的对象
```

* 指针运算 → 数组

  * *（p + 5）则可以用 args[5]

* 函数指针 → 接口、Lambda表达式

  * 求积分、线程、回调函数、事件处理

* 指向结点的指针 → 对象的引用

  ```java
  class Node{
      Object data;
      Node next;
  }
  ```

* 使用JNI
  * Java Native Interface(JNI)
  * 它允许Java代码和其他语言写的代码进行交互

#### 相等还是不等

* ==（基本类型是++值相等++，引用类型是++引用相等++）

#### 基本类型的相等

* 基本类型
  * 数值类型：转换后比较
  * 浮点数，最好不直接用 ==
  * Double.NAN == Double.NAN 结果为 false
  * boolean型无法与int相比较

````java
Integer i = new Integer(10);
Integer j = new Integer(10);
System.out.println(i == j); //false,因为对象是两个
Integer m = 10;
Integer n = 10;
System.out.println(m == n);//true,因为对象有缓存
Integer p = 200;
Integer q = 200;
System.out.println(p == q);//false，因为对象是两个
````

#### 枚举、引用对象是否相等

* 枚举类型
  * 内部进行了唯一实例化，所以可以直接判断
* 引用对象
  * 是直接看两个引用是否一样
  * 如果要判断内容是否一样，则要重写equals方法
  * 如果重写equals方法，则最好重写hashCode()方法

#### String对象的特殊性

* String对象
  * 判断相等，一定不要用 == ，要用 equals
  * 但是字符串常量（String literal）及字符串常量会进行内部化（interned），相同的字符串常量是 == 的

```java
String hello = "Hello", lo = "lo";
System.out.println(hello == "Hello"); //true
System.out.println(Other.hello == hello); //true
System.out.println(hello == ("Hel" + "lo")); //true
System.out.println(hello == ("Hel" + "lo")); //false
System.out.println(hello == new String("Hello")); //false 
System.out.println(hello == ("Hel" + lo).intern()); //true
```


### 反射 reflection

#### 反射（reflection）

* 反射（reflection）
  * 在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性
* 在一些框架性的程序中，反射是相当重要的（如 plugin）

#### Class 对象

​	java.lang.reflect.*

* 首先要得到类的Class

* 得到 Class 对象的三种方法

  * 类名,class

    `Class <?> cls = String.class;`

  * 对象.getClass()

    `String str = 'abc';` `Class<?> cls = str.getClass();`

  * Class.forName(类的全名)

    `Class <?> cls = Class.forName("java.lang.String");`

#### 得到字段及方法

* 由 Class 获得该类的信息
  * 得到成员（字段、方法）

#### 动态创建对象

* 由 Class 来创建相关的实例、调用相关的方法

#### 再谈 Annotation

* Annotation：注记，有译为注解、注释、标记、元数据
* JDK 内置的 Annotation
  * @Override（表示覆盖）
  * @Deprecated（表示过时）
  * @SuppressWarnings（{“unchecked”,"deprecation"}）(表示不产生警告信息)

#### 自定义注记

* 注记的定义
  * 使用 @interface 来定义一个类型，表示它是一个注记
  * 使用 方法名() 表示它的一个属性（值或数组）
    * 其中 value() 是默认属性，使用 default 表示其默认值

#### 注记的使用

* @注记名
* （属性 = 值，属性 = {值，值}）

```java
//使用注记
class MyClass{
    @debugTime(value = true,timeout = 10,msg = "时间太长"，other = {1，2，3})
    public double fib(int n){
        if(n == 0||n ==1)return 1;else return fib(n - 1) + fib(n - 2);
    }
}
```

#### 用反射来读取注记

* method.getAnnotation( 注记.calss )
* method.getAnnotations()
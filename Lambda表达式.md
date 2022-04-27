### Lambda表达式

#### Lambda表达式(==代码也当成数据来处理==)

* Lambda表达式（λ expression）的基本写法
  * （参数）→ 结果

```java
(String s) → s.length()
x → x * x
() → {System.out.println("aaa");}
```

* 大体上相当于其他语言的“匿名函数”或“函数指针”
* 在Java中它实际上是“匿名类的一个实例”

#### 举例

```java
Runnable dolt = new Runnable(){
    public void run(){
        System.out.println("aaa");
    }
};
new Thread(dolt).start();
//简化
Runnable dolt = () → System.out.println("aaa");
new Thread(dolt).start();
//再简化
new Thread(()→System.out.println("aaa")).start();
```

#### 基本格式

* Lambda表达式是==接口==或者说是==接口函数==的简写
* 基本写法是（参数 → 结果）

> 参数是（）或1个参数或（多个参数）
>
> 结果是指 表达式或语句或{语句}

#### 示例

```java
//interface Fun{double fun(double x);}
double d = integral(new Fun(){
    public double fun(double x){
        return Math.sin(x);
    }
},0,Math.PI,1e-5);
//double d = Integral(x → Math.sin(x)),0,Math.PI,1e-5
```

#### 实例

* Lambda大大地简化了书写

* 在线程的例子中

  `new Thread(() → {...}).start();`

* 在积分的例子中

  `d = Integral(x → Math.sin(x), 0, 1, EPS);`

  `d = Integral(x → x * x, 0, 1, EPS);`

  `d = Integral(x → 1, 0, 1, EPS);`

* 在==按钮事件处理==中

  `btn.addActionListener(e → {...});`

#### 能写成Lambda的接口的条件

* 由于Lambda只能表示一个函数，所以能写成Lambda的接口要==求包含且最多只能有一个==抽象函数
* 这样的接口可以（但不强求）用注记

> @FunctionalInterface 来表示，称为==函数式接口==

```java
@FunctionalInterface
interface Fun{double fun(double x);}
```


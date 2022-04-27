### 并发 API

#### 并发 API

* **java.util.concurrent** 包及其子包
  * 从 JDK1.5 开始
  * 提供了一系列的工具，更好、更方便地使用线程
* 几个实用的类
  * 单变量、集合、Timer、线程池

#### 原子变量

* **java.util.concurrent.atomic** 包

  `AtomicInteger `类

  `getAndlncrement()`方法

#### 集合与线程

* 在 JDK1.5 以前

  * **ArrayList/HashMap** 不是线程安全的

    * **Vector** 及 **Hashtable** 是线程安全的

  * 产生一个线程安全的集合对象

    `Collections.synchronizedArrayList(list)`

#### 并发的集合类

* **java.util.concurrent** 包中增加了一些方便的类

  `CopyOnWriteArrayList、copyOnWriteArraySet`

  适合于很少写入而读取频繁的对象

* **ConcurrentHashMap**

  `putIfAbsent()` `remove()` `replace()`

* **ArrayBlockingQueue**

  * 生产者与消费者，使用 `put()` 及 `take()`

#### 使用线程池

* 线程池相关的类

  $ExecutorService$ 接口、$ThreadPoolExecutor$ 类、$Executors$ 工具类

* 常用的用法

  `ExecutorService pool = Executors.newCachedThreadPool()`;

  使用其 **execute(Runnable r)** 方法

#### 使用 Timer 

* 使用 **java.util.Timer** 类

  重复某件事

* 使用 **javax.swing.Timer** 类

  重复执行 ++ActionListener++

> 在线程中更新图形化界面，要调用 **SwingUtilites.invokeLater**


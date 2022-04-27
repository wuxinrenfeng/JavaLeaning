### JVM性能监控和故障处理

#### 概述

工具分为两大类

* 命令行工具
* 可视化工具

++命令行工具++是运行期定位线上问题的首选工具

#### 常用方法

* 用 ps、jps 找出线程号
* 如果怀疑是死循环、线程类的问题、使用 **jstack -l** 来查看
* 如果是 JVM 内存问题，使用jstate来进行查看，比较常用的是jstate -gcutil
* 如果线上问题通过命令行工具不能定位，可以使用 jmap 导出快照，使用其他可视化工具进行分析，或者保留一台机器做现场

> 注：jmap 慎用，会stop the world，暂停 JVM，慎用

#### 查看虚拟机进程状况，用于获取进程ID：jps

* 用于获取虚拟机进程的ID，该ID是其他命令行工具的输入

* 列出正在与运行的虚拟机进程及进程的本地唯一 ID（LVMID）

  对于本地虚拟机进程来说，LVMID和PID是一致的（用ps命令也可以拿到）

  ```java
  jps -l   //输出主类全名
  jps -v   //输出启动参数
  ps -ef | grep java //在本地使用ps命令也可以获取 lvmid
  ```

#### 查看虚拟机线程快照，用于定位死循序、死锁等：jstack

用于生成虚拟机当前时刻的线程快照，一般用于定位线程出现长时间停顿的原因，例如死锁、死循环等

`jstack -l 3418`

我们一般查看用户进程，每个用户进程包括三部分内容

* 线程的状态
* 线程的调用栈
* 线程当前锁住的资源

> 死循环：可多次执行jstack，如果某个用户进程一致 runnable，说明这个用户进程一直在运行，考虑是不是有死循环
>
> 死锁：存在互相等待，查看所著的资源，jstack可以直接检测

#### 线程状态

* NEW：至今尚未启动的线程的状态（jstack中不会出现）
* RUNNABLE：可运行线程的线程状态。处于可运行状态的某一线程正在 Java 虚拟机中运行在等待操作系统中的其他资源，比如处理器
* BLOCKED：受阻塞并且正在等待监视器锁的某一线程的线程状态。（比如 synchronized(lock){ } 而lock被其他线程持有时，当前线程就会进入BLOCKED状态）
* WAITING
  * Object.wait	不带超时值的
  * Thread.join    不带超时值的
  * LockSupport.park
* TIMED_WAITING
  * Thread.sleep
  * Object.wait     带有超时值的
  * Thread.join     带有超时值的
  * LockSupport.parkNanos    
  * LockSupport.parkUntil
  * TERMINATED 线程已终止（jstack中不会出现）

#### 虚拟机统计信息监控，用于定位内存泄露、FullGC等：jstat

用于获取虚拟机各种运行状态信息，非常实用，推荐在线定位GC问题的首选工具

用法：

`jstat option vmid interval count `对进程vmid运行jstat option，每隔interval时间，共运行count次

* `jstat -class`

  查看类装载、卸载数量、总空间、以及类装载所耗费的时间

  Loaded:  类装载数量  Bytes： 总空间（KB） UnLoaded：卸载数量 Time： 类装载耗费的时间（ms）

* `jstat -gc 3418 200 10`

  查看堆状况，包括eden区、两个s区、老年代、持久代的容量、已用空间、GC时间等， 200ms执行一次，共执行10次

  * S0C：年轻代S0区的容量  S1C：年轻代S1区的容量  S0U：年轻代S0区目前已使用的空间  S1U：年轻代S1区已使用的容量 EC： 年轻代Eden的容量  EU：年轻代Eden已使用的容量
  * OC：年老代的容量  OU： 年老代已使用的容量
  * PC：Perm的容量 PU：Perm已使用的容量
  * YGC： 从启动到现在YoungGC的次数 YGCT：YoungGC所用的时间(s)
  * FGC：从启动到现在FullGC的次数 FGCT： 从启动到现在FullGC所用的时间(s)
  * GCT: 从启动到现在GC的总时间

> GC会Stop the world，经常关注这个时间非常有意义，我们的报警里面也包含该信息。

* `jstat -gccapacity`

  查看堆各个代使用的最大最小空间

  * NGCMN: 年轻代最小的容量  NGCMX： 年轻代最大的容量  NGC：年轻代当前的容量  SOC S1C EC同上面的解释
  * OGCMN：年老带最小的容量 OGCMX： 年老带最大容量， OGC： 年老代当前的容量 【OGC = sum(all OC），只有一个OC，OGC=OC】 OC： 年老代当前的容量
  * PGCMN：Perm区的最小容量  PGCMX： Perm区最大容量 PGC：Perm区当前容量  PC： Perm区当前容量

* `jstat -gcutil`

  查看堆各个代已使用空间占总空间的百分比，最常用的命令

  ++S0、S1、E、O、P 表示各个区已使用空间的百分比++

* 监控各个代的情况

  * `jstat  -gcnew` 新生代的GC情况
  * `jstat  -gcnewcapacity` 新生代的最大、最小空间
  * `jstat  -gcold`  老年代的GC情况
  * `jstat -gcoldcapacity` 老生代的最大、最小空间
  * `jsata -gcpermcapacity` 永久带的最大、最小空间

#### Dump堆快照，保存现场、线下分析：Jmap

用于dump堆的快照，使用其他工具进行线下分析

例如： `jmap -dump:format=b,file=a.bin 3418` 



[原文阅读](https://blog.csdn.net/u010372867/article/details/51438557)
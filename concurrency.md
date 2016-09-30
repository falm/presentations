title: 并发模型 Actor &amp; CSP
speaker: Jason Hou
theme: dark
transition: slide
[slide]

# 并发模型 Actor & CSP

[slide]
## 并发和并行
----
![](http://jolestar.com/images/concurrent/concurrent_vs_parallel.png)

[slide]
## 并发的方案
----
- 进程
- 线程
- 事件循环
[slide]
## 进程 or 线程
[slide]

## 线程遇到的问题
----
- 竞争条件
- 死锁
- ![](http://images.51cto.com/files/uploadimg/20090805/120148542.jpg)
- 执行顺序依赖

[slide]

## 系统在多少线程下是最优的？
----
![](http://jolestar.com/images/concurrent/cpu_ratio.png)

[slide]
## 如何有效利用在阻塞期间的资源
[slide]

----
- 异步回调
- GreenThread/Coroutine/Fiber

[slide]
## GreenThread/Coroutine/Fiber
----
- 运行在用户空间，占用较少的资源，可以创建大量的实例
- ![](http://docs.oracle.com/cd/E19455-01/806-3461/images/nancb6.eps.gif)

[slide]
----
- 异步回调会遇到，回调地狱问题
- GreenThread/Coroutine/Fiber 需要手动的切换和管理
[slide]

## CSP
----
![](http://www.jdon.com/simgs/performance/channel.png)
[slide]
## Go
----
- 用goroutine作为做小执行单元
- channel作为通讯通道
- 语言层面实现goroutine调度器
[slide]
## Goroutine调度器
----
![](http://morsmachine.dk/in-motion.jpg)

[slide]
## 实现M:M
----
![](http://www.studytonight.com/operating-system/images/many-to-many-model.png)
[slide]
## Actor
----
- 通过发送消息，来共享资源
- actor可以创建其他actor
- actor可以接受并处理消息，及修改自身的状态
- actor作为独立的实体可以热更新
- 一个actor关掉的时候可以发送出消息通知其他的actor
- 不区分本地和远程
[slide]
----
![](http://blog.scottlogic.com/rdoyle/assets/ActorModel.png)
[slide]
## Actor模型的实现
----
- Erlang/Elixir
- Akka(JVM)
- Celluloid(ruby)
[slide]
## Golang CSP & Actor
----
![](http://www.jdon.com/simgs/performance/csp.png)
- CSP : Channel是主体，处理器是匿名的，实体和实体之间是松耦合的.
- Actor: Actor是主体,MailBox是透明的，实体之间是紧耦合.
[slide]
# 谢谢大家
[slide]

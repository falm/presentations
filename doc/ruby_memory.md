title: Ruby Memory
speaker: Jason Hou
<!-- transition: slide -->
theme: dark
transition: cycle
[slide]
# Ruby Memory
[slide]

## 问题
----
- Ruby的内存结构是什么样？
- 为什么Ruby应用非常吃内存?
- 有什么方法可以优化内存使用？

[slide]

## 内存结构
----
![memory-structure](http://upload-images.jianshu.io/upload_images/1767848-b9038945718dbbf4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


[slide]

## 组成部分
---
* **栈** 指针
* **堆** 25/heap_page 10_000/slot
* **heap page** 408/slot   HEAP_OBJ_LIMIT
* **slot** : 40bytes的RVALUE(RObject...)   GC_HEAP_INIT_SLOTS
* **系统堆** : 数据

[slide]

[magic data-transition="zoomin"]


## 为什么吃内存

====

![](https://collectiveidea.com/assets/malloc_memory_fragmentation.png?size=fit_in_blog_postk) 

====
## RUBY_GC_HEAP_GROWTH_FACTOR 1.8
====


[/magic]


[slide]

## 优化
---
- 参数优化
- 程序优化

[slide]

## 参数优化
--- 
* **RUBY_GC_HEAP_INIT_SLOTS**: Ruby初始化slots数量，数量越大后续malloc次数越小
* **RUBY_GC_HEAP_GROWTH_FACTOR**: 内存分配增长因子
* **RUBY_GC_MALLOC_LIMIT**: GC触发条件之一, 分配内存超过限制后运行GC
* **RUBY_GC_HEAP_FREE_SLOTS**: 对堆空间free slot少于该参数是 触发GC

[slide]

## 总结
---
* **核心参数**
* **内存结构**
* **GC**


[slide]

# 谢谢大家




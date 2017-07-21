title: Ruby Hash
speaker: Jason Hou
transition: slide3
theme: moon
usemathjax: yes
[slide]
# Ruby 哈希表
[slide]

## 索引
----
- Ruby Hash的内部结构
- Ruby Hash工作方式
- Ruby Hash的优化和改进

[slide]
[magic data-transition="zoomin"]

## 内部结构
====

![](http://upload-images.jianshu.io/upload_images/1767848-db54507480b8e365.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

====


![](http://upload-images.jianshu.io/upload_images/1767848-e40c2a71dda1dc5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

====



[/magic]

[slide]
## 工作方式
----
- 链地址法解决冲突
- MurmurHash 散列函数, 每次重启应用生成随机种子
- 重新散列, 链地址长度5个限制
- 散列扩容
[slide]

## 链地址法
----
![memory-structure](https://ruby-china-files.b0.upaiyun.com/photo/2017/1738a6f05673cb5cdefe03ba6eb41c95.svg)

[slide]
## 散列扩容
----
<pre>
<code class="c">
/* st.c */
/* Table of prime numbers 2^n+a, 2<=n<=30. */
static const unsigned int primes[] = {
  8 + 3,
  16 + 3,
  32 + 5,
  64 + 3,
  128 + 3,
  256 + 27,
  512 + 9,
  ...
}
</code>
</pre>

[slide]
## 优化和改进
[slide]

## Ruby 2.0
---
![](http://upload-images.jianshu.io/upload_images/1767848-00b21e694b5076c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]
## Ruby 2.2
---
- 按照2^n扩容, 初始值16
- 去除质数取模, #define hash_pos(h,n) ((h) & (n - 1))

[slide]
## Ruby 2.4
---
[slide]
## 开放地址法
---
![](https://ruby-china-files.b0.upaiyun.com/photo/2017/59d8cd8013d80c6a9f47cf0ce00d5620.svg)

[slide]

## 线性同余方法(LCG)
----
> Xn+1 = (a * Xn + c ) % m

[slide]
## Benchmark
----
![](https://ruby-china-files.b0.upaiyun.com/photo/2017/01a016cdd47aa652a684c79a6a5bdb56.png!large)


[slide]

# 谢谢大家




title: MySQL事务隔离和加锁分析
speaker: Jason Hou
transition: slide
theme: dark
transition: zoomin
[slide]
# MySQL事务隔离和加锁分析
[slide]
## MVCC(多版本并发控制)
----
- 当前读
(加锁)
- 快照读
(不加锁)

[slide]

## 快照读
- 
<pre>
<code class="sql">
select * from users where id=1;
</code>
</pre>

[slide]

![](http://tech.meituan.com/img/innodb_lock/1.png)

[slide]

## 当前读
<pre>
<code class="sql">
select * from users where ? lock in share mode;
</code>
</pre>
<pre>
<code class="sql">
select * from users where ? for update;
</code>
</pre>
<pre>
<code class="sql">
insert into users values (…);
</code>
</pre>
<pre>
<code class="sql">
update users set ? where ?;
</code>
</pre>
<pre>
<code class="sql">
delete from users where ?;
</code>
</pre>


[slide]

## 事务隔离
----
- read uncommitted（读取未提交数据）
- read committed（可以读取其他事务提交的数据）
- repeatable read（可重读）
- serializable（串行化）

[slide]

## 加锁分析
---
> 
<pre>
<code class="sql">
select * from users where id = 1;
delete from users where id = 1;
</code>
</pre>

- id列是主键，RC隔离级别 
- id列是二级唯一索引，RC隔离级别
- id列是二级非唯一索引，RC隔离级别
- id列上没有索引，RC隔离级别
- id列是主键，RR隔离级别
- id列是二级唯一索引，RR隔离级别
- id列是二级非唯一索引，RR隔离级别
- id列上没有索引，RR隔离级别
- Serializable隔离级别

[slide]
## id主键+RC 和 id主键+RR 
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6RtaP/medish.jpg)
[slide]
## id唯一索引+RC 和 id唯一索引+RR
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6PDep/medish.jpg)
[slide]
## id非唯一索引+RC
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6RA8t/medish.jpg)
[slide]
## id无索引+RC
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6Rt0M/medish.jpg)

[slide]
## id非唯一索引+RR
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6R7wu/medish.jpg)
[slide]
## id无索引+RR
--- 
![](http://pic.yupoo.com/hedengcheng/DnJ6Rf3q/medish.jpg)
[slide]

# 谢谢大家
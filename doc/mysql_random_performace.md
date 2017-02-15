title: MySQL随机查询性能分析
speaker: Jason Hou
transition: slide
theme: dark
transition: zoomin
[slide]
# MySQL随机查询性能分析
[slide]
## 大数据量下随机查询的方法
----
- Order by Rand()
- Rand() 改进方法1
- Rand() 改进方法2
- Inner join

[slide]

## Order by Rand()
<pre>
<code class="sql">
mysql> explain select * from users order by RAND() limit 1\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: users
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 8
        Extra: Using temporary; Using filesort
1 row in set (0.00 sec)
</code>
</pre>


[slide]
## Rand() 改进方法1

<pre>
<code class="sql">
SELECT id FROM users, (
  SELECT ((1/COUNT(*))*100) as n FROM users
) as x WHERE RAND()<=x.n LIMIT 1
</code>
</pre>

[slide]

<pre>
<code class="sql">
*************************** 1. row ***************************
           id: 1
  select_type: PRIMARY
        table: <derived2>
         type: system
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 1
        Extra: NULL
*************************** 2. row ***************************
           id: 1
  select_type: PRIMARY
        table: users
         type: index
possible_keys: NULL
          key: index_users_on_user_key
      key_len: 767
          ref: NULL
         rows: 210220
        Extra: Using where; Using index
*************************** 3. row ***************************
           id: 2
  select_type: DERIVED
        table: users
         type: index
possible_keys: NULL
          key: index_users_on_user_key
      key_len: 767
          ref: NULL
         rows: 210220
        Extra: Using index
</code>
</pre>

[slide]
## Rand() 改进方法2
<pre>
<code class="sql">
SELECT id FROM users, (
  SELECT ((1/COUNT(*))*100) as n FROM users
) as x WHERE RAND()<=x.n ORDER BY RAND() LIMIT 1;
</code>
</pre>

[slide]
## Inner join
<pre>
<code class="sql">
SELECT * FROM users as u JOIN (
  SELECT ROUND(RAND() * (SELECT MAX(id) FROM users)) AS id 
) AS u2 WHERE u.id >= u2.id ORDER BY u.id DESC LIMIT 1;
</code>
</pre>

[slide]
## 性能比较
![](http://upload-images.jianshu.io/upload_images/1767848-e1c38de23f65db29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
[slide]
# 谢谢大家
[slide]



title: Ruby Object & Class
speaker: Jason Hou
<!-- transition: slide -->
theme: dark
transition: cycle
[slide]
# Ruby对象与类的实现
[slide]
## 对象
-----
![](http://bachue.github.io/ruby-under-a-microscope-introduction-slides/img/r_object.png)

[slide]

## RObject结构体

* **RBasic** 中的 flags存储内部专有值
* **RBasic** 中的klass指针，用于指向RObject所属于的类
* **numiv** 实例变量的数量
* **ivptr** 实例变量值的数组


[slide]

## 实例
-----
<pre>
<code class="ruby">
class Mathematician
  attr_accessor :first_name
  attr_accessor :last_name
end

euler = Mathematician.new
euler.first_name = 'Leonhard'
euler.last_name = 'Euler'

euclid = Mathematician.new
euclid.first_name = 'Euclid'
</code>
</pre>
[slide]
## 实例
-----
![](http://upload-images.jianshu.io/upload_images/1767848-32ebb5e9a9346ee9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]

# 内置对象
-----
![](http://upload-images.jianshu.io/upload_images/1767848-9ae270a31518de40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]

# 立即值
-----
![](http://upload-images.jianshu.io/upload_images/1767848-95923855e98719b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
[slide]
# 类
-----
![](http://upload-images.jianshu.io/upload_images/1767848-78005ae411a8ddf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]

# 类结构
-----

* **m_tal**   用于存储类的实例方法表
* **iv_index_tbl** 实例变量的名称，实例变量的值是存放在**RObject**中的
* **super** 指向超类的指针
* **iv_tbl** 类实例变量表
* **const_tbl** 常量表


[slide]

# 元类
-----

![singleton_class](http://upload-images.jianshu.io/upload_images/1767848-49246ce8ee150356.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]

# 模块
-----

![](http://bachue.github.io/ruby-under-a-microscope-introduction-slides/img/r_class_for_module.png)

[slide]


<pre>
<code class="ruby">
module Professor
end
class Mathematican < Person
  include Professor
end
</code>
</pre>

[slide]

![](http://bachue.github.io/ruby-under-a-microscope-introduction-slides/img/include_a_module_in_class.png)


[slide]

# 方法查找
-----

![ruby_method_lookup.png](http://upload-images.jianshu.io/upload_images/1767848-6d11272f109b39bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/720)

[slide]

- 全局方法缓存
- 内联方法缓存
- 共享方法表

[slide]

# prepend
-----
![](http://bachue.github.io/ruby-under-a-microscope-introduction-slides/img/prepend_module_in_class.png)

[slide]
# 常量查找

[slide]
# 词法作用域
-----
![](http://bachue.github.io/ruby-under-a-microscope-introduction-slides/img/lexical_scope.png)

[slide]
# Autoload
-----
![ruby_cons_lp.png](http://upload-images.jianshu.io/upload_images/1767848-0b793e17f77cf926.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[slide]


# 谢谢大家




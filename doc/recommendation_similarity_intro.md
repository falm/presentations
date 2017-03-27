title: 文本相似性计算介绍
speaker: Jason Hou
transition: slide
theme: dark
transition: zoomin
[slide]
# 文本相似性计算介绍
[slide]
## 推荐系统
----
- 基于用户行为特征
- 基于内容相似度

[slide]

## 分词
## 词袋

[slide]

## Jaccard Index
![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Intersection_of_sets_A_and_B.svg/256px-Intersection_of_sets_A_and_B.svg.png)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ee/Union_of_sets_A_and_B.svg/256px-Union_of_sets_A_and_B.svg.png)
[slide]
## Jaccard Index
![](https://wikimedia.org/api/rest_v1/media/math/render/svg/eaef5aa86949f49e7dc6b9c8c3dd8b233332c9e7)
[slide]

## 向量空间相似度
----
- 欧式距离
- 余弦相似度

[slide]

## TF-IDF向量化
- TF（词频）
- IDF（逆向文件频率）

[slide]

## 计算方式 

![](http://www.it165.net/uploadfile/files/2015/1118/20151118181440118.jpg)
![](http://www.it165.net/uploadfile/files/2015/1118/20151118181440121.jpg)

![](http://www.it165.net/uploadfile/files/2015/1118/20151118181441122.png)

[slide]
## 代码

<pre>
<code class="ruby">
require 'ruby-tf-idf'

corpus = [
  'A big enough hammer can usually fix anything',
  'A bird in the hand is a big mistake .',
  'A bird in the hand is better than one overhead!',
  'A career is a job that takes about 20 more hours a week.',
  'A clean desk is a sign of a cluttered desk drawer.',
  'A cynic smells flowers and looks for the casket.'
]

limit = 3 #每个文档最多的三个词
exclude_stop_words = false

@t = RubyTfIdf::TfIdf.new(corpus,limit,exclude_stop_words)
output =  @t.tf_idf
</code>
</pre>

<pre>
<code class="ruby">
[
  {"anything"=>0.7781512503836436,"fix"=>0.7781512503836436, "enough"=>0.7781512503836436},
  {"mistake"=>0.7781512503836436, "bird"=>0.47712125471966244, "in"=>0.47712125471966244},
  {"overhead!"=>0.7781512503836436, "better"=>0.7781512503836436, "one"=>0.7781512503836436},
  {"week"=>0.7781512503836436, "career"=>0.7781512503836436, "hours"=>0.7781512503836436},
  {"desk"=>1.5563025007672873, "drawer"=>0.7781512503836436, "clean"=>0.7781512503836436},
  {"casket"=>0.7781512503836436, "cynic"=>0.7781512503836436, "smells"=>0.7781512503836436}
]
</code>
</pre>

[slide]

## 欧式距离
![](https://segmentfault.com/img/bVwg8L)

[slide]

## ruby代码
ruby gem : measurable

<pre>
<code class="ruby">
require 'measurable'

# Calculate the distance between two points in space.
Measurable.euclidean([1, 1], [0, 0]) # => 1.41421
</code>
</pre>

[slide]

## 余弦相似度
![](https://segmentfault.com/img/bVwg8M)

[slide]

## ruby代码

<pre>
<code class="ruby">
# Get the cosine distance between
Measurable.cosine_distance([1, 2], [2, 3]) # => 0.007722123286332261
</code>
</pre>

[slide]

## 谢谢大家

[slide]


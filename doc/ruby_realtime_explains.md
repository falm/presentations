## Ruby Web实时通讯方案剖析

<span style="font-size: 30px;width: 80%">侯俊杰</span>

---


<!-- ## 关于我 -->

<div style="display: flex;margin-top: 10px;justify-content: space-around;">

<img src="http://upload-images.jianshu.io/upload_images/1767848-cb97cc54f694c7a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" style="width: 300px; height: 300px" />

<ul class='about-me'>
<li>侯俊杰</li>
<li>github: **@falm**</li>
<li>email: **houjunjie@boohee.com**</li>
<li>
  <img 
    src="http://upload-images.jianshu.io/upload_images/1767848-e7bd78ad36452a8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
    style="height: 20px;width: 20px;vertical-align: -15px;" 
  >
  薄荷科技 - Ruby工程师
  <!-- 薄荷科技 - 健康领域领先的移动互联网公司 -->
</li>
</ul>



</div>


----

```php
    public function index(){
      define('LISTROW',$this->LISTROWS);
      $db = D("Market");
      import("ORG.Util.Page");
      $count = $db->count();
      $Page = new Page($count,LISTROW);
      $show = $Page->show();
      $page = $_GET['p'] ? $_GET['p'] : 1; 
      $sort = listSort($_GET['sort'],$_GET['way']);
      $key = listSearchTP($_GET['field'],$_GET['key'],$_GET['searchWay']);
      $list = $db->page($page.','.LISTROW)->where($key)->order($sort[0])->select();
      $list = keyHighLight($list,$_GET['field'] ,$_GET['key']);
      $this->assign("tabaleName",$db->getModelName());
      $this->assign("way",$sort[1]);
      $this->assign("list",$list);
      $this->assign("show",$show);
      $this->display();
    }
```

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-54dae4a814b54972.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

![](http://upload-images.jianshu.io/upload_images/1767848-828404417b65f6bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-6049ae2383dd1313.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

![after](http://upload-images.jianshu.io/upload_images/1767848-15133d267c7536c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-9c5463e927b5fe66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## PHP是世界上最好的语言

---

<!-- .slide: data-background="http://upload-images.jianshu.io/upload_images/1767848-41dc2e39d477f792.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" -->

健康领域领先的移动互联网公司

<ul class='horizen'>
<li>
<img src="http://upload-images.jianshu.io/upload_images/1767848-fd73d10039f48853.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" class="bh_logo" />
<div class="bh_desc">薄荷</div>
</li>

<li style="margin-right: 40px;">

<img src="http://upload-images.jianshu.io/upload_images/1767848-962d4988e542ccb7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" class="bh_logo" />
<div class="bh_desc">食物库</div>

</li>

</ul>

---

## 提纲

<!-- * 为什么要做web实时通讯? -->

* web实时通讯方案有哪些? <!-- .element: class="fragment fade-in" -->

* 解决方案的工作机制和性能指标? <!-- .element: class="fragment fade-in" -->

* 选择上有什么建议? <!-- .element: class="fragment fade-in" -->


---


## 为什么要做web实时通讯?

----

<ul class='horizen'>
<li>

![image.png](http://upload-images.jianshu.io/upload_images/1767848-5d4ed7f1226786ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</li>

<li style="margin-right: 40px;">

![image.png](http://upload-images.jianshu.io/upload_images/1767848-cc4e76b5d97a6e70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

</li>

</ul>



---

## web实时通讯方案有哪些?

----

## web实时通讯方案

<section>
  <p class="fragment fade-in">基于Http连接</p>
  <p class="fragment fade-in">第三方Socket服务</p>
  <p class="fragment fade-in">Websocket</p>
</section>

---


## 基于Http连接

----

Polling & Long Polling & Comet

<ul class='horizen'>
<li>

![polling](http://upload-images.jianshu.io/upload_images/1767848-dff04606145edfcf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

</li>

<li>

![comet](http://upload-images.jianshu.io/upload_images/1767848-b2f6e4557cbb905f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

</li>

</ul>

----
![](http://upload-images.jianshu.io/upload_images/1767848-ffdd16a6e196aa11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----


<ul class='horizen'>
<li>
![伪实时](http://upload-images.jianshu.io/upload_images/1767848-75171011692538e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<div>伪实时<div>
</li>
<li>

![效率低](http://upload-images.jianshu.io/upload_images/1767848-33a1529538e165fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<div>效率低</div>
</li>
<li>

![体验差](http://upload-images.jianshu.io/upload_images/1767848-be7cfe2da8f82578.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<div>体验差</div>
</li>

</ul>


---


## 第三方Socket服务

* 环信, 融云, 云通信

----

### 第三方Socket服务

![](https://camo.githubusercontent.com/99e623976fd7f8e3221a2dbfd7ab7674c0221f87/687474703a2f2f6465762e6e6574656173652e696d2f696d616765732f75706c6f61642f6e696d5f66756e632e706e67)


----

<ul class='horizen'>
<li>
![bh_app_store](http://upload-images.jianshu.io/upload_images/1767848-00d26939fb7bbd84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</li>
<li>

![bh_store_chat](http://upload-images.jianshu.io/upload_images/1767848-6af81df94b6d4656.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</li>

</ul>


----

- 优点： 简单，功能丰富
- 缺点： 定制困难, 收费

----

| DAU  | 环信       | 融云       | 云通信      |
| ---- | -------- | -------- | -------- |
| 50万  | 25,000/月 | 12,000/月 | 50,000/月 |


---

## WebSocket


![websocket](http://upload-images.jianshu.io/upload_images/1767848-b88a22e0284df9cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) <!-- .element: class="fragment fade-in" -->

---

## 总结

* **HTTP链接** - 技术简单, 但体验差，技术陈旧
* **第三方云服务** - 功能强大, 服务稳定，但是无法定制且收费不低
* **WebSocket** - 标准定义，兼容性稍差, 但不失为好点选择

---

### Ruby有哪些Websocket解决方案?

* 四个Ruby方案 <!-- .element: class="fragment fade-in" -->
* 两个扩展方案 <!-- .element: class="fragment fade-in" -->

---



## Ruby Websocket

**ActionCable**  <!-- .element: class="fragment fade-in" -->


---


## ActionCable
* Rails5提供的新特性 <!-- .element: class="fragment fade-in"  -->
* Rails进行无缝结合 <!-- .element: class="fragment fade-in"  -->

----

ActionCable server 可单独运行，也可以与App Server一起运行

![actioncable architect](http://upload-images.jianshu.io/upload_images/1767848-34503a76637deab7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

利用Redis，可扩展部署多台ActionCable Server

![actioncable scale](http://upload-images.jianshu.io/upload_images/1767848-5e52d008332c3424.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

![was he slow](http://upload-images.jianshu.io/upload_images/1767848-23ae6752549bad93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

### Benchmark


![actionCable](http://upload-images.jianshu.io/upload_images/1767848-492754e1be71dde5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----


调用栈

![J](http://upload-images.jianshu.io/upload_images/1767848-a011dcc42eaf389c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




----

启动流程

![](http://upload-images.jianshu.io/upload_images/1767848-29178469d99eaf2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

I/O事件监听

![ActionCable事件监听](http://upload-images.jianshu.io/upload_images/1767848-c1bc0f7dae25d4df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

内部结构

![image.png](http://upload-images.jianshu.io/upload_images/1767848-a344a9edd438ad35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


<!-- ---- -->

<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-f6e99fd265b9cd71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-ea329f0846046355.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

```ruby
  # which decodes JSON and transmits to the client.
  #
  # TODO: Room for optimization. Update transmit API to be coder-aware
  # so we can no-op when pubsub and connection are both JSON-encoded.
  # Then we can skip decode+encode if we're just proxying messages.
  def default_stream_handler(broadcasting, coder:)
    coder ||= ActiveSupport::JSON
    stream_transmitter stream_decoder(coder: coder), broadcasting: broadcasting
  end

  def stream_decoder(handler = identity_handler, coder:)
    if coder
      -> message { handler.(coder.decode(message)) }
    else
      handler
    end
  end
```

----

问题

* deep call stack <!-- .element: class="fragment fade-in"  -->
* hijacking API, doubled reactors <!-- .element: class="fragment fade-in"  -->
* blocking redis client <!-- .element: class="fragment fade-in"  -->
* meaningless decode/encode callback<!-- .element: class="fragment fade-in"  --> 

---



## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="fragment fade-in">**Faye-websocket**</p>
</section>


---

## Faye-websocket

* websocket-driver <!-- .element: class="fragment fade-in"  -->
* EventMachine处理I/O <!-- .element: class="fragment fade-in"  -->
* 运行在支持rack.hijack API的App Server <!-- .element: class="fragment fade-in" -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-0a889e22306c7962.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  <!-- .element: class="fragment fade-in" -->

----


![image.png](http://upload-images.jianshu.io/upload_images/1767848-90b5860eb5116b0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

### Hijacking API

* rack 1.5 <!-- .element: class="fragment fade-in"  -->
* 应用可以获取和操作socket <!-- .element: class="fragment fade-in"  -->

----

```ruby
def hijack_rack_socket
  return unless @socket_object.env['rack.hijack']
  @socket_object.env['rack.hijack'].call
  @rack_hijack_io = @socket_object.env['rack.hijack_io']
  ...
end
```


https://github.com/faye/faye-websocket-ruby/blob/c16c1cb7a27ff53e07bc45b661fac7abef2837c1/lib/faye/rack_stream.rb#L30

----

Code Example

```ruby
class Server
  def initialize
    @conns = Set.new
  end
  def call(env)
    if Faye::WebSocket.websocket?(env)
      ws = Faye::WebSocket.new(env)
      ws.on :open { |event| @conns.add(ws) }
      ws.on :message do |event|
        cmd, payload = JSON(event.data).values_at('type', 'payload')
        msg = {type: 'broadcast', payload: payload}.to_json
        @conns.each { |c| c.send(msg) }
        ws.send({type: "broadcastResult", payload: payload}.to_json)
      end
      ws.on :close { |event| @conns.delete(ws) }
      ws.rack_response
    else
      [200, {'Content-Type' => 'text/plain'}, ['Please connect a websocket client']]
    end
  end
end
```

----

Benchmark(Thin)


![Faye](http://upload-images.jianshu.io/upload_images/1767848-c2c09a7db9b3e751.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

Benchmark(Puma)

![faye](http://upload-images.jianshu.io/upload_images/1767848-e631af7994fc019f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

### 多进程 多机部署

需要自己使用Redis pub/sub

```ruby
class Server
  CHANNEL = 'benchmark'
  def initialize
    @conns = Set.new
    @redis = redis_connection
    Thread.new do
      redis_sub = redis_connection
      redis_sub.subscribe(CHANNEL) do |on|
        on.message do |_, msg|
          @conns.each {|ws| ws.send(msg) }
        end
      end
    end
  end
```

----

问题

* hijacking API
* 没有内置Pub/Sub
* EventMachine

---


## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="">**Faye-websocket**</p>
  <p class="fragment fade-in">**EM-websocket**</p>
</section>

---


## EM-websocket

----

Code Example

```ruby
EM.epoll
EM.run {
  @channel = EM::Channel.new
  EM::WebSocket.run(:host => address, :port => port) do |ws|
    ws.onopen {
      @channel.subscribe {|msg| ws.send msg }
    }
    ws.onmessage { |msg|
      cmd, payload = JSON(msg).values_at('type', 'payload')
      @channel.push({type: 'broadcast', payload: payload}.to_json)
      ws.send({type: "broadcastResult", payload: payload}.to_json)
  }
  end
}
```

----

benchmark

![EventMachine](http://upload-images.jianshu.io/upload_images/1767848-21df056e28d5b327.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

* 项目基本不在维护

![em-active](http://upload-images.jianshu.io/upload_images/1767848-3064716acb4a618d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---


## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="">**Faye-websocket**</p>
  <p class="">**EM-websocket**</p>
  <p class="fragment fade-in">**Plezi**</p>
</section>

---

## Plezi

* 支持Rack的(M)VC框架 <!-- .element: class="fragment fade-in" -->


![image.png](http://upload-images.jianshu.io/upload_images/1767848-099565dd9dc1ac92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) <!-- .element: class="fragment fade-in" -->

----

### 结构

![image.png](http://upload-images.jianshu.io/upload_images/1767848-4a5d45652731fbcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



----

### Code Example

```ruby
require 'plezi'
class ShootoutApp
  def on_open
    subscribe channel: "shootout"
  end
  def on_message data
    cmd, payload = JSON(data).values_at('type', 'payload')
    publish(channel: "shootout", message: ({type: 'broadcast', payload: payload}.to_json))
    write({type: "broadcastResult", payload: payload}.to_json)
  rescue
    puts "Incoming message format error!"
  end
end
Plezi.route '*', ShootoutApp
run Plezi.app
```

----

Benchmark


![Plzei](http://upload-images.jianshu.io/upload_images/1767848-6c541a5f44daf989.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

**Iodine**

* "native" websocket, no hijacking API

* Core and parsers are running outside of GIL

* EventDrive single reactor


---



![image.png](http://upload-images.jianshu.io/upload_images/1767848-41c4b34b78d89e12.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## 模式

<section>
  <p class="fragment fade-in" data-fragment-index="5">使用Redis作为消息队列，进行水平扩展</p>
  <p class="fragment fade-in" data-fragment-index="4">WebSocket Parser</p>
  <p class="fragment fade-in" data-fragment-index="3">Event/Thread</p>
  <p class="fragment fade-in" data-fragment-index="2">Reactor模式事件驱动</p>
  <p class="fragment fade-in" data-fragment-index="1">I/O多路复用(epoll, kqueue)</p>
</section>

---

## 扩展方案

* Nchan <!-- .element: class="fragment fade-in"  -->
* AnyCable <!-- .element: class="fragment fade-in"  -->

---

<!-- ## Nginx Nchan -->
![Nchan Logo](http://upload-images.jianshu.io/upload_images/1767848-bba6db09cfa1c7c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## Nchan
* 消息发布/订阅服务器
* 基于Nginx的扩展模块

----

## 特点

* 简单易用，可利用现有架构的RESTful API
* 高性能，高并发，易于扩展 
* 配置灵活，支持多种hook

----

## 结构

![structure of nchan](http://upload-images.jianshu.io/upload_images/1767848-0f3acc068447b6f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## websocket 负载均衡

![websocket load balancing](http://upload-images.jianshu.io/upload_images/1767848-0bff11ee1fff6f1a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## nchan 负载均衡

![nchan load balancing](http://upload-images.jianshu.io/upload_images/1767848-fb79f5cab3f6de45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


<!-- ---- -->

<!-- ## 性能  -->

<!-- ![](https://nchan.io/img/benchmark_internal_total.png) -->

----

## nchan与Rails结合的方案

![nchan_rails.png](http://upload-images.jianshu.io/upload_images/1767848-021b977d5abbb911.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## AnyCable

* 兼容ActionCable的 WS Server 

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-1afe520c223993cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## AnyCable Server
* anycable-go
* anycable-erlang

----

```ruby
# Gemfile
gem 'anycable', group: :production

# generate rpc server script
rails generate anycable

# run gRPC server
./bin/anycable

# run websocket server
anycable-go -addr=0.0.0.0:3334

```

---

![anycable and nchan](http://upload-images.jianshu.io/upload_images/1767848-cff62bc31565722c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


---

![image.png](http://upload-images.jianshu.io/upload_images/1767848-b2286d7d1902d4c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## 选择的建议

* 关键取决于应用场景, 适合的是最好的。  <!-- .element: class="fragment fade-in"  -->
* 一般场景下ActionCable可以满足需求, 尤其正在使用Rails5 <!-- .element: class="fragment fade-in"  -->
* 不依赖Rails, 应该尝试 - Faye Plezi Midori <!-- .element: class="fragment fade-in"  -->
* 非Rails5, 未来需要多语言支持 - Nchan  <!-- .element: class="fragment fade-in"  -->


---

# 谢谢大家
## Q&A

<img src="http://upload-images.jianshu.io/upload_images/1767848-fad8d4065517ac9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" style="width: 300px" />



<!-- % 关于Ruby Web实时通信方案的深度剖析
% -->
# Ruby Web实时通讯方案剖析

侯俊杰 @薄荷

2017.9.16

---


## 关于我

<div style="display: flex;margin-top: 100px;">

<img src="http://upload-images.jianshu.io/upload_images/1767848-cb97cc54f694c7a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" style="border:none;background: none;width: 300px; height: 300px" />

<ul class='about-me', style="font-size: 30px;display: flex;flex-direction: column;justify-content: center; text-align: right;list-style: none">
<li>侯俊杰@falm</li>
<li>全栈程序员</li>
<li>github.com/falm</li>
<li>薄荷科技 - 健康领域领先的移动互联网公司</li>
</ul>



</div>


---

## 薄荷

<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-a276a35aafaeb02d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-0fafab09d37cd4ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## 薄荷


![image.png](http://upload-images.jianshu.io/upload_images/1767848-1a1740cbfe97f38c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


---


## 为什么要做web实时通讯?

---

即时通讯需求的日益增长，薄荷在健康领域想要打造一款链接健康从业者和消费人群的工具，薄荷使用IM工具将两者联系在一起，针对这个需求，我们开发了集成在App内的通讯系统的功能。 


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

<!-- ---- -->

<!-- 轮询  -->


----

Polling & Comet & Long Polling

<ul class='horizen'>
<li>

![polling](http://upload-images.jianshu.io/upload_images/1767848-dff04606145edfcf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

</li>

<li>

![comet](http://upload-images.jianshu.io/upload_images/1767848-b2f6e4557cbb905f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

</li>

</ul>

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

* 云信, 环信, 融云

----

### 第三方Socket服务

![](https://camo.githubusercontent.com/99e623976fd7f8e3221a2dbfd7ab7674c0221f87/687474703a2f2f6465762e6e6574656173652e696d2f696d616765732f75706c6f61642f6e696d5f66756e632e706e67)

----

- 优点： 简单，功能丰富
- 缺点： 集成复杂，无法定制配置，收费

---

## WebSocket

<!-- ![](https://heroku-blog-files.s3.amazonaws.com/posts/1473343847-1462551384-websocket-protocol.png) -->
<!-- ![websocket](http://upload-images.jianshu.io/upload_images/1767848-19804b99abd1d75f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![websocket](http://upload-images.jianshu.io/upload_images/1767848-b88a22e0284df9cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) <!-- .element: class="fragment fade-in" -->

---

## 总结

* **HTTP链接** 技术简单, 但体验差，技术陈旧
* **第三方服务** 服务好，但是无法定制且收费不低
* **WebSocket** 自建实时通讯的不二之选

---

## Ruby 有哪些Websocket解决方案?

----

## Ruby Websocket

**ActionCable**  <!-- .element: class="fragment fade-in" -->
<!-- <section> -->
  <!-- <p class="fragment fade-in">**ActionCable**</p> -->
<!-- </section> -->


---


## ActionCable
* Rails5提供的新特性
* Rails进行无缝结合

----

ActionCable server 可单独运行，也可以与App Server一起运行

![](https://heroku-blog-files.s3.amazonaws.com/posts/1473343848-1462551406-rails-rack.png)

----

利用Redis，可扩展部署多台ActionCable Server
<!-- ![](http://upload-images.jianshu.io/upload_images/1767848-26a65b267ee05710.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->
<img src="http://upload-images.jianshu.io/upload_images/1767848-26a65b267ee05710.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" style="background: none; border: none;"/>

----

![was he slow](http://upload-images.jianshu.io/upload_images/1767848-23ae6752549bad93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

### Benchmark

<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-b8e4a6311b4df9ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->
<!-- ![image.png](http://upload-images.jianshu.io/  upload_images/1767848-c097dead4827f34f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-1fded2e7fe6f9b98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



----

内部结构

<!-- 内部使用 websocket-driver，nio4r和concurrent-ruby -->

<!-- ![](http://upload-images.jianshu.io/upload_images/1767848-6c86e55598532ba6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->
![image.png](http://upload-images.jianshu.io/upload_images/1767848-a344a9edd438ad35.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


<!-- ![](http://upload-images.jianshu.io/upload_images/1767848-8c84aca103892197.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

----

启动流程

![](http://upload-images.jianshu.io/upload_images/1767848-29178469d99eaf2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

I/O事件监听

![ActionCable事件监听](http://upload-images.jianshu.io/upload_images/1767848-c1bc0f7dae25d4df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

分析

![J](http://upload-images.jianshu.io/upload_images/1767848-a011dcc42eaf389c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

![image.png](http://upload-images.jianshu.io/upload_images/1767848-f6e99fd265b9cd71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## 阻塞


----

问题

* 因为与对象过多消耗内存和GC时间
* 消息同步使用阻塞的Redis客户端
* 连接使用线程处理但是线程锁也花时间

---

## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="fragment fade-in">**EM-websocket**</p>
</section>

---

## EM-websocket
* 基于EventMachine

----

Code

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

<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-4644d0ff2ef87a13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-f2df4ef1ed34b416.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

* 项目基本不在维护

![image.png](http://upload-images.jianshu.io/upload_images/1767848-6c6764b7b67205b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="">**EM-websocket**</p>
  <p class="fragment fade-in">**Faye-websocket**</p>
</section>

---

## Faye-websocket

* websocket-driver <!-- .element: class="fragment fade-in"  -->
* EventMachine处理I/O <!-- .element: class="fragment fade-in"  -->
* 运行在支持rack.hijack API的App Server <!-- .element: class="fragment fade-in" -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-0a889e22306c7962.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  <!-- .element: class="fragment fade-in" -->

----

![faye-start](http://upload-images.jianshu.io/upload_images/1767848-a0328659ed7ed8f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

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

      ws.on :open do |event|
        @conns.add(ws)
      end

      ws.on :message do |event|
        cmd, payload = JSON(event.data).values_at('type', 'payload')
        msg = {type: 'broadcast', payload: payload}.to_json
        @conns.each { |c| c.send(msg) }
        ws.send({type: "broadcastResult", payload: payload}.to_json)
      end

      ws.on :close do |event|
        @conns.delete(ws)
      end

      ws.rack_response
    else
      [200, {'Content-Type' => 'text/plain'}, ['Please connect a websocket client']]
    end
  end
end
```

----

Benchmark
<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-2a5cd07328c9c607.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->


![image.png](http://upload-images.jianshu.io/upload_images/1767848-da75b8bdd6c9c67a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


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

---


## Ruby-Websocket

<section>
  <p class="">**ActionCable**</p>
  <p class="">**EM-websocket**</p>
  <p class="">**Faye-websocket**</p>
  <p class="fragment fade-in">**Plezi**</p>
</section>

---

## Plezi

* 支持Rack的(M)VC框架
* 内置异步RedisEngine

![image.png](http://upload-images.jianshu.io/upload_images/1767848-099565dd9dc1ac92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

### 结构

![image.png](http://upload-images.jianshu.io/upload_images/1767848-4a5d45652731fbcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!-- ![plezi-component](http://upload-images.jianshu.io/upload_images/1767848-cc0b7b15a79e3fd3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->


----

### Code

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

<!-- ![](http://upload-images.jianshu.io/upload_images/1767848-57918408c70e0f1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-c095095bd9edf4b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

**Iodine**

* "native" websocket 没有使用hijacking API

* 协议和Reactor C实现 (多线程协议解析 无GIL 无GC)

* 事件驱动, Reactor模式, (单进程 单事件循环) 


---

## 模式

<section>
  <p class="fragment fade-in" data-fragment-index="5">**使用Redis作为消息队列，进行水平扩展**</p>
  <p class="fragment fade-in" data-fragment-index="4">**WebSocket Parser**</p>
  <p class="fragment fade-in" data-fragment-index="3">**Event/Thread**</p>
  <p class="fragment fade-in" data-fragment-index="2">**Reactor模式事件驱动**</p>
  <p class="fragment fade-in" data-fragment-index="1">**I/O多路复用(epoll, kqueue)**</p>
</section>

---

## Nginx Nchan
![Logo](https://camo.githubusercontent.com/99dde2976b3b18edb59dd185404d6395196b04d1/68747470733a2f2f6e6368616e2e696f2f6769746875622d6c6f676f2e706e67)

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

## HTTP 负载均衡

![](http://upload-images.jianshu.io/upload_images/1767848-410e20d28ad11ca5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## websocket 负载均衡

![websocket load balancing](http://upload-images.jianshu.io/upload_images/1767848-0bff11ee1fff6f1a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----

## nchan 负载均衡

![nchan load balancing](http://upload-images.jianshu.io/upload_images/1767848-fb79f5cab3f6de45.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----

## 性能 

![](https://nchan.io/img/benchmark_internal_total.png)

----

## nchan与Rails结合的方案

![nchan_rails.png](http://upload-images.jianshu.io/upload_images/1767848-021b977d5abbb911.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## 对比

<!-- ![image.png](http://upload-images.jianshu.io/upload_images/1767848-fe5b57e29db432ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) -->

![image.png](http://upload-images.jianshu.io/upload_images/1767848-1888e59e3544f8c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

## 如何选择

* 关键取决于应用场景, 适合的是最好的。  <!-- .element: class="fragment fade-in"  -->
* 一般场景下ActionCable可以满足需求, 尤其是依赖Rails - ActionCable <!-- .element: class="fragment fade-in"  -->
* 不依赖Rails, 期望有较好的并发性能 - Faye Plezi <!-- .element: class="fragment fade-in"  -->
* 非Rails5, 有较高并发需求, 未来需要多语言支持 - Nchan  <!-- .element: class="fragment fade-in"  -->


---

## Thank You 
## Q&A



<!-- % 关于Ruby Web实时通信方案的深度剖析
% -->
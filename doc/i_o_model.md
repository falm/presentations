title: I/O 模型
speaker: Jason Hou
transition: slide3
theme: moon
usemathjax: yes
[slide]
# I/O模型
[slide]

## 大纲
----
- 操作系统I/O模型分类
- 每种I/O模型在服务端的应用
- I/O模型的性能比较和发展

[slide]
[magic data-transition="zoomin"]

## 同步阻塞I/O
====

![](http://my.csdn.net/uploads/201204/12/1334216532_9745.jpg)

====

## Rack CGI, Webrick
---
<pre>
<code class="ruby">
TCPServer.open("127.0.0.1", 14641) {|serv|
  s = serv.accept
  s.puts Time.now
  s.close
}
</code>
</pre>

====

[/magic]

[slide]
[magic data-transition="zoomin"]
## 同步非阻塞I/O
====
![](http://my.csdn.net/uploads/201204/12/1334216607_3004.jpg)
====
<pre>
<code class="ruby">
serv = TCPServer.new(2202)
begin
  sock = serv.accept_nonblock
rescue IO::WaitReadable, Errno::EINTR
  IO.select([serv])
  retry
end
</code>
</pre>
[/magic]

[slide]

[magic data-transition="zoomin"]
## I/O 多路复用
====
![](http://my.csdn.net/uploads/201204/12/1334216620_6310.jpg)
====

## 系统调用

---

* select/poll O(n)
* epoll/kqueue O(1)

====
- Nginx
- EventMachine
- Redis
- Node.js
====
## Redis Reactor
![](http://1e-gallery.redisbook.com/_images/graphviz-3c09f0e53bd9d786aa646e5e4c289a11d97d40d7.png)

[/magic]

[slide]
[magic]
## 信号驱动I/O
====
![](http://my.csdn.net/uploads/201204/12/1334216632_6025.jpg)

[/magic]

[slide]
[magic]
## 异步I/O
====
![](http://my.csdn.net/uploads/201204/12/1334216641_7821.jpg)
====
- linux POSIX AIO: libeio, glibc libaio 
- windows IOCP
====
## nginx
![](http://cdn2.infoqstatic.com/statics_s2_20170620-0701/resource/articles/thread-pools-boost-performance-9x/zh/resources/0622006.jpg)
[/magic]


[slide]
## 比较
---
![](http://my.csdn.net/uploads/201204/12/1334216724_2405.jpg)

[slide]
## 网络库
---
- libevent
- libev
- libuv

[slide]
## Ruby
---
- **EventMachine**
- **nio4r** : libev


[slide]

# 谢谢大家 Q&A





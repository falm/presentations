title: Json Web Token
speaker: Jason Hou
<!-- transition: slide -->
theme: dark
transition: cycle
[slide]
# JWT (JSON Web Token)
[slide]

## 服务器端用户验证
----
* 基于Cookie
* 基于Token

[slide]

## 基于Cookie 
----
![](http://codastic.github.io/talk-jwt/figures/cookie_api_request.svg)

[slide]

## 遇到的问题
---
* CORS
* Session
* CSRF

[slide]
## 基于Token
-----
![](http://codastic.github.io/talk-jwt/figures/token_api_request.svg)

[slide]

## Token优势
----
* 性能(相对)
* 扩展性
* CSRF/CORS
* 多终端支持

[slide]

## 传统Token依然存在的问题
--- 
* 性能: 数据库存储token及过期时间
* 扩展: 每个服务都需要，集成token验证代码
* 安全: token可以被篡改请求

[slide]

## JWT
----
* 无状态
* 性能
* 标准化
* 安全

[slide]

[magic data-transition="zoomin"]

JWT结构
---
xxx.yyy.zzz

====

<span style="color: green">
(base64-encoded header)
</span>
.
<span style="color: yellow">
(base64-encoded payload)
</span>
.
<span style="color: red">
(encrypt signature)
</span>

[/magic]


[slide]

<span style="color: green">
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9

</span>
.
<span style="color: yellow">
yJ1c2VyX2tleSI6Inh4eHh4eHh4eHh4eHh4eHgiLCJleHAiOjE0MDc4MjkyNjgsImlhdCI6MTQwNzgyMjA2OCwiYWRtaW4iOnRydWV9
</span>
.
<span style="color: red">
JiRQIZojC6DTBM607e1fyxP0bmDSE_STuNxV-f4-7Qk
</span>

[slide]

## Header
----
<span style="color: green">
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
</span>

<pre>
<code class="json">
{
  "alg": "HS256",
  "typ": "JWT"
}
</code>
</pre>

[slide]

* **typ** : JWT
* **alg** : 加密算法


[slide]
## Payload
----
<span style="color: yellow">
yJ1c2VyX2tleSI6Inh4eHh4eHh4eHh4eHh4eHgiLCJleHAiOjE0MDc4MjkyNjgsImlhdCI6MTQwNzgyMjA2OCwiYWRtaW4iOnRydWV9
</span>

<pre>
<code class="json">
{
  "user_key": 'xxxxxxxxxxxxxxxx',
  "exp": 1407829268,
  "iat": 1407822068,
  "admin": true
}
</code>
</pre>

[slide]

<pre>
<code class="json">
{
    "iss" : "JWT-Rails-Server", // 签发者
    "aud" : "www.baidu.com", // 接收者
    "iat" : 1472263256, // JWT 签发的时间
    "exp" : 1472522525, // 过期时间
    "sub" : "jwt@baidu.com" // JWT对应的用户 
    "userId" : 1211 // 自定义
}
</code>
</pre>

[slide]

## JWS Signature
---
<span style="color: red">
JiRQIZojC6DTBM607e1fyxP0bmDSE_STuNxV-f4-7Qk
</span>

<pre>
<code class="javascript">
HMACSHA256(
    base64UrlEncode(header) + "." +
    base64UrlEncode(payload),
    "supersafe_secret"
)
</code>
</pre>

[slide]

## 使用

[slide]

## 注意
----
* 登出
* 载荷(payload)数据比较过的，避免token过长

[slide]

## 总结

[slide]

# 谢谢大家




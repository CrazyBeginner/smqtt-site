<!--
.. title: Main启动
.. slug: main-start
-->

## 启动服务:

### 阻塞启动
```java

Bootstrap.builder()
.rootLevel(Level.INFO)
.wiretap(false)
.port(8555)
.websocketPort(8999)
.options(channelOptionMap -> {
})//netty options设置
.childOptions(channelOptionMap -> {
}) //netty childOptions设置
.highWaterMark(1000000)
.reactivePasswordAuth((U, P) -> true)
.lowWaterMark(1000)
.ssl(false)
.sslContext(new SslContext("crt", "key"))
.isWebsocket(true)
.httpOptions(Bootstrap.HttpOptions.builder().enableAdmin(true).ssl(false).accessLog(true).build())
.build()
.startAwait();
    
```

### 非阻塞启动

```java
Bootstrap bootstrap = Bootstrap.builder()
.rootLevel(Level.INFO)
.wiretap(false)
.port(8555)
.websocketPort(8999)
.options(channelOptionMap -> {
})//netty options设置
.childOptions(channelOptionMap -> {
}) //netty childOptions设置
.highWaterMark(1000000)
.reactivePasswordAuth((U, P) -> true)
.lowWaterMark(1000)
.ssl(false)
.sslContext(new SslContext("crt", "key"))
.isWebsocket(true)
.httpOptions(Bootstrap.HttpOptions.builder().enableAdmin(true).ssl(false).accessLog(true).build())
.build()
.start().block();   

```
<!--
.. title: 启动Http服务
.. slug: start-http-server
-->

启动Broker时候开启Http服务：

```java
Bootstrap bootstrap = Bootstrap.builder()
        .httpOptions(Bootstrap.HttpOptions
                .builder()
                .ssl(false)
                .sslContext(new SslContext("crt","key"))
                .accessLog(true).build())
        .build()
        .start().block();
```
Bootstrap.HttpOptions参数:

|  参数   | 说明  | 必传  |
|  ----  | ----  |----  |
| ssl  | 开启ssl加密 |否 |
| sslContext  | ssl证书配置,为空则使用系统生成 |否 |
| enableAdmin  | 管理后台开启（默认60000端口） |否 |
| username  |管理后台登录用户名 |否 |
| password  | 管理后台登录密码 |否 |
| accessLog  | http日志开启 |否 |

sslContext参数：

|  sslContext   | 说明  | 必传  |
|  ----  | ----  |----  |
|  server.crt   | CA认证后的证书文件 |是|
| server.key | 密钥文件 |是 |
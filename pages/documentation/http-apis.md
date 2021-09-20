<!--
.. title: Http内置接口
.. slug: http-apis
-->

## 推送消息接口

> 系统内置了io.github.quickmsg.core.http.PublishActor接口，用于推送mqtt消息。使用方式如下：

- 请求url /smqtt/publish
- 请求方式 POST
- 请求Body

|  参数   | 说明  | 必传  |
|  ----  | ----  |----  |
| topic  | topiuc |是 |
| qos  | 服务等级 |是 |
| retain  | 保留消息 |是 |
| message  | 消息 |是 |

- 返回body
空
- 返回状态码
200 成功


```bash
curl -H "Content-Type: application/json" -X POST -d '{"topic": "test/teus", "qos":2, "retain":true, "message":"我来测试保留消息3" }' "http://localhost:1999/smqtt/publish"
```


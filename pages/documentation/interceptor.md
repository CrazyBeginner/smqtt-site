<!--
.. title: 拦截器
.. slug: interceptor
-->

## Interceptor接口详解

- io.github.quickmsg.common.interceptor.Interceptor

|  方法   | 说明  | 必传  |
|  ----  | ----  |----  |
|     Object doInterceptor(Invocation invocation)  | 拦截方法 |是 |
|     int order()  | 拦截排序 |是 |



- Invocation  属性说明

|  参数   | 说明  | 必传  |
|  ----  | ----  |----  |
|   method  | 请求的 MqttChannel |是 |
|   target   | 请求的 MqttMessage |是 |
|    args   | 请求的ReceiveContext |是 |

- 方法

|  方法   | 说明  | 
|  ----  | ----  |
|    public Object proceed() | 放行拦截器|


## 自定义拦截器

-  实现接口

```java

public class DemoInterceptor implements Interceptor {


    @Override
    public Object intercept(Invocation invocation) {
        try {
            Method method = invocation.getMethod();
            Object[] args = invocation.getArgs();
            Object target = invocation.getTarget();
//            MqttChannel mqttChannel, MqttMessage mqttMessage, ReceiveContext<C> receiveContext

            MqttChannel mqttChannel = (MqttChannel) args[0]; // channel
            MqttMessage mqttMessage = (MqttMessage) args[1]; // MqttMessage
            ReceiveContext receiveContext = (ReceiveContext) args[2]; // ReceiveContext

            // 拦截业务

            return invocation.proceed(); // 放行
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
        return null;
    }

    @Override
    public int sort() {
        return 0;
    }
}

```


- SPI注入

`具体参考java SPI注入`

resources/WEB-INF/services 目录下新建
名为io.github.quickmsg.common.interceptor.Interceptor文件,
将自定义实现类全限定名写入文件中即可完成注入。

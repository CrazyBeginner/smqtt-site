<!--
.. title: 数据持久化
.. slug: persistence
-->


## 持久化接口 

- 接口：`io.github.quickmsg.common.message.MessageRegistry`

> 主要提供 session消息 && 保留消息的持久化 

|  方法   | 说明  |
|  ----  | ----  |
|     List<SessionMessage> getSessionMessages(String clientIdentifier)  | 获取连接下线后的session消息 |
|     void saveSessionMessages(SessionMessage sessionMessage) | 保存连接下线后的session消息 |
|     void saveRetainMessage(RetainMessage retainMessage) | 保留Topic保留消息|
|     List<RetainMessage> getRetainMessage(String topic)| 获取Topic保留消息 |


### 使用数据库去存储session/保留消息

- 引入DB依赖

```xml
    
    <dependency>
      <groupId>io.github.quickmsg</groupId>
        <artifactId>smqtt-persistent-db</artifactId>
        <version>1.0.5</version>
    </dependency>
    
 ```

- 引入驱动依赖

> 根据版本引入 mysql/pg/oracle等驱动依赖


```xml
    　　<!--mysql驱动包-->
     <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.35</version>
    </dependency>
```

- 服务启动时config.properties 添加 配置参数

```properties
# 数据库配置
db.driverClassName=com.mysql.jdbc.Driver
db.url=jdbc:mysql://127.0.0.1:3306/smqtt?characterEncoding=utf-8&useSSL=false&useInformationSchema=true&serverTimezone=UTC
db.username=root
db.password=123
# 连接池初始化连接数
db.initialSize=10
# 连接池中最多支持多少个活动会话
db.maxActive=300
# 向连接池中请求连接时,超过maxWait的值后,认为本次请求失败
db.maxWait=60000
# 回收空闲连接时，将保证至少有minIdle个连接
db.minIdle=2

```

- 启动服务后会自动生成session表跟retain表

### 使用Redis去存储session/保留消息

* 引入依赖

```xml
 <dependency>
 	<groupId>io.github.quickmsg</groupId>
 	<artifactId>smqtt-persistent-redis</artifactId>
 	<version>1.0.5</version>
 </dependency>
```

* config.properties 配置参数

```properties
# redis配置
# 单机模式：single 哨兵模式：sentinel 集群模式：cluster
redis.mode=single
# 数据库
redis.database=0
# 密码
redis.password=
# 超时时间
redis.timeout=3000
# 最小空闲数
redis.pool.min.idle=8
# 连接超时时间(毫秒)
redis.pool.conn.timeout=3000
# 连接池大小
redis.pool.size=10

# 单机配置
redis.single.address=127.0.0.1:6379

# 集群配置
# 集群扫描间隔时间(毫秒)
redis.cluster.scan.interval=1000
# 节点
redis.cluster.nodes=127.0.0.1:7000,127.0.0.1:7001,127.0.0.1:7002,127.0.0.1:7003,127.0.0.1:7004,127.0.0.1:7005
# 读取操作的负载均衡模式
redis.cluster.read.mode=SLAVE
# 命令失败重试次数
redis.cluster.retry.attempts=3
# 从节点连接池大小
redis.cluster.slave.connection.pool.size=64
# 主节点最小空闲连接数
redis.cluster.master.connection.pool.size=64
# 命令重试发送时间间隔(毫秒)
redis.cluster.retry.interval=1500

# 哨兵配置
# master名称
redis.sentinel.master=mymaster
# 节点
redis.sentinel.nodes=127.0.0.1:26379,127.0.0.1:26379,127.0.0.1:26379
```

### 自定义实现持久化
resources/META-INF/services 目录下新建
名为`io.github.quickmsg.common.message.MessageRegistry`文件,
将自定义实现类全限定名写入文件中即可完成注入。

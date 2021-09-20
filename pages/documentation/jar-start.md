<!--
.. title: Jar包启动
.. slug: jar-start
-->

## 下载源码 

`git clone https://gitee.com/quickmsg/mqtt-cluster`

`git clone https://github.com/quickmsg/smqtt`

## 打包
    
### 1. smqtt-ui安装前端依赖
    
```bash
npm install
```
    
### 2. 打包java代码

```bash
mvn compile package -Dmaven.test.skip=true -P jar,web
```
在smqtt-bootstrap/target目录下生成jar包
        
> 或者直接去下载最新的jar 
>
> - https://github.com/quickmsg/smqtt/releases   
>  
> - https://gitee.com/quickmsg/mqtt-cluster/releases

### 3. 准备配置文件

选择空目录下新建一个config.properties文件

```bash
# 日志级别 ALL｜TRACE｜DEBUG｜INFO｜WARN｜ERROR｜OFF
smqtt.log.level=INFO
# 开启tcp端口
smqtt.tcp.port=1883
# 高水位
smqtt.tcp.lowWaterMark=4000000
# 低水位
smqtt.tcp.highWaterMark=80000000
# 开启ssl加密
smqtt.tcp.ssl=false
# 证书crt smqtt.tcp.ssl.crt =
# 证书key smqtt.tcp.ssl.key =
# 开启日志
smqtt.tcp.wiretap=false
# boss线程
smqtt.tcp.bossThreadSize=4
# work线程
smqtt.tcp.workThreadSize=8
# websocket端口
smqtt.websocket.port=8999
# websocket开启
smqtt.websocket.enable=true
# smqtt用户
smqtt.tcp.username=smqtt
# smqtt密码
smqtt.tcp.password=smqtt
# 开启http
smqtt.http.enable=true
# 开启http日志
smqtt.http.accesslog=true
# 开启ssl
smqtt.http.ssl.enable=false
# smqtt.http.ssl.crt =
# smqtt.http.ssl.key =
# 开启管理后台（必须开启http）
smqtt.http.admin.enable = true
# 管理后台登录用户
smqtt.http.admin.username=smqtt
# 管理后台登录密码
smqtt.http.admin.password=smqtt
# 开启集群
smqtt.cluster.enable=false
# 集群节点地址
smqtt.cluster.url=127.0.0.1:7771,127.0.0.1:7772
# 节点端口
smqtt.cluster.port=7771
# 节点名称
smqtt.cluster.node=node-1

# 数据库配置(选配)
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

# redis配置(选配)
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
redis.cluster.scan.interval=1000
redis.cluster.nodes=127.0.0.1:7000,127.0.0.1:7001,127.0.0.1:7002,127.0.0.1:7003,127.0.0.1:7004,127.0.0.1:7005
redis.cluster.read.mode=SLAVE
redis.cluster.retry.attempts=3
redis.cluster.slave.connection.pool.size=64
redis.cluster.master.connection.pool.size=64
redis.cluster.retry.interval=1500

# 哨兵配置
redis.sentinel.master=mymaster
redis.sentinel.nodes=127.0.0.1:26379,127.0.0.1:26379,127.0.0.1:26379
```

### 4. 启动服务

```bash
java -jar smqtt-bootstrap-1.0.1-SNAPSHOT.jar <conf.properties路径>
```



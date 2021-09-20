<!--
.. title: Jar/Docker启动集群
.. slug: start-cluster-jar-docker
-->

## config.properties文件添加配置


## jar/docker 配置文件启动


### 配置文件如下

```properties

# 开启集群
smqtt.cluster.enable=false
# 集群节点地址
smqtt.cluster.url=127.0.0.1:7771,127.0.0.1:7772
# 节点端口
smqtt.cluster.port=7771
# 节点名称
smqtt.cluster.node=node-1

```



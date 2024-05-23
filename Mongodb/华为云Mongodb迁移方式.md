# 华为云—>联通云Mongodb

[TOC]

## MongDump导入导出

### 华为云导出数据

> 如果源端是阿里云获取其他云厂商不支持导出备份文件，那么可以采用如下方式进行导出
>
> 1. 在源端开通一台ECS，通过内部进行导出到本地，然后再通过公网传输到目标端
> 2. 在目标端开通一台ECS，通过公网进行导出到本地，然后再通过公网传输到目标端

![image-20240521103306571](./华为云Mongodb迁移方式.assets/\image-20240521103306571.png)

![image-20240521103340792](./华为云Mongodb迁移方式.assets/\image-20240521103340792.png)

![image-20240521103359752](./华为云Mongodb迁移方式.assets/\image-20240521103359752.png)

![image-20240521103440468](./华为云Mongodb迁移方式.assets/\image-20240521103440468.png)

![image-20240521103541119](./华为云Mongodb迁移方式.assets/\image-20240521103541119.png)

安装网页进行挂载外部桶
![image-20240521103604312](./华为云Mongodb迁移方式.assets/\image-20240521103604312.png)

![image-20240521103700900](./华为云Mongodb迁移方式.assets/\image-20240521103700900.png)

![image-20240521103715147](./华为云Mongodb迁移方式.assets/\image-20240521103715147.png)

### 目标端部署中转Mongodb

> 注意：云产品到云产品是不能直接恢复数据的，只能导入数据。
>
> 因为源端华为下载下来的备份文件为数据文件形式，只能通过部署自建Mongodb进行恢复数据，恢复数据后，然后通过自建的Mongodb进行导出，导出后将导出的数据导入到云产品中。

- 安装软件包

```apl
tar -zxf mongodb-linux-x86_64-rhel70-4.0.0 -C /usr/local
mv /usr/local/mongodb-linux-x86_64-rhel70-4.0.0
```

- 创建日志目录和数据目录

```apl
cd /usr/local/mongodb/
mkdir /data1/logs/ -p
```

- 编写配置文件进行启动Mongodb

```apl
[root@02 ~]# cat /usr/local/mongodb/mongo.cnf
systemLog:
  destination: file
  logAppend: true
  path: /data1/logs/mongod.log

storage:
  dbPath: /data1
  journal:
    enabled: true
  directoryPerDB: true
  wiredTiger:
    engineConfig:
      directoryForIndexes: true

net:
  bindIp: 127.0.0.1
  port: 27017
```

- 创建软连接

```apl
ln -s /usr/local/mongodb/bin/* /usr/local/bin/
mongod -f data1/mongodb.cnf 
```

### 上传备份文件

通过winscp

![image-20240521104744006](./华为云Mongodb迁移方式.assets/\image-20240521104744006.png)

### 自建Mongodb导出数据

```apl
自建导出
mongodump -h 127.0.0.1:27017 -u rwuser --authenticationDatabase admin --out=/data/a --gzip
——————————————————————————————
云产品导入
mongorestore -h 10.10.1.237:27017 -u admin --authenticationDatabase admin --gzip /data/a/
```

![image-20240521112843413](./华为云Mongodb迁移方式.assets/image-20240521112843413.png)

![image-20240521112857736](./华为云Mongodb迁移方式.assets/image-20240521112857736.png)

### 查看数据

```apl
华为云源端Mongodb云产品
[root@02 ~]# mongo 123.60.24.98:8635/admin -u rwuser
MongoDB shell version v4.0.0
Enter password:
replica:PRIMARY> show dbs
TelCount    0.001GB
admin       0.000GB
config      0.000GB
handle     42.155GB
idis_lhs  232.607GB
local      20.502GB
replica:PRIMARY>
————————————————————————————————————————
目标端Mongodb云产品
[root@02 ~]# mongo 10.10.0.230/admin -u admin
MongoDB shell version v4.0.0
Enter password:
ac9693101-a7e6-4dde-abc5-dfdc6ecf0617:PRIMARY> show dbs
TelCount    0.001GB
admin       0.000GB
config      0.000GB
handle     49.317GB
idis_lhs  183.589GB
local       9.143GB
```

## MongoShake工具

[[alibaba/MongoShake：MongoShake 是一个基于 MongoDB oplog 的通用数据复制平台。冗余复制和主动-主动复制是两个最重要的功能。基于mongodb oplog的集群复制工具，可以满足迁移和同步的需求，进一步实现灾备和多活功能。 (github.com)](https://github.com/alibaba/MongoShake)](https://github.com/alibaba/MongoShake)

[MongoShake最佳实践-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/719704)

- https://developer.aliyun.com/article/719704

### 介绍

MongoShake从源库抓取oplog数据，然后发送到各个不同的tunnel通道。源库支持：ReplicaSet，Sharding，Mongod，目的库支持：Mongos，Mongod。现有通道类型有：

1. Direct：直接写入目的MongoDB
2. RPC：通过net/rpc方式连接
3. TCP：通过tcp方式连接
4. File：通过文件方式对接
5. Kafka：通过Kafka方式对接
6. Mock：用于测试，不写入tunnel，抛弃所有数据

消费者可以通过对接tunnel通道获取关注的数据，例如对接Direct通道直接写入目的MongoDB，或者对接RPC进行同步数据传输等。此外，用户还可以自己创建自己的API进行灵活接入。下面2张图给出了基本的架构和数据流。

![pic1](./华为云Mongodb迁移方式.assets/dataflow-1716271607263-15.png)

### 从MongoDB从副本集同步到MongDB副本集

- 内网环境(专线)

```apl
设源端是三副本：10.1.1.1:1001, 10.2.2.2:2002, 10.3.3.3:3003，目的端也是三副本：10.5.5.5:5005, 10.6.6.6:6006, 10.7.7.7:7007。同步模式是全量+增量同步。
```

- 公网

```
设源端是三副本：142.24.42.222:8635 目的端也是三副本,但是只有一个公网地址：10.5.5.5:5005, 10.6.6.6:6006, 10.7.7.7:7007。同步模式是全量+增量同步。
```

副本同步到副本

```apl
# 同步模式，all表示全量+增量同步，full表示全量同步，incr表示增量同步。
sync_mode = all
# 副本集：mongodb://username1:password1@primaryA,secondaryB,secondaryC
# 分片集:mongodb://username1:password1@primaryA,secondaryB,secondaryC;mongodb://username2:password2@primaryX,secondaryY,secondaryZ

mongo_urls = mongodb://rwuser:1234%40Idis@123.60.24.98:8635
# 此处配置通道的地址，格式与mongo_urls对齐。(目标端)
tunnel.address = mongodb://admin:Njlt0514@116.147.34.212:2701

# checkpoint的具体写入的MongoDB地址，如果不配置，对于副本集将写入源库(db=mongoshake)，对于分片集
# 将写入config-server（db=admin），注意创建mongoshake表，用于校验数据，可以在源端和目标端
checkpoint.storage.url =mongodb://admin:Njlt0514@116.147.34.212:2701
# 内部发送的worker数目，如果机器性能足够，可以提高worker个数。
incr_sync.worker = 8

```

#### 配置文件解析

```apl
v2.4开始的参数请参考github wiki配置参数说明，下面是2.2及之前的参数。具体请查看配置文件的注释，此处只做简单解释

mongo_urls: 源mongodb的连接地址
mongo_connect_mode: 源端连接的模式，有几种模式可选：从seconary拉取；从primary拉取；secondary优先拉取；单节点拉取
sync_mode: sync模式，有几种模式可选：全量，增量，全量+增量
http_profile: 提供restful接口，用户可以查看一些内部运行情况，也可以对接监控。
system_profile: profile端口，可以查看进程运行的堆栈情况。
log: log日志相关参数。
filter.namespace.black: 黑名单过滤。黑名单内的库表不会被同步，剩下的同步。
filter.namespace.white: 白名单过滤。白名单内的库表会被同步，剩下的过滤掉。黑白名单最多只能配置一个，不配置会同步所有库表。
filter.pass.special.db: 有些特别的库表会被过滤，如admin，local, config库，如果一定要开启，可以在这里进行配置。
oplog.gids: 用于云上双向同步。
shard_key: 内部对数据多线程的哈希方式，默认collection表示按表级别进行哈希。
worker: 增量阶段并发写入的线程数，如果增量阶段性能不够，可以提高这个配置。
worker内部相关配置: worker.batch_queue_size, adaptive.batching_max_size, fetcher.buffer_capacity, 关于内部队列的相关配置，具体请参考github wiki文档。
worker.oplog_compressor: 压缩模式，如果是非direct模式开启这个可以减少网络传输的开销。
tunnel.address: 目的端对接的地址。
context.storage: checkpoint存储的位置，database表示把数据存入MongoDB，api表示把数据存入用户自己提供的http接口。
context.storage.url: checkpoint写入到哪个MongoDB，如果源是sharding，此处配置cs地址，checkpoint会写入admin库；如果是副本集，不配置，会默认写入源库，配置则写入配置的库里面。
context.address: checkpoint写入的表的名字。
context.start_position: checkpoint启动开始拉取的增量时间位点。如果本身checkpoint已经存在（参考上述context的位置），那么则按照context信息进行拉取，如果不存在，则按照这个位点进行增量拉取。
master_quorum: 如果以主备模式拉取同一个源，则这个参数需要启用。
transform.namespace: 命名空间的转换，a.b:c.d表示把源端a库下面的c表同步到目的端c库下面的d表。
replayer.dml_only: 默认不同步DDL，false表示同步DDL。DDL包括建表，删库，建索引等语句。
replayer.executor.upsert: 目的端如果update语句对应的主键id不存在，是否将update语句更改为insert语句。
replayer.executor.insert_on_dup_update: 目的端如果insert语句对应的主键id已经存在，是否将insert语句更改为update语句。
replayer.conflict_write_to: 对于写入冲突的情况，是否需要记录冲突的文档。
replayer.durable: 测试选项，false表示取消写入，只用于拉取调试。
replayer.collection_parallel: 全量同步按表并发的并发度。
replayer.document_parallel: 全量同步同一个表内并发写入的线程数。
replayer.document_batch_size: 全量同步一次性batch的大小。
replayer.collection_drop: 如果目的库表存在，是否先删除目的库再进行同步。
```



## 阿里云DTS迁移

![image-20240521210945120](./华为云Mongodb迁移方式.assets/image-20240521210945120.png)

## Cloudcancal

- 接入数据源

![image-20240521211156147](./华为云Mongodb迁移方式.assets/image-20240521211156147.png)

创建并启动任务

![image-20240521211220676](./华为云Mongodb迁移方式.assets/image-20240521211220676.png)

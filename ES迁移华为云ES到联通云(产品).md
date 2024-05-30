# ES迁移华为云ES到联通云(产品)

[TOC]

**测试华为云**

## 华为云部署Elasticsearch

### 创建ES产品

1. **创建css**

   ![image-20240304094954438](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304094954438.png?raw=true)

2. **定义资源配置**

   ![image-20240304095124337](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304095124337.png?raw=true)

3. 配置VPC网络，和用户密码

   ![image-20240304095203162](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304095203162.png?raw=true)

   **查看安全组，并且配置**

   ![image-20240304095415070](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304095415070.png?raw=true)

   ![image-20240304095512153](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304095512153.png?raw=true)

4. **创建相关存储操作**

   ![image-20240304095722904](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304095722904.png?raw=true)

### 进入kibana(创建数据)

![image-20240304102523016](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304102523016.png?raw=true)

### 测试连通性

![image-20240304102941333](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304102941333.png?raw=true)

## 华为云备份Elasticsearch

### 进入集群快照

**该方式是将es集群状态通过快照的方式存储在OBS对象存储中（snapshot）**

![image-20240304103217080](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304103217080.png?raw=true)

### 创建快照

**备份所有索引（*）**

![image-20240304103325019](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304103325019.png?raw=true)

## 华为OBS快照查看

### 查看es备份是snapshot的快照文件

![image-20240304103647943](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304103647943.png?raw=true)

## 华为快照同步目标端

### 目标端安装juicefs

**通过juicefs同步源端OBS快照文件**

```apl
juicefs sync --no-https s3://AQSNVWEXAR6DL1Q5IC08:m93QjhqldlMqBq0is2RsAu5FjlNLhnE4ZxqKraUj@elasti-oss.obs.cn-north-4.myhuaweicloud.com/css_repository/css-cc27/ /data/backup/
```

![image-20240304105237520](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304105237520.png?raw=true)

# 联通云部署ES(可忽略)

## 下载ES

官网：https://www.elastic.co/cn/downloads/elasticsearch

> 由于es和jdk是一个强依赖的关系，所以当我们在新版本的ElasticSearch压缩包中包含有自带的jdk，但是当我们的Linux中已经安装了jdk之后，就会发现启动es的时候优先去找的是Linux中已经装好的jdk，此时如果jdk的版本不一致，就会造成jdk不能正常运行，报错如下：
>
> 注：如果Linux服务本来没有配置jdk，则会直接使用es目录下默认的jdk，反而不会报错

### 执行解压缩命令

```apl
tar -zxvf elasticsearch-7.13.2-linux-x86_64.tar.gz -C /usr/local
```

- 进入bin目录
  - cd /usr/local/elasticsearch-7.13.2/bin

### 修改elastisearch JDK 环境配置

- 修改elastisearch JDK 环境配置

  - vim ./elasticsearch

  - ```apl
    #下添加如下内容
    export ES_JAVA_HOME=/usr/local/elasticsearch-7.13.2/jdk
    export PATH=$ES_JAVA_HOME/bin:$PATH
    
    if [ -x "$ES_JAVA_HOME/bin/java" ]; then
            JAVA="/usr/local/elasticsearch-7.13.2/jdk/bin/java"
    else
            JAVA=`which java`
    fi
    ```

## 解决ES启动问题

### 内存不足问题

#### **报错内容：** 

```apl
error:
OpenJDK 64-Bit Server VM warning: INFO: os::commit_memory(0x00000000c6a00000, 962592768, 0) failed; error='Not enough space' (errno=12)
        at org.elasticsearch.tools.launchers.JvmOption.flagsFinal(JvmOption.java:119)
        at org.elasticsearch.tools.launchers.JvmOption.findFinalOptions(JvmOption.java:81)
        at org.elasticsearch.tools.launchers.JvmErgonomics.choose(JvmErgonomics.java:38)
        at org.elasticsearch.tools.launchers.JvmOptionsParser.jvmOptions(JvmOptionsParser.java:13

```

#### **修复：**

> 进入es的jvm.options配置文件进行修改

```apl
vim /usr/local/elasticsearch-7.13.2/config/jvm.options
末行模式输入: /Xms （进行查找）
添加如下内容：
默认配置如下：
-Xms2g
-Xmx2g
默认的配置占用内存太多了，调小一些：将256改为2g
-Xms256m
-Xmx256m
```



### 解决系统默认mmap （内存映射）

**Elasticsearch 使用较大的内存映射文件（mmap）来管理其索引文件，所以需要修改**

```apl
su root
vim /etc/sysctl.conf
添加：
vm.max_map_count=300000

sysctl -p
	输出↓
    net.ipv4.neigh.default.gc_thresh1 = 8192
    net.ipv4.neigh.default.gc_thresh2 = 32768
    net.ipv4.neigh.default.gc_thresh3 = 65536
	vm.max_map_count = 300000

```

### 进程文件打开数量限制

**为了确保 Elasticsearch 能够正常运行，建议将操作系统的 `max file descriptors` 设置调整到足够大的数值，以满足 Elasticsearch 集群的需求**

```apl
vim /etc/security/limits.conf

# End of file 
#soft 软限制
#hard 硬限制
#nofile 打开文件数量
#nproc 创建的进程数量
* soft nofile 65536
* hard nofile 131072
* soft nproc 2048
* hard nproc 4096

————
reboot重启系统
```

## 配置使用环境

### 创建用户

- `useradd user-es`

### 创建属组

- `chown user-es:user-es -R /usr/local/elasticsearch-7.13.2`

### 切换用户

- `su user-es`

### 修改ES config配置文件

```apl
添加修改：
cat /usr/local/elasticsearch-7.13.2/config/elasticsearch.yml  | grep -v [#]

添加注释的这两行，后面安装head有用
#http.cors.enabled: true 
#http.cors.allow-origin: "*"

cluster.name: elasticsearch
node.name: es-node-1

path.data: /path/to/data
path.logs: /path/to/logs

network.host: 0.0.0.0
http.port: 19200

cluster.initial_master_nodes: ["es-node-1"]
path.repo: ["/data/backup"]

```



###  启动es

- `cd /usr/local/elasticsearch-7.13.2/bin`
- `./elasticsearch`

**访问公网IP**

![image-20240229201449356](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240229201449356.png?raw=true)



## 安装Elasticsearch-head插件

>ealsticsearch只是后端提供各种resulful api，那么怎么直观的看它的信息呢？
>
>elasticsearch-head是一款专门针对于elasticsearch的客户端工具，用来展示数据。
>
>elasticsearch-head是基于JavaScript语言编写的，可以使用npm部署
>npm是Nodejs下的包管理器。

**下载地址：** https://github.com/mobz/elasticsearch-head

- mv elasticsearch-head-5.0.0 /usr/local/
- `cd /usr/local/elasticsearch-head-5.0.0`

### 安装插件

- yum install epel-release bzip2（安装插件库）
- yum install nodejs npm （安装npm）

### 安装head自带环境包

- npm install （如果执行失败则跟换下面命令，通过更换镜像地址，再次执行）
- npm config set registry https://registry.npmmirror.com

### 安装head环境依赖插件

- ```
  - （报错时安装也行）
  npm install -g grunt
  npm install -g grunt-cli
  
  - （安装head环境包）
  npm install -g nrm
  ```

### 启动head

- 修改ES config 配置文件

  > vim /usr/local/elasticsearch-7.13.2/config/elasticsearch.yml

  - ```apl
    添加修改：
    cat /usr/local/elasticsearch-7.13.2/config/elasticsearch.yml  | grep -v [#]
    
    将注释的这两行重新启用即可，表示允许head进行跨域访问
    http.cors.enabled: true 
    http.cors.allow-origin: "*"
    
    cluster.name: elasticsearch
    node.name: es-node-1
    
    path.data: /path/to/data
    path.logs: /path/to/logs
    
    network.host: 0.0.0.0
    http.port: 19200
    
    cluster.initial_master_nodes: ["es-node-1"]
    path.repo: ["/data/backup"]
    ```

- npm run start

**访问测试：**

![image-20240229220655159](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240229220655159.png?raw=true)

# 联通云 恢复ES数据

### 创建备份创库

```apl
curl -u elastic:Lzh123com -XPUT "http://localhost:9200/_snapshot/my_backup" -H 'Content-Type: application/json' -d '
{
  "type": "fs",
  "settings": {
    "location": "/data/backup"
  }
}'
```

### 查看源端备份文件名称

**查看名称进行恢复该名称**

![image-20240304105716729](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304105716729.png?raw=true)

### 数据恢复

```apl
curl -XPOST "http://localhost:19200/_snapshot/my_backup/snapshot-a186/_restore"

{"accepted":true}[root@es backup]#
```

![image-20240304105803537](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304105803537.png?raw=true)

# 数据验证

```apl
curl -XGET "http://localhost:19200/_snapshot/my_backup/snapshot-a186/_status"
```

![image-20240304110404661](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304110404661.png?raw=true)

**查看目标端数据是否同步过来**

![image-20240304110455684](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304110455684.png?raw=true)

![image-20240304110513053](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304110513053.png?raw=true)

![image-20240304110540879](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304110540879.png?raw=true)


# 华为云CCE容器服务迁移到联通云CSK/

[TOC]

**测试购买资源**

## 购买华为云CCE

### 进入购买页面

![image-20240311142636455](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311142636455.png?raw=true)

### 选择资源配置

![image-20240311142810936](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311142810936.png?raw=true)

### 插件选择

![image-20240311142935877](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311142935877.png?raw=true)

![image-20240311142959291](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311142959291.png?raw=true)



## CCE节点配置

### 创建节点

![image-20240311144050955](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311144050955.png?raw=true)



![image-20240311144159674](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311144159674.png?raw=true)

### 选择节点资源



![image-20240311144642721](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311144642721.png?raw=true)

### 查看节点(节点创建成功后自动创建ecs)

![image-20240311145909818](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311145909818.png?raw=true)

### 部署kubectl

**查考如何内容进行创建**

https://console.huaweicloud.com/cce2.0/?agencyId=509c01f0db694366b8e8a8a74847bbdd&region=cn-north-4&locale=zh-cn#/cce/cluster/c39f6842-df70-11ee-be77-0255ac10026e/detail?category=Turbo

![image-20240311151047388](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311151047388.png?raw=true)

![image-20240311151658470](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240311151658470.png?raw=true)

## 安装velero

官方文档：https://velero.io

Github软件包地址：https://github.com/vmware-tanzu/velero/releases

>wget https://github.com/vmware-tanzu/velero/releases/download/v1.12.3/velero-v1.12.3-linux-amd64.tar.gz 
>
>>tar -zxf velero-v1.12.3-linux-amd64.tar.gz
>>
>>cp velero-v1.12.3-linux-amd64/velero /usr/local/bin/velero
>
>>velero version
>>
>>> 因为目前还未部署velero的server端所以找不到
>>>
>>> Client:
>>> 	Version: v1.12.3
>>> 	Git commit: 684f71306e9c2fda204a16cb012dc209523cfae1
>>> <error getting server version: no matches for kind "ServerStatusRequest" in version "velero.io/v1">

### 创建密钥(联通云AK SK)

指定velero使用的AK：SK

> mkdir /k8s-test/velero/velero -p
>
> vim /k8s-test/velero/velero/oss-credentials.txt

```apl
腾讯云
[default]
aws_access_key_id = AQSNVWEXAR6DL1Q5IC08
aws_secret_access_key = m93QjhqldlMqBq0is2RsAu5FjlNLhnE4ZxqKraUj
-----
联通云
[default]
aws_access_key_id = 82E7E67E37F041DFA8308A04F3BFB4D08968
aws_secret_access_key = E3F2DE4E3D2E4A15B511BDA1946311BC6793
```

### 创建velero

```apl
华为云
velero install \
  --provider aws \
  --bucket elasti-oss \
  --image velero/velero:v1.12.3 \
  --plugins velero/velero-plugin-for-aws:v1.8.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=north-4,s3ForcePathStyle="false",s3Url=https://obs.cn-north-4.myhuaweicloud.com \
 --use-restic \
 --use-node-agent \
  --uploader-type=restic

----
联通云
velero install \
  --provider aws \
  --bucket liuzhenh01test \
  --image velero/velero:v1.12.3 \
  --plugins velero/velero-plugin-for-aws:v1.8.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=gzgy2,s3ForcePathStyle="false",s3Url=https://obs-gzgy2.cucloud.cn

```

**选项说明：**

- `--provider`：定义插件提供方；aws、alibaba等待
- `--bucket`：指定对象存储Bucket桶名称；

- `--image`：定义运行velero的镜像，默认与velero客户端一致；
- `--plugins`：指定使用aws s3兼容的插件镜像；
- `--namespace`：指定部署的namespace名称，默认为velero；
- `--secret-file`：指定对象存储认证文件；
- `--use-node-agent`：创建Velero Node Agent守护进程，托管FSB模块；
- `--use-volume-snapshots`：是否启使用快照；
- `--backup-location-config`：指定对象存储地址信息；
- region=`gzgy2`,s3ForcePathStyle="false",s3Url=https://obs-gzgy2.cucloud.cn
  - [`region=`是指定**AWS区域**的名称，例如`gzgy2`表示**华北地区**](https://github.com/vmware-tanzu/velero/issues/5360)[2](https://github.com/vmware-tanzu/velero/issues/5360)[；`s3ForcePathStyle="false"`表示是否使用**路径式**的S3 URL，即以域名开头的URL](https://github.com/grafana/loki/issues/8638)[3](https://github.com/grafana/loki/issues/8638)[。如果您使用的是**AlibabaCloud OSS**等不支持路径式的S3服务，那么您需要将`s3ForcePathStyle="false"`设置为`true`](http://localstack:4566/)[4](http://localstack:4566/)。

#### 如果出现ImageError

> 手动拉取，并且更行velero的pod

```apl
crictl pull velero/velero-plugin-for-aws:v1.8.1
crictl pull velero/velero:v1.12.3
kubectl rollout restart deployment -n velero velero
velero backup-location get
```

![image-20240313095534967](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313095534967.png?raw=true)

### 创建Pod资源

![image-20240313093444048](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313093444048.png?raw=true)

### Velero备份资源

```apl
velero backup create lzh-velero-test --include-namespaces="*" -n velero

velero backup create lzh-velero-test --include-namespaces="*" --exclude-namespaces="kube-system" -n velero

velero backup create 2024-3-25-no-kubesystem-storage --include-namespaces="*" --exclude-namespaces="kube-system" --exclude-resources="storageclasses.storage.k8s.io" -n velero

```

![image-20240313093530335](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313093530335.png?raw=true)

### 查看OBS对象存储

**查看备份是否成功**

![image-20240313095641078](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313095641078.png?raw=true)

## 联通云CKS恢复

![image-20240313095822666](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313095822666.png?raw=true)

### 安装velero

官方文档：https://velero.io

Github软件包地址：https://github.com/vmware-tanzu/velero/releases

>wget https://github.com/vmware-tanzu/velero/releases/download/v1.12.3/velero-v1.12.3-linux-amd64.tar.gz 
>
>>tar -zxf velero-v1.12.3-linux-amd64.tar.gz
>>
>>cp velero-v1.12.3-linux-amd64/velero /usr/local/bin/velero
>
>>velero version
>>
>>> 因为目前还未部署velero的server端所以找不到
>>>
>>> Client:
>>> 	Version: v1.12.3
>>> 	Git commit: 684f71306e9c2fda204a16cb012dc209523cfae1
>>> <error getting server version: no matches for kind "ServerStatusRequest" in version "velero.io/v1">

### 创建密钥(联通云AK SK)

指定velero使用的AK：SK

> mkdir /k8s-test/velero/velero -p
>
> vim /k8s-test/velero/velero/oss-credentials.txt

```apl
腾讯云
[default]
aws_access_key_id = AQSNVWEXAR6DL1Q5IC08
aws_secret_access_key = m93QjhqldlMqBq0is2RsAu5FjlNLhnE4ZxqKraUj
-----
联通云
[default]
aws_access_key_id = 82E7E67E37F041DFA8308A04F3BFB4D08968
aws_secret_access_key = E3F2DE4E3D2E4A15B511BDA1946311BC6793
```

### 创建velero

```apl
华为云
velero install \
  --provider aws \
  --bucket elasti-oss \
  --image velero/velero:v1.12.3 \
  --plugins velero/velero-plugin-for-aws:v1.8.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=north-4,s3ForcePathStyle="false",s3Url=https://obs.cn-north-4.myhuaweicloud.com \
  --use-node-agent \
  --uploader-type=restic

----
联通云
velero install \
  --provider aws \
  --bucket liuzhenh01test \
  --image velero/velero:v1.12.3 \
  --plugins velero/velero-plugin-for-aws:v1.8.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=gzgy2,s3ForcePathStyle="false",s3Url=https://obs-gzgy2.cucloud.cn

```

**选项说明：**

- `--provider`：定义插件提供方；aws、alibaba等待
- `--bucket`：指定对象存储Bucket桶名称；

- `--image`：定义运行velero的镜像，默认与velero客户端一致；
- `--plugins`：指定使用aws s3兼容的插件镜像；
- `--namespace`：指定部署的namespace名称，默认为velero；
- `--secret-file`：指定对象存储认证文件；
- `--use-node-agent`：创建Velero Node Agent守护进程，托管FSB模块；
- `--use-volume-snapshots`：是否启使用快照；
- `--backup-location-config`：指定对象存储地址信息；
- region=`gzgy2`,s3ForcePathStyle="false",s3Url=https://obs-gzgy2.cucloud.cn
  - [`region=`是指定**AWS区域**的名称，例如`gzgy2`表示**华北地区**](https://github.com/vmware-tanzu/velero/issues/5360)[2](https://github.com/vmware-tanzu/velero/issues/5360)[；`s3ForcePathStyle="false"`表示是否使用**路径式**的S3 URL，即以域名开头的URL](https://github.com/grafana/loki/issues/8638)[3](https://github.com/grafana/loki/issues/8638)[。如果您使用的是**AlibabaCloud OSS**等不支持路径式的S3服务，那么您需要将`s3ForcePathStyle="false"`设置为`true`](http://localstack:4566/)[4](http://localstack:4566/)。

#### 如果出现ImageError

> 手动拉取，并且更行velero的pod

```apl
crictl pull velero/velero-plugin-for-aws:v1.8.1
crictl pull velero/velero:v1.12.3
kubectl rollout restart deployment -n velero velero
```

### 恢复

> 获取备份资源信息

```apl
velero backup get
velero backup-location get
```

![image-20240313100202414](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313100202414.png?raw=true)

```apl
velero restore create --from-backup lzh-velero-test 
```

### 查看资源是否恢复

![image-20240313100650862](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240313100650862.png?raw=true)



- 刘振华  lzh_888888_1223@163.com

![image-20240325232354706](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240325232354706.png?raw=true)

![image-20240325232846453](https://github.com/liuzhenhua1223/Image/blob/master/img/001image-20240325232846453.png?raw=true)

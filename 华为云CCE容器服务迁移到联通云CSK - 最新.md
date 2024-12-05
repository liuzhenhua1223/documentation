# 华为云CCE容器服务迁移到联通云CSK

[TOC]

**测试购买资源**

## 购买华为云CCE

### 进入购买页面

![image-20240311142636455](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311142636455.png?raw=true)

### 选择资源配置

![image-20240311142810936](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311142810936.png?raw=true)

### 插件选择

![image-20240311142935877](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311142935877.png?raw=true)

![image-20240311142959291](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311142959291.png?raw=true)

## CCE节点配置

### 创建节点

![image-20240311144050955](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311144050955.png?raw=true)

![image-20240311144159674](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311144159674.png?raw=true)

### 选择节点资源

![image-20240311144642721](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311144642721.png?raw=true)

### 查看节点(节点创建成功后自动创建ecs)

![image-20240311145909818](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311145909818.png?raw=true)

### 部署kubectl

**查考如何内容进行创建**

https://console.huaweicloud.com/cce2.0/?agencyId=509c01f0db694366b8e8a8a74847bbdd&region=cn-north-4&locale=zh-cn#/cce/cluster/c39f6842-df70-11ee-be77-0255ac10026e/detail?category=Turbo

![image-20240311151047388](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311151047388.png?raw=true)

![image-20240311151658470](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240311151658470.png?raw=true)

## velero 简介

Velero 是一个提供 Kubernetes 集群和持久卷的备份、迁移以及灾难恢复等的开源工具。

Velero 是一个云原生的灾难恢复和迁移工具，它本身也是开源的, 采用 Go 语言编写，可以安全的备份、恢复和迁移Kubernetes集群资源和持久卷。

Velero 是一种云原生的Kubernetes优化方法，支持标准的K8S集群，既可以是私有云平台也可以是公有云。除了灾备之外它还能做资源移转，支持把容器应用从一个集群迁移到另一个集群。

使用velero可以对集群进行备份和恢复，降低集群DR造成的影响。velero的基本原理就是将集群的数据以json格式备份到对象存储中，在恢复的时候将数据从对象存储中拉取下来。

### **组成部分**

Velero组件一共分两部分，分别是客户端和服务端。

- 客户端：运行在本地的velero命令行工具，包括安装服务端、备份、定时任务备份、恢复等命令，特别需要注意的是，安装服务端时需要在机器上已配置好kubectl及集群kubeconfig。
- 服务端：运行在Kubernetes集群中（运行在Pod中）。

### **velero使用场景**

- 灾备场景：提供备份恢复k8s集群的能力
- 迁移场景：提供拷贝集群资源到其他集群的能力（两个集群连接同一个对象存储地址）

### **velero备份与直接对etcd备份区别**

- 直接备份 Etcd 是将集群的全部资源备份起来，而 Velero 可以对 Kubernetes 集群内对象级别进行备份。
- 除了对 Kubernetes 集群进行整体备份外，Velero 还可以通过对 Type、Namespace、Label、Pod
  等对象进行分类备份或者恢复。

### Velero备份恢复思维导图

![image-20240809090106039](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240809090106039.png?raw=true)

## 原理

### Velero工作原理

每个Velero的操作（如按需备份backup，计划备份schdule，还原restore）都是自定义资源，使用Kubernetes [自定义资源定义（CRD）定义](https://kubernetes.io/docs/concepts/api-extension/custom-resources/#customresourcedefinitions)并存储在 etcd中，Velero还包括 对自定义资源执行备份、恢复和所有相关操作的控制器，例如备份控制器BackupController、恢复控制器RestoreController ，诸如此类的控制器在成功部署velero服务器后就生效了，它们负责监听对应的自定义资源（backup，schdule，restore），在监听到这些自定义资源后，验证它们，通过验证的资源将加入到velero的工作队列中，有序的完成它们对应的工作流程。Velero非常灵活，可以备份或还原群集中的所有对象，也可以按类型，命名空间或标签过滤对象。

### 工作模式

- `数据文件复制：`
  方式：通过工具（如 Restic）将数据文件从源位置复制到目标存储位置。
  优点：适用于没有原生快照功能的存储类型，如 NFS、AzureFile 等。灵活性高，可以备份任意类型的文件。
  缺点：速度较慢，特别是对于大数据量的备份。需要更多的存储空间，因为每次备份都是完整的文件复制。
- `卷快照：`
  方式：利用存储提供商的原生快照功能来创建卷的快照。
  优点：速度快，因为它利用了存储系统的原生功能。占用的存储空间较少，因为快照通常是增量的，只记录变化部分。
  缺点：依赖于存储提供商的支持，不是所有存储类型都支持快照功能。可能需要额外的配置和权限。

### 备份工作流程

当运行velero backup create 时：

1. Velero客户端调用Kubernetes API server以创建Backup对象；
2. 该BackupController检测到Backup对象被创建并执行验证；
3. BackupController开始备份过程，它通过向Kubernetes API server查询资源来收集要备份的数据；
4. BackupController调用对象存储服务（例如AWS S3 ： MinIO）上载备份文件。

默认情况下，velero backup create支持任何持久卷的磁盘快照，您可以通过指定其他标志来调整快照，运行velero backup create --help可以查看可用的标志，可以使用--snapshot-volumes=false选项禁用快照。

![image-20240809090223889](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240809090223889.png?raw=true)

### 恢复工作流程

当运行 velero restore create 时:

1. Velero客户端调用Kubernetes API server以创建Restore对象；
2. 该RestoreController 检测到Restore对象被创建并执行验证；
3. RestoreController 从对象存储服务中获取指定备份信息。然后，它在备份的资源上运行一些预处理，以确保资源能在新的集群上工作。

4. RestoreController开始逐个恢复符合条件的资源。Velero将当前资源提取到Kubernetes资源对象中。根据您指定的资源类型和恢复选项，Velero将在尝试创建资源之前对资源进行以下修改或对目标集群进行准备：

1. 1. RestoreController确保目标命名空间存在。如果目标命名空间不存在，RestoreController将在集群上创建一个新的命名空间;
   2. 如果资源是PersistentVolume（PV），RestoreController将重命名PV并重新映射其namespace;
   3. 如果资源是 PersistentVolumeClaim（PVC），RestoreController将修改PVC元数据;

5. RestoreController在目标集群上创建资源对象。如果资源是PV，则RestoreController将根据PV的备份方式从持久快照、文件系统备份或CSI快照中恢复PV数据;

6. 默认情况下，Velero 执行的是非破坏性还原，意味着它不会删除目标集群上的任何数据。如果备份中的某个资源已经存在于目标集群中，Velero 将跳过该资源;

## 安装velero

官方文档：https://velero.io

Github软件包地址：https://github.com/vmware-tanzu/velero/releases

>wget https://github.com/vmware-tanzu/velero/releases/download/v1.7.0/velero-v1.7.0-linux-amd64.tar.gz
>
>>tar -zxf velero-v1.12.3-linux-amd64.tar.gz
>>
>>cp velero-v1.7.0-linux-amd64/velero /usr/local/bin/velero
>
>>velero version
>>
>>> 因为目前还未部署velero的server端所以找不到
>>>
>>> Client:
>>> 	Version: v1.12.3
>>> 	Git commit: 684f71306e9c2fda204a16cb012dc209523cfae1
>>> <error getting server version: no matches for kind "ServerStatusRequest" in version "velero.io/v1">

### CRD资源

```apl
kubectl get customresourcedefinitions.apiextensions.k8s.io | grep velero
```

| CRD 全名                            | 描述                             |
| ----------------------------------- | -------------------------------- |
| `backuprepositories.velero.io`      | 用于存储备份存储库的信息         |
| `backups.velero.io`                 | 用于管理备份操作的自定义资源     |
| `backupstoragelocations.velero.io`  | 定义备份存储位置                 |
| `datadownloads.velero.io`           | 用于管理数据下载操作的自定义资源 |
| `datauploads.velero.io`             | 用于管理数据上传操作的自定义资源 |
| `deletebackuprequests.velero.io`    | 用于删除备份的请求               |
| `downloadrequests.velero.io`        | 用于管理下载请求的自定义资源     |
| `podvolumebackups.velero.io`        | 用于管理 Pod 卷备份的自定义资源  |
| `podvolumerestores.velero.io`       | 用于管理 Pod 卷恢复的自定义资源  |
| `resticrepositories.velero.io`      | 用于存储 Restic 存储库的信息     |
| `restores.velero.io`                | 用于管理恢复操作的自定义资源     |
| `schedules.velero.io`               | 用于定义和管理备份计划           |
| `serverstatusrequests.velero.io`    | 用于请求服务器状态的自定义资源   |
| `volumesnapshotlocations.velero.io` | 定义卷快照的位置                 |

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

### v1.7--版本创建velero（推荐）

```apl
velero install \
  --provider aws \
  --bucket velero-oss \
  --image velero/velero:v1.7.0 \
  --plugins velero/velero-plugin-for-aws:v1.2.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=north-4,s3ForcePathStyle="true",s3Url=https://obs.cn-north-4.myhuaweicloud.com \
  --use-restic \
  --default-volumes-to-restic
```

```apl
velero install \
  --provider aws \
  --bucket elasti-oss \
  --image velero/velero:v1.7.1 \
  --plugins velero/velero-plugin-for-aws:v1.7.1 \
  --namespace velero default-volumes-to-restic \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=north-4,s3ForcePathStyle="false",s3Url=https://obs.cn-north-4.myhuaweicloud.com \
 --use-restic 

```

### v1.12--版本创建velero

```apl
华为云
velero install \
  --provider aws \
  --bucket elasti-oss \
  --image velero/velero:v1.12.3 \
  --plugins velero/velero-plugin-for-aws:v1.8.1 \
  --namespace velero default-volumes-to-restic \
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
- `--use-volume-snapshots`：是否启使用快照；需要云厂商支持（建议false)
- `--backup-location-config`：指定对象存储地址信息；
- `--use-restic` ：用 Restic 来备份和恢复卷数据，而不是依赖于底层的存储提供商
- `--default-volumes-to-restic `: 默认情况下所有卷都会通过 Restic 进行备份。也就是说，如果你使用这个选项，除非你明确指定某些卷不使用 
- region=`gzgy2`,s3ForcePathStyle="false",s3Url=https://obs-gzgy2.cucloud.cn
  - [`region=`是指定**AWS区域**的名称，例如`gzgy2`表示**华北地区**](https://github.com/vmware-tanzu/velero/issues/5360)[2](https://github.com/vmware-tanzu/velero/issues/5360)[；`s3ForcePathStyle="false"`表示是否使用**路径式**的S3 URL，即以域名开头的URL](https://github.com/grafana/loki/issues/8638)[3](https://github.com/grafana/loki/issues/8638)[。如果您使用的是**AlibabaCloud OSS**等不支持路径式的S3服务，那么您需要将`s3ForcePathStyle="false"`设置为`true`](http://localstack:4566/)[4](http://localstack:4566/)。

#### 如果出现ImageError

> 手动拉取，并且更行velero的pod

```apl
crictl pull velero/velero-plugin-for-aws:v1.2.1
crictl pull velero/velero:v1.7.0

crictl pull velero/velero-plugin-for-aws:v1.8.1
crictl pull velero/velero:v1.12.3
kubectl rollout restart deployment -n velero velero
velero backup-location get
```

![image-20240313095534967](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240313095534967.png?raw=true)

### 创建Pod资源

> 清楚PV

```apl
kubectl get pv --no-headers | awk '{print $1}' | xargs -I {} kubectl delete pv {}

```



#### 创建SC动态存储

> 创建动态存储之前保证已经可以正确连接后端存储
>
> vim  nfs-provisioner-deploy.yaml

```apl
kind: Deployment
apiVersion: apps/v1
metadata:
  name: nfs-client-provisioner
  namespace: bdqn
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nfs-client-provisioner
  strategy:
    type: Recreate        #设置升级策略为删除再创建(默认为滚动更新)
  template:
    metadata:
      labels:
        app: nfs-client-provisioner
    spec:
      serviceAccountName: nfs-client-provisioner  #上一步创建的ServiceAccount名称
      containers:
        - name: nfs-client-provisioner
          image: registry.cn-beijing.aliyuncs.com/mydlq/nfs-subdir-external-provisioner:v4.0.0
          volumeMounts:
            - name: nfs-client-root
              mountPath: /persistentvolumes
          env:
            - name: PROVISIONER_NAME  # Provisioner的名称,以后设置的storageclass要和这个保持一致
              value: storage-nfs
            - name: NFS_SERVER        # NFS服务器地址,需和valumes参数中配置的保持一致
              value: 192.168.71.161
            - name: NFS_PATH          # NFS服务器数据存储目录,需和valumes参数中配置的保持一致
              value: /GlusterFS
            - name: ENABLE_LEADER_ELECTION
              value: "true"
      volumes:
        - name: nfs-client-root
          nfs:
            server: 192.168.71.161        # NFS服务器地址
            path: /GlusterFS      # NFS共享目录
```

#### 创建NFS_RBAC

```apl
apiVersion: v1
kind: ServiceAccount
metadata:
  name: nfs-client-provisioner
  namespace: bdqn
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: nfs-client-provisioner-runner
rules:
  - apiGroups: [""]
    resources: ["persistentvolumes"]
    verbs: ["get", "list", "watch", "create", "delete"]
  - apiGroups: [""]
    resources: ["persistentvolumeclaims"]
    verbs: ["get", "list", "watch", "update"]
  - apiGroups: ["storage.k8s.io"]
    resources: ["storageclasses"]
    verbs: ["get", "list", "watch"]
  - apiGroups: [""]
    resources: ["events"]
    verbs: ["create", "update", "patch"]
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: run-nfs-client-provisioner
subjects:
  - kind: ServiceAccount
    name: nfs-client-provisioner
    namespace: bdqn
roleRef:
  kind: ClusterRole
  name: nfs-client-provisioner-runner
  apiGroup: rbac.authorization.k8s.io
---
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: leader-locking-nfs-client-provisioner
  namespace: bdqn
rules:
  - apiGroups: [""]
    resources: ["endpoints"]
    verbs: ["get", "list", "watch", "create", "update", "patch"]
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: leader-locking-nfs-client-provisioner
  namespace: bdqn
subjects:
  - kind: ServiceAccount
    name: nfs-client-provisioner
    namespace: bdqn
roleRef:
  kind: Role
  name: leader-locking-nfs-client-provisioner
  apiGroup: rbac.authorization.k8s.io

```

#### bdqn命名空间创建

> 动态存储cat storage.yaml 

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  namespace: bdqn
  name: nfs-storage
  annotations:
    storageclass.kubernetes.io/is-default-class: "false"  ## 是否设置为默认的storageclass
provisioner: storage-nfs                                   ## 动态卷分配者名称，必须和上面创建的deploy中环境变量“PROVISIONER_NAME”变量值一致
parameters:
  archiveOnDelete: "true"                                 ## 设置为"false"时删除PVC不会保留数据,"true"则保留数据
reclaimPolicy: Retain # 回收策略，默认为 Delete 可以配置为 Retain
#volumeBindingMode: Immediate # 默认为 Immediate，表示创建 PVC 立即进行绑定，只有 azuredisk 和 AWSelasticblockstore 支持其他值  
mountOptions: 
  - hard                                                  ## 指定为硬挂载方式
  - nfsvers=3
```

> 创建PVC

```apl
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: storage-pvc
  namespace: bdqn
spec:
  storageClassName: nfs-storage    ## 需要与上面创建的storageclass的名称一致
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10G
```

> 创建Pod

```apl
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
  namespace: bdqn
spec:
  containers:
    - name: test-container
      image: registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.21 
      volumeMounts:
        - mountPath: /mnt
          name: nfs-volume
  volumes:
    - name: nfs-volume
      persistentVolumeClaim:
        claimName: storage-pvc
```

#### dev2 命名空间

> 创建Deployment,pv,pvc,svc,ing

```apl
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs-pvc
  namespace: dev2
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  storageClassName: nfs-storage
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-old
  namespace: dev2
spec:
  minReadySeconds: 2
  revisionHistoryLimit: 3
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: nginx-old
  template:
    metadata:
      labels:
        app: nginx-old
    spec:
      containers:
      - name: nginx
        image: registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.22
        imagePullPolicy: IfNotPresent
        ports:
        - name: nginx-port
          containerPort: 80
          protocol: TCP
        volumeMounts:
        - name: nfs-volume
          mountPath: /usr/share/nginx/html/
      volumes:
      - name: nfs-volume
        persistentVolumeClaim:
          claimName: nfs-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: old-nginx
  namespace: dev2
spec:
  selector:
    app: nginx-old
  ports:
  - name: nginx-port
    port: 80
    targetPort: 80
    protocol: TCP
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: old-nginx-ing
  namespace: dev2
spec:
  ingressClassName: nginx
  rules:
  - host: "www.news.com"
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: old-nginx
            port:
              number: 80
      - pathType: Prefix
        path: /guonei
        backend:
          service:
            name: old-nginx
            port:
              number: 80
      - pathType: Prefix
        path: /guowai
        backend:
          service:
            name: old-nginx
            port:
              number: 80
```

#### ng-php命名空间

> 创建configmaps

```apl
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.php index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    location ~ \.php$ {
        root           /var/www/html;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

```

> 创建PVC

```apl
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ng-pvc
  namespace: ng-php
spec:
  storageClassName: nfs-storage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 200Gi
```

> 创建POD

```apl
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ng-php
  namespace: ng-php
  labels:
    app: nginx-php
spec:
  minReadySeconds: 3
  revisionHistoryLimit: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 30%
      maxUnavailable: 30%
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      nodeName: k8s-02
      containers:
      - name: nginx
        image: registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.22
        imagePullPolicy: IfNotPresent
        ports:
        - name: nginx-port
          containerPort: 80
          protocol: TCP
        volumeMounts:
        - name: nginx-data
          mountPath: /etc/nginx/conf.d/
        - name: pvc-volume
          mountPath: /usr/share/nginx/html
      - name: php
        image: registry.cn-beijing.aliyuncs.com/lzh-bj/php:7.1
        imagePullPolicy: IfNotPresent
        ports:
        - name: php-port
          containerPort: 9000
          protocol: TCP
        volumeMounts:
        - name: pvc-volume
          mountPath: /var/www/html/
      volumes:
      - name: nginx-data
        configMap:
          name: nginx.conf
          items:
          - key: nginx.conf
            path: default.conf
      - name: pvc-volume
        persistentVolumeClaim:
          claimName: ng-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: myapp
  namespace: ng-php
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
  - name: nginx-port
    port: 80
    targetPort: 80
    protocol: TCP
```



## Velero备份资源

```apl
velero backup create lzh-velero-test --include-namespaces="*" -n velero

velero backup create lzh-velero-test --include-namespaces="*" --exclude-namespaces="kube-system" -n velero

velero backup create 2024-3-25-no-kubesystem-storage --include-namespaces="*" --exclude-namespaces="kube-system" --exclude-resources="storageclasses.storage.k8s.io" -n velero

velero backup create 2024-8-8-no-kubesystem --include-namespaces="*" --exclude-namespaces="kube-system"  -n velero

velero backup create 2024-3-25-no-kubesystem-storage \
  --include-namespaces="*" \
  --exclude-namespaces="kube-system" \
  --exclude-resources="storageclasses.storage.k8s.io,persistentvolumes,persistentvolumeclaims,deployments.apps" \
  -n velero


```

> 使用 Restic：

```apl
velero backup create 2024-8-9-1-no-kubesystem  \
  --include-namespaces="*" \
   --exclude-namespaces="kube-system" \
  --include-resources="*" \
  --default-volumes-to-restic \
  -n velero
```

> 使用卷快照：

```apl
velero backup create 2024-8-8-no-kubesystem  \
  --include-namespaces="*" \
  --include-resources=persistentvolumes,persistentvolumeclaims,storageclasses \
  --snapshot-volumes=true \
  -n velero
```

![image-20240313093530335](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240313093530335.png?raw=true)

### 查看OBS对象存储

**查看备份是否成功**

```apl
velero backup get
velero backup describe POD_NAME --details
```

![image-20240313095641078](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240313095641078.png?raw=true)

## 删除资源

```apl
kubectl delete -f nginx-php.yaml -f nginx.conf -f old.nginx-2.yaml -f pvc-ng-php.yaml  -f svc-end.yaml -f sc/sc-pod.yaml -f sc/storage-pvc.yaml -f sc/storage.yaml
kubectl delete -f nfs-rbac.yaml -f nfs-provisioner-deploy.yaml
kubectl delete ingressclasses.networking.k8s.io nginx
kubectl delete deployments.apps -n ingress-nginx ingress-nginx-controller
```



## 目标集群部署



### 创建velero

```apl
华为云
velero install \
  --provider aws \
  --bucket velero-oss \
  --image velero/velero:v1.7.0 \
  --plugins velero/velero-plugin-for-aws:v1.2.1 \
  --namespace velero \
  --secret-file /k8s-test/velero/velero/oss-credentials.txt \
  --use-volume-snapshots=false \
  --backup-location-config region=north-4,s3ForcePathStyle="true",s3Url=http://obs.cn-north-4.myhuaweicloud.com \
  --use-restic \
  --default-volumes-to-restic

----
联通云
velero install \
  --provider aws \
  --bucket velero-oss \
  --image velero/velero:v1.7.0 \
  --plugins velero/velero-plugin-for-aws:v1.2.1 \
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

#### 查看AK/SK

```apl
[root@k8s-01 aws]# kubectl get secret cloud-credentials -n velero -o yaml
apiVersion: v1
data:
  cloud: W2RlZmF1bHRdCmF3c19hY2Nlc3Nfa2V5X2lkID0gQVFTTlZXRVhBUjZETDFRNUlDMDgKYXdzX3NlY3JldF9hY2Nlc3Nfa2V5ID0gbTkzUWpocWxkbE1xQnEwaXMyUnNBdTVGamxOTGhuRTRaeHFLcmFVago=
kind: Secret
metadata:
  creationTimestamp: "2024-08-05T07:39:05Z"
  labels:
    component: velero
  name: cloud-credentials
  namespace: velero
  resourceVersion: "39320"
  uid: 20986855-f109-40ff-85fc-5fd1568d6e98
type: Opaque
[root@k8s-01 aws]# echo "W2RlZmF1bHRdCmF3c19hY2Nlc3Nfa2V5X2lkID0gQVFTTlZXRVhBUjZETDFRNUlDMDgKYXdzX3NlY3JldF9hY2Nlc3Nfa2V5ID0gbTkzUWpocWxkbE1xQnEwaXMyUnNBdTVGamxOTGhuRTRaeHFLcmFVago=" | base64 --decode
[default]
aws_access_key_id = AQSNVWEXAR6DL1Q5IC08
aws_secret_access_key = m93QjhqldlMqBq0is2RsAu5FjlNLhnE4ZxqKraUj
```

## S3访问

```
aws s3 ls --endpoint-url http://obs.cn-north-4.myhuaweicloud.com

```



## 目标的集群恢复

>- 由于不同厂商集群与后端的存储基础设施不同，集群迁移后会遇到Pod无法挂载PV的问题。因此在进行迁移时需要对新集群中的StorageClass进行适配，从而在创建工作负载时可以屏蔽两个集群之间底层存储接口的差异，申请相应类型的存储资源。
> - 可以创建一个与原集群中相同名称StorageClass来完成适配

### 查看pod信息，添加对应标签

> 添加备份标签，

```
kubectl -n ng-php annotate pod/ng-php-7857bccf8d-mtr9m backup.velero.io/backup-volumes=ng-pvc --overwrite
```



> 获取备份资源信息

```apl
velero backup get
velero backup-location get
```

#### 创建image更新适配

```apl
apiVersion: v1
kind: ConfigMap
metadata:
  name: change-image-name-config
  namespace: velero
  labels:
    velero.io/plugin-config: ""
    velero.io/change-image-name: RestoreItemAction
data:
  "rule1": "registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.20,swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx:1.20"
  "rule2": "registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.21,swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx:1.21"
  "rule3": "registry.cn-beijing.aliyuncs.com/lzh-bj/nginx:1.22,swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx:1.22"
  "rule4": "registry.cn-beijing.aliyuncs.com/lzh-bj/php:7.1,swr.cn-north-4.myhuaweicloud.com/liuzhenhua/php:7.1"
  "rule5": "registry.cn-beijing.aliyuncs.com/lzh-bj/mysql:5.7,swr.cn-north-4.myhuaweicloud.com/liuzhenhua/mysql:5.7"

```

#### 创建StorageClass更新适配

>- 由于集群的存储基础设施不同，迁移后的集群将无法正常挂载存储卷，您可执行以下方法的任意一种来完成存储卷的更新适配。
>  - 两种StorageClass的适配方法均需在**目标集群**中于**恢复应用前**完成，否则可能出现PV数据资源无法恢复的情况，此时在完成StorageClass适配后使用Velero重新恢复应用即可

##### 方式一：创建ConfigMap映射

```apl
apiVersion: v1
kind: ConfigMap
metadata:
  name: change-storageclass-plugin-config
  namespace: velero
  labels:
    app.kubernetes.io/name: velero
    velero.io/plugin-config: "true"
    velero.io/change-storage-class: RestoreItemAction
data:
  {原集群StorageClass name01}: {目标集群StorageClass name01}
  {原集群StorageClass name02}: {目标集群StorageClass name02}

```

---

```apl
kubectl create -f change-storage-class.yaml
configmap/change-storageclass-plugin-config created
```

##### 方式二：创建同名StorageClass

> 查询CCE支持的默认StorageClass。
>
> ```
> kubectl get sc
> ```
>
> | StorageClass名称  | 对应的存储资源   |
> | ----------------- | ---------------- |
> | csi-disk          | 云硬盘           |
> | csi-disk-topology | 延迟绑定的云硬盘 |
> | csi-nas           | 文件存储         |
> | csi-obs           | 对象存储         |
> | csi-sfsturbo      | 极速文件存储     |

```apl
velero restore create --from-backup 2024-8-8-no-kubesystem-data  -n velero
```



```apl
[root@k8s-01 k8s]# velero restore create --from-backup 2024-8-6-no-kubesystem-storage -n velero
Restore request "2024-8-6-no-kubesystem-storage-20240807000522" submitted successfully.
Run `velero restore describe 2024-8-6-no-kubesystem-storage-20240807000522` or `velero restore logs 2024-8-6-no-kubesystem-storage-20240807000522` for more details.
[root@k8s-01 k8s]# velero restore get
NAME                                            BACKUP                           STATUS       STARTED                         COMPLETED   ERRORS   WARNINGS   CREATED                         SELECTOR
2024-8-6-no-kubesystem-storage-20240807000522   2024-8-6-no-kubesystem-storage   InProgress   2024-08-07 00:05:22 +0800 CST   <nil>       0        0          2024-08-07 00:05:22 +0800 CST   <none>

```

### 查看 backup/restore

```apl
[root@k8s-01 k8s]# kubectl get backup  -n velero 
NAME                             AGE
2024-8-8-no-kubesystem-storage   3m12s
[root@k8s-01 k8s]# kubectl get restore -n velero
NAME                                            AGE
2024-8-6-no-kubesystem-storage-20240807000522   39h
2024-8-6-no-kubesystem-storage-20240807003919   39h
```

### 查看restic

```apl
[root@k8s-01 k8s]# velero restic repo get
NAME                   STATUS   LAST MAINTENANCE
bdqn-default-ftlrl     Ready    2024-08-08 10:48:21 +0800 CST
dev2-default-c57mp     Ready    2024-08-08 10:49:07 +0800 CST
ng-php-default-b4ssb   Ready    2024-08-08 11:28:40 +0800 CST
velero-default-fdjmd   Ready    2024-08-08 10:49:44 +0800 CST
```

### 查看恢复详细信息

```apl
velero backup describe 2024-8-6-no-kubesystem-storage --details
```

### 查看自动的API

```
velero plugin get
```



### 查看恢复描述

```apl
velero restore describe 2024-8-6-no-kubesystem-storage-20240807000522
```

### 查看恢复日志

```apl
velero restore logs 2024-8-6-no-kubesystem-storage-20240807000522
```

![image-20240313100202414](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240313100202414.png?raw=true)

```apl
velero restore create --from-backup lzh-velero-test 
```

### 查看资源是否恢复

![image-20240313100650862](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240313100650862.png?raw=true)



- 刘振华  lzh_888888_1223@163.com

![image-20240325232354706](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240325232354706.png?raw=true)

![image-20240325232846453](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20240325232846453.png?raw=true)

## 问题

总结：

1. StoreageClass恢复顺序问题

   - 在恢复过程中可能会出现pv/pvc在sc之前恢复，从而导致pv/pvc恢复过程中，找不到后端存储，数据无法恢复，从而出现异常任务僵死。

   可以在恢复之前手动恢复sc(提前创建),然后再通过velero进行恢复

2. **StorageClass `reclaimPolicy` 和 `archiveOnDelete` 参数**: 如果 `reclaimPolicy` 设置为 "Retain"，而 `archiveOnDelete` 设置为 "true"，那么在恢复时，PV 可能不会自动删除和重新创建，从而导致无法正确恢复到新的 SC。

   - 在恢复前，手动删除那些状态为 `Released` 的旧 PV。

3. restore一直处于恢复中

   - 如果在恢复过程中restore出现状态一直恢复中

     - 重启删除restice容器Pod

     - 重启删除velero容器Pod
     - 都没效果就重新部署
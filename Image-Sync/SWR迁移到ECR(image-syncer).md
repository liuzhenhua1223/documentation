# SWR迁移到ECR(image-syncer)

**创建资源**

![image-20240313141810657](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313141810657.png)

[TOC]

## 场景描述

- 当处理较少的镜像迁移任务时，可以通过手动`tag`,`push`进行上传，但是在实际生产重涉及到成千上买个镜像，几T的镜像创库数据时，迁移过程就耗时，甚至丢数据。这时，可以使用开源的迁移镜像工具image-syncer来处理任务

## 操作步骤

### 查看华为云SWR镜像

**进入组织管理**

![image-20240313144850803](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313144850803.png)

![image-20240313144923390](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313144923390.png)

### 镜像上传方式

```apl
sudo docker tag [{镜像名称}:{版本名称}] swr.cn-north-4.myhuaweicloud.com/{组织名称}/{镜像名称}:{版本名称}

sudo docker push swr.cn-north-4.myhuaweicloud.com/{组织名称}/{镜像名称}:{版本名称}
```

**将这些镜像全部迁移过去**

### 下载image-syncer，解压并运行工具

**随便进入一台ECS**

![image-20240313145040015](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313145040015.png)

![image-20240313145531736](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313145531736.png)

```apl
以v1.3.1版本为例，您也可以选择其他版本。

wget https://github.com/AliyunContainerService/image-syncer/releases/download/v1.3.1/image-syncer-v1.3.1-linux-amd64.tar.gz

tar -zvxf image-syncer-v1.3.1-linux-amd64.tar.gz
```

### 常见认证文件auth.json

![image-20240313150053414](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313150053414.png)

#### 查看华为云登录方式

- ![image-20240313150600939](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313150600939.png)

  ![image-20240313150546017](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313150546017.png)

> 其中其中swr.××××.myhuaweicloud.com为镜像仓库地址，username、password可以在登录命令中获取，获取方法如下：
>
> 登录SWR控制台，在右上角单击“登录指令”，在弹出的窗口中获取登录指令，如上图所示。
>
> - 红色部分为用户名和密码
> - 蓝色部分为区域地址
>
> ```
> docker login -u cn-north-4@AQSNVWEXAR6DL1Q5IC08 -p ab4afc99af762cbe1558820ddc424ce73f4400ec4c538825c621fdb24382cf72 swr.cn-north-4.myhuaweicloud.com
> ```

#### 查看联通云登录方式

![image-20240313151055944](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313151055944.png)

![image-20240313151136682](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313151136682.png)

#### 根据信息生成auth.json

```apl
{
    "swr.cn-north-4.myhuaweicloud.com": {
        "username": "cn-north-4@AQSNVWEXAR6DL1Q5IC08",
        "password": "ab4afc99af762cbe1558820ddc424ce73f4400ec4c538825c621fdb24382cf72"
    },
    "nmhhht2-registry.cucloud.cn": {
        "username": "shichunda@SDPTYWYZtest2",
        "password": "Lzh123.com"
    }
}
```

注意如果联通云上部署ECS的主机和镜像是同一个地区则需要使用如下地址（镜像和ECS都在联通`呼和浩特基地二区`)

- **vpc-nmhhht2-registry.cucloud.cn，为目标端内网镜像域名地址**

- ```apl
  cat auth.json 
  {
      "swr.cn-north-4.myhuaweicloud.com": {
          "username": "cn-north-4@AQSNVWEXAR6DL1Q5IC08",
          "password": "ab4afc99af762cbe1558820ddc424ce73f4400ec4c538825c621fdb24382cf72"
      },
      "vpc-nmhhht2-registry.cucloud.cn": {
          "username": "shichunda@SDPTYWYZtest2",
          "password": "Lzh123.com"
      }
  }
  ```

  

### 创建同步镜像描述文件image.json

![image-20240313151424982](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313151424982.png)

#### 查看迁移的SWR镜像文件

- **都属于一个仓库**

![image-20240313151729333](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313151729333.png)

![image-20240313151922338](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313151922338.png)

#### 联通云创建镜像仓库

![image-20240313154023403](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313154023403.png)

![image-20240313154041371](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313154041371.png)

#### 生产images.json文件

```apl
{
    "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx-2-1:1.21": "nmhhht2-registry.cucloud.cn/liuzhenhua/nginx-2-1:1.21",
    "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx:1.21": "nmhhht2-registry.cucloud.cn/liuzhenhua/nginx:1.21",
   "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/swr-demo-2048:latest": "nmhhht2-registry.cucloud.cn/liuzhenhua/swr-demo-2048:latest"

}
```

- 注意如果联通云上不上ECS的主机和镜像是同一个地区则需要使用如下地址（镜像和ECS都在联通`呼和浩特基地二区`)

  - **vpc-nmhhht2-registry.cucloud.cn，为目标端内网镜像域名地址**

  - ```apl
    cat images.json 
    {
        "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx-2-1:1.21": "vpc-nmhhht2-registry.cucloud.cn/liuzhenhua/nginx-2-1:1.21",
        "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/nginx:1.21": "vpc-nmhhht2-registry.cucloud.cn/liuzhenhua/nginx:1.21",
       "swr.cn-north-4.myhuaweicloud.com/liuzhenhua/swr-demo-2048:latest": "vpc-nmhhht2-registry.cucloud.cn/liuzhenhua/swr-demo-2048:latest"
    
    }
    
    ```

    

### 执行imagesyncer进行同步

```apl
./image-syncer --proc=6 --auth=./auth.json --images=./images.json --auth=./auth.json --retries=3
```

![image-20240313153307680](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313153307680.png)

### 查看镜像是否同步成功

![image-20240313153857078](C:\Users\lmp\AppData\Roaming\Typora\typora-user-images\image-20240313153857078.png)
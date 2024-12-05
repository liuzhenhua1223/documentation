# 阿里云-自建k8s迁移镜像、应用至ACK最佳实践

[TOC]

![image-20241203224958079](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203224958079.png?raw=true)

## 前言

### 概述

- 随着技术的逐步发展，企业的应用越来越复杂，如何高效的保障好系统且又能提升基础资源的利用率是企业一直在追求的方向。云原生技术 K8S 以其易管控，自动化操作，自修复等特点充分满足了企业的需求，越来越多的企业都加入容器化这个队伍中。但随着技术的更新迭代，自建的 K8S 相关的容器镜像服务、集群管理、稳定性保障也让企业 IT 人员感觉到压力，所以上云成了一些企业的选择，将底层的 IAAS 基础设施和 K8S 的基础 PASS 能力交给阿里云来管理，企业本身抽出更多精力聚焦业务的创新。
  针对以上需求通过使用 image-syncer、velero 来介绍如何平滑、便捷的迁移自建的K8S 镜像和应用至阿里云容器镜像服务和 ACK；本文通过使用河源的 ECS 自建 K8S集群和 Harbor 镜像仓库来模拟 IDC 环境，具体环境信息见下文细节。

### 应用范围

### 名词解释

- 容器服务ACK：提供高性能可伸缩的容器应用管理能力，支持企业级 Kubernetes 容器化应用的全生命周期管理。容器服务 Kubernetes 版简化集群的搭建和扩容等工作，整合阿里云虚拟化、存储、网络和安全能力，打造云端最佳的 Kubernetes 容器化应用运行环境。详见：https://www.aliyun.com/product/kubernetes
- 容器镜像服务 ACR：Alibaba Cloud Container Registry，默认实例版提供基础的容器镜像服务，包括安全的应用镜像托管能力、精确的镜像安全扫描功能、稳定的国内外镜像构建服务以及便捷的镜像授权功能，从而方便用户进行镜像全生命周期管理。详见：https://www.aliyun.com/product/acr
  自建 K8S 迁移镜像、应用至阿里云 ACK
  目录
- 云服务器 ECS（Elastic Compute Service）是一种弹性可伸缩的计算服务，助您降 低 IT 成 本 ， 提升 运 维 效 率 ， 使 您 更 专 注 于 核 心 业 务 创 新 。 详见：https://www.aliyun.com/product/ecs
- 专有网络 VPC：Virtual Private Cloud，简称 VPC，是基于阿里云创建的自定义私有网络，不同的专有网络之间二层逻辑隔离。您可以在自己创建的专有网络内创建和管理云产品实例，比如 ECS、负载均衡、RDS 等。在部署云资源前，您需 要 结 合 具 体 业 务 ， 规 划 VPC 和 交 换 机 的 数 量 及 网 段 等 。 详见：https://www.aliyun.com/product/vpc
- NAT 网关：NAT Gateway，是一款企业级的 VPC 公网网关，提供 NAT 代理（SNAT、DNAT）、10Gbps 级别的转发能力、以及跨可用区的容灾能力。NAT 网关与共享带宽包配合使用，可以组合成为高性能、配置灵活的企业级网关。详见：https://www.aliyun.com/product/nat
- 弹性公网 IP（Elastic IP Address）：是可以独立购买和持有的公网 IP 地址资源。目前，EIP 可绑定到专有网络类型的 ECS 实例、专有网络类型的私网 SLB 实例、专有网络类型的辅助弹性网卡、NAT 网关和高可用虚拟 IP 上。详见：https://www.aliyun.com/product/eip
- 负载均衡 SLB：对多台云服务器进行流量分发的负载均衡服务，可以通过流量分发扩展应用系统对外的服务能力，通过消除单点故障提升应用系统的可用性。详见：https://www.aliyun.com/product/slb
- 访问控制 RAM：是阿里云提供的管理用户身份与资源访问权限的服务。详见：
  https://www.aliyun.com/product/ram

## 最佳实践

### 场景描述

- 本最佳实践构建以下场景：
  - 以河源 ECS 构建 Harbor 仓库，模拟 IDC 的镜像仓库服务。
  - 以河源 ECS 构建 Registry 仓库，模拟 IDC 的镜像仓库服务。
  - 以河源地域模的 ECS 搭建 K8S 集群，模拟线下 IDC 的 K8S 环境。
  - 使用 velero 对云上的 K8S 应用进行定期备份，并存至 OSS 上，确保应用数据不丢失。

### 示例应用场景

- 自建 harbor 镜像仓库，将镜像迁移到阿里云容器镜像服务 OCR（含企业版）。
- 自建 Registry 镜像仓库，将镜像迁移到阿里云容器服务 OCR（含企业版）。
- 自建&IDC 的 K8S 业务，通过 velero 将应用迁移至阿里云容器服务 ACK。
- 通过 velero 将 K8S（云上&云下均可）应用备份至 OSS，确保配置数据同城&异地容灾。

### 方案架构

![image-20241203225537669](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203225537669.png?raw=true)

## 前置条件

在进行本文操作前，您需要完成以下准备：

- 注册阿里云账号，并完成实名认证。您可以登录阿里云控制台，并前往实名认证页面（https://account.console.aliyun.com/v2/#/authc/home）查看是否已经完成实名认证。
- 阿里云账户余额大于 100 元。您可以登录阿里云控制台，并前往账户总览页面（https://expense.console.aliyun.com/#/account/home）查看账户余额。
- 开通如下服务：
  - 对象存储 OSS
  - 云架构设计工具 CADT
  - 容器服务 Kubernetes 版 ACK
  - 容器镜像服务 ACR

# 测试资源准备

> - 背景信息
>   - 在本章中，将以阿里云河源地域模拟线下 IDC，使用云架构设计工具 CADT 快速创建IDC 的 K8S 集群所需的基础资源。

## 资源规划列表

![image-20241203230207428](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230207428.png?raw=true)

## 基础资源创建

- `步骤一`使用云账号登录阿里云架构 设 计 工 具 CADT 控制台。（https://bpstudio.console.aliyun.com/）
- `步骤二`选择新建架构应用 > 快速创建 页面，并将基础网络拖拽至右侧空白处 。

![image-20241203230337021](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230337021.png?raw=true)

- `步骤三`在 右侧面板 > 分别双击 region、vpc、交换机 边框，按照如上资源列表进行填写配
  置。

![image-20241203230413761](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230413761.png?raw=true)

![image-20241203230431230](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230431230.png?raw=true)

![image-20241203230441291](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230441291.png?raw=true)

- `步骤四`左侧菜单选择 > 弹性计算 > 云服务器 ECS；存储服务 > 对象存储 OSS 拖拽至右
  侧面版，后双击 ECS 和 OSS 图标进行资源配置

![image-20241203230541121](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230541121.png?raw=true)

![image-20241203230633614](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230633614.png?raw=true)

- `步骤五`完成所有资源的配置后，点击右上角“保存”按钮，然后选择部署 > “部署验证”。

![image-20241203230708020](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230708020.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230708020.png?raw=true)

- `步骤六`登陆控制台查看，确认对应的资源是否都已经创建好

![image-20241203230825833](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230825833.png?raw=true)

![image-20241203230843978](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203230843978.png?raw=true)

#  自建Harbor迁移至ACR默认实例版

>本章介绍如何使用 image_syncer 将 ECS 上自建的 Harbor 镜像平滑快速的迁移至阿里云容器镜像服务 ACR，关于如何自建 Harbor 本章节中不在赘述，可参考官网按照说明：https://goharbor.io/docs/2.1.0/install-config/。
>容器镜像服务 ACR（Alibaba Cloud Container Registry）默认实例版提供基础的容器镜像服
>务，包括安全的应用镜像托管能力、精确的镜像安全扫描功能、稳定的国内外镜像构建服务
>以及便捷的镜像授权功能，从而方便用户进行镜像全生命周期管理。
>容器镜像服务简化了 Registry 的搭建运维工作，支持多地域的镜像托管，并联合容器服务等云产品，打造云上使用 Docker 的一体化体验。

## 容器镜像服务开通&配置

- 步骤一：登陆控制台 https://cr.console.aliyun.com/ ，若未激活，则会有如下提示

![image-20241203231022015](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231022015.png?raw=true)

![image-20241203231034327](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231034327.png?raw=true)

![image-20241203231044096](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231044096.png?raw=true)

- 步骤二：在左侧导航栏，选择默认实例 > 命名空间，创建命名空间。

![image-20241203231917636](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231917636.png?raw=true)

- 步骤三：在左侧导航栏，选择默认实例 > 镜像仓库，创建对应镜像的仓库。

![image-20241203231945063](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231945063.png?raw=true)

![image-20241203231956778](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231956778.png?raw=true)

- 步骤四：创建后，查看镜像仓库列表如下

![image-20241203231756032](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203231756032.png?raw=true)

## 准备测试镜像至Harbor

**操作步骤**
详细的上传镜像步骤，这边不在赘述。Harbor 完成对应的仓库创建、镜像上传后，如下图所
示

![image-20241203232132973](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232132973.png?raw=true)

![image-20241203232246465](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232246465.png?raw=true)

## 安装&配置Image_syncer

**操作步骤**

- 步骤一：下载image_syncer程序包

```apl
wget https://github.com/AliyunContainerService/image-syncer/releases/download/v1.2.0/image-
syncer-v1.2.0-linux-amd64.tar.gz
```

- 步骤二：解压程序包

![image-20241203232639101](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232639101.png?raw=true)

- 步骤三： 复制配置文件模板文件 config.json 为 harbor-to-acr.json，并进行修改。

```apl
cp config.json harbor-to-acr.json
```

![image-20241203232547597](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232547597.png?raw=true)

**注意点：**

- 同步的最大单位是仓库（repo），不支持通过一条规则同步整个 namespace 以及 registry
- 当源仓库字段中不包含 tag 时，表示将该仓库所有 tag 同步到目标仓库，此时目标仓库不能包含
  tag
- 当源仓库字段中包含 tag 时，表示只同步源仓库中的一个 tag 到目标仓库，如果目标仓库中不包含tag，则默认使用源 tag
- 源仓库字段中的 tag 可以同时包含多个（比如"a/b/c:1,2,3"），tag 之间通过","隔开，此时目
  标仓库不能包含 tag，并且默认使用原来的 tag

## 启动image_syncer同步镜像

- 步骤一：

  ```apl
  ./image-syncer --proc=6 --config=./harbor-to-acr.json --namespace=acr-ns --registry=registry.cn-shenzhen.aliyuncs.com --retries=3
  
  # 设置默认目标 registry 为 registry.cn-shenzhen.aliyuncs.com，默认目标 namespace 为
  image-syncer,本案例中为 acr-ns
  # --proc=6 并发数为 6，--retries=3 重试次数为 3
  # 日志输出到./log 文件下，不存在会自动创建，不指定的话默认会将日志打印到 Stderr
  # 指定配置文件为 harbor-to-acr.json，内容如上所述
  若有镜像不存在或者配置错误，则日志会打印对应错误，本案例中是显示未找到这个镜像。
  ```

![image-20241203232857924](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232857924.png?raw=true)

![image-20241203232917283](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203232917283.png?raw=true)

- 步骤二：将对应镜像重新上传至Harbor

![image-20241203233011562](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233011562.png?raw=true)

- 步骤三：重新启动 image_syncer 命令，查看上传情况（支持续传）

![image-20241203233047950](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233047950.png?raw=true)

![image-20241203233314065](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233314065.png?raw=true)

## 检查上传至云上ACR的结果

>使用 image_syncer 工具迁移完成后，在目标端阿里云容器镜像服务确认镜像是否都已
>正常上传。

**操作步骤**

- 步骤一：登陆 https://cr.console.aliyun.com/cn-shenzhen/instances/repositories ，查看镜像仓
  库

![image-20241203233442467](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233442467.png?raw=true)

- 步骤二：查看镜像版本信息，确认与上传符合。
  - 经确认发现上传版本和上传日志中的版本一致，如下图所示

![image-20241203233520663](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233520663.png?raw=true)

![image-20241203233540625](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233540625.png?raw=true)

## 基于Harbor镜像同步实施迁移

- 除了基于 image_syncer 工具进行容器镜像迁移外，还可以使用 harbor 自带的镜像同步功能进行迁移。（注：harbor 从 v1.9 之后开始支持 ACR）。
-  同样，我们先在 harbor 下 test-ack 项目，上传测试镜像，如下图：

![image-20241203233645651](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203233645651.png?raw=true)

- 步骤一：创建迁移目标

![image-20241203234443518](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234443518.png?raw=true?raw=true)

![image-20241203234503621](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234503621.png?raw=true?raw=true)

在列表中可以看到创建好的仓库

![image-20241203234619024](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234619024.png?raw=true?raw=true)

**主参数配置**

```apl
主要参数配置：
	①复制模式：push-based 是把镜像由本地 harbor 推送到远端仓库；pull-based 是将镜像由远端仓库拉取到本地 harbor；
	②资源过滤器：过滤出要同步的资源，包括资源的名称（由项目名+仓库名组成，如示例中 test-ack/nginx，支持通配符，例如要同步整个项目中镜像，可以填写 test-ack/**）、tag、标签、类型等；
	③目的 Registry：下拉框中选择步骤 1 中创建的远端仓库（toali）；④目的 Namspace：acr 中对应的 namespace。
```

- 步骤三：触发负责迁移

![image-20241203234746172](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234746172.png?raw=true)

稍等几分钟后，可以看到迁移进度完成

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234746172.png?raw=true)

登录 ACR，查看镜像：

![image-20241203234858657](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203234858657.png?raw=true)

# 自建Harbor迁移至ACR企业版

>本章介绍如何使用 image_syncer 将自建的 Harbor 镜像平滑快速的迁移至阿里云容器镜像服务 ACR 企业版，关于如何自建 Harbor 本章节中不在赘述，可参考官网按照说明：https://goharbor.io/docs/2.1.0/install-config/。
>容器镜像服务 ACR（Alibaba Cloud Container Registry）默认实例版提供基础的容器镜像服
>务，包括安全的应用镜像托管能力、精确的镜像安全扫描功能、稳定的国内外镜像构建服务
>以及便捷的镜像授权功能，从而方便用户进行镜像全生命周期管理。
>容器镜像服务简化了 Registry 的搭建运维工作，支持多地域的镜像托管，并联合容器服务等云产品，打造云上使用 Docker 的一体化体验。

## 企业版实例创建&配置

**操作步骤**

- 步骤一：登陆控制台 https://cr.console.aliyun.com/ ，选择企业版实例

![image-20241204152650704](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152650704.png?raw=true)

![image-20241204152705180](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152705180.png?raw=true)

- 步骤二：在选择对应的区域，并根据实际需求选择企业版实例规格，后进行支付

![image-20241204152730932](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152730932.png?raw=true)

![image-20241204152744206](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152744206.png?raw=true)



- 步骤三：在左侧导航栏，选择企业版实例 > 实例列表，选择对应的实例，并点击管理。

![image-20241204152805557](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152805557.png?raw=true)

- 步骤四：单击左侧导航栏的仓库管理 > 命名空间， 在创建命名空间页面中自定义命名空间，勾选自动创建仓库和默认仓库类型后，并单击确定。

![image-20241204152840809](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204152840809.png?raw=true?raw=true)

- 步骤五：在左侧导航栏中，选择企业版实例 > 实例列表，在实例列表页面中，单击所需配置的企业版实例，进入该实例的配置页面，

![image-20241204161111294](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161111294.png?raw=true)

- 步骤六：选择仓库管理 > 访问控制，进入访问控制的配置页面

![image-20241204161130623](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161130623.png?raw=true)

- 步骤七：若是云上的内网访问，则选择对应添加对应的专有网络。 本案例模拟 IDC 镜像数据上云，所以选择公网标签

![image-20241204161201608](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161201608.png?raw=true)

- ！！注意：

  - 如果您希望所有公网下的 ECS 均可以访问企业版实例，需要保持公网访问入口开启并删除所有

  - 公网白名单。请注意完全暴露在公网的企业版实例存在被攻击的风险，请谨慎操作。

- 步骤八：单击左侧导航栏的实例管理 > 访问凭证，点击设置固定密码，输入密码后点击确认

![image-20241204161318705](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161318705.png?raw=true)

![image-20241204161331960](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161331960.png?raw=true)

## 准备测试镜像至Harbor

**操作步骤**

详细的上传镜像步骤，这边不在赘述。Harbor 完成对应的仓库创建、镜像上传后，如下图所示

![image-20241204161515373](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161515373.png?raw=true)

![image-20241204161532193](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161532193.png?raw=true)

## 安装&配置image_syncer

**操作步骤同2.3章节**

- 步骤一：下载 image_syncer 程序包。

```apl
wget https://github.com/AliyunContainerService/image-syncer/releases/download/v1.2.0/image-syncer-v1.2.0-linux-amd64.tar.gz
```

![image-20241204161704760](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161704760.png?raw=true)

- 步骤二：解压程序包

![image-20241204161751729](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161751729.png?raw=true)

- 步骤三 复制配置文件模板文件 config.json 为 harbor-to-acr-ent.json，并进行修改。cp config.json harbor-to-acr-ent.json

![image-20241204161825023](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204161825023.png?raw=true)

- ！！**注意点**
  - 同步的最大单位是仓库（repo），不支持通过一条规则同步整个 namespace 以及 registry
  - 当源仓库字段中不包含 tag 时，表示将该仓库所有 tag 同步到目标仓库，此时目标仓库不能包含tag
  - 当源仓库字段中包含 tag 时，表示只同步源仓库中的一个 tag 到目标仓库，如果目标仓库中不包含tag，则默认使用源 tag
  - 源仓库字段中的 tag 可以同时包含多个（比如"a/b/c:1,2,3"），tag 之间通过","隔开，此时目标仓库不能包含 tag，并且默认使用原来的 tag

## 启动image_syncer同步镜像

- 步骤一：执 行 如下命令 

```apl
./image-syncer --proc=6 --config=./harbor-to-acr-ent.json --
namespace=ent-acr --registry=ent-acr-registry.cn-shenzhen.cr.aliyuncs.com --retries=3

# 设置默认目标 registry 为 ent-acr-registry.cn-shenzhen.cr.aliyuncs.com，默认目标
namespace 为 image-syncer,本案例中 namespace 为 ent-acr
# --proc=6 并发数为 6，--retries=3 重试次数为 3
# 日志输出到./log 文件下，不存在会自动创建，不指定的话默认会将日志打印到 Stderr
# 指定配置文件为 harbor-to-acr-ent.json，内容如上所述
```

- 步骤二： 若 image_syncer 的公网服务器 IP 未配置到公网白名单中，则会报如下错误（本案例中特意模拟公网白名单配置错误情况）。

![image-20241204162437717](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162437717.png?raw=true)

- 步骤三：将对应公网白名单配置正确后，重新启动 image_syncer 命令，如下。

![image-20241204162455738](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162455738.png?raw=true)

![image-20241204162514776](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162514776.png?raw=true)

## 检查上传至云上ACR的结果

>使用 image_syncer 工具迁移完成后，在目标端阿里云容器镜像服务确认镜像是否都已
>正常上传。

**操作步骤**

- 步骤一：登陆 https://cr.console.aliyun.com/cn-shenzhen/instances/repositories ，点击进入ent-acr 实例。

![image-20241204162815088](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162815088.png?raw=true)

- 步骤二：选择对应的仓库名字，进入查看镜像版本信息，确认与上传符合。

![image-20241204162929155](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162929155.png?raw=true)

![image-20241204162942508](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204162942508.png?raw=true)

# 自建Registry上的镜像迁移至阿里云ACR

>本章节通过在 ECS 上自建 Registry 仓库，然后使用 image_syncer 和自己编写 SHELL 脚本来进行同步镜像至 ACR（只介绍默认实例版），企业实例版参加章节 3 来进行对应配置。 其中 shell 脚本在存在
>大量镜像需要迁移时候，需要关注运行脚本所在服务器的磁盘空间，因为过程中需要将镜像先 pull。

## 上传测试镜像

> 为减少篇幅大小，详细的上传镜像步骤，这边不在赘述。

**操作步骤**

完成镜像上传后，Registry 的仓库如下图所示。Ps:为方便展示，安装了

![image-20241204163042623](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163042623.png?raw=true)

## 使用image_syncer进行镜像迁移

- 步骤一：下载 image_syncer 程序包。

```apl
wget https://github.com/AliyunContainerService/image-syncer/releases/download/v1.2.0/image-syncer-v1.2.0-linux-amd64.tar.gz
```

![image-20241204163134854](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163134854.png?raw=true)

- 步骤二：解压程序包

![image-20241204163214780](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163214780.png?raw=true)

- 步骤三：复制配置文件模板文件 config.json 为 registry-to-acr.json，并进行修改。cp config.json registry-to-acr.json

![image-20241204163233609](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163233609.png?raw=true)

- ！！注意点：
  - 同步的最大单位是仓库（repo），不支持通过一条规则同步整个 namespace 以及 registry
  - 当源仓库字段中不包含 tag 时，表示将该仓库所有 tag 同步到目标仓库，此时目标仓库不能包含tag自建 K8S 迁移镜像、应用至阿里云 ACK
  - 当源仓库字段中包含 tag 时，表示只同步源仓库中的一个 tag 到目标仓库，如果目标仓库中不包含tag，则默认使用源 tag
  - 源仓库字段中的 tag 可以同时包含多个（比如"a/b/c:1,2,3"），tag 之间通过","隔开，此时目标仓库不能包含 tag，并且默认使用原来的 tag
- 步骤四：启动 image_syncer 命令

```apl
./image-syncer --proc=6 --config=./regisrty-to-acr.json --registry=ent-acr-registry.cn-shenzhen.cr.aliyuncs.com --retries=3
```

![image-20241204163350646](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163350646.png?raw=true)

![image-20241204163401993](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163401993.png?raw=true)

- 步骤五：检查上传至 ACR 的结果，打开容器镜像服务-镜像仓库，控制台集群列表页面。（https://cr.console.aliyun.com/cn-shenzhen/instances/repositories）

![image-20241204163446445](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204163446445.png?raw=true)

## 使用SHELL脚本进行镜像迁移

**操作步骤**

- 步骤一：安装依赖组件 yum install –y jq

- 步骤二：编写镜像迁移脚本

  - ```shell
    #!/bin/sh
    
    # 源仓库和目标仓库的地址作为参数传入
    source_registry=$1
    target_registry=$2
    
    # 如果源仓库需要用户名和密码，则取消注释并替换下面的用户名和密码
    # docker login --username=用户名 --password=密码 $source_registry
    
    # 登录目标仓库
    docker login --username=用户名 --password=密码 registry.cn-shenzhen.aliyuncs.com
    
    # 获取源仓库中的所有镜像名称
    image_names=$(curl http://$source_registry/v2/_catalog 2>/dev/null | jq '.repositories[]' | tr -d '"')
    
    # 遍历所有镜像名称
    for i in $image_names
    do
        echo "$i"
    
        # 获取每个镜像的所有标签
        tags=$(curl http://$source_registry/v2/$i/tags/list 2>/dev/null | jq ".tags[]" | tr -d '"')
    
        # 遍历每个标签
        for j in $tags
        do
            echo "$j"
    
            # 拉取源仓库中的镜像
            docker pull $source_registry/$i:$j
    
            # 给镜像打上目标仓库的标签
            docker tag $source_registry/$i:$j $target_registry/$i:$j
    
            # 将镜像推送到目标仓库
            docker push $target_registry/$i:$j
        done
    done
    ```

- 步骤三：在容器镜像服务上，预先创建好对应的命名空间，如本案例中的 test-ack

![image-20241204164240475](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204164240475.png?raw=true)

![image-20241204164252449](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204164252449.png?raw=true)

- 步骤四：执行迁移命令脚本

```apl
sh image_migration.sh 192.168.12.213:5000 registry.cn-shenzhen.aliyuncs.com

其中 192.168.12.213:5000 为自建 registry 的地址，registry.cn-shenzhen.aliyuncs.com 为云上 ACR 的地址。 由于本实例中测试已上传过，所以这些 layer 曾都已经存在。
```

![image-20241204164330626](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204164330626.png?raw=true)

- 步骤五：检查上传至 ACR 的结果，打开容器镜像服务-镜像仓库，控制台集群列表页面。（https://cr.console.aliyun.com/cn-shenzhen/instances/repositories）

![image-20241204164356737](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204164356737.png?raw=true)

确认以上上传的镜像数量和 Registry 的镜像一致。

![image-20241204164415543](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204164415543.png?raw=true)

## 安装配置Registry

>- 具体安装步骤不在这里赘述，大家有需要可以参照官网 URL：
>  https://docs.docker.com/registry/
>- 由于 Docker 官方只提供了 REST API，并没有给我们一个 UI 界面，这边安装了个简单的页面工具 hyper/docker-registry-web，详情参见
>  https://hub.docker.com/r/hyper/docker-registry-web/

# 使用Velero 迁移自建K8s应用至阿里云ACK

>本章节介绍 使用 velero 将 K8S 上的应用 POD 迁移至阿里云 ACK 的方法，其中通过ECS 创建来手动搭建 K8S，具体搭建步骤这边不在赘述，大家可参考云上另外一篇最佳
>实践  https://bp.aliyun.com/detail/161?spm=a2cls.b8387508.0.0.4e784a212nrW59

## 创建RAM账号并授权

**操作步骤**

- 步骤一：使用云账号登录阿里云 RAM 访问控制控制台。（https://ram.console.aliyun.com）
- 步骤二：前往人员管理 > 用户页面，并单击新建用户。

![image-20241203235137117](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235137117.png?raw=true)

- 步骤三：在新建用户页面，完成以下配置，并单击确定。

![image-20241203235202038](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235202038.png?raw=true)

![image-20241203235224992](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235224992.png?raw=true)

- 步骤四：下载CSV文件，保存用户信息。

![image-20241203235302157](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235302157.png?raw=true)

- 步骤五：在用户信息列表，勾选 migrate_user 用户，并单击添加权限。

![image-20241203235348261](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235348261.png?raw=true)

- 步骤六：在添加权限侧边页，选择自定义授权，选择新增。

  - 如果使用主账号权限，则跳过这步

  - ```
    {
     "Version": "1",
     "Statement": [
      {
     "Action": [
     "ecs:DescribeSnapshots",
     "ecs:CreateSnapshot", "ecs:DeleteSnapshot", "ecs:DescribeDisks", "ecs:CreateDisk", "ecs:Addtags",
     "oss:PutObject", "oss:GetObject", "oss:DeleteObject", "oss:GetBucket", "oss:ListObjects" ],
     "Resource": [
     "*"
     ],
     "Effect": "Allow"
     }
     ]
    }
    ```

![image-20241203235459729](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235459729.png?raw=true)

- 步骤7：返回对应的添加权限创建，选择上面新创建的 verelo 权限，单击确定。

![image-20241203235545893](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235545893.png?raw=true)

![image-20241203235622856](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235622856.png?raw=true?)

## 自建k8s集群安装配置Velero

**操作步骤：**

- 步骤一：创建 OSS bucket, 控制台 https://oss.console.aliyun.com/overview，选 择深圳区域，创建 ls-velero 的 bucket

![image-20241203235934671](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235934671.png?raw=true)

![image-20241203235955386](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241203235955386.png?raw=true)

- 步骤二：下载 velero 命令客户端

```apl
curl -o /usr/bin/velero https://public-bucket-1.oss-cn-hangzhou.aliyuncs.com/velero 
&& chmod +x /usr/bin/velero
```

![image-20241204000027668](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204000027668.png?raw=true?raw=true)

- 步骤三：将前面生产的 AccessKey 信息填入 Velero 的部署文件 credentials-velero 中。

![image-20241204000056797](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204000056797.png?raw=true)

- 步骤四：部署 velero 服务端

```apl
文档版本：20200525
 velero install \
 --provider alibabacloud \
 --image registry.cn-hangzhou.aliyuncs.com/acs/velero:1.4.2-2b9dce65-aliyun \
 --bucket ls-velero \
 --secret-file ./credentials-velero \
 --use-volume-snapshots=false \
 --backup-location-config region=cn-shenzhen \
 --use-restic \
 --plugins registry.cn-hangzhou.aliyuncs.com/acs/velero-plugin-alibabacloud:v1.0.0-2d33b89 \
  --wait
```

！！若过程中有配置出错的，可以使用进行卸载重装

```apl
kubectl delete namespace/velero clusterrolebinding/velero
kubectl delete crds -l component=velero
```

![image-20241204000214461](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204000214461.png?raw=true)

![image-20241204000236881](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204000236881.png?raw=true)

## 自建k8s备份应用至OSS

- 步骤一：登录自建 K8S 的 Master 节点（安装了 verelo 组件），执下备份命令

```apl
velero backup create webapp --include-namespaces default

#其中 webapp 是备份应用备份名称，default 为命名空间。
```

![image-20241204112132589](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112132589.png?raw=true)

- 步骤二：在 OSS 控制台 https://oss.console.aliyun.com/查看备份文件

![image-20241204112151607](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112151607.png?raw=true)

![image-20241204112203928](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112203928.png?raw=true)

![image-20241204112412699](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112412699.png?raw=true)

## 创建阿里云ACK集群

- 步骤一：创建 ACK 集群，登陆控制台（https://cs.console.aliyun.com/），选择创建集群

![image-20241204112447988](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112447988.png?raw=true)

- 步骤二：在按需填写对应集群类别，本案例选择标准托管版，并按照导航完成如下配置

![image-20241204112508475](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112508475.png?raw=true)

- 步骤三：选择对应的 WORKER 配置和密码配置，点击下一步“组件配置”

![image-20241204112529142](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112529142.png?raw=true)

- 步骤四：按需选择对应的组件配置

![image-20241204112553883](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112553883.png?raw=true)

- 步骤五：确认配置无误后，且依赖检查都通过后，选择创建集群，然后等待集群完成。

![image-20241204112609283](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112609283.png?raw=true)

- 步骤六：集群创建完成后，点击集群名称进入，查看集群详细信息

![image-20241204112629531](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112629531.png?raw=true)

## 阿里云ACK安装配置Velero

- 步骤一：将集群的访问信息复制至安装好 kubectl 的节点的$HOME/.kube/config 目录下。

![image-20241204112703409](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112703409.png?raw=true)

- 步骤二：在部署完成 kubectl 的 ACK 节点上安装 verelo 客户端

```apl
curl -o /usr/bin/velero https://public-bucket-1.oss-cn-hangzhou.aliyuncs.com/velero 
&& chmod +x /usr/bin/velero
```

- 步骤三：将云上 ACK 的 AccessKey 信息填入 velero 的部署文件 credentials-velero 中。

![image-20241204112738381](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112738381.png?raw=true)

- 步骤四：部署 velero 服务端

```apl
 velero install \
 --provider alibabacloud \
 --image registry.cn-hangzhou.aliyuncs.com/acs/velero:1.4.2-2b9dce65-aliyun \
 --bucket ls-velero \
 --secret-file ./credentials-velero \
 --use-volume-snapshots=false \
 --backup-location-config region=cn-shenzhen \
 --use-restic \
 --plugins registry.cn-hangzhou.aliyuncs.com/acs/velero-plugin-alibabacloud:v1.0.0-2d33b89 \
  --wait
```

![image-20241204112823925](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112823925.png?raw=true)

## 阿里云ACK恢复应用

- 步骤一：执行 恢复

```apl
- velero restore create --from-backup webapp //webapp 为前面自建 K8S 备份
  应用的名称
```

![image-20241204112929972](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204112929972.png?raw=true)

- 步骤二：查看 restore 的任务执行情况，可看到任务已完成

![image-20241204113145949](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204113145949.png?raw=true)

- 步骤三：查看迁移后的 POD,RC 等确认均运行正常

![image-20241204113204130](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204113204130.png?raw=true)

- 若存在 ErrImagepull 启动失败，可对 YML 文件的镜像地址就那些修改。
  - 登录容器服务管理控制台，单击左侧导航栏的服务 ，选择命名空间和目标服务，点击查看 YML

![image-20241204113229350](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204113229350.png?raw=true)

修改对应的镜像地址后，点击更新

![image-20241204113302099](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204113302099.png?raw=true)

![image-20241204165353656](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241204165353656.png?raw=true)

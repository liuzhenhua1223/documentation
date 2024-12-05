# Huawei Cloud Stack（HCS）

# 第一章云计算概述

## IT的核心

- 以数据中心为基础的核心架构

  ![image-20240529094243856](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240529094243856.png?raw=true)

## 传统IT面临的挑战

![image-20240422103040115](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422103040115.png?raw=true)

## IT发展趋势

> 未来一定是云计算-大数据，大量计算的时代，和生活一一相关的计算资源，并且要更加快速和准确的进行运算(边缘云)

![image-20240422102834695](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422102834695.png?raw=true)

### PC时代

- 也就一两台服务器，并且使用的是机架式的大服务器，价格也比较贵

### 虚拟化时代

- **典型的公司有XEN和VMware**
- **开源虚拟化(所有云平台底座)**
  - **KVM**
  - **XEN**
- **个人环境**
  - **vmwareworkstaction**
- **企业级别**
  - **Vmware vsphere（vmware公司)**
  - **Fusion Compute（华为公司)**
    - **CNA—Compute Node Agent 计算节点**
    - **VRM—vrital Resource Manegent 虚拟资源管理器**
- 微软
  - Hyper-V

​	通过对物理主机进行虚拟化操作，从而针对单主机上运行多个不同的虚拟主机，并且资源是进行隔离的，又能保证资源的高利用率。并且快照和备份也保证了业务的安全性![image-20240422111126196](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422111126196.png?raw=true)

### 云计算时代

也是一种服务，集中一切资源提供对外服务。

- `按需自主服务`：消费者可以按需部署处理能力，如服务器时间和网络存储，而不需要与每个服务供应商进行人工交互。

- `可计量服务`：云服务的收费是基于用户实际使用的资源进行计量，比如云主机的 CPU、内存、

  存储容量，网络带宽的消耗，按小时计费或者包年包月。

- `快速部署，弹性扩容`云计算可以迅速、弹性的提供能力，能快速扩展，也可以快速释放 实现快速扩缩容。对客户来说，可以租用的资源似乎是无限的，并且可以任何时间购买任何数量的资源

- `资源池化`：供应商将开源技术的计算资源进行集合起来，以便以多用户租用模式服务不同的客户，同时不同的物理服务器和虚拟资源可以根据客户需求分配和重分配。客户一般无法控制或知道资源的确切位置。这些资源包括存储、处理器、内存、网络带宽和虚拟机等。

- `广泛网络接入`：可以通过互联网获取各种能力，并可以通过标准方向进行访问，客户可以通过移动电话、笔记本、PAD等。![image-20240422110502060](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422110502060.png?raw=true)

![image-20240422111216452](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422111216452.png?raw=true)

### 容器时代

Docker\Kubernetes\Openstak

### 云原生和微服务时代

云原生：就是从云中出运行和维护的应用

微服务：就是每个业务模块，比如一个`财务模块`包含了多个子模块，并且多个子模块都有互相调用的关系(账单、流水、花销)

### 总结：

> - IT核心
>   - 针对IAAS(即基础设施及服务)、PAAS（应用设施即服务）、SAAS（软件以服务）
> - 传统IT面临的挑战
>   - 业务上线慢、更新稳定性差、磁盘I/O性能会达到一定程度、计算资源成本堆叠
> - IT发展史（主要说明几点）
>   - 虚拟化时代
>     - 巨头公司：Xen、KVM、Vmwareworkstaction，FusionCompute
>   - 云计算时代
>     - 各大互联网公司先继发布，自家云平台，其本质大致相同，按需自主、按量服务等。并且通过将开源的计算软件进行整合，为多租户用户提供不同的租用应用模式，也就形成了资源池化
>   - 容器时代
>     - Docker、kubernetes、open stack（主要实现了秒级运行一个应用程序，更方便与管理，也提高了计算资源的利用率）
>   - 微服务时代
>     - 针对单个部门实现多功能的分化关联



---

----

## 云计算

### 华为 云计算分类

- 华为云分为两条线：分别为私有云和公有云
  - Huawei Cloud Computing 华为私有云(华为云Stack)
  - Huawei Cloud Service 华为公有云(华为云)

### 云计算部署方式

- 私有云

  ```apl
  私有云通常部署在企业或单位内部，运行在私有云上的数据全部保存在企业自有的数
  据中心内，如果需要访问这些数据，就需要经过部署在数据中心入口的防火墙，这样可以在最大程度上保护数据的安全。
  ```
  
- 公有云

  ```apl
  阿里云、华为云、腾讯云、京东云、青云、九州云、天翼云、移动云、长江云、武汉
  云等。云服务运营商拥有云基础设施，并且为公众或者企业用户提供云服务。云计算基础设施
  由一个组织拥有并且向公众或者大型的工业团体销售云计算服务，用户可以通过互联网像使用水电一样使用 IT 服务。
  ```
  
- 混合云

  ```apl
  混合云是一种比较灵活的云计算模式，它可能包含了公有云、私有云或者后面要讲的
  行业云中的两种或两种以上的云，用户的业务可以根据需求在这几种云上切换。
  ```

- 政务云/行业云/社区云

  ```apl
  以政企客户或者立足于某个行业，如教育、医疗、金融、政府、游
  戏等行业，为这些行业提供全套的云平台解决方案。
  ```

国内公有云排行：阿里云、华为云、腾讯云

国内私有云排行：华为独一份

### 云计算服务模式

![image-20240422111303028](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422111303028.png?raw=true)

#### Iaas

`Infrastructure as a Service`

基础设施即服务，就是由云平台提供基础设施（如：服务器、存储、网络、虚拟化资源）以及负责相关资源的维护，用户只需要关注系统和应用层面的部分即可。比如 ECS/EVS/VPC/EIP/ELB 等服务

#### PaaS

`Platform as a Service`

平台服务，就是有平台提供基础设施和应用部署（如：服务器、存储、网络、虚拟资源、操作系统、中间件、软件运行环境），以及负责相关维护，只需要关注引用和数据本身就行。典型产品：RDS数据库、CCE、SWR、中间件服务器等

#### SaaS

`Software as a Service`

软件及服务，就是有平台提供全部资源以及维护，用户只需要付费使用即可。比如 云视频会议/云桌面/语音服务等。

---

### 总结：

> - 云计算分类
>   - Huwei Cloud Computing（公有云）Huawei Cloud Service(私有云)
> - 云计算部署方式
>   - 公有云（为公众和企业提供计算服务）
>   - 私有云（针对特殊的企业或单位提供计算服务器）
>   - 混合云（即要使用公有云的服务，也需要保证数据的安全性）
>   - 政务云/行业云/社区云
> - 服务模式
>   - IAAS
>     - 应用、数据、存储、运行环境、中间件、操作系统
>   - PAAS
>     - 应用、数据
>   - SAAS
>     - 开箱即用

---

---



# 第二章服务器基础

## 1.服务器介绍

### 1.1 服务器类型

![image-20240422132108391](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422132108391.png?raw=true)

注意：1U等于：4.445cm

- **机架式服务器**

  ![image-20240422130656011](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422130656011.png?raw=true)

- **塔式服务器**

  ![image-20240422130710376](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422130710376.png?raw=true)

- **刀片服务器**

  ![image-20240422130628406](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422130628406.png?raw=true)

- **滑轨服务器**

  ![image-20240422130726758](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422130726758.png?raw=true)

### 1.2 服务器正面和背面

![image-20240422130916845](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422130916845.png?raw=true)

![image-20240422131844597](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422131844597.png?raw=true)

## 2.服务器关键技术

### 2.1 IPMI(智能平台管理接口)

​	**Interlligent Platfrom Management interface的缩写。原本是一种Inel架构的企业系统的周边设备所采用的一种工业标准。IPMI 亦是一个开放的免费标准，用户无需支付额外的费用即可使用此标准。**

​	**IPMI能够横跨不同的操作系统、固件和硬件平台，可以只能的监视、控制和自动回报大量服务器的运作状态，降低服务器系统成本。** 

![image-20240422133557705](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133557705.png?raw=true)

​	**不同的服务器厂商它们管理名称（主板上的）还有点不一样大部分服务器后面都叫Mgmt接口**

- HP 服务器主板后面叫 iLO
- IBM：管理平台叫RSA2
- DELL：管理平台叫iDRAC
- 华为：管理平台v1/v2 iMana v3 iBMC（只能基板管理控制）
- Huawei Interlligent Baseboard Management Controller，简称BMC口
  ![image-20240422133136995](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133136995.png?raw=true)



### 2.2 BMC

![image-20240422133631915](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133631915.png?raw=true)

### 2.3 IBMC

![image-20240422133644422](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133644422.png?raw=true)

### 2.4 BIOS

![image-20240422133700976](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133700976.png?raw=true)

### 2.5 RAID

![image-20240425232021581](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240425232021581.png?raw=true)

![image-20240422135313219](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135313219.png?raw=true)

![image-20240422135325847](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135325847.png?raw=true)

![image-20240422135346729](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135346729.png?raw=true)

![image-20240422135353740](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135353740.png?raw=true)

![image-20240422135405407](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135405407.png?raw=true)

![image-20240422135413138](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422135413138.png?raw=true)

![image-20240422133726290](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422133726290.png?raw=true)

## 总结

----

---

# 实验华为企业级虚拟化解决方案（FC）

## **Fusion Compute虚拟化平台（FC）**

`注意！！CNA和VRM版本必须一直`

![image-20240422153600458](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422153600458.png?raw=true)

### 主要组件及介绍：

- **CNA** Computing Node Agent `计算节点管理`
  - 是FS的躯干，它是安装了虚拟化操作系统的服务器，主机直接向云资源池提供计算资源（包括CPU和内存），另外主机还连接交换机和存储设备，将网络存储资源一起接入云资源池中
    - 只能通过ISO镜像文件部署到物理服务器上（虚拟服务器无法导入VRM）
- **VRM** Virtual Resource ManageMent`虚拟资源管理`
  - 是FS的大脑，对云资源池管理和协调，使云资源池中的资源可以被合理的使用
    - 可以通过IOS镜像文件部署到物理服务器上
    - 可以通过ZIP压缩文件部署到虚拟服务器上（例如部署到CNA，并且通过installer工具进行部署）

资源下载参考

https://www.yuque.com/tianhairui/mnpclz/tex4s4mmoa0w4xbv

所有软件和工具下载，一定去官方下载，不要在三方下载一些所谓的破解版或绿色版（小心后门），养成好习惯，尤其在生产环境中使用的软件和工具。

## **ComPuting Node Agent（CNA）**

### 配置RAID

#### 登录IPMI智能卡

- **配置为单次光盘启动**

![image-20240422141217498](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422141217498.png?raw=true)

![image-20240422141248603](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422141248603.png?raw=true)

#### KVM连接服务器

![image-20240422141402041](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422141402041.png?raw=true)

![image-20240422142030889](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422142030889.png?raw=true)

![image-20240422142059459](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422142059459.png?raw=true)

#### 进入RAID

- 再强制重启过程中，时刻保持输出信息，以便通过ctrl+R进入RAID模式
  ![image-20240422142231398](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422142231398.png?raw=true)

  ![image-20240422142244502](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422142244502.png?raw=true)

##### 创建RAID

- 通过create进行创建

  ![image-20240422144848136](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422144848136.png?raw=true)

  ![image-20240422144902687](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422144902687.png?raw=true)

##### 初始化

- 初始RAID磁盘，填写对应的校验值

  ![image-20240422145016643](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145016643.png?raw=true)

##### 热备盘

- 可以根据需求配置热备盘

  ![image-20240422145037426](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145037426.png?raw=true)

### 重启配置CNA操作系统

- **根据提示进行配置**

  ![image-20240422145547510](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145547510.png?raw=true)

  ![image-20240422145842064](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145842064.png?raw=true)

  ![image-20240422145554213](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145554213.png?raw=true)

#### 网络配置(Network)

- **选择IPV4**

  ![image-20240422145908699](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422145908699.png?raw=true)

  ![image-20240422150040730](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422150040730.png?raw=true)

- **选择第一个回车进入**

  ![image-20240422150200073](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422150200073.png?raw=true)

- **配置IP地址，并且带VLAN选项**

  ![image-20240422150236812](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422150236812.png?raw=true)

#### 密码配置(Password)

- **`注意`：这个密码是root的密码，不能太过于简单：推荐Huawei-Cloud@123**

  ![image-20240422150603954](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422150603954.png?raw=true)

#### Grub密码

- **注意这个是用于破解密码时，需要输入的grub密码哈哈哈无语了**

  ![image-20240422150851063](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422150851063.png?raw=true)

#### 初始胡CNA

- **执行命令：`canInit`**

  - **选择加密类型：`国记通用型：0`**
  - **为gandalf用户设置密码：`Huaweicloud@123`**
  - **为redis数据库设置密码：`Huaweicloud@123`**

  ![image-20240422152241087](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422152241087.png?raw=true)

**`注意`如何需要通过第三方连接工具连接，则需要使用gandalf用户进行连接，并通过gandalf用户su -进入root即可**

## Virtual Resource ManageMent

**`注意!!！`：**

- **如果使用的是虚拟机部署可以通过部署在CNA节点上。部署在不同的CNA节点达到主备模式**
- **如何公司比较有**钱，对服务器性能要求比较严格，则可以部署在物理服务器上

### 开启SFTP服务

```apl
使用“PuTTY”，登录待开启SFTP服务的主机。 以“gandalf”用户，通过管理IP地址登录。
系统同时支持密码和公私钥对身份进行认证，如果使用公私钥对进行登录认证，具体操作请参见使用PuTTY通过公私钥对认证方式登录节点。

执行以下命令，并按提示输入“root”用户的密码，切换至“root”用户。
su - root

执行以下命令，防止系统超时退出。
TMOUT=0

执行以下命令，开启SFTP服务。
sh /opt/galax/gms/common/util/configSshSftp.sh open

当提示以下信息，表示命令执行成功。
open sftp service succeed.
```

### CNA上传Installer

- 注意：使用远程传输工具WinSCP将FusionCompute安装工具的zip包传输至“/home/GalaX8800”目录下。

  - ```apl
    登录WinSCP时，需填写以下参数：
    主机名：CNA主机IP地址。
    用户名：gandalf
    密码：gandalf的密码
    FusionCompute安装工具的zip包：
    x86架构
    Intel/Hygon/AMD：FusionCompute-LinuxInstaller-8.6.0-X86_64.zip
    AMD架构
    Hisilicon/Phytium：FusionCompute-LinuxInstaller-8.6.0-ARM_64.zip
    ```

- 执行以下命令，并按提示输入“root”用户的密码，切换至“root”用户，进入“/home/GalaX8800/”目录。

  ```apl
  cd /home/GalaX8800
  ```

- 执行命令解压软件包

  ```apl
  unzip 安装包名称.zip
  ```

- 安装installer

  ```apl
  cd 软件包路径/bin/
  sh webinstaller.sh install
  ```

  ![image-20240422162450241](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422162450241.png?raw=true)

### 自定义安装Fusion Compute

- **默认账户和密码**

  - ```apl
    初始账号信息：admin
    初始密码：IaaS@PORTAL-CLOUD8!
    第一次登录需要修改默认密码。
    当前仅支持单用户登录。
    ```

  ![image-20240422163215848](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422163215848.png?raw=true)

  ![image-20240422163538629](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422163538629.png?raw=true)

  ![image-20240422163737890](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422163737890.png?raw=true)

- **VRM包上传**

  ![1713775333381](https://github.com/liuzhenhua1223/Image/blob/master/IE/1713775333381.png?raw=true)

- **配置VRM**

  ![image-20240422203002645](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203002645.png?raw=true)

- **选择主机**

  ![image-20240422203237997](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203237997.png?raw=true)

- **配置数据存储**

  ![image-20240422203305522](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203305522.png?raw=true)

- **权限管理模式**

  ![image-20240422203330843](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203330843.png?raw=true)

- **安装VRM**

  ![image-20240422203439489](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203439489.png?raw=true)

- **下载登录信息**

  ![image-20240422203509109](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422203509109.png?raw=true)

### 登录VRM

- **通过定义的admin用户和密码进行登录**

  ![image-20240422205225899](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422205225899.png?raw=true)

## FusionCompute运营

- 如果使用FusionCompute Web工具安装VRM，系统会自动创建一个`ManagementCluster集群`

- 加载licens
- 配置时区时间：如果CNS两台时差超过五分钟着无法进行添加
  - ![image-20240422211327224](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422211327224.png?raw=true)

### 什么是集群

- **有两台或两台以上的主机，为了一个共同的商业目标，根据商业目标不同，集群分为以下三类**

1. **HA(Haproxy)高可用集群，用来解决业务的连续性**
2. **故障域SLB()**

### 创建主机windows

- **右键ManageMentCluster创建主机**

  ![image-20240422231215888](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231215888.png?raw=true)

- **基本配置**

  ![image-20240422231340587](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231340587.png?raw=true)

- **配置数据存储**

  ![image-20240422231359793](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231359793.png?raw=true)

- **配置虚拟机规格**

  ![image-20240422231422607](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231422607.png?raw=true)

- **确认虚拟机信息**

  ![image-20240422231442817](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231442817.png?raw=true)

  ![image-20240422231518338](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231518338.png?raw=true)

- **配置光驱启动**

  挂载光驱一共3种方式

  本地方式：一旦点击，会加载当前跳板机的本地磁盘里面的文件，受网络影响，不推荐
  
  共享方式：通过cifs/nfs网络共享的方式访问，也会受到网络影响，不推荐
  
  文件方式：推荐。首先要把iso文件上传到CNA的本地存储里面，之后直接加载存储磁盘里面的iso。
  
  - 上传镜像
  
  ![image-20240513214336476](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214336476.png?raw=true)
  
  加载镜像
  
  ![image-20240422231546600](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231546600.png?raw=true)
  
  ![image-20240422231554760](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231554760.png?raw=true)

#### VNC登录windows主机

- **找到主机对应的CNA右键VNC连接**

  ![image-20240422231642502](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231642502.png?raw=true)

- 正常创建windows

  ![image-20240422231659262](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231659262.png?raw=true)

  ![image-20240422231706398](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422231706398.png?raw=true)

#### 加载Windows硬盘驱动

- **因为磁盘类型为`VIRTIO`需要加载软盘驱动，所以在安装过程中无法显示识别磁盘，需要通过软盘驱动进行加载**

  ![image-20240422232021834](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422232021834.png?raw=true)

  ![image-20240422232026964](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422232026964.png?raw=true)

  ![image-20240422232032096](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422232032096.png?raw=true)

  ![image-20240422232036898](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422232036898.png?raw=true)

创建进入系统即可。

- 进入即可

  ![image-20240422232445918](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422232445918.png?raw=true)

#### 加载Windows网络驱动

### VirtIO类型介绍

- **Windows默认不携带VirtIO,Linux自带**
- **vfd：Virtual floppy disk**

### 安装Tools

- **卸载关盘**

  ![image-20240422235502040](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235502040.png?raw=true)

  ![image-20240422235540078](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235540078.png?raw=true)

  ![image-20240422235609673](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235609673.png?raw=true)

- **安装完成重启即可**

  ![image-20240422235707983](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235707983.png?raw=true)

  ![image-20240422235755274](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235755274.png?raw=true)

  ![image-20240422235810929](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235810929.png?raw=true)

  ![image-20240422235824554](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240422235824554.png?raw=true)

### 创建集群

- **右键资源池—创建集群**

  ![image-20240423130920651](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423130920651.png?raw=true)

  ![image-20240423131123464](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423131123464.png?raw=true)

#### 基本配置

##### 内存复用

- 所有虚拟机分配的内存会超出宿主机内存，可以提高虚拟机开机密度

  - 开启提高机器的利用率，影响性能
  - 关闭：提高虚拟机的性能，浪费资源

  ![image-20240423131830861](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423131830861.png?raw=true)

##### 虚拟机启动策略

- 负载均衡： 系统自动根据使用CPU和内存各自的加权值计算，选择占用率最小的主机
- 自动分配：虚拟机启动时，在集群中满足资源条件的节点中随机进行节点的选择。

- 虚拟机NUMA结构自动调整：虚拟机NUMA结构自动调整开关：默认关闭。如果虚拟机使用GPU直通场景，建议开启。
  - ![image-20240423133453220](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423133453220.png?raw=true)

#### HA配置

- > 当物理主机或者源VM故障时，会根据集群HA策略将宕掉的VM在正常工作的主机上开启，范围是集群内，HA有集群策略管控，HA是在VM宕机的时候进行VM恢复，要求使用共享存储，当VRM故障时，集群内所有CAN节点可以自治

  ![image-20240423133918360](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423133918360.png?raw=true)

  ![image-20240423134103108](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423134103108.png?raw=true)

  ![image-20240423134118976](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423134118976.png?raw=true)



#### 计算资源调度配置(DRS)

- DRS(分布式资源调度)
- DPM(分布式电源管理)

VRM 检测到整个集群资源利用率低于20%，则触发 DPM←关闭一部分 CNA 主机，但是，所有的业务不能中止“在关闭 CNA 之前，将待关闭 CNA 主机上的虚拟机迁移到其他 CNA 中

![image-20240429152552859](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429152552859.png?raw=true)

# 第三章存储技术基础

## 1.存储基础介绍

### 1.1 什么是存储

- **数据产生——数据处理——数据管理，形成整体的存储架构**

  ![image-20240423171424171](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171424171.png?raw=true)

### 1.2主流应硬盘类型

#### 硬盘简介

![image-20240423171514706](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171514706.png?raw=true)

![image-20240423171535161](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171535161.png?raw=true)

### 1.3 存储组网类型

#### DAS存储

![image-20240423171811249](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171811249.png?raw=true)

#### NAS存储

>NFS（Network File System）是Sun Microsystems在1984年创建的Internet标准协议。开发NFS是为了允许在局域网上的系统之间共享文件。Linux NFS客户端支持三个版本的NFS协议：NFSv2 [RFC1094]、NFSv3 [RFC1813] 和NFSv4 [RFC3530]。其中NFSv2使用UDP协议，数据访问和传输能力有限，已经过时；NFSv3版本在1995年发布，添加了TCP协议作为传输选项，被广泛使用；NFSv4版本在2003年发布，已获得更好的性能和安全性。NFS的工作机制：主要是采用远程过程调用RPC机制。RPC提供了一组与机器、操作系统以及低层传送协议无关的存取远程文件的操作，允许远程客户端以与本地文件系统类似的方式，来通过网络进行访问。NFS客户端向NFS服务器端发起RPC请求，服务器将请求传递给本地文件访问进程，进而读取服务器主机上的本地磁盘文件，返回给客户端。CIFS（Common Internet File System）是一种网络文件系统协议，用于在网络上的机器之间提供对文件和打印机的共享访问。现在主要实现在Windows主机之间进行网络文件共享功能。

![image-20240423171833282](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171833282.png?raw=true)

>NAS可作为网络节点，直接接入网络中，理论上NAS可支持各种网络技术，支持多种网络拓扑，但是以太网是目前最普遍的一种网络连接方式，我们主要讨论是以以太网为网络基础的NAS环境。NAS本身能够支持多种协议（如NFS、CIFS等），而且能够支持各种操作系统。通过任何一台工作站，采用IE或Netscape浏览器就可以对NAS设备进行直观方便的管理。

![image-20240423171855666](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171855666.png?raw=true)

#### SAN存储

>存储区域网络（Storage Area Networks，SAN）：一个存储网络是一个用在服务器和存储资源之间的、专用的、高性能的网络体系。 SAN是独立于LAN的服务器后端存储专用网络。 SAN采用可扩展的网络拓扑结构连接服务器和存储设备，每个存储设备不隶属于任何一台服务器，所有的存储设备都可以在全部的网络服务器之间作为对等资源共享。SAN主要利用Fibre Channel Protocol（光纤通道协议），通过FC交换机建立起与服务器和存储设备之间的直接连接，因此我们通常也称这种利用FC连接建立起来的SAN为FC-SAN。FC特别适合这项应用，原因在于一方面它可以传输大块数据，另一方面它能够实现较远距离传输。SAN主要应用在对于性能、冗余度和数据的可获得性都有很高要求的高端、企业级存储应用上。随着存储技术的发展，目前基于TCP/IP协议的IP-SAN也得到很广泛的应用。IP-SAN具备很好的扩展性、灵活的互通性，并能够突破传输距离的限制，具有明显的成本优势和管理维护容易等特点。NAS和SAN最大的区别就在于NAS有文件操作和管理系统，而SAN却没有这样的系统功能，其功能仅仅停留在文件管理的下一层，即数据管理。SAN和NAS并不是相互冲突的，是可以共存于一个系统网络中的，但NAS通过一个公共的接口实现空间的管理和资源共享，SAN仅仅是为服务器存储数据提供一个专门的快速后方存储通道。

![image-20240423171932049](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423171932049.png?raw=true)

#### FC-SAN

>FC：Fiber Channel，光纤通道，是指一种用于在光纤或者铜缆上传输100 Mbit/s到4.25 Gbit/s信号的标准数据存储网络。用于建立存储区域网的高速传输技术。光纤通道能够用于支持ATM， IP等协议的一般网络，但它主要用途是从服务器上传输小型计算机系统接口（SCSI）流量到磁盘阵列。

![image-20240423172012437](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172012437.png?raw=true)

#### IP-SAN

>iSCSI：Internet Small Computer System Interface，Internet小型计算机系统接口，是一种基于因特网及SCSI-3协议下的存储技术，它将原来只用于本机的SCSI协议透过TCP/IP网络发送，使连接距离可作无限延伸。在后续课程中我们会了解到它的协议封装、工作原理及使用场景。

![image-20240423172038435](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172038435.png?raw=true)

#### 三种存储组网总结对比

![image-20240423172119718](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172119718.png?raw=true)

### 1.4 存储形态介绍

#### 集中式存储

>集中式存储的缺点：孤立的存储资源，存储通过专用网络连接到有限数量的服务器；集中式纵向扩容通过增加硬盘框实现，硬件控制器性能（单控制器带盘能力）成为瓶颈；集中式存储横向扩容需要通过控制器全连接实现，硬件控制器性能成为扩容瓶颈；集中式存储资源缺乏共享，存储设备和资源往往由不同厂家提供，设备之间无法进行资源共享，数据中心看到的是一个个孤立的存储池；集中式存储采用集中式元数据管理方式，系统所能提供的并发操作能力将受限于元数据服务的性能，元数据服务也将会成为系统的性能瓶颈；如何解决传统集中式存储扩容、性能瓶颈的问题？

![image-20240423172153793](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172153793.png?raw=true)

#### 分布式存储

>分布式存储利用软件重构存储服务形式，通过软件模拟原先硬件控制器实现功能的同时，规避硬件控制器的种种弊端。资源池：类似于SAN的RAID组概念。

![image-20240423172210033](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172210033.png?raw=true)

#### 存储业务类型

>对象存储是一种新兴存储技术，对象存储系统综合了NAS和SAN的优点，同时具有SAN的高速直接访问和NAS的数据共享等优势，提供了高可靠性、跨平台性以及安全的数据共享的存储体系结构。对象存储与块存储、文件存储的对比如下：块存储对存储层直接访问，开销最小，效率最高，速度最快。但成本最高，扩展困难。块存储采用iSCSI/FC协议，很难跨网络传输。适合的应用场景是企业数据库，如运行Oracle等；文件存储是在块存储之上构建了文件系统，采用目录-目录-文件的方式组织数据，更容易管理。因为大多数应用程序都是对文件进行操作，因此文件存储更容易和应用系统对接。文件系统受目录树的限制，扩展性受限，一般最多扩展到几十PB。文件系统适用于企业内部应用整合，文件共享场景；对象存储是在块存储之上构建了对象管理层，与文件系统相比，对象系统层是扁平的，扩展限制少，因此拥有近乎无限的扩展性。对象由唯一的Key，文件，数据（文件），元数据，自定义元数据构成，由于包含了自管理信息，更加智能。对象存储采用兼容标准的互联网协议接口，可以跨地域传输。对象存储适用于面向互联网服务的存储场景，以及企业内部的归档、备份场景。

![image-20240423172229299](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240423172229299.png?raw=true)

## 2.存储关键技术

- RAID基本概念

  ![image-20240424093811817.png](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424093811817.png?raw=true)

- 形式

  ![image-20240424094033420](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094033420.png?raw=true)

- 保护

  ![image-20240424094049753](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094049753.png?raw=true)

- 热备

  ![image-20240424094111957](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094111957.png?raw=true)

- 常见RAID

  ![image-20240424094134361](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094134361.png?raw=true)

### 1.1 RAID 2.0

![image-20240426131024373](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426131024373.png?raw=true)

#### 技术介绍

- ![image-20240424094641134](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094641134.png?raw=true)

#### 原理

- ![image-20240424094825214](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094825214.png?raw=true)

- ![image-20240424095013569](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424095013569.png?raw=true)

### 1.2RAID2.0+

#### 技术介绍

- ![image-20240424094658075](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094658075.png?raw=true)

#### 逻辑原理

- ![image-20240424094740668](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424094740668.png?raw=true)

##### 硬盘域（DISK Domain)

![image-20240426095252668](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426095252668.png?raw=true)

> DiskDomain即硬盘域，是一堆硬盘的组合（可以是整个系统所有硬盘），这些硬盘整合并预留热备容量后统一想存储池提供存储资源

​		![image-20240426093845408](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426093845408-1714095588071-1.png?raw=true)

##### 存储池 (Storage Pool)

![image-20240426095304575](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426095304575.png?raw=true)

> - Storage Pool即存储池，是存放存储空间资源的容器，所有应用服务器使用的存储空间都来自于存储池
>
> - Tier即存储层级别，通过不通的分层进行数据存储，以便满足不通性能要求的应用提供不同存储空间
>
>   - SSD高性能层：访问频繁的数据可以放入高性能层
>
>   - SAS性能层：访问数据频繁一般的
>
>   - NL-SAS容量层：不怎么访问的数据，备份数据
>
>     ![image-20240426131052987](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426131052987.png?raw=true)
>
> ---
>
> 总结：一个LUN由三部分空间组成，即提升了性能由节约了成本
>
> 

- ![image-20240426095707843](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426095707843.png?raw=true)



##### Disk Group（DG)

> 即硬盘组，由硬盘域内相同类型的多个银盘组成的集合，硬盘包括SSD、SAS、NL-SAS
>
> - OcenStore存储系统在每个磁盘域内，根据每种磁盘数量自动划分一个或多个Disk Group
> - 一个DG智能包含一种硬盘类型
> - 任意一个CKGd 的多个CK都来自同一个DG的不同硬盘



##### LD(逻辑磁盘)

![image-20240426100105216](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426100105216.png?raw=true)

> Logical Drive 即逻辑磁盘，是存储系统管理的磁盘，和物理磁盘一一对应，提供逻辑的物理磁盘空间

- ![image-20240426100042720](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426100042720.png?raw=true)

##### Chunk（CK）

![image-20240426100507064](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426100507064.png?raw=true)

> Chunk简称CK，是存储池内的硬盘空间切分若干固定大小的物理空间，每块物理空间大小为64MB，是组成RAID的基本单位。

- ![image-20240426100456838](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426100456838.png?raw=true)

##### Chunk Group(CKG)

> - Chunk Group 是由来自同一个DG内不同硬盘的CK按照RAID算法组成的逻辑存储单元，是存储池从硬盘域上分配资源的最小单位
>
> - 一个CKG中的CK均来自于同一个DG中的硬盘，CKG具有RAID属性（RAID属性实际配置在Tier上），CK和CKS均属于系统内部对象，由存储系统自动完成配置，对外不体现。

- ![image-20240426125717234](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426125717234.png?raw=true)

##### Extent

> - Extent是在CKG基础上划分的固定大小的逻辑存储空间，大小可调，是热点数据统计和迁移的最小单元，也是存储池中申请空间，释放空间的最小单位
> - 一个Extent归属于一个Volume或一个LUN，Extenl大小在创建存储池可以进行设置，创建之后不可更改，不同存储池的Extenl大小可以不同，但同于一存储池中的Extenl大小是统一的。

- ![image-20240426130024425](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426130024425.png?raw=true)

##### Grain

> 在Thin LUN模式下，Extenl按照固定大小被进一步划分为更细颗度的块，这些块称为Grain。Thin LUN以Grain为客户里进行空间分配，Grain内的LBA是连续的

- ![image-20240426130256895](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426130256895.png?raw=true)

##### LUN

> Volume即卷，是存储系统内部管理对象，LUN是可以直接映射给主机读写的存储单元，是Volume对象的外体观

- ![image-20240426130719457](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426130719457.png?raw=true)

#### 两种重构方式对比

>在传统RAID的重构中，故障盘的数据只能向一个热备盘上重构写。在RAID2.0的重构中，由于热备空间是分散在多个盘上的，故障盘上的数据可以重构到多个盘上，避免了对单热备盘的写瓶颈，因此重构速度很快。另外，RAID2.0的重估是按Chunk重构的，重构时只重构LUN中分配了业务数据的Chunk，比传统RAID需要重构所有LUN空间的方式，减少了不必要的重构读写，也能提高整体重构速度。那么，对重构速度的提升有多少呢？1TB的NL-SAS盘的重构，使用传统RAID的方式需要10小时，而使用RAID2.0技术，只需要0.5个小时，也就是说，重构速度是原来的20倍。重构速度的提高，减少了重构时间，因此减少了重构过程中对主机业务性能的影响时间，也减少了重构过程中双盘失效导致数据丢失的风险。

![image-20240426131004522](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426131004522.png?raw=true)

### 1.3存储协议

- SCSI协议

  ![image-20240424102827251](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424102827251.png?raw=true)

- ISCSI协议

  ![image-20240424102844886](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424102844886.png?raw=true)

  ![image-20240424102903884](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424102903884.png?raw=true)

### 1.4FC协议与TCP协议融合

- >FCIP：Fibre Channel over IP，基于IP的光纤通道，是连接TCP/IP网络链路上的光纤通道架构的一项IETF建议标准。利用目前的IP协议和设施来连接两个异地FC SAN的隧道，用以解决两个FC SAN的互连问题。iFCP：Internet Fibre Channel Protocol，Internet光纤信道协议，是一种网关到网关的协议，为TCP/IP网络上的光纤设备提供光纤信道通信服务。iFCP 使用 TCP提供拥塞控制、差错监测与恢复功能。iFCP主要目标是使现有的光纤信道设备能够在IP网络上以线速互联与组网。此协议及其定义的帧地址转换方法允许通过透明网关（transparent gateway）将光纤信道存储设备附加到基于IP的网络结构。FCoE：Fibre Channel over Ethernet，利用以太网路，传送光纤通道（Fibre Channel）的信号，让光纤通信的资料可以在10 Gigabit以太网路网络骨干中传输，但仍然是使用光纤通道的协定。IPFC：IP over Fiber Channel，在光纤通道上的IP。IPFC使用在两个服务器之间的光纤通道连接作为IP数据交换的媒介。为此，IPFC定义了如何通过光纤通道网络传送IP分组。跟所有的应用协议一样，IPFC实现为在操作系统中的一个设备驱动器。对本地IP配置的连接使用“ifconfig”“或“ipconfig”。然后IPFC驱动器寻址光纤通道主机适配卡，就可以在光纤通道上发送IP分组。

  ![image-20240424103023617](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424103023617.png?raw=true)

  ![image-20240424103053830](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424103053830.png?raw=true)

- iFCP协议栈

  ![image-20240424103252966](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424103252966.png?raw=true)

- FCoE协议

  ![image-20240424103311577](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424103311577.png?raw=true)

  ![image-20240424103325119](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240424103325119.png?raw=true)

## 多路径问题

> 华为UItraPath多路径技术 解决了主机数据冗余问题，提高了数据链路的安全性，又具备了 路径闪断、路径测试、路径隔离和路径警告推送问题。

- 没有使用多路径软件的Windows主机

- 每条单独的路径都代表了一个独立卷

  ![image-20240426173545408](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240426173545408.png?raw=true)SUSE Linux Enterprise

# 实验华为对接v3存储

> 创建vmware虚拟机-自定义-SUSE 11 Ea—选择已有磁盘镜像——选择8G内存——6个网卡——2个硬盘——开机配置IP和网卡网关——默认账户和密码：admin/Admin@storage

>进入OcenStor DeviceManager
>
>- 创建硬盘域——创建存储池——创建LUN——创建LUN主机——创建主机——创建主机组——创建映射——应用主机发起iscis拨号——添加主机驱动

## CNA配置LUNC

![image-20240427235935022](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427235935022.png?raw=true)

### CNA配置Ip（CNA02同步骤）

- 进入Fusion Compute进行配置CNA IP地址，用于和OcenStorDeviceManage进行LUN共享链接

  - 逻辑接口

  ![image-20240427234843097](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427234843097.png?raw=true)

  ![image-20240427234911282](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427234911282.png?raw=true)

  **名称——VLAN：0表示没有——随便一个IP**

  ![image-20240427235307478](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427235307478-1714233194521-1.png?raw=true)

  ![image-20240427235503285](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427235503285.png?raw=true)

#### 添加存储资源

- 发

  ![image-20240427235550763](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240427235550763.png?raw=true)

- 添加OcenStorDeviceManager端口IP地址——管理IP可以根据实际情况配置也可以随便

  - 选择关联主机

  ![image-20240428000244110](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000244110.png?raw=true)

  - 生产环境可以添加两条

    ![image-20240428000121308](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000121308.png?raw=true)

![image-20240428000350514](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000350514.png?raw=true)

![image-20240428000356108](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000356108.png?raw=true)

![image-20240428000541595](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000541595.png?raw=true)

#### 添加启动器

- ![image-20240428000619332](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000619332.png?raw=true)

#### 扫描磁盘

- ![image-20240428000721775](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428000721775.png?raw=true)

#### 创建数据存储

- ![image-20240428001030679](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001030679.png?raw=true)

  ![image-20240428001050894](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001050894.png?raw=true)

  ![image-20240428001129576](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001129576.png?raw=true)

  ### 创建虚拟机

  ![image-20240428001247037](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001247037.png?raw=true)

  ![image-20240428001338336](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001338336.png?raw=true)

  ![image-20240428001404125](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001404125.png?raw=true)

# 实验华为对接V6存储

## 搭建V6存储仿真器

- Hyper-v不建议搭建，因为使用完删除后，vmware无法正常使用。

### 导入模板

![image-20240513170020603](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170020603.png?raw=true)

![image-20240513170043781](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170043781.png?raw=true)

![image-20240513170207899](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170207899.png?raw=true)

- 同事加载3个文件（1个配置文件、2个磁盘文件）

![image-20240513170246606](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170246606.png?raw=true)

![image-20240513170314991](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170314991.png?raw=true)

![image-20240513170325737](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170325737.png?raw=true)

![image-20240513170344817](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170344817.png?raw=true)

![image-20240513170402960](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170402960.png?raw=true)

![image-20240513170413798](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170413798.png?raw=true)

![image-20240513170424620](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170424620.png?raw=true)\

![image-20240513170459113](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170459113.png?raw=true)

- 如果操作时间长，被弹出去，建议修改超时时间。

![image-20240513170743467](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513170743467.png?raw=true)

### 通过模板部署V6

![image-20240513213259338](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213259338.png?raw=true)

![image-20240513213313916](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213313916.png?raw=true)

![image-20240513213325359](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213325359.png?raw=true)

![image-20240513213333346](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213333346.png?raw=true)

![image-20240513213342148](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213342148.png?raw=true)



![image-20240513213355371](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213355371.png?raw=true)

### 登录OcenStor DeviceManager

- 默认的账号密码：admin Admin@storage
  - 也可以直接通过VNC进行修改密码

![image-20240513213520584](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213520584.png?raw=true)

### 访问存储

https://192.168.22.250:8088

![image-20240513213550796](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213550796.png?raw=true)

![image-20240513213557877](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213557877.png?raw=true)

![image-20240513213609697](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213609697.png?raw=true)

### 初始化

- #### 初始化就是建硬盘域和存储池

#### 导入Licens

![image-20240513213722196](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213722196.png?raw=true)

![image-20240513213729266](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213729266.png?raw=true)

![image-20240513213739949](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213739949.png?raw=true)

![image-20240513213747647](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213747647.png?raw=true)

![image-20240513213752507](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213752507.png?raw=true)

## 配置存储

### 配置存储IP

![image-20240513213837201](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213837201.png?raw=true)

![image-20240513213848197](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213848197.png?raw=true)

![image-20240513213900987](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213900987.png?raw=true)

![image-20240513213912150](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213912150.png?raw=true)

### 创建LUN

![image-20240513213926667](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513213926667.png?raw=true)

### 创建LUN组

![image-20240513214001269](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214001269.png?raw=true)

### 创建主机

![image-20240513214017229](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214017229.png?raw=true)

### 创建主机组

![image-20240513214040888](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214040888.png?raw=true)

![image-20240513214049097](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214049097.png?raw=true)

### 创建映射视图

![image-20240513214119993](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214119993.png?raw=true)

![image-20240513214130022](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214130022.png?raw=true)

![image-20240513214149371](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513214149371.png?raw=true)

## FC对接共享存储

> 1. 客户端发起ISCSI发起程序(拨号)
> 2. 存储端将主机的IQN号添加到主机(标签)中
> 3. 客户端扫描磁盘、分区格式化、使用

### 添加存储资源（iSCSI发起程序)

```apl
chap认证，一般情况下，当你知道存储业务ip地址，并且你的客户端和存储业务ip地址互通，你就可以直接向存储发起连接。
但是，某些情况下，存储为了安全起见，需要设置一个功能，就算你知道了业务ip，并且也能和存储业务ip互通，我也不让你发起连接。
就可以在存储里面添加一个chap认证的用户和密码，如果你想让对应的客户端主机连接存储，那么就需要在客户端主机里面，修改chap配置文件，输入存储创建的那个用户名和密码。
```

![image-20240513220204309](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220204309.png?raw=true)

![image-20240513220232474](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220232474.png?raw=true)

![image-20240513220313345](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220313345.png?raw=true)

![image-20240513220318129](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220318129.png?raw=true)

### 存储测添加IQN

![image-20240513220351979](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220351979.png?raw=true)

### 扫描磁盘

![image-20240513220428403](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220428403.png?raw=true)

![image-20240513220443444](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220443444.png?raw=true)

### 添加数据存储（格式化）

![image-20240513220552321](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220552321.png?raw=true)

![image-20240513220600553](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220600553.png?raw=true)

![image-20240513220617765](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240513220617765.png?raw=true)



# FusionCompute管理操作

## 磁盘管理

### 磁盘类型

#### 普通

- 根据实际的空间进行创建，创建过程首先将磁盘进行填满，之后进行置零。这种模式的性能要优于其他两种，但是时间会长

#### 精简

- 根据数据的存储，逐渐填充，直到磁盘用完，

#### 普通延迟置零

- 根据磁盘空间分配的空间，创建时没有任何数据，一点写入数据，就会自动填满磁盘，在删除填充数据，就可以正常使用了。

### 迁移磁盘（基于数据）

- ![image-20240428001451369](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001451369.png?raw=true)
- ![image-20240428001508681](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001508681.png?raw=true)
- ![image-20240428001619576](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001619576.png?raw=true)
- ![image-20240428001631754](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001631754.png?raw=true)

![image-20240428001641854](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001641854.png?raw=true)

![image-20240428001651125](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428001651125.png?raw=true)

### 迁移磁盘（基于虚机）

DRS热迁移

- ![image-20240428002118773](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428002118773.png?raw=true)

- 迁移到CNA01

  ![image-20240428002140987](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428002140987.png?raw=true)

  ![image-20240428002153727](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428002153727.png?raw=true)

  ![image-20240428002220152](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428002220152.png?raw=true)

### 磁盘属性

#### 从属

> 正常的磁盘模式，支持快照功能，并且是永久写入磁盘

#### 独立—持久

>相对于从属不支持快照功能，也是永久写入磁盘，可以用于针对一些缓存和不太重要的磁盘，从而减少整体性能和速率

#### 独立—非持久

> 类型于学校的`还原卡`,首先进行`从属模式`搭建完成后，然后切换为独立—非持久化即可实现，也不支持快照

## 快照技术

> 速度块、占用空间小

一致性快照：在创建快照前，强制将脏页写回硬盘，再创建快照前提是虚拟机需要安装tools

#### 快照工作原理

##### COW Copy-On-Write 

- 写时复制    块设备

  ![image-20240428112212461](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428112212461.png?raw=true)

##### ROW Redirect-On-Write

- 写时重定向   文件型
- 用户永远读取最后一个快照，对写性能不会有影响，但是对读数据会有影响![image-20240428130257235](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428130257235.png?raw=true)

- KVM虚拟化配置文件CNA

  ```apl
  cna002:~ # cd /etc/libvirt/qemu
  cna002:~#ls
  cna002:/etc/libvirt/qemu # cat i-00000023.xml
  </disk>
      <disk type='file' device='disk'>
        <driver name='qemu' type='raw' cache='none' io='native' iothread='1'/>
        <source file='/POME/datastore_25/vol/vol_3bb95d26-e616-467b-9498-47f2d472351b/vol_3bb95d26-e616-467b-9498-47f2d472351b.img'/>
        <target dev='vda' bus='virtio'/>
        <serial>3bb95d26-e616-467b-9498-47f2d472351b</serial>
        <boot order='1'/>
        <address type='pci' domain='0x0000' bus='0x02' slot='0x01' function='0x0'/>
      </disk>
  ```

- ![image-20240428154234985](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428154234985.png?raw=true)

  ![image-20240428154319654](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428154319654.png?raw=true)

- 拍摄快照再次查看该目录

  ![image-20240428154731451](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428154731451.png?raw=true)

- 发现CNA配置文件修改为了新的
  ![image-20240428154850993](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428154850993.png?raw=true)

## 克隆

- 给虚拟机做完整备份

- 业务测试

- 改变磁盘类型（普通 精简）

- 克隆完成，自动删除快照，快照中的数据会合并到虚拟机磁盘中，克隆的虚拟机依旧保持某个时间节点的数据不变

  ![image-20240428212410119](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428212410119.png?raw=true)

## 模板

- 批量部署虚拟机

- 制作模板流程

- c:\windows\system32\sysprep\sysprep.exe

  - > 1. 安装OS、anzhuangTools
    >
    > 2. 安装所需要的应用程序
    >
    > 3. 将IP地址设置为DHCP方式
    >
    > 4. 去除个性化信息（MAC地址、计算名，SID）

### 安装Tools

![image-20240428220703941](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428220703941.png?raw=true)

### 卸载光盘

![image-20240428220724578](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428220724578.png?raw=true)

### VPN进入系统设置DHCP

![image-20240428221816335](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428221816335.png?raw=true)

### 去个性化

c:\windows\system32\sysprep\sysprep.exe

- 做模板通常选择如下
  - 全新体验
  - 通用
  - 关机（纯净版）
    - 运行完 sysprep.exe 后，建议直接关机，如果再次开机，又会生成个性化信息<关机后，该虚拟机就是

![image-20240428222307760](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428222307760.png?raw=true)

### 转为模板

#### 转换位模板

- 只改变磁盘格式，如vhd改为vhdx，转换非常快，虚拟机转换为模板，原虚拟机就不存在了

  ![image-20240428222523587](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428222523587.png?raw=true)

  ![image-20240428222537828](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428222537828.png?raw=true)

#### 克隆为模板

- 通过该虚拟机创建一个新的模板，源虚拟机继续存储在

#### 导出为模板

- 导出之后也可以进行导入，类似于打镜像，

- OVF Open Virtal Format 公开镜像格式

- 导出的为ovf格式，不同虚拟化版本不兼容，支持跨平台使用，可以通过转换工具进行转换类型，比如转为为qcow2、vdh等等

  ![image-20240428222952435](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428222952435.png?raw=true)

![image-20240428223000687](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223000687.png?raw=true)

## 按模板部署虚拟机

- 省份

  ![image-20240428223523633](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223523633.png?raw=true)

  ![image-20240428223609705](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223609705.png?raw=true)

- ![image-20240428223659529](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223659529.png?raw=true)

- ![image-20240428223846041](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223846041.png?raw=true)

  ![image-20240428223915445](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223915445.png?raw=true)

- ![image-20240428223937222](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428223937222.png?raw=true)

### 重复规格创建

- 创建完一台模板后，定义了规格之后，再次创建时就可以根据定义的属性规格再次定义相同的规格

  ![image-20240428224059088](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428224059088.png?raw=true) 

## 虚拟机热迁移

1. 资源不均衡
2. CNA主机停机维护，但不能影响业务

#### 冷迁移

#### 热迁移

1. 当用户发起迁移时，CNA主机会生成内存位图区（包含旧内存的索引），新写入的数据写入到该位图区域内，开始迁移旧内存（20s)迁移过程中多出了100MB
2. 多次迭代，着100MB到新内存中
3. 阻止上层IO下发，最后一次同步内存数据到目标主机，将配置文件迁移到目标主机
4. 在目标主机上运行

- ![image-20240428233517412](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428233517412.png?raw=true)

- ![image-20240428233531175](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428233531175.png?raw=true)
- ![image-20240428233754974](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428233754974.png?raw=true)

- ![image-20240428234228973](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428234228973.png?raw=true)

- ![image-20240428234347492](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428234347492.png?raw=true)

- ![image-20240428234419336](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240428234419336.png?raw=true)

## VIMS虚拟集群存储文件系统

### 存储热迁移

源存储太老旧，需要更换新存储，其次就是存储的IO的读写能力

源存储负载太重，购买了一台新存储，把源存储上部分业务迁移数据迁移到新存储上

业务虚拟机对性能有些高，需要迁移到新存储

想改变磁盘模式，普通模式、精简模式、普通延迟置零模式

![image-20240429101913289](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429101913289.png?raw=true)

- 工作在本地磁盘无法迁移，则需要修改数据存储

  ![image-20240429100739166](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429100739166.png?raw=true)

![image-20240429100825959](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429100825959.png?raw=true)

![image-20240429100835245](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429100835245.png?raw=true)

![image-20240429100923058](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429100923058.png?raw=true)

## 光纤交换机配置

- 进入zone（图形化）

  - zone：隔离流量

  ![image-20240429133008709](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429133008709.png?raw=true)

  

# FusionCompute四个网络平面

## 管理平面

- **VRM——>连接CNA即为管理平面**
  - 如果VRM虚拟化部署，则系统会自动创建集群和分布式交换机，管理平面

### 双网卡绑定

- ![image-20240429165938392](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429165938392.png?raw=true)

## 业务平面

### 创建分布式交换机

- 批量为每台CNA创建OVS

![image-20240429225049645](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429225049645.png?raw=true)

- 为CNA节点绑定网卡（也可以批量绑定）

  ![image-20240429224211085](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224211085.png?raw=true)

  ![image-20240429224255269](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224255269.png?raw=true)

  ![image-20240429223922128](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429223922128.png?raw=true)

  ![image-20240429224037196](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224037196.png?raw=true)

  ![image-20240429224435273](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224435273.png?raw=true)

  

  ![image-20240429224444094](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224444094.png?raw=true)

- ![image-20240429224733163](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429224733163.png?raw=true)

  

### 创建端口租

#### OVS

- 使用OVS模式，该存储接口使用的VLAN可以与管理平面、业务平面共同使用。

#### Linux子接口交换模式

- 可以减少存储平面与管理平面、业务平面在主机内部的相互影响。存储接口所关联网口的VLAN被该存储接口独自占有且VLAN的ID不能为0：该网口上的管理平面、业务平面与其他存储接口无法使用该VLAN

- ![image-20240429231904370](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429231904370.png?raw=true)

#### DHCP工作原理

1. 客户端要获取IP地址时，则会向DHCP发送Discover 全网广播寻找DHCP服务器进行申领
2. DHCP服务器回应客户端，DHCP offer，回应说我有可用地址空间
3. 客户端发送请求，DHCP Equest
4. DHCP服务器响应 客户端请求DHCP Ack

- 如果一个网络中出现两个DHCP服务器时，则有可能获取到不如意的DHCP

![image-20240429230623253](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429230623253.png?raw=true)

![](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240429233759229.png?raw=true)

![image-20240430104147450](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240430104147450.png?raw=true)

## 存储平面

- eth4和eth5连接存储平面

  ![image-20240430104806358](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240430104806358.png?raw=true)

## VIMS心跳平面

- 心跳平面

- 虚拟机热迁移流量

  ![image-20240506164014575](https://github.com/liuzhenhua1223/Image/blob/master/IE/image-20240506164014575.png?raw=true)

# FusionCompute高级特性

# 


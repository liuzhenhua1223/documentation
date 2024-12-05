# Network

## 计算机网络定义

- 用通信线路将分散在不同地方的、具有独立功能的计算机系统相互连接，并按网络协议，进行数据通信和实现资源共享的计算机集  合，称为计算机网络。

### 计算机网络的组成

![image-20241010141431305](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010141431305.png?raw=ture)

### 网络与连网

- **网络**：把许多计算机连接在一起
- **互联网**：把许多网络通过一些路由器连接在一起

![image-20241010141627500](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010141627500.png?raw=true)

## 计算机网络发展

![image-20241010141926219](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010141926219.png?raw=true)

### 第一阶段

![image-20241010142011689](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142011689.png?raw=true)

### 第二阶段

![image-20241010142037758](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142037758.png?raw=true)

### 第三阶段

![image-20241010142120671](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142120671.png?raw=ture)

### 第四阶段

![image-20241010142156073](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142156073.png?raw=true)

### 因特网发展的三个阶段

![image-20241010142715862](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142715862.png?raw=true)

## 计算机网络的分类

![image-20241010142858467](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010142858467.png?raw=true)

![image-20241010143300519](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010143300519.png?raw=true)

![image-20241010143324983](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010143324983.png?raw=true)

![image-20241010143416084](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010143416084.png?raw=true)

![image-20241010143439485](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010143439485.png?raw=true)

### OSI七层模型

![image-20241010144120940](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010144120940.png?raw=true)

![image-20241010144226365](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010144226365.png?raw=true)

### TCP/IP参考模型

![image-20241010144521804](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010144521804.png?raw=true)

![image-20241010145142669](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010145142669.png?raw=true)

# 物理层

## 物理成概述

![image-20241010145947474](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010145947474.png?raw=true)

## 传输介质

![image-20241010150249566](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010150249566.png?raw=true)

## 传输方式

![image-20241010150934168](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010150934168.png?raw=true)

## 数据通信基础

### 数据通信基础知识

- **术语**
  - 数据(data)：传递(携带)信息的实体
  - 信息(Information)：是数据的内容和含义。以文字、声音、图形和图像形式。
  - 信号（Signal）：数据的表示形式，数据以信号的形式在介质中传播
  - 信道（Channel）：传输信息的线路(或通路)

- **模拟信号与数字信号**

  ![image-20241010163413177](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010163413177.png?raw=true)

  ![image-20241010163759593](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010163759593.png?raw=true)

  - 模拟信号和数字信号的区别可以简单理解为：
    - **模拟信号**是连续的，可以取任意值，比如声音的波形，像一条连续的曲线。
    - **数字信号**是离散的，只能取有限的值，比如二进制中的“0”和“1”。

  - **主要区别：**

  1. **表现方式**：
     - 模拟信号：连续变化，可以是任何值。
     - 数字信号：离散变化，通常只有“0”和“1”两种状态。
  2. **抗干扰性**：
     - 模拟信号：容易受到噪声影响，信号质量可能变差。
     - 数字信号：不容易受干扰，传输更稳定。
  3. **应用**：
     - 模拟信号：常见于传统的收音机、老式电话。
     - 数字信号：广泛用于计算机、手机、互联网等现代技术。

  - 简单来说，模拟信号更像自然的连续波动，而数字信号是断断续续的、精准的“0”和“1”状态。

### 数据编码

### **数据传输与基带传输**

- **频带传输：**指利用模拟信道通过调制解调器传输模拟信号的方法
- **基带传输：**指利用数字信道`直接传输数字信号的方法`

![image-20241010171600440](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010171600440.png?raw=true)

![image-20241010172723514](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010172723514.png?raw=true)

### 脉冲编码调制PCM

- 将模拟信号转换为数字信号

  ![image-20241010172901940](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010172901940.png?raw=true)

  ![image-20241010173100015](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241010173100015.png?raw=true)


## 交换技术

- **定义**：按某种方式动态的分配传输线路资源
- **原因：**节省线路投资，提高线路利用率
- **分类：**电路交换、报文交换、分组交换

### 电路交换

**三个阶段**

- 建立连接
  - 建立一条专用的物理通路（占用通信资源）
- 通话
  - 主叫和被叫双方互相电话(一直暂用通信资源)
- 释放连接
  - 释放刚才使用的专用物理通路(归还通信资源)

### 分组交换

- **采用存储转发技术**

  - ![image-20241011093534391](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011093534391.png?raw=true)

  - 数据段前面添加首部就构成了分组(Packet)

    ![image-20241011093705145](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011093705145.png?raw=true)

- 互联网采用分组交换技术。分组是在互联网中传送的数据单元。
- 发送端依次把各分组发送到接收端。

### 报文交换

- 电报通信就采用了基于存储转发原理的报文交换
- 但报文交换的时延较长，从几分钟到几小时不等
- 现在报文交换已经很少有人使用了。
  - ![image-20241011094444211](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011094444211.png?raw=true)

# 数据链路层

- **设计的目的：**
  - 为网络层提供涉及良好的服务接口
  - 实现在相邻网络实体之间建立、维持和释放数据链路连接
  - 传输数据链路服务数据单元。
- **数据链路与物理路**
  - 链路(Link)：
    - 一条链路只是一条通路的一个组成部分。
- 数据链路(data Link)
  - 控制数据传输的协议的硬件和软件加到链路上，就构成了数据链路或逻辑链路
  - 典型实现：适配器（网卡）

![image-20241011104728566](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011104728566.png?raw=true)

## CRC冗余码

![image-20241011112225653](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011112225653.png?raw=true)

![image-20241011112234326](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011112234326.png?raw=true)

## PPP协议

- 对于点对点的链路，目前使用最广泛的数据链路路层协议是`点对点协议PPP`
- PPP协议在1994成立互联网的正式标准【RFC 1661，STD51】。

![image-20241011144557797](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011144557797.png?raw=tr)

### 协议组成

- 将IP数据报封装到串行链路的方法
- 一个`链路控制协议LCP`
- 一套`网络控制协议NCP`

![image-20241011150025368](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011150025368.png?raw=true)

# 局域网

## 局域网概述

- **总线型**：所有节点都能直接连接到共享信道
  - ![image-20241011150456316](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011150456316.png?raw=true)
- **星型**：所有节点都链接到中央节点
  - ![image-20241011150520075](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011150520075.png?raw=true)
- **环型**：节点通过点到点链路与相邻节点连接
  - ![image-20241011150621626](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011150621626.png?raw=true)

![image-20241011151025934](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011151025934.png?raw=true)

### 局域网的网络层和高层

- **IEEE 802标准没有定义网络层和更高层**
  - 没有路由选择功能
    - 局域网拓扑结构比较简单，一般不需中间转接
  - 流量控制、寻址、排序、差错控制等功能有数据链层完成
- 网络层和更高层通常由协议软件（如TCP/IP协议）、IPX/SPX协议）和网络操作系统来实现。

## 以太网

![image-20241011152031678](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011152031678.png?raw=true)

### 以太网连接方式

![image-20241011155713337](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011155713337.png?raw=true)

![image-20241011155906122](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011155906122.png?raw=true)

![image-20241011160114803](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011160114803.png?raw=true)



### MAC地址

- 又称`物理地址`，他是网络站点的全球唯一的标识符，与其他物理位置无关。
  - 注意：MAC地址是在数据链路程进行处理，而不是在物理层
- 网络站点的每一个网络接口都有一个MAC地址。

#### MAC三种类型：

- 单播地址
  - 拥有单播地址的帧将发送给网络中唯一一个由单播地址指定的站点。——`点对多点传输`
- 多播地址
  - 拥有多播地址的帧将发送给网络中由组播地址指定的一组攒点。 ——点对多点传输
- 广播地址
  - 拥有广播地址的帧将发送给网络中所有的站点 ——广播传输

## 扩展局域网

### 网桥内部转发表

![image-20241011163240014](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011163240014.png?raw=true)

### 网桥宅转发表中登记

- 站地址：登记收到的帧的`源MAC地址`
- 端口：登记收到的帧进入该网桥的端口号
- 时间：登记收到的帧进入该网桥的时间。

### 以太网交换机的特点

![image-20241011165257539](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011165257539.png?raw=true)

### 以太网交换机互连

![image-20241011171340782](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241011171340782.png?raw=true)

### VLAN划分的方法

- **基于端口(静态划分)**
  - 根据端口号划分VLAN
- **根据MAC地址(动态划分)**
  - 根据用户计算机的MAC地址划分VLAN
- **基于网络地址或网络协议类型(动态)**
  - 根据用户计算机的IP地址划分VLAN

![image-20241012103149155](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012103149155.png?raw=true)

# 网络层

![image-20241012154929412](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012154929412.png?raw=true)

## 网络层的两种服务

- 网络层要设计得尽量简单，向其上层只提供简单灵活的、无连接的，尽量最大努力交付的数据报服务。
- 网络在发送分组时不需要先建立连接
- 网络层不提供服务质量的承诺。即所传送的分组可能出错、丢失、重复和失序，也不保证分组传送的时限。

## 路由器

- **路由器的主要工作**：转发分组
  - 把从某个输入端口收到的分组，按照分组要去的目的地(即目的网络)，把该分组从路由器的某个合适的输出端口转发给吓一跳路由器。

- **路由选择**：
  - 功能：将分组从源节结点`经选定的路由`传输到目的结点。
  - 理想路由算法：负责确定所收到的分组应传送的线路。
  - 路由表
    - ![image-20241012163244184](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012163244184.png?raw=true)
    - ![image-20241012163321734](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012163321734.png?raw=true)

## ARP和RARP协议

- 地址解析解析

  - 将IP地址解析为MAC地址
  - 在实际网络的链路上传送数据帧时，最终还是必须使用硬件地址。
  - 每个主机都没有一个 ARP 高速缓存（ARP cache），里面有所在的局域网上的各主机和路由器的IP 地址到硬件地址的映射表。

- ARP高速缓存（ARP cache）

  - 存放IP 地址到MAC地址映射表。

  - 映射表动态更新

    ![image-20241012172018504](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012172018504.png?raw=true)

### ARP工作

![image-20241012172156835](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012172156835.png?raw=true)

![image-20241012173039659](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012173039659.png?raw=true)

### 不在同一局域网

![image-20241012173253005](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241012173253005.png?raw=true)

## ICMP报文类型

- ![image-20241014095652660](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241014095652660.png?raw=true)

## 路由选择协议

### RIP内部网关协议

- 静态路由
  - 非自适应路由选择
  - 不能及时适应网络的变化
  - 简单，开销小
- 动态路由
  - 自适应路由选择
  - 能较好地适应网络状态的变化
  - 实现较为复杂，开销较大

**路由选择协议**

- 内部网关协议IGP
  - 在一个自治系统嫩使用的路由选择协议
  - 常用：RIP,OSPF
- 外部网关协议EGP
  - 在不同自治系统之间进行路由选择时使用的协议
  - 使用最多：BGP-4

#### RIP工作原理

- 路由信息协议，是一种分布式的、基于距离向量的路由选择协议
- 互联网的标准协议。
- 最大有点：简单
- 要求网络中的每台路由器都要维护从它自己到其他每个目的网络的距离记录。

#### RIP三个特点

- 仅和相邻路由器交换信息
- 交换的信息是当前本路由器所知道的全部信息，即自己的路由表
- 按固定时间间隔交换路由信息，例如，每隔30秒。当网络拓扑发生变化时，路由器也及时向相邻路由器通告拓扑变化后的路由信息。

### OSPF

**开发路径最短协议**

- 使用了DijKstra 提出的最短路径算法 SPF。
- 采用分布式的链路状态协议
- 现在使用OSPFv2.
- 采用洪泛法，向本自治系统中的所有路由器发送信息。
- 链路状态：说明本路由器都和那些路由器相邻

#### 工作过程

1. 确定领站可达。

- 相邻路由器每隔10秒钟要交换一次问候分组。
- 若有`40秒钟没有收到某个相邻路由器发来的问候分组，则可认为该相邻路由器是不可达的。

2. 同步链路状态数据库

- 同步：指不同路由器的链路状态数据库的内容是一样的
- 两个同步的路由器叫做完全邻接的路由器。

#### 外部网关协议BGP

协议BGP的主要特点

- 用于自治系统AS之间的选择
- 自治系统AS之间的罗友悬着必须是考虑有关策略。
- 采用了路径向量路由选择协议。

![image-20241014160642265](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241014160642265.png?raw=true)

#### eBGP和iBGP

![image-20241014160827725](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241014160827725.png?raw=true)

#### BGP路由信息

![image-20241014161535706](https://github.com/liuzhenhua1223/2024-10-image/blob/master//computernetworks/image-20241014161535706.png?raw=true)


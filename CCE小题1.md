# 题目二CCEV1

![image-20241230202250768](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230202250768.png?raw=true)

![image-20241230172332562](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230172332562.png?raw=true)

- **HCIE01-08/HCIE14-17是可以做CCE的远程环境账号**
  - 第一次公网远程lab.yutianedu.com:33333
  - 第二次公网3333里面在远程win10的环境，可以练习操作CCE题目

- **创建好的CCE集群**
  - 可以节约时间

- **个人租户申请CCE集群（可能会失败）**
  - 考前2周以外是1个CCE集群配额

  - 考前2周以内是2个CCE集群配额

- **申请VPC网段**
  - 练习环境可以自定义网段
  - `考试环境必须用参数表的网段`

![image-20241230202526116](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230202526116.png?raw=true)

## 一小题

### 创建CCE集群，命名为test

- 制作容器镜像创建必要的CCE集群(命名为test)、节点池几测试节点(节点密码设置成Huawei@1234)

![image-20250110155325690](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110155325690.png?raw=true)

创建资源

- 进入ManageOne OM 运维面

![image-20241230205223752](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205223752.png?raw=true)

![image-20241230205242768](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205242768.png?raw=true)

![image-20241230205640646](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205640646.png?raw=true)

![image-20241230205710428](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205710428.png?raw=true)

![image-20241230205905778](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205905778.png?raw=true)

- 从节点

![image-20241230210019263](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210019263.png?raw=true)

![image-20241230210034155](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210034155.png?raw=true)

#### 查看对等连接信息

**登录Ie_vdcadmin02查看**

![image-20241230210223167](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210223167.png?raw=true)

![image-20241230210121172](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210121172.png?raw=true)

![image-20241230212425935](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212425935.png?raw=true)

![image-20241230212456521](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212456521.png?raw=true)

![image-20241230212537058](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212537058.png?raw=true)

![image-20241230212608174](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212608174.png?raw=true)

- 住户Ie_vdcadmin04配置对等连接

![image-20241230212650823](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212650823.png?raw=true)

![image-20241230212743285](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212743285.png?raw=true)

- Ie_vdcadmin02接受对等连接的请求

![image-20241230212842873](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212842873.png?raw=true)

![image-20241230212850759](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230212850759.png?raw=true)

- Ie_vdcadmin02添加本端路由

![image-20241230213043617](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230213043617.png?raw=true)

- Ie_vdcadmin04添加本段路由

![image-20241230213123257](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230213123257.png?raw=true)

#### 从节点绑定弹性公网IP

![image-20241230214737581](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214737581.png?raw=true)

![image-20241230214744868](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214744868.png?raw=true)

![image-20241230214829306](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214829306.png?raw=true)

![image-20241230214843655](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214843655.png?raw=true)

![image-20241230214912200](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214912200.png?raw=true)

- cce自动创建的安全组放行ICMP

![image-20241230214945689](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214945689.png?raw=true)

#### 连接从节点

![image-20241230215015565](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215015565.png?raw=true)

![image-20241230215038067](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215038067.png?raw=true)

- 从节点测试到总部YUM源连通性

![image-20241230215103322](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215103322.png?raw=true)

![image-20241230215127415](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215127415.png?raw=true)

#### 从节点配置Yum源上传软件包

![image-20241230215225409](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215225409.png?raw=true)

![image-20241230215240025](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215240025.png?raw=true)

![image-20241230215250480](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215250480.png?raw=true)

### 创建的镜像能够支持后续的测试(编写dockerfile)

![image-20241230231041327](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231041327.png?raw=true)

![image-20241230231053871](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231053871.png?raw=true)

![image-20241230231107601](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231107601.png?raw=true)

- 上传镜像

![image-20241230231142125](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231142125.png?raw=true)

![image-20241230231202790](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231202790.png?raw=true)



![image-20241230231253491](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231253491.png?raw=true)

### 必须要在容器中解压solo的程序包和环境依赖包

![image-20250110160331801](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110160331801.png?raw=true)

![image-20241230231436737](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231436737.png?raw=true)

### 基于当前租户SWR中镜像创建

![image-20250110161149350](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110161149350.png?raw=true)

![image-20250110161209417](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110161209417.png?raw=true)

### 使用Dockerfile创建

### 制作的镜像上传SWR后大小不超过500M

![image-20250110160453697](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110160453697.png?raw=true)

![image-20241230231323660](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231323660.png?raw=true)

![image-20241230231456009](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231456009.png?raw=true)

![image-20241230231522836](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231522836.png?raw=true)

![image-20241230231611277](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231611277.png?raw=true)

![image-20241230231631751](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231631751.png?raw=true)

![image-20241230231644591](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231644591.png?raw=true)

![image-20241230231723659](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231723659.png?raw=true)

![image-20241230231734074](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231734074.png?raw=true)

### Dockerfile的行数不超过10行

![image-20241230231323660](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231323660.png?raw=true)

### 下载Dockerfile保存到桌面文件夹

- 文件夹 HCIE-Cloud-Design中，命名为2.2-Dockerfile

![image-20241230231824687](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231824687.png?raw=true)

![image-20241230231807877](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231807877.png?raw=true)

## 小题二

![image-20241231112209895](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231112209895.png?raw=true)

### 新建CCE集群solo，安装插件

- 插件就按照默认的两个就行

![image-20241231110557294](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110557294.png?raw=true)

- 绑定公网IP

![image-20241231110656742](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110656742.png?raw=true)

![image-20241231110713419](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110713419.png?raw=true)

### 创建工作负载solo  3副本

![image-20241231110809935](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110809935.png?raw=true)

![image-20241231110829263](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110829263.png?raw=true)

- 选择使用的镜像

![image-20241231111014121](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111014121.png?raw=true)



### 设置资源限制

![image-20241231111105093](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111105093.png?raw=true)

![image-20241231111147778](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111147778.png?raw=true)

![image-20241231111240956](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111240956.png?raw=true)

![image-20241231111322590](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111322590.png?raw=true)

![image-20241231111428667](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111428667.png?raw=true)

### 业务启动前检查

![image-20241231111458331](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111458331.png?raw=true)

![image-20241231111657627](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111657627.png?raw=true)

![image-20250116172442699](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250116172442699.png?raw=true)

![image-20241231111728358](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111728358.png?raw=true)

![image-20241231111741165](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111741165.png?raw=true)

![image-20241231111754049](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111754049.png?raw=true)

![image-20241231111806523](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111806523.png?raw=true)

### 合理配置容器健康检查

#### 容器在6秒内完成启动，否则杀死对应容器

#### 如果发现业务1秒后无响应，访问流量将不会传至该容器，3秒内如果恢复响应，访问流量将继续发至该容器

#### 如果发现业务3秒后无响应，杀死对应容器，并进行重启

![image-20250116173816343](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250116173816343.png?raw=true)

### 合理配置Service和Ingress

![image-20241231113227818](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113227818.png?raw=true)

![image-20241231113359720](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113359720.png?raw=true)

![image-20241231113429974](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113429974.png?raw=true)



![image-20241231113437189](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113437189.png?raw=true)

![image-20241231113445838](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113445838.png?raw=true)

![image-20241231113453035](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113453035.png?raw=true)

## 小题三

![image-20250110170241217](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250110170241217.png?raw=true)

### 保留镜像solo:1.0，并基于solo：1.0创建solo:2.0

#### 编写Dockerfile

- 基于solo1.0的Dockerfile进行编写

![image-20241231152157931](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152157931.png?raw=true)

![image-20241231152146483](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152146483.png?raw=true)

![image-20241231152234041](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152234041.png?raw=true)

![image-20241231152320933](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152320933.png?raw=true?raw=true)

![image-20241231152624867](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152624867.png?raw=true)

![image-20241231152648226](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152648226.png?raw=true)

![image-20241231152718026](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152718026.png?raw=true)

![image-20241231152752705](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152752705.png?raw=true)

![image-20241231152835076](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231152835076.png?raw=true)





### 使用PV/PVC将路由为99.0.0.100/home/nfs的创建为持久存储，并挂载给工作负载

#### 创建云硬盘存储卷

![image-20241231154000801](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154000801.png?raw=true)

![image-20241231153039107](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153039107.png?raw=true)

![image-20241231153057317](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153057317.png?raw=true)

![image-20241231153113275](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153113275.png?raw=true)

![image-20241231153131932](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153131932.png?raw=true)

![image-20241231153138677](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153138677.png?raw=true)

![image-20241231153147232](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153147232.png?raw=true)

### 创建新的工作负载，命名为solo-2，并能正常访问测试页面

![image-20241231153218519](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153218519.png?raw=true)

![image-20241231153249673](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153249673.png?raw=true)

![image-20241231153307478](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153307478.png?raw=true)

![image-20241231154145928](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154145928.png?raw=true)

![image-20241231153624397](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231153624397.png?raw=true)

![image-20241231154242360](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154242360.png?raw=true)

![image-20241231154304780](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154304780.png?raw=true)

![image-20241231154323264](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154323264.png?raw=true)

![image-20241231154403928](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154403928.png?raw=true)

![image-20241231154609627](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154609627.png?raw=true)

![image-20241231154759379](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154759379.png?raw=true)

![image-20241231154908699](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154908699.png?raw=true)

![image-20241231154927521](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154927521.png?raw=true)

![image-20241231154952838](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231154952838.png?raw=true)

![image-20250117105241051](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250117105241051.png?raw=true)
![image-20241231155017075](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155017075.png?raw=true)

![image-20241231155158432](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155158432.png?raw=true)

![image-20241231155237278](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155237278.png?raw=true)

![image-20241231155314519](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155314519.png?raw=true)

![image-20250117104721723](https://github.com/liuzhenhua1223/2024-12-image/blob/master/computernetworks/image-20250117104721723.png?raw=true)

![image-20241231155457111](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155457111.png?raw=true)
![image-20241231155444042](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155444042.png?raw=true)

![image-20241231155447328](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155447328.png?raw=true)

![image-20241231155609291](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155609291.png?raw=true)

![image-20241231160147457](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160147457.png?raw=ture)
![image-20241231160136363](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160136363.png?raw=true)

![image-20241231160205882](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160205882.png?raw=true)

![image-20241231160221858](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160221858.png?raw=true)

![image-20241231160233221](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160233221.png?raw=true)

![image-20241231160250446](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160250446.png?raw=true)

![image-20241231160336609](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160336609.png?raw=true)

![image-20241231160343241](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160343241.png?raw=true)

![image-20241231160402429](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231160402429.png?raw=true)

---

**注意**：`应用运行环境依赖包已经存放在持久化存储中`

---

**请按照以下要求完成运行配置文件的创建**

#### 创建ConfigMaps,通过其配置JAVA所设计环境变量

#### 创建Secret，通过其配置Mysql登录密码

**请按照一下要求完成节点负载的调度配置**

1. 新增一个包含8U16G节点的节点池（节点密码设置为Huawei@1234），并使用工作负载尽可能的调度到该节点。
2. 配置节点伸缩策略，当CPU资源占用超过85%或者内存资源占用超过80%是，自动增加一个节点。

![image-20241231172815319](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172815319.png?raw=true)

![image-20241231172943841](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172943841.png?raw=true)

![image-20241231172948768](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172948768.png?raw=true)

![image-20241231173047979](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173047979.png?raw=true)

![image-20241231173059585](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173059585.png?raw=true)

![image-20241231173118089](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173118089.png?raw=true)

![image-20241231173157159](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173157159.png?raw=true)

![image-20241231173201695](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173201695.png?raw=true)

![image-20241231173222939](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173222939.png?raw=true)

![image-20241231173226535](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173226535.png?raw=true)

![image-20241231173230702](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173230702.png?raw=true)

![image-20250102095805547](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095805547.png?raw=true)

![image-20250102095822150](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095822150.png?raw=true)

![image-20250102095832590](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095832590.png?raw=true)

![image-20250102095847758](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095847758.png?raw=true)

![image-20250102095859112](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095859112.png?raw=true)

![image-20250102095950818](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095950818.png?raw=true)

![image-20250102095954443](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102095954443.png?raw=true)

![image-20250102100000512](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100000512.png?raw=true)

![image-20250102100006752](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100006752.png?raw=true)

![image-20250102100011228](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100011228.png?raw=true)

![image-20250102100043401](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100043401.png?raw=true)

![image-20250102100049441](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100049441.png?raw=true)

![image-20250102100105808](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100105808.png?raw=true)

![image-20250102100108579](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102100108579.png?raw=true)


# HCIE备考

## 环境说明：

- **备考六周**
  - 前两周
  - 中两周
  - 后两周

>- 新进群的小伙伴请先备注，备注格式：考试地点--姓名--考试日期，注意事项：将群公告和资料都仔细看一遍，所有的重要信息都在公告中（包括实验环境）
>
>
>
>- 新进群的同学，如果没有个人HCS租户，将无法练习实验，进群之后主动找辅导老师申请HCS个人租户，默认个人租户登录名：为姓名全拼，默认密码：Yutian12#$
>
>
>
>- 因为本地环境的远程登录账号由于操作不当可能会出现黑屏的情况，当黑屏无法登录的时候，可以临时使用HCIETEST01/HCIETEST02/HCIETEST03密码HCIE@30000进行远程登录查看在线登录用户
>
>
>
>- 截图要求关键步骤，关键结果 截图命名格式“大题.小题-XX”，迁移题目为例2.1-01,2.1-02,2.1-03……
>
>
>
>- 1. WAF实例已经在WAF01/WAF02/WAF03/WAF04租户创建好了，不要删掉实例了，可能过几天就无法再创建实例了，直接使用已经存在的实例即可。 
>
>- 2. 因为CCE申请可能会概率失败，可以使用HCIE01--HCIE17登陆密码Huawei12#$%，该租户已经创建CCE控制集群，请不要删掉该控制集群，否则可能过几天无法再创建集群了。为了节省创建时间，避免创建失败浪费时间，推荐可以直接使用里面创建好的CCE集群，用完清理掉自己的操作部分即可，不要删掉控制集群。在个人租户申请CCE集群也可以，可能会创建失败浪费时间，如何选择，自行决定啦。
>
>  
>
>- 对于HCS环境的bss_admin权限账号，可在考前2周时间找辅导老师申请，在没有bss_admin权限的情况下，无法创建租户，分配外部网络和专线接入点，修改配额等操作，不能操作的部分可以跳过，等拿到超管账号再操作即可
>
>  



>- 以下网段为私有云HCS系统网段，创建虚拟私有云VPC和外部网络时禁止使用，防止和系统网段冲突，影响环境正常使用。10.200.4.0 ，10.200.7.0 ，10.200.15.0 ，10.64.0.0 ，10.72.10.0 ，172.28.0.0 ，192.168.5.0 ，192.168.6.0 ，192.168.10.0 ，192.168.20.0 ，192.168.29.0 ，192.168.30.0 ，192.168.31.0 ，192.168.66.0 ，192.168.67.0 ，192.168.68.0 ，192.168.100.0。
>
>
>
>- 考试技巧：实际参加考试需要调整好心态，考试过程中，如果遇到报错，在30分钟之内无法解决，可以考虑先做其他能做的题目，转换思路然后在回去排错，在规划题更新优化之后，操作题的容错空间大了一些，部分题目做不出来，依然是有机会通过考试的，但是整个大题都不做，那分数不够就无法通过考试了，这个情况大家灵活处理。
>
>
>
>- Windows远程桌面用户说明： 
>  - 地址：lab.yutianedu.com:33333 
>  - 密码：HCIE@30000 租户有CCE配额用户：HCIE01,HCIE02,HCIE03,HCIE04,HCIE05,HCIE06,HCIE07,HCIE08,HCIE14,HCIE15,HCIE16,HCIE17 
>  - 租户无CCE配额用户：HCIE09,HCIE11,HCIE12,HCIE13 
>  - 查看在线用户的用户：HCIETEST



> - 新人进群请主动填写该统计表，实验辅导以该统计表名单信息为准 【腾讯文档】2024年云计算考试名单统计表1 https://docs.qq.com/form/page/DR3ZFUEFrWEhkenNl
>
> 
>
> - 【腾讯文档】云计算LAB3.0实验环境安排表 https://docs.qq.com/sheet/DR09UTXR1Y0Zka0l6?tab=BB08J2
>
> 
>
> - 云计算HCIEV3.0软件包 链接：https://pan.baidu.com/s/1F9W_VwaMBil1LGfKvg5Nog 提取码：1234
>
> 
>
> - 考试资料申请流程： 请填写誉天学员考试资料申请表： http://bqg07wpxi37hd6p6.mikecrm.com/Gh7BmTz审核通过后，考试资料会在1-2个工作日发到大家填写的邮箱，请知悉～ 考试资料阅读系统地址：http://1.95.9.152，账号姓名 默认密码是123456 ，首次申请资料资料注意短信通知，后续不用重复申请相同的资料，系统会自动更新相关资料!
>
> 

## 前两周

- 私有云HCS811
  - 考前2周之外
    - 个人租户
      - 用于登录HCS环境进行练习的考试题目
  - 考前2周之内
    - 超管账号
      - 用户创建分布租户等相关操作
- windows远程桌面
  - 介入入口：lab.yutianedu.com:33333
    - 开始菜单
      - mstsc 
  - 登录用户
    - HCIE01-08/HCIE14-17
      - 全套考试题目实验环境 (需要安排)
    - HCIE09/1HCIE11-13
      - 初学者练习迁移800 (不需要安排)
      - 迁移8193和dbas
    - HCIECSD
      - 练习规划第五小题 (PC机器可以部署环境)
    - HCIETEST/HCIETEST-03
      - 查看远程用户HCIE09-13是否在线
      - 当HCIEOX账号黑屏，可以临时使用
- 时间观念
  - 合理安排练习环境
    - 预留清理环境的时间
- 环境安排表
  - 备考6周，每周安排4次4小时 (保底安排)
    - 2次4小时+1次8小时
    - 4次4小时
    - 2次8小时
  - 如果环境有空位，可以继续添加，这个不算次数
  - 0-8点的时间，不计算安排次数
  - 环境安排表更新时间
    - 每周三
      - 第一阶段-考前4周的同学
      - 第二阶段考前4周外的同学

# 题目一迁移

![9d89f042569a4133b813e621bd4e429f](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/9d89f042569a4133b813e621bd4e429f.jpeg?raw=true)

![image-20241229220852316](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229220852316.png?raw=true)

## 确定登录用户

- HCIE01-17都可以排队使用8103环境
- HCIE01-03不需要排队，可以直接使用迁移800环境
- HCIE14-17-使用迁移800可以在HCIE09-13选择空闲的账号使用

```apl
考前2周以外推荐使用HCIE09-13的环境练习迁移，把安排环境尽量练习CCE题目
通过HCIETEST用户查看有没有空闲用户可以登录
远程桌面推荐注销用户下线，而不是直接关闭窗口
```

## 版本一

### 第一小题

![image-20241228135027830](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241228135027830.png?raw=true)

#### 在HCS环境操作，不需要排队

- OC运维面
  - 迁移前准备资源：为目的ECS创建镜像、规格、外部网络
  - https://oc-yt.yutian.com:31943
  - 登录用户：admin/Huawei12#$%

![image-20241228135900119](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241228135900119.png?raw=true)

- 由于没有导入license所以需要点击这个界面进入系统。 

![image-20241228135955631](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241228135955631.png?raw=true)

- 考试时并没有提供OM，需要通过常用链接进入Service OM平面

![image-20241228142022026](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241228142022026.png?raw=true)

##### 注册镜像

![image-20241228142131313](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241228142131313.png?raw=true)

![image-20241229215917501](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229215917501.png?raw=true)

![image-20241229215935896](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229215935896.png?raw=true)

![image-20241229215954412](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229215954412.png?raw=true)

#### 进入KVM主机查看solo博客和mysql

![image-20241229221755369](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229221755369.png?raw=true)

![image-20241231092507656](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231092507656.png?raw=true)

![image-20241229221819404](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229221819404.png?raw=true)

##### 启动solo博客

![image-20241229222055893](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222055893.png?raw=true)

![image-20241229222114895](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222114895.png?raw=true)

- **启动solo应用**

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222157176.png?raw=true)

- **查看博客**

![image-20241229222310772](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222310772.png?raw=true)

#### 查看镜像资源

![image-20241229222425872](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222425872.png?raw=true)

#### 创建外部网路，子网

![image-20241230143625504](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230143625504.png?raw=true)

![image-20241230143635157](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230143635157.png?raw=true)



#### SC运营面

- 迁移前准备资源：申请迁移目的的ECS
- https://ytedu.extenal.com
- 登录用户：个人租户姓名全拼/默认密码：Yutian12#$

##### 有超管的账户

![image-20241230142649478](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230142649478.png?raw=true)

![image-20241230142719250](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230142719250.png?raw=true)

![image-20241230142749070](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230142749070.png?raw=true)

![image-20241230142816886](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230142816886.png?raw=true)

![image-20241230143650677](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230143650677.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230143650677.png?raw=true)

##### 没有超管的账户

![image-20241229223317296](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229223317296.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222425872.png?raw=true)

##### 第一次登录需要修改密码

![image-20241229222750720](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222750720.png?raw=true)

##### 创建VPC

![image-20241229222809979](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222809979.png?raw=true)

申请私有云——创建私网网段

![image-20241229222815108](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222815108.png?raw=true)

##### 创建子网

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229222819147.png?raw=true)

![image-20241229223216575](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229223216575.png?raw=true)

##### 创建安全组

![image-20241229224008791](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224008791.png?raw=true)

![image-20241229224026194](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224026194.png?raw=true)

##### 创建弹性云服务器

![image-20241229224114625](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224114625.png?raw=true)

![image-20241229224341388](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224341388.png?raw=true)

![image-20241229224259091](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224259091.png?raw=true)

![image-20241229224429557](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224429557.png?raw=true)

![image-20241229224451894](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241229224451894.png?raw=true)



### 第二小题

- 在迁移8103环境操作，需要排队申请 （大概1小时以内）前提，第一小题已经完成

#### Rainbow迁移

- 实施迁移任务
- 恢复Rainbo快照

![image-20241230153435488](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230153435488.png?raw=true)

![image-20241230153444760](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230153444760.png?raw=true)

- VNC验证

![image-20241230153537147](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230153537147.png?raw=true)

- 测试连通性

![image-20241230153653911](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230153653911.png?raw=true)

![image-20241230153707148](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230153707148.png?raw=true)

##### 配置迁移任务

![image-20241230154043757](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154043757.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154043757.png?raw=ture)

![image-20241230154116423](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154116423.png?raw=true)

![image-20241230154129029](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154129029.png?raw=true)

![image-20241230154155086](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154155086.png?raw=true)

![image-20241230154213205](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154213205.png?raw=true)

![image-20241230154300708](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154300708.png?raw=true)

![image-20241230154328476](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154328476.png?raw=true)

![image-20241230154402383](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154402383.png?raw=true)

##### 部署Agent

![image-20241230154441645](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154441645.png?raw=true)

![image-20241230154427606](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154427606.png?raw=true)

- 拷贝agent工具（推荐压缩）

![image-20241230154557432](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154557432.png?raw=true)

- 运行open_agent_directory

![image-20241230154628536](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154628536.png?raw=true)

粘贴到这里

![image-20241230154639580](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230154639580.png?raw=true)

##### 启动同步任务

![image-20241230155604417](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230155604417.png?raw=true)

### 第三小题

#### 安装Cloud Init

![image-20241230165124691](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230165124691.png?raw=true)

![image-20241230165605228](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230165605228.png?raw=true)

![image-20241230165733297](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230165733297.png?raw=true)

![image-20241230170108532](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230170108532.png?raw=true)



#### 安装Tools

![image-20241230170027992](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230170027992.png?raw=true)

![image-20241230170137153](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230170137153.png?raw=true)

### 第四小题

- 进入Mysql主机

![image-20241230171027580](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230171027580.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230171005110.png?raw=true)

![image-20241230170852545](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230170852545.png?raw=true)

![image-20241230170830506](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230170830506.png?raw=true)

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

## 创建资源

![image-20241230205223752](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205223752.png?raw=true)

![image-20241230205242768](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205242768.png?raw=true)

![image-20241230205640646](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205640646.png?raw=true)

![image-20241230205710428](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205710428.png?raw=true)

![image-20241230205905778](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230205905778.png?raw=true)

- 从节点

![image-20241230210019263](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210019263.png?raw=true)

![image-20241230210034155](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230210034155.png?raw=true)

### 查看对等连接信息

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

### 从节点绑定弹性公网IP

![image-20241230214737581](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214737581.png?raw=true)

![image-20241230214744868](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214744868.png?raw=true)

![image-20241230214829306](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214829306.png?raw=true)

![image-20241230214843655](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214843655.png?raw=true)

![image-20241230214912200](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214912200.png?raw=true)

- cce自动创建的安全组放行ICMP

![image-20241230214945689](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230214945689.png?raw=true)

### 连接从节点

![image-20241230215015565](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215015565.png?raw=true)

![image-20241230215038067](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215038067.png?raw=true)

- 从节点测试到总部YUM源连通性

![image-20241230215103322](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215103322.png?raw=true)

![image-20241230215127415](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215127415.png?raw=true)

### 从节点配置Yum源上传软件包

![image-20241230215225409](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215225409.png?raw=true)

![image-20241230215240025](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215240025.png?raw=true)

![image-20241230215250480](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230215250480.png?raw=true)

### 创建镜像仓库

![image-20241230231041327](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231041327.png?raw=true)

![image-20241230231053871](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231053871.png?raw=true)

![image-20241230231107601](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231107601.png?raw=true)

![image-20241230231142125](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231142125.png?raw=true)

![image-20241230231202790](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231202790.png?raw=true)

![image-20241230231253491](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231253491.png?raw=true)

- 编写dockerfile

![image-20241230231336286](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231336286.png?raw=true)

![image-20241230231323660](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231323660.png?raw=true)

![image-20241230231436737](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231436737.png?raw=true)

![image-20241230231456009](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231456009.png?raw=true)

![image-20241230231522836](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231522836.png?raw=true)

![image-20241230231611277](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231611277.png?raw=true)

![image-20241230231631751](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231631751.png?raw=true)

![image-20241230231644591](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231644591.png?raw=true)

![image-20241230231723659](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231723659.png?raw=true)

![image-20241230231734074](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231734074.png?raw=true)

![image-20241230231824687](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231824687.png?raw=true)

![image-20241230231807877](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241230231807877.png?raw=true)

## 小题三

![image-20241231112209895](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231112209895.png?raw=true)

### 新建CCE集群，安装插件

- 插件就按照默认的两个就行

![image-20241231110557294](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110557294.png?raw=true)

- 绑定公网IP

![image-20241231110656742](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110656742.png?raw=true)

![image-20241231110713419](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110713419.png?raw=true)

### 创建工作负载

![image-20241231110809935](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110809935.png?raw=true)

![image-20241231110829263](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231110829263.png?raw=true)

- 选择使用的镜像

![image-20241231111014121](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111014121.png?raw=true)



### 设置资源限制

![image-20241231111105093](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111105093.png)

![image-20241231111147778](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111147778.png?raw=true)

![image-20241231111240956](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111240956.png?raw=true)

![image-20241231111322590](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111322590.png?raw=true)

![image-20241231111428667](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111428667.png?raw=true)

### 业务启动前检查

![image-20241231111458331](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111458331.png?raw=true)

![image-20241231111657627](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111657627.png?raw=true)

![image-20241231111710869](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111710869.png?raw=true)

![image-20241231111728358](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111728358.png?raw=true)

![image-20241231111741165](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111741165.png?raw=true)

![image-20241231111754049](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111754049.png?raw=true)

![image-20241231111806523](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231111806523.png?raw=true)****

### 合理配置容器健康检查

#### 容器在6秒内完成启动，否则杀死对应容器

#### 如果发现业务1秒后无响应，访问流量将不会传至该容器，3秒内如果恢复响应，访问流量将继续发至该容器

#### 如果发现业务3秒后无响应，杀死对应容器，并进行重启

### 合理配置Service和Ingress

![image-20241231113227818](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113227818.png?raw=true)

![image-20241231113359720](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113359720.png?raw=true)

![image-20241231113429974](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113429974.png?raw=true)

![image-20241231113437189](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113437189.png?raw=true)

![image-20241231113445838](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113445838.png?raw=true)

![image-20241231113453035](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231113453035.png?raw=true)

## 小题四

### 基于solo1.0创建solo2.0，后续基于solo2.0进行

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

![image-20241231155017075](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155017075.png?raw=true)

![image-20241231155158432](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155158432.png?raw=true)

![image-20241231155237278](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155237278.png?raw=true)

![image-20241231155314519](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155314519.png?raw=true)

![image-20241231155433098](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231155433098.png?raw=true)

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

1. **创建ConfigMaps,通过其配置JAVA所设计环境变量**
2. **创建Secret，通过其配置Mysql登录密码**

**请按照一下要求完成节点负载的调度配置**

1. 新增一个包含8U16G节点的节点池（节点密码设置为Huawei@1234），并使用工作负载尽可能的调度到该节点。
2. 配置节点伸缩策略，当CPU资源占用超过85%或者内存资源占用超过80%是，自动增加一个节点。

![image-20241231172815319](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172815319.png?raw=true)

![image-20241231172943841](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172943841.png?rraw=true)

![image-20241231172948768](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231172948768.png?rraw=true)

![image-20241231173047979](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173047979.png?raw=true)

![image-20241231173059585](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173059585.png?raw=true)

![image-20241231173118089](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20241231173118089.png?ra=true)

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

# 题目三CCEv2

![image-20250102110601750](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110601750.png?raw=true)

## 配置云连接

![image-20250102110808833](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110808833.png?raw=true)

![image-20250102110816832](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110816832.png?raw=true)

![image-20250102110822961](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110822961.png?raw=true)

![image-20250102110851267](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110851267.png?raw=true)

![image-20250102110927586](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110927586.png?raw=true)

![image-20250102110940041](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110940041.png?raw=true)

![image-20250102110950455](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102110950455.png?raw=true)

![image-20250102111046110](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102111046110.png?raw=true)

![image-20250102111219984](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102111219984.png?raw=true)

![image-20250102111227571](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102111227571.png?raw=true)

![image-20250102111249010](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102111249010.png?raw=true)

![image-20250102111342669](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102111342669.png?raw=true)

##  一小题：CCE集群信息

![image-20250102154520903](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154520903.png?raw=true)

![image-20250102154552708](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154552708.png?raw=true)

![image-20250102154745704](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154745704.png?raw=true)

![image-20250102154802202](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154802202.png?raw=true)

![image-20250102154812122](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154812122.png?raw=true)

![image-20250102154919928](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154919928.png?raw=true)

![image-20250102154947562](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154947562.png?raw=true)

![image-20250102155021025](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155021025.png?raw=true)

![image-20250102155042765](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155042765.png?raw=true)

![image-20250102155102946](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155102946.png?raw=true)

![image-20250102155516253](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155516253.png?raw=true)

![image-20250102155545585](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155545585.png?raw=true)

![image-20250102155600972](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155600972.png?raw=true)

![image-20250102155636144](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102155636144.png?raw=)

![image-20250102162028094](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102162028094.png?raw=true)

![image-20250102162237940](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102162237940.png?raw=true)

![image-20250102162432379](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102162432379.png?raw=true)



![image-20250102154235326](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102154235326.png?raw=true)

## 一小题：创建CCE，按照插件

![image-20250102171255947](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102171255947.png?raw=true)

![image-20250102171307133](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102171307133.png?raw=true)

![image-20250102171322278](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102171322278.png?raw=true)



## 二小题：创建命名空间solo，后续基于该命名空间

![image-20250102173145036](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173145036.png?raw=true)

![image-20250102173210066](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173210066.png?raw=true)

![image-20250102173229748](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173229748.png?raw=true)

![image-20250102173234753](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173234753.png?raw=true)

![image-20250102173256890](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173256890.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173420894.png?raw=true)

![image-20250102173530265](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173530265.png?raw=true)

![image-20250102173552397](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173552397.png?raw=true)

![image-20250102173622578](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173622578.png?raw=true)

![image-20250102173639046](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173639046.png?raw=true)

![image-20250102173723098](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173723098.png?raw=true)

![image-20250102173728781](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173728781.png?raw=true)

![image-20250102173732895](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173732895.png?raw=true)

![image-20250102173739322](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173739322.png?raw=true)

![image-20250102173824254](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173824254.png?raw=true)

![image-20250102173905945](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173905945.png?raw=true)

![image-20250102173924590](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173924590.png?raw=true)

![image-20250102173943992](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250102173943992.png?raw=true)



![image-20250103110705386](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110705386.png?raw=true)

![image-20250103110715461](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110715461.png?raw=true)

![image-20250103110722440](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110722440.png?raw=true)

![image-20250103110840701](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110840701.png?raw=true)

![image-20250103110859060](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110859060.png?raw=true)

![image-20250103110950964](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103110950964.png?raw=true)

![image-20250103111238411](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111238411.png?raw=true)

![image-20250103111244839](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111244839.png?raw=true)

![image-20250103111418761](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111418761.png?raw=true)

![image-20250103111424802](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111424802.png?raw=true)

​	

![image-20250103111505376](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111505376.png?raw=true)

![image-20250103111511397](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103111511397.png?raw=true)

## 四大题

![image-20250103143929906](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103143929906.png?raw=true)

![image-20250103153848612](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103153848612.png?raw=true)

![image-20250103153905158](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103153905158.png?raw=true)

![image-20250103153933672](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103153933672.png?raw=true)

![image-20250103153948283](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103153948283.png?raw=true)

![image-20250103154001648](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154001648.png?raw=true)

![image-20250103154017873](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154017873.png?raw=true)

![image-20250103154032841](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154032841.png?raw=true)

![image-20250103154037940](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154037940.png?raw=true)

![image-20250103154042786](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154042786.png?raw=true)

![image-20250103154107821](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154107821.png?raw=true)

![image-20250103154123782](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154123782.png?raw=true)

![image-20250103154154201](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154154201.png?raw=true)

![image-20250103154336787](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154336787.png?raw=true)

![image-20250103154342020](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154342020.png?raw=true)

![image-20250103154436241](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154436241.png?raw=true)



![image-20250103154556078](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154556078.png?raw=true)

![image-20250103154606590](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154606590.png?raw=true)

![image-20250103154810922](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154810922.png?raw=true)

![image-20250103154840611](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154840611.png?raw=true)

![image-20250103154905026](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103154905026.png?raw=true)

![](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155009024.png?raw=true)

![image-20250103155037859](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155037859.png?raw=true)

![image-20250103155120185](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155120185.png?raw=true)

![image-20250103155154729](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155154729.png?raw=true)

![image-20250103155644682](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155644682.png?raw=true)
![image-20250103155419812](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155419812.png?raw=true)

![image-20250103155507530](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155507530.png?raw=true)

![image-20250103155620305](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103155620305.png?raw=true)

![image-20250103161322815](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103161322815.png?raw=true)

![image-20250103161336246](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103161336246.png?raw=true)

![image-20250103161342734](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103161342734.png?raw=true)

![image-20250103161359527](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103161359527.png?raw=true)

![image-20250103162214894](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103162214894.png?raw=true)

![image-20250103162224154](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103162224154.png?raw=true)

![image-20250103164213570](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103164213570.png?raw=true)

![image-20250103164249289](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103164249289.png?raw=true)

![image-20250103164301675](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103164301675.png?raw=true)

![image-20250103164315789](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103164315789.png?raw=true)

![image-20250103173206934](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173206934.png?raw=true)

![image-20250103173214244](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173214244.png?raw=true)

![image-20250103173217695](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173217695.png?raw=true)

![image-20250103173220666](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173220666.png?raw=true)

![image-20250103173227688](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173227688.png?raw=true)

![image-20250103173231927](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173231927.png?raw=true)

![image-20250103173236403](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173236403.png?raw=true)

![image-20250103173240189](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173240189.png?raw=true)

![image-20250103173244005](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173244005.png?raw=true)

![image-20250103173248009](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173248009.png?raw=true)

![image-20250103173340400](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173340400.png?raw=true)

![image-20250103173345762](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173345762.png?raw=true)

![image-20250103173350732](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173350732.png?raw=true)

![image-20250103173354614](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173354614.png?raw=true)

![image-20250103173416179](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173416179.png?raw=true)

![image-20250103173420328](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173420328.png?raw=true)

- 创建节点池

![image-20250103173424319](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250103173424319.png?raw=true)

![image-20250106112256969](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112256969.png?raw=true)

![image-20250106112348108](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112348108.png?raw=true)

![image-20250106112457697](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112457697.png?raw=true)

![image-20250106112531161](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112531161.png?raw=true)

![image-20250106112605251](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112605251.png?raw=true)

![image-20250106112752870](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112752870.png?raw=true)

![image-20250106112819108](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112819108.png?raw=true)

![image-20250106112852660](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112852660.png?raw=true)

![image-20250106112914578](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106112914578.png?raw=true)

![image-20250106113047634](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113047634.png?raw=true)

![image-20250106113131641](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113131641.png?raw=true)

![image-20250106113206316](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113206316.png?raw=true)

![image-20250106113325207](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113325207.png?raw=true)

![image-20250106113440866](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113440866.png?raw=true)

![image-20250106113508915](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113508915.png?raw=true)

![image-20250106154908993](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106154908993.png?raw=true)

- 安装插件

![image-20250106113547435](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106113547435.png?raw=true)

![image-20250106150054104](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150054104.png?raw=true)

![image-20250106150120579](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150120579.png?raw=true)

![image-20250106150205588](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150205588.png?raw=true)

![image-20250106150224668](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150224668.png?raw=true)

![image-20250106150252837](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150252837.png?raw=true)

![image-20250106150316399](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150316399.png?raw=true)

![image-20250106150337896](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106150337896.png?raw=true)

![image-20250106155019180](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106155019180.png?raw=true)

![image-20250106155050189](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106155050189.png?raw=true)

![image-20250106155111786](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106155111786.png?raw=true)

![image-20250106155141440](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106155141440.png?raw=true)

# 题目四安全和规划

![image-20250106171705097](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106171705097.png?raw=true)

- 练习环境
  - 练习环境只有一套，大家需要排队使用，一次时间约一小时
  - 考前2周以外
    - 搭配DBAS02的租户来练习

  - 考前2周以内
    - 可以自己申请租户来练习该实验

  - 云专线网络规划
    - 在环境安排表有详细规划配置，需要按照规划的配置来使用，才能保证VPC网络互通

- **考试环境说明：**
  - **申请DBAS实例在总部用户**
    - 对应的PVC要看参数表使用，不能自定义使用
    - 申请云专线
      - 专线接入点已经创建并分配，直接使用
      - 物理专线
      - 虚拟网关
      - 虚拟接口
  - **Mysql的实例是迁移之后的ECS**
    - 对应的PVC要看参数表使用，不能自定义使用
    - 分支到总部的DC地址规划--local_cidrs网段是创建VPC的网段
    - 申请云专线
      - 专线接入点已经创建并分配，直接使用
        - OM界面申请接入点
        - SC界面使用超管账号分配专线接入点
      - 物理专线
      - 虚拟网关
      - 虚拟接口
  - 对Mysql主机安装代理，配置审核规则

![image-20250106172653341](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106172653341.png?raw=true)

![image-20250106221624833](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106221624833.png?raw=true)

- 创建VPC

![image-20250106221747686](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106221747686.png?raw=true)

- 创建Mysql ECS

![image-20250106221901467](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106221901467.png?raw=true)

![image-20250106221927317](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106221927317.png?raw=true)

![image-20250106221956444](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106221956444.png?raw=true)

- 配置安全组

![image-20250106222013681](../../../../liuzh/AppData/Roaming/Typora/typora-user-images/image-20250106222013681.png)

- 创建弹性IP

![image-20250106222034858](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222034858.png?raw=true)

![image-20250106222046966](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222046966.png?raw=true)

- Mysql-ECS绑定弹性公网IP

![image-20250106222103301](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222103301.png?raw=true)

- OC运维面创建专线接入

![image-20250106222425801](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222425801.png?raw=true)

![image-20250106222512773](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222512773.png?raw=true)

![image-20250106222813062](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222813062.png?raw=true)

![image-20250106222827386](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222827386.png?raw=true)

- 分配专线

![image-20250106222912518](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106222912518.png?raw=true)

![image-20250106222949259](../../../../liuzh/AppData/Roaming/Typora/typora-user-images/image-20250106222949259.png)

- 申请专线

![image-20250106223017732](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223017732.png?raw=true)

![image-20250106223029742](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223029742.png?raw=true)

![image-20250106223127144](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223127144.png?raw=true)

![image-20250106223202546](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223202546.png?raw=true)

![image-20250106223213224](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223213224.png?raw=true)

- SC运营面

![image-20250106223528671](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106223528671.png?raw=true)

![image-20250106230730696](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106230730696.png?raw=true)

![image-20250106230802787](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106230802787.png?raw=true)

![image-20250106230820891](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106230820891.png?raw=true)

![image-20250106230858290](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106230858290.png?raw=true)

![image-20250106230946484](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106230946484.png?raw=true)

![image-20250106231028953](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231028953.png?raw=true)

![image-20250106231107284](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231107284.png?raw=true)

![image-20250106231128219](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231128219.png?raw=true)

![image-20250106231204511](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231204511.png?raw=true)

![image-20250106231236521](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231236521.png?raw=true)

![image-20250106231251978](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231251978.png?raw=true)

![image-20250106231331973](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231331973.png?raw=true)

![image-20250106231358176](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231358176.png?raw=true)

![image-20250106231554995](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231554995.png?raw=true)

![image-20250106231634681](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231634681.png?raw=true)

![image-20250106231816660](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231816660.png?raw=true)

- 查看agent日志

![image-20250106231906059](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231906059.png?raw=true)

- 查看端口组

![image-20250106231925512](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106231925512.png?raw=true)

![image-20250106232006969](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232006969.png?raw=true)

![image-20250106232025430](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232025430.png?raw=true)

![image-20250106232038332](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232038332.png?raw=true)

![image-20250106232110325](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232110325.png?raw=true)

![image-20250106232122799](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232122799.png?raw=true)

![image-20250106232140629](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106232140629.png?raw=true)

- 软件包上传错误报错

![image-20250106233944525](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106233944525.png?raw=true)

![image-20250106233959859](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106233959859.png?raw=true)

- 安装agent错误，删除错误的agent,使用脚本uninstall.sh

![image-20250106234014520](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106234014520.png?raw=true)

![image-20250106234143193](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106234143193.png?raw=true)

![image-20250106234152138](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106234152138.png?raw=true)

![image-20250106234228462](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250106234228462.png?raw=true)

---

- 注意事项
  - 云专线的配置
    - 必须和规划好的网络对应上
  - 安装agent代理
    - 确保添加的agent的ID一致，有可能会出现用错ID的情况
  - 安全组，防火墙，网络ACL
    - 可能会造成网络不通，需要检查相关配置

---

- ie_vdcadmin04部署ECS运行solo

![image-20250107172526278](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172526278.png?raw=true)

![image-20250107172554404](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172554404.png?raw=true)

![image-20250107172608822](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172608822.png?raw=true)

![image-20250107172648969](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172648969.png?raw=true)

![image-20250107172724647](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172724647.png?raw=true)

![image-20250107172740772](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172740772.png?raw=true)

![image-20250107172834900](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107172834900.png?raw=true)

![image-20250107173008664](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173008664.png?raw=true)

![image-20250107173031219](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173031219.png?raw=true)

![image-20250107173042924](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173042924.png?raw=true)

![image-20250107173053326](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173053326.png?raw=true)

![image-20250107173101381](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173101381.png?raw=true)

![image-20250107173108944](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173108944.png?raw=true)

![image-20250107173129362](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173129362.png?raw=true)

![image-20250107173139185](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173139185.png?raw=true)

![image-20250107173148167](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173148167.png?raw=true)

![image-20250107173156729](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173156729.png?raw=true)

![image-20250107173210228](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173210228.png?raw=true)

![image-20250107173228880](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173228880.png?raw=true)

![image-20250107173237538](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173237538.png?raw=true)

![image-20250107173249107](https://github.com/liuzhenhua1223/2024-12-image/blob/master//computernetworks/image-20250107173249107.png?raw=true)


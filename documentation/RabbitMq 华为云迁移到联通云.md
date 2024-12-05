# RabbitMq 华为云迁移到联通云

## 创建元数据信息

RabbitMQ管理界面介绍

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70.png?raw=true)


connections：无论生产者还是消费者，都需要与RabbitMQ建立连接后才可以完成消息的生产和消费，在这里可以查看连接情况

channels：通道，建立连接后，会形成通道，消息的投递获取依赖通道。

Exchanges：交换机，用来实现消息的路由

Queues：队列，即消息队列，消息存放在队列中，等待消费，消费后被移除队列。

### **Overview模块**
服务节点:

![image-20240527093326708](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527093326708.png?raw=true)


Nodes项，显示的是RabbitMQ的服务节点,目前有一个本地节点，可以有多个服务节点（比如集群的时候）。

#### **端口**

这里一共有三个端口，其中5672是amqp协议的端口，15672是RabbitMQ的管理工具端口(这就是我们现在操作的)，25672是做集群的端口。

如果我们现在的Java程序要与RabbitMQ进行交互，需要和哪个端口交互呢？是5672。因为Java客户端需要与RabbitMQ服务进行数据交互，必须要遵循amqp协议协议，所以要走5672端口。

而15672是RabbitMQ的管理工具的端口，与服务无关，仅仅是管理工具运行的端口。

Export definitions为导出RabbitMQ的基本信息

Import definitions为导入RabbitMQ的基本信息

### **添加用户**


上面的Tags选项，其实是指定用户的角色，可选的有以下几个：

超级管理员(administrator)

可登陆管理控制台，可查看所有的信息，并且可以对用户，策略(policy)进行操作。

监控者(monitoring)

可登陆管理控制台，同时可以查看rabbitmq节点的相关信息(进程数，内存使用情况，磁盘使用情况等)

策略制定者(policymaker)

可登陆管理控制台, 同时可以对policy进行管理。但无法查看节点的相关信息(上图红框标识的部分)。

普通管理者(management)

仅可登陆管理控制台，无法看到节点信息，也无法对策略进行管理。

其他

无法登陆管理控制台，通常就是普通的生产者和消费者。


.

#### **创建虚拟主机（Virtual Hosts）**
为了让各个用户可以互不干扰的工作，RabbitMQ添加了虚拟主机（Virtual Hosts）的概念。其实就是一个独立的访问路径，不同用户使用不同路径，各自有自己的队列、交换机，互相不会影响。

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70-1709797731389-5.png?raw=true)


创建好虚拟主机，我们还要给用户添加访问权限：

点击添加好的虚拟主机：

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70-1709797738877-8.png?raw=true)

进入虚拟主机设置界面，给用户设置权限

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70-1709797746695-11.png?raw=true)

### **Connections选项**
在这里可以看客户端连接RabbitMQ服务的信息。目前尚未有客户端连接，所以上面看不到连接信息。

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70-1709797756707-14.png?raw=true)

### **Channels（通道）选项**
在这里可以看客户端连接RabbitMQ通道的信息。通道是建立在连接之上的，因为现在没有连接，所以也没有通道

![在这里插入图片描述](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTUxOTkx,size_16,color_FFFFFF,t_70-1709797766243-17.png?raw=true)

### **Exchanges（交换机）选项**
Exchanges选项有交换机的信息，并且可以通过Add a new exchange来添加交换机

![image-20240527093721725](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527093721725.png?raw=true)

添加exchange的属性说明：

Name: exchange的名称

Type：exchange的类型，可选值为direct, headers, topic, fanout

Durability：是否需要持久化, Durable表示持久化，即rabbitmq重启后exchange不会被清除，依旧存在

Auto Delete：是否自动删除，默认是No。

自动删除的触发条件是：当绑定到该exchange上的所有queue和exchange都已经解除绑定时，rabbitmq自动删除该exchange。

Internal：是否为rabbitmq内部使用，默认NO。如果是，客户端不能直接投递消息到此交换器，只能由rabbitmq自己向这个exchange投递消息，一般用于exchange到exchange的绑定。

Arguments：其他选项参数, 一般设置为 []，不需要。

下面是我在管理页面创建一个直连exchange，添加完就可以在exchange表格看到我们刚创建的exchange（exchange）。

![image-20240527093755676](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527093755676.png?raw=true)

### **Queues选项**
Queues选项有queue的信息，并且可以通过Add a new queue来添加queue

![image-20240527093816102](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527093816102.png?raw=true)


添加queue属性说明：

Name: queue的名称

Durability：Durable表示持久化，即rabbitmq重启后，不会清除该queue，保留queue

Auto delete: 是否自动删除，默认NO。

自动删除触发条件：当所有消费客户端连接断开后，会删除该消息队列。

例：

当Queue中的 autoDelete 属性被设置为true时，那么，当所有消息接收者宕机或者关闭连接后，消息队列则会删除，消息发送者一直发送消息，当消息接收者重新启动恢复正常后，会接收最新的消息，而宕机期间的消息则会丢失。

当Quere中的 autoDelete 属性被设置为false时，那么，当消息接收者宕机，关闭后，消息队列不会删除，消息发送者一直发送消息，当消息接收者重新启动恢复正常后，会接收包括宕机期间的消息。

Arguments：其他选项参数，如TTL，Auto expire等，在该选项下面有参数选择。

下面，我创建一个name为myqueue的消息队列，创建完成后，会在queue表格中看到

![image-20240527093855700](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527093855700.png?raw=true)

创建了exchange和queue之后，我们还需要将queue绑定到exchange。下面我将上面创建的myqueue绑定到exchange上，在queues页面，点击我们需要绑定的队列，进入到详情页，在Add binding to this queue中填入exchange名称和路由键。然后就可以在对应的exchange详情页的bingdings看到绑定信息

![image-20240527094033322](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527094033322.png?raw=true)

### **测试**

直接点击exchange.direct，在Publish message区域发送消息：

routing key:指定路由键，exchange.direct交换器根据路由键将消息转发到对应的队列中。

delivery mode:消息是否持久存储，non-persistent表示不持久，persistent表示持久化。

header：可以设置一些头信息进去

Properties：您可以在这里设置其他消息属性(最常见的情况是设置发送模式和标题)。

payload:消息体

![image-20240527094053611](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527094053611.png?raw=true)

发送消息后，在myQueue的消息队列中可以看到已经读到一条消息（ready为1）。点击queue的Get message获取信息后，就可以看到消息被消费了。

![image-20240527094114420](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527094114420.png?raw=true)

![image-20240527094121518](https://github.com/liuzhenhua1223/Image/blob/master//MongoImage/image-20240527094121518.png?raw=true)

## 导出元数据

1. 在Overview页签中，单机“Download broker definitions",导出元数据

- ![image-20240307145005162](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307145005162.png?raw=true)

2. 停止生产，等待消费完，然后删出原有队列

> 在Overview页签中，确认数据是否已经消费完。

- ![image-20240307145555618](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307145555618.png?raw=true)

> 等数据消费完后，删出原有队列

1. 在Queues页签，单机需要删出的队列名称，进入队列详细页面。

- ![image-20240307150011309](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150011309.png?raw=true)
- ![image-20240307150028931](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150028931.png?raw=true)

4. 在Overview中，上传导出的元数据

> 在Overview中，单机选择文件，选择已经导出的元数据，进行导入上传

![image-20240307150258379](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150258379.png?raw=true)

上传成功后显示如下信息。

![image-20240307150339133](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150339133.png?raw=true)

进行验证查看

![image-20240307150411362](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150411362.png?raw=true)

数据发送测试

![image-20240307150436977](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307150436977.png?raw=true)

# 联通云导入元数据

![image-20240307151634501](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307151634501.png?raw=true)

## 数据测试

![image-20240307151657822](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307151657822.png?raw=true)

![image-20240307151759405](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307151759405.png?raw=true)

![image-20240307151814760](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307151814760.png?raw=true)

![image-20240307151824300](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240307151824300.png?raw=true)


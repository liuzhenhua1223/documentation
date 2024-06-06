# 华为云 RDS Mysql迁移到联通云RDS Mysql

[TOC]

**测试华为云到联通云RDS**

## 华为云开通RDS Mysql

![image-20240304202756925](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304202756925.png?raw=true)

### 创建负载均衡ELB

![image-20240304204313456](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204313456.png?raw=true)

![image-20240304204437593](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204437593.png?raw=true)

### 添加监听器

![image-20240304204532494](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204532494.png?raw=true)

![image-20240304204551319](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204551319.png?raw=true)

![image-20240304204619608](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204619608.png?raw=true)

![image-20240304204750368](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204750368.png?raw=true)

### 测试连接

![image-20240304204842206](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304204842206.png?raw=true)

### 写入测试数据

![image-20240304205639123](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304205639123.png?raw=true)

# 联通云开通RDS Mysql(略)

![image-20240304205022710](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304205022710.png?raw=true)

# 部署CloundCanal

## 全新安装(Docker Linux/MacOS)

本文主要介绍如何在 Linux/MacOS 操作系统下安装 CloudCanal Docker 版。

Windows 操作系统请参考[全新安装(Docker Windows)](https://www.clougence.com/cc-doc/productOP/docker/install_windows)。

## 安装步骤[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#安装步骤)

### 硬件和系统准备[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#硬件和系统准备)

- 操作系统
  - CentOS/RHEL
  - Ubuntu
  - MacOS
- CPU架构
  - x86
  - arm64v8
  - [TIPS] 不支持 vmware、virtualbox 和 windows 的 linux 子系统
- 最低配置
  - 2 核cpu
  - 6GB 内存

### 环境准备[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#环境准备)

- 部署前请确保以下端口未被占用

  | 组件                  | 端口  | 用途                                     |
  | --------------------- | ----- | ---------------------------------------- |
  | cloudcanal-mysql      | 25000 | 元数据库 mysql 对外映射端口              |
  | cloudcanal-prometheus | 19090 | prometheuse 监控指标查询端口             |
  | cloudcanal-console    | 7007  | console 和 sidecar 通信端口              |
  | cloudcanal-console    | 8111  | console web控制台端口                    |
  | cloudcanal-sidecar    | 18787 | 任务 debug 端口（e.g.,自定义代码 debug） |

### 软件准备[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#软件准备)

- 安装 **Chrome 浏览器**

- 安装 **基础工具**

  ```shell
  ## centos / rhel
  sudo yum update
  sudo yum install -y yum-utils
  sudo yum install -y lsof
  sudo yum install -y bc
  sudo yum install -y p7zip p7zip-plugins 
  
  ## ubuntu
  sudo apt update
  sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  sudo apt-get install -y lsof
  sudo apt-get install -y bc
  sudo apt-get install -y p7zip-full
  
  ## MacOS
  ## download 7-zip from official website and install
  ```

  

### 安装包准备[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#安装包准备)

- 登录[官方网站](https://www.clougence.com/?src=cc-doc-install-linux)，点击**下载私有部署版**按钮，获取 **软件包下载连接** ![downloadtgz](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/download-5b9cc9f732280029f421359985b5bdcc.png?raw=true)

- 下载安装包

  ```shell
  wget -cO cloudcanal.7z "${软件包下载连接}"
  ```

  

- 解压安装包

  ```text
  7z x cloudcanal.7z -o./cloudcanal_home
  cd cloudcanal_home/install_on_docker
  ```

  

- 解压目录内容包括

  - 镜像

    - images 目录下四个 tar 结尾的压缩文件

  - docker 容器编排文件

    （位置：解压目录/install_on_docker/）

    - docker-compose.yml 文件

  - **脚本**（位置：解压目录/install_on_docker/）

  | 脚本                            | 用途                                                         |
  | ------------------------------- | ------------------------------------------------------------ |
  | ./install.sh                    | 全新安装 CloudCanal, 其中会调用 ./scripts/precheck_install.sh 做预检 |
  | ./upgrade.sh                    | 升级 CloudCanal, 清理相关内容后调用 install.sh 安装          |
  | ./uninstall.sh                  | 卸载 CloudCanal，包含停止容器、删除镜像、删除元数据库、删除相应的卷等操作 |
  | ./stop.sh                       | 停止 CloudCanal 相关容器运行                                 |
  | ./start.sh                      | 启动 CloudCanal 相关容器                                     |
  | ./restart.sh                    | 重启 CloudCanal 相关容器                                     |
  | ./install_one_node.sh           | 新部署一个同步节点, 具体参考高可用部署文档                   |
  | ./scripts/precheck_install.sh   | 预检脚本，检查依赖软件安装状况，端口占用状况等               |
  | ./scripts/initDB.sh             | 更新 CloudCanal 元数据库                                     |
  | ./support/install_xxx_docker.sh | 辅助安装 docker 和 docker-compose 脚本                       |
  | other                           | 其他辅助脚本                                                 |

### 运行环境准备[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#运行环境准备)

- 安装 docker 和 docker-compose,可参考 [官方文档](https://docs.docker.com/engine/install/) (版本 **17.x.x** 及以上)，也可直接使用安装包提供的脚本

  ```shell
  ## centos / rhel,进入 install_on_docker 目录
  sh ./support/install_centos_docker.sh
  
  ## ubuntu,进入 install_on_docker 目录
  bash ./support/install_ubuntu_docker.sh
  
  ## amazon linux,进入 install_on_docker 目录
  sh ./support/install_amazon_linux_docker.sh
   
  ## MacOS,参考[docker MacOS 安装文档](https://docs.docker.com/desktop/install/mac-install/)
  ```

  

- MacOS 系统请为 Docker 分配内存 ![f0f8aece-be13-44f6-be2b-d5fecd9a7b67-image.png?raw=true](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/Linux-MacOS-6ff839041e78cfd7808bac32c686ed79.png?raw=true)

### 安装 CloudCanal[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#安装-cloudcanal)

- 执行安装脚本

  ```shell
  ## centos / rhel / MacOS
  sh install.sh 
   
  ## ubuntu
  bash install.sh
  
  ## amazon linux
  sudo sh install.sh
  ```

  

- 出现如下标识即安装成功 ![7b00e562-cd45-4905-a626-1356503d8213-image.png?raw=true](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/Linux-MacOS2-25cc4883701969e19536726e3834efee.png?raw=true)

### 开始使用[](https://www.clougence.com/cc-doc/productOP/docker/install_linux_macos#开始使用)

- 使用浏览器登陆控制台

  ```shell
  http://{your deploy CloudCanal ip}:8111
  ```

  

- 试用账号登陆

  - 账号: **`test@clougence.com`**
  - 密码: **`clougence2021`**
  - 默认验证码: **777777**

# CloudCanal 启动迁移任务

## 源端注入数据源

![image-20240304210030426](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304210030426.png?raw=true)

## 目标端注入数据源

![image-20240304210704019](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304210704019.png?raw=true)

## 添加迁移任务

![image-20240304210856503](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304210856503.png?raw=true)

![image-20240304211011664](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211011664.png?raw=true)

![image-20240304211103137](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211103137.png?raw=true)

## 查看迁移结果

![image-20240304211342037](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211342037.png?raw=true)

## 数据迁移完毕

![image-20240304211415337](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211415337.png?raw=true)

## 查看数据

![image-20240304211547047](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211547047.png?raw=true)

![image-20240304211743248](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20240304211743248.png?raw=true)

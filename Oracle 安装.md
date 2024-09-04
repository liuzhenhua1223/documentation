# Oracle 安装

## 安装准备

### 配置YUM源

> 本次安装客户由于是centos6.8本版，需要使用旧的一些yum源
>
> ```apl
> [root@luzhougpsoracledata ~]# cat /etc/yum.repos.d/CentOS-Base.repo
> [base]
> name=CentOS-6.8 - Base
> baseurl=http://vault.centos.org/6.8/os/$basearch/
> enabled=1
> gpgcheck=1
> gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
> 
> [updates]
> name=CentOS-6.8 - Updates
> baseurl=http://vault.centos.org/6.8/updates/$basearch/
> enabled=1
> gpgcheck=1
> gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
> 
> [extras]
> name=CentOS-6.8 - Extras
> baseurl=http://vault.centos.org/6.8/extras/$basearch/
> enabled=1
> gpgcheck=1
> gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
> 
> [epel]
> name=Extra Packages for Enterprise Linux 6 - $basearch
> mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=epel-6&arch=$basearch&country=US
> failovermethod=priority
> enabled=1
> gpgcheck=0
> ```
>
> 7版本yum源
>
> ```apl
> [base]
> name=CentOS-$releasever - Base - mirrors.aliyun.com
> failovermethod=priority
> baseurl=http://mirrors.aliyun.com/centos/$releasever/os/$basearch/
>         http://mirrors.aliyuncs.com/centos/$releasever/os/$basearch/
>         http://mirrors.cloud.aliyuncs.com/centos/$releasever/os/$basearch/
> gpgcheck=1
> gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
> 
> #released updates
> [updates]
> name=CentOS-$releasever - Updates - mirrors.aliyun.com
> failovermethod=priority
> baseurl=http://mirrors.aliyun.com/centos/$releasever/updates/$basearch/
>         http://mirrors.aliyuncs.com/centos/$releasever/updates/$basearch/
>         http://mirrors.cloud.aliyuncs.com/centos/$releasever/updates/$basearch/
> gpgcheck=1
> gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
> 
> #additional packages that may be useful
> [extras]
> name=CentOS-$releasever - Extras - mirrors.aliyun.com
> failovermethod=priority
> baseurl=http://mirrors.aliyun.com/centos/$releasever/extras/$basearch/
>         http://mirrors.aliyuncs.com/centos/$releasever/extras/$basearch/
>         http://mirrors.cloud.aliyuncs.com/centos/$releasever/extras/$basearch/
> gpgcheck=1
> gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
> 
> #additional packages that extend functionality of existing packages
> [centosplus]
> name=CentOS-$releasever - Plus - mirrors.aliyun.com
> failovermethod=priority
> baseurl=http://mirrors.aliyun.com/centos/$releasever/centosplus/$basearch/
>         http://mirrors.aliyuncs.com/centos/$releasever/centosplus/$basearch/
>         http://mirrors.cloud.aliyuncs.com/centos/$releasever/centosplus/$basearch/
> gpgcheck=1
> enabled=0
> gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
> 
> #contrib - packages by Centos Users
> [contrib]
> name=CentOS-$releasever - Contrib - mirrors.aliyun.com
> failovermethod=priority
> baseurl=http://mirrors.aliyun.com/centos/$releasever/contrib/$basearch/
>         http://mirrors.aliyuncs.com/centos/$releasever/contrib/$basearch/
>         http://mirrors.cloud.aliyuncs.com/centos/$releasever/contrib/$basearch/
> gpgcheck=1
> enabled=0
> gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
> ```
>
> 

### 配置本地主机名称

```apl
[root@luzhougpsoracledata ~]# hostnamectl set-hostname oracle
[root@luzhougpsoracledata ~]# vim /etc/sysconfig/network-scripts/ifcfg-ens33
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=67ca1066-1e2e-4d84-9fad-512abe2f715b
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.71.140
PREFIX=24
GATEWAY=192.168.71.1
HOSTNAME=oracle

```

### 关闭防火墙

```apl
setenforce 0
systemctl stop firewalld
[root@luzhougpsoracledata ~]# cat /etc/selinux/config

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted disable firewalld
[root@luzhougpsoracledata ~]# cat /etc/selinux/config

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

### 创建oracle用户

```
[root@luzhougpsoracledata ~]# mkdir /soft
[root@luzhougpsoracledata ~]# mkdir /home/oracle
[root@luzhougpsoracledata ~]# groupadd oinstall
[root@luzhougpsoracledata ~]# groupadd dba
[root@luzhougpsoracledata ~]# groupadd oper
[root@luzhougpsoracledata ~]# useradd -g oinstall -G dba,oper oracle
[root@luzhougpsoracledata ~]# passwd oracle
qianyi12!
```

### 创建目录

```apl
mkdir /soft
chwon -R oracle /soft
chmod -R 755 /soft
```

### 增加sudoers用户

```apl
sudo vi /etc/sudoers
oracle ALL=(ALL)       NOPASSWD: ALL
```

```apl
id oracle
uid=500(oracle) gid=500(oinstall) groups=500(oinstall),501(dba)
```

### 修改limits.conf限制

```apl
[root@luzhougpsoracledata ~]# vim /etc/security/limits.conf
    oracle soft nproc 2047
    oracle hard nproc 16384
    oracle soft nofile 1024
    oracle hard nofile 65536

```

### 需要改/etc/pam.d/login

```apl
[root@luzhougpsoracledata ~]# vim /etc/pam.d/login
session required/lib64/security/pam_limits.so
```

### 修改bash_profile文件

```apl
[root@luzhougpsoracledata ~]# vim /etc/profile
# add by tim.man
if [ $USER = "oracle" ]; then
if [ $SHELL = "/bin/ksh" ]; then
   ulimit -p 16384
   ulimit -n 65536
else
   ulimit -u 16384 -n 65536
fi
fi


[oracle@oracle ~]$ cat .bash_profile
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs
export ORACLE_SID=lzgps
export ORACLE_BASE=/oracle
export ORACLE_HOME=/oracle/product/11.2
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib:/usr/local/lib
export DISPLAY=:0.0
export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
export LANG=C
PATH=$ORACLE_HOME/bin:/opt/bin:/bin:/usr/bin:/usr/local/bin:/usr/sbin:/usr/X11R6/bin:/usr/local/java/bin:$HOME/bin
export PATH
```

## 安装前

### 修改内核

```apl
[root@luzhougpsoracledata ~]# vim /etc/sysctl.conf
[root@luzhougpsoracledata ~]# sysctl -p
kernel.shmmax = 277495689510912
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048586
fs.file-max = 6815744
kernel.shmall = 4294967296
net.ipv4.tcp_max_tw_buckets = 6000
net.ipv4.ip_local_port_range = 9000 65500
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_tw_reuse = 1
#net.core.somaxconn = 262144
net.core.netdev_max_backlog = 262144
net.ipv4.tcp_max_orphans = 262144
net.ipv4.tcp_max_syn_backlog = 262144
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 1
net.ipv4.tcp_fin_timeout = 1
net.ipv4.tcp_keepalive_time = 30
net.ipv4.tcp_keepalive_probes = 6
net.ipv4.tcp_keepalive_intvl = 5
net.ipv4.tcp_timestamps = 0
fs.aio-max-nr = 1048576
```



### 创建目录

```apl
[root@luzhougpsoracledata ~]# mkdir /oracle
[root@luzhougpsoracledata ~]# chown oracle.dba /oracle -R
[root@luzhougpsoracledata ~]# mkdir /oraInventory
[root@luzhougpsoracledata ~]# mkdir /luzhougpsoracledata/
[root@luzhougpsoracledata ~]# chmod 755 /luzhougpsoracledata/
[root@luzhougpsoracledata ~]# chown oracle.dba /luzhougpsoracledata/
[oracle@oracle ~]$ sudo chown oracle.dba /oraInventory -R
```



### 配置yum源

```apl
yum -y install  binutils compat-libcap1  compat-libstdc++-33 compat-libstdc++-33*.i686 elfutils-libelf-devel gcc gcc-c++ glibc*.i686 glibc glibc-devel glibc-devel*.i686 ksh libgcc*.i686 libgcc libstdc++ libstdc++*.i686 libstdc++-devel libstdc++-devel*.i686 libaio libaio*.i686 libaio-devel libaio-devel*.i686 make sysstat unixODBC unixODBC*.i686 unixODBC-devel unixODBC-devel*.i686 libXp compat-libcap1-1.10 compat-libstdc++-33-3.2.3 libstdc++-devel-4.4.7 gcc-4.4.7 gcc-c++-4.4.7 ksh elfutils-libelf-devel.i686 0:0.164-2.el6 libaio-devel-0.3.107-10.el6.x86_64 binutils compat-libstdc+±33 elfutils-libelf elfutils-libelf-devel gcc gcc-c++ glibc glibc-common glibc-devel glibc-headers ksh libaio libaio-devel libgcc libstdc++ libstdc+±devel make sysstat unixODBC unixODBC-de 
```

### 配置X11

```apl
yum -y install X11*
vim /etc/ssh/sshd_config
	X11Forwarding yes
	X11DisplayOffset 10
yum -y install xclock*
yum -y install xorg-x11-utils
yum -y install unzip
sudo yum install xorg-x11-xauth
```

### 切换oracle用户

```apl
ssh -X oracle@192.168.71.140
	Warning: Permanently added '192.168.71.140' (ED25519) to the list of known hosts.
	oracle@192.168.71.140's password:

/usr/bin/xauth:  file /home/oracle/.Xauthority does not exist

[oracle@luzhougpsoracledata ~]$ export DISPLAY=:10.0
[oracle@oracle ~]$ xdpyinfo
name of display:    localhost:10.0
version number:    11.0
vendor string:    Moba/X
vendor release number:    12101012
maximum request size:  16777212 bytes
motion buffer size:  256
bitmap unit, bit order, padding:    32, LSBFirst, 32
image byte order:    LSBFirst
number of supported pixmap formats:    7
supported pixmap formats:
    depth 1, bits_per_pixel 1, scanline_pad 32
    depth 4, bits_per_pixel 8, scanline_pad 32
    depth 8, bits_per_pixel 8, scanline_pad 32
    depth 15, bits_per_pixel 16, scanline_pad 32
    depth 16, bits_per_pixel 16, scanline_pad 32
    depth 24, bits_per_pixel 32, scanline_pad 32
    depth 32, bits_per_pixel 32, scanline_pad 32
keycode range:    minimum 8, maximum 255
focus:  PointerRoot
number of extensions:    19
    BIG-REQUESTS
```

### 

### oracle用户配置

```apl
[oracle@oracle soft]$ ls
p13390677_112040_Linux-x86-64_1of7.zip  p13390677_112040_Linux-x86-64_2of7.zip
[oracle@oracle soft]$ unzip p13390677_112040_Linux-x86-64_1of7.zip
[oracle@oracle ~]$ sudo chown oracle.dba /soft/

```

### 解压

```apl
[oracle@oracle ~]$ ls /soft/
p13390677_112040_Linux-x86-64_1of7.zip  p13390677_112040_Linux-x86-64_2of7.zip
[oracle@oracle ~]$ cd /soft/
[oracle@oracle soft]$ unzip p13390677_112040_Linux-x86-64_1of7.zip
[oracle@oracle soft]$ unzip p13390677_112040_Linux-x86-64_2of7.zip
```

![image-20240719170727652](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240719170727652.png?raw=true)

![image-20240719170739775](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240719170739775.png?raw=true)

## 图形化安装Oracle

```apl
[oracle@oracle ~]$ ls
[oracle@oracle ~]$ cd
[oracle@oracle ~]$ pwd
/home/oracle
[oracle@oracle ~]$ cd /soft/database/
[oracle@oracle database]$ ls
install  readme.html  response  rpm  runInstaller  sshsetup  stage  welcome.html
```

![image-20240722230735977](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722230735977.png?raw=true)

![image-20240722230821288](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722230821288.png?raw=true)

![image-20240722230909375](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722230909375.png?raw=true)

### 如果创建数据库后续不需要dbca

![image-20240722231017487](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231017487.png?raw=true)

![image-20240722231042430](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231042430.png?raw=true)

![image-20240722231138993](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231138993.png?raw=true)

![image-20240722231203925](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231203925.png?raw=true)

![image-20240722231334266](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231334266.png?raw=true)

![image-20240722231615829](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231615829.png?raw=true)

![image-20240722231738308](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231738308.png?raw=true)

![image-20240722231952305](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722231952305.png?raw=true)

![image-20240722232154961](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722232154961.png?raw=true)

![image-20240722232241035](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722232241035.png?raw=true)

![image-20240722232420195](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722232420195.png?raw=true)

![image-20240722232644395](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722232644395.png?raw=true)

![image-20240722232739544](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722232739544.png?raw=true)

![image-20240722233047741](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722233047741.png?raw=true)

![image-20240722233126862](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722233126862.png?raw=true)

### 设置管理员密码

我是图省事，直接一个密码(1)

![image-20240722233340920](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722233340920.png?raw=true)

![image-20240722233411519](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722233411519.png?raw=true)

![image-20240722234340591](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722234340591.png?raw=true)



### 配置

```apl
wget http://mirror.yandex.ru/altlinux/p11/branch/x86_64/RPMS.classic/pdksh-5.2.14-alt5.x86_64.rpm
[root@luzhougpsoracledata ~]# rpm -ivh pdksh-5.2.14-alt5.x86_64.rpm --nodeps
警告：pdksh-5.2.14-alt5.x86_64.rpm: 头V4 RSA/SHA512 Signature, 密钥 ID da2773bb: NOKEY
准备中...                          ################################# [100%]
正在升级/安装...
   1:pdksh-1:5.2.14-alt5              ################################# [100%]

```

![image-20240722234535888](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722234535888.png?raw=true)

![image-20240722235433822](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240722235433822.png?raw=true)

![image-20240723000245264](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723000245264.png?raw=true)

```apl
[root@luzhougpsoracledata ~]# /oracle/product/11.2/bin/emca ss -anptlu | grep 15
[root@luzhougpsoracledata ~]# /oraInventory/orainstRoot.sh
Changing permissions of /oraInventory.
Adding read,write permissions for group.
Removing read,write,execute permissions for world.

Changing groupname of /oraInventory to oinstall.
The execution of the script is complete.
[root@luzhougpsoracledata ~]# /oracle/product/11.2/root.sh
Performing root user operation for Oracle 11g

The following environment variables are set as:
    ORACLE_OWNER= oracle
    ORACLE_HOME=  /oracle/product/11.2

Enter the full pathname of the local bin directory: [/usr/local/bin]:
   Copying dbhome to /usr/local/bin ...
   Copying oraenv to /usr/local/bin ...
   Copying coraenv to /usr/local/bin ...


Creating /etc/oratab file...
Entries will be added to the /etc/oratab file as needed by
Database Configuration Assistant when a database is created
Finished running generic part of root script.
Now product-specific root actions will be performed.
Finished product-specific root actions.
[root@luzhougpsoracledata ~]#

```

![image-20240723000335247](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723000335247.png?raw=true)

### netac

[oracle@luzhougpsoracledata ~]$ netca

Oracle Net Services Configuration:

![image-20240723093550908](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093550908.png?raw=true)

![image-20240723093556408](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093556408.png?raw=true)

![image-20240723093605607](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093605607.png?raw=true)

![image-20240723093717420](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093717420.png?raw=true)

![image-20240723093724794](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093724794.png?raw=true)

![image-20240723093741599](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093741599.png?raw=true)

![image-20240723093805348](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093805348.png?raw=true)

![image-20240723093812825](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093812825.png?raw=true)

![image-20240723093820884](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093820884.png?raw=true)

![image-20240723093833906](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093833906.png?raw=true)

![image-20240723093856937](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723093856937.png?raw=true)

### 安装dbca

![image-20240723094132260](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723094132260.png?raw=true)

![image-20240723094139318](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723094139318.png?raw=true)

![image-20240723094308484](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723094308484.png?raw=true)

![image-20240723095239700](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723095239700.png?raw=true)

![image-20240723100133317](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100133317.png?raw=true)

[oracle@oracle oradata]$ tail -1  /etc/oratab
#lzgps:/oracle/product/11.2:N

![image-20240723100234752](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100234752.png?raw=true)



### 设置密码：qianyi12!

![image-20240723100309691](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100309691.png?raw=true)

![image-20240723100329169](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100329169.png?raw=true)

![image-20240723100419058](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100419058.png?raw=true)

![image-20240723100548783](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100548783.png?raw=true)

**配置sga、pga，默认是40%，这里因为是专用的db服务器，可以调整到70%**

![image-20240723100636286](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723100636286.png?raw=true)

![image-20240723101056646](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723101056646.png?raw=true)

![image-20240723101153136](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723101153136.png?raw=true)

![image-20240723101241630](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723101241630.png?raw=true)

![image-20240723101418640](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723101418640.png?raw=true)

![image-20240723101444744](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Oracle/image-20240723101444744.png?raw=true)

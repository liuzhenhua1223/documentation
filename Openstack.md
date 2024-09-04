# Openstack基本操作

## 手动搭建流程

https://docs.openstack.org/install-guide/

##  发放云主机(命令行)

> 1、清空图形化中的所有memeda项目信息
>
> 2、配置keyston_memeda信息

```apl
[root@Openstack01 ~(keystone_memeda)]# cat keystonerc_memeda
unset OS_SERVICE_TOKEN
    export OS_USERNAME=memeda
    export OS_PASSWORD='redhat'
    export OS_REGION_NAME=RegionOne
    export OS_AUTH_URL=http://192.168.71.70:5000/v3
    export PS1='[\u@\h \W(keystone_memeda)]\$ '

export OS_PROJECT_NAME=promemeda
export OS_USER_DOMAIN_NAME=Default
export OS_PROJECT_DOMAIN_NAME=Default
export OS_IDENTITY_API_VERSION=3
```

### 1.1.1创建租户

```apl
[root@Openstack01 ~(keystone_admin)]# openstack project list
+----------------------------------+----------+
| ID                               | Name     |
+----------------------------------+----------+
| 65be68c4aad646b6b006b0332c796bfa | admin    |
| ac56c8c1bd794be78e04efb471b22d1a | services |
+----------------------------------+----------+
[root@Openstack01 ~(keystone_admin)]# openstack project create --help
usage: openstack project create [-h] [-f {json,shell,table,value,yaml}]
                                [-c COLUMN] [--noindent] [--prefix PREFIX]
                                [--max-width <integer>] [--fit-width]
                                [--print-empty] [--domain <domain>]
                                [--parent <project>]
                                [--description <description>]
                                [--enable | --disable]
                                [--property <key=value>] [--or-show]
                                [--immutable | --no-immutable] [--tag <tag>]
                                <project-name>

[root@Openstack01 ~(keystone_admin)]# openstack project create promemeda
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| domain_id   | default                          |
| enabled     | True                             |
| id          | 1c940c1b0da84f70aa3acf0f0d951fb5 |
| is_domain   | False                            |
| name        | promemeda                        |
| options     | {}                               |
| parent_id   | default                          |
| tags        | []                               |
+-------------+----------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack project list
+----------------------------------+-----------+
| ID                               | Name      |
+----------------------------------+-----------+
| 1c940c1b0da84f70aa3acf0f0d951fb5 | promemeda |
| 65be68c4aad646b6b006b0332c796bfa | admin     |
| ac56c8c1bd794be78e04efb471b22d1a | services  |
+----------------------------------+-----------+
```

### 1.1.2创建用户

```apl
[root@Openstack01 ~(keystone_admin)]# openstack user list
+----------------------------------+------------+
| ID                               | Name       |
+----------------------------------+------------+
| 773aa440724f4f819e56ca4f762d4ba6 | admin      |
| 0b314236018e416097fe984d0ee6960f | heat_admin |
| a07aece9dc41462e8bd6cdfa7c030ac8 | glance     |
| 57fb2d544ab2474c88caff2b3108f578 | cinder     |
| 12cb7199bbd14c8a938deb80c810257a | nova       |
| c39711fd2e7b48c2a58ac1a53a784dbd | placement  |
| 75175a09427e40af97ca4f11d1c0b8e4 | neutron    |
| 069bef01d66f481d8e393862f00e1449 | swift      |
| c4a1716253d14ca28c50b5c40a262c8b | heat       |
| 2118a703e2ae4a01b0501e080c6ed73a | heat-cfn   |
| 8c5644c9ec484cdbb2cd919c9f9a227f | gnocchi    |
| d221dc0badc54845afddaf49eff7c78b | ceilometer |
| 0a088296bdc440cda0d4db41e84a88a8 | aodh       |
+----------------------------------+------------+
[root@Openstack01 ~(keystone_admin)]# openstack user create --help
usage: openstack user create [-h] [-f {json,shell,table,value,yaml}]
                             [-c COLUMN] [--noindent] [--prefix PREFIX]
                             [--max-width <integer>] [--fit-width]
                             [--print-empty] [--domain <domain>]
                             [--project <project>]
                             [--project-domain <project-domain>]
                             [--password <password>] [--password-prompt]
                             [--email <email-address>]
                             [--description <description>]
                             [--ignore-lockout-failure-attempts]
                             [--no-ignore-lockout-failure-attempts]
                             [--ignore-password-expiry]
                             [--no-ignore-password-expiry]
                             [--ignore-change-password-upon-first-use]
                             [--no-ignore-change-password-upon-first-use]
                             [--enable-lock-password]
                             [--disable-lock-password]
                             [--enable-multi-factor-auth]
                             [--disable-multi-factor-auth]
                             [--multi-factor-auth-rule <rule>]
                             [--enable | --disable] [--or-show]
                             <name>
[root@Openstack01 ~(keystone_admin)]# openstack user create --password redhat --project promemeda memeda
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| default_project_id  | 1c940c1b0da84f70aa3acf0f0d951fb5 |
| domain_id           | default                          |
| enabled             | True                             |
| id                  | 97eab00287d64401bd39fc4bbb9b369e |
| name                | memeda                           |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
```

### 1.1.3 绑定用户项目角色

```apl
[root@Openstack01 ~(keystone_admin)]# openstack role list
+----------------------------------+------------------+
| ID                               | Name             |
+----------------------------------+------------------+
| 0c9e17806c3b4b54bea66616a72ebb11 | heat_stack_user  |
| 1d7239f1c4c04642bae78f327c0932a3 | SwiftOperator    |
| 1fa34a9e3d834f49ad7a78bec881e41a | ResellerAdmin    |
| 215dd170748142d5938e24564768e06a | _member_         |
| 40c759bd13a04738a909bb856aa0886d | heat_stack_owner |
| 6c13a021163e45888d9192e355d4b482 | admin            |
| dc658eb79d764b75ac22d953497e785c | member           |
| f1ec649070b246959c6775ab5a1eca11 | reader           |
+----------------------------------+------------------+
[root@Openstack01 ~(keystone_admin)]# openstack role add --help
usage: openstack role add [-h]
                          [--system <system> | --domain <domain> | --project <project>]
                          [--user <user> | --group <group>]
                          [--group-domain <group-domain>]
                          [--project-domain <project-domain>]
                          [--user-domain <user-domain>] [--inherited]
                          [--role-domain <role-domain>]
                          <role>
[root@Openstack01 ~(keystone_admin)]# openstack role add --project promemeda --user memeda _member_
```

### 1.1.4 创建规格

> 加载admin管理员环境变量进行操作。

```apl
[root@Openstack01 ~(keystone_admin)]# openstack flavor list
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| ID                                   | Name      |   RAM | Disk | Ephemeral | VCPUs | Is Public |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| 1                                    | m1.tiny   |   512 |    1 |         0 |     1 | True      |
| 2                                    | m1.small  |  2048 |   20 |         0 |     1 | True      |
| 3                                    | m1.medium |  4096 |   40 |         0 |     2 | True      |
| 4                                    | m1.large  |  8192 |   80 |         0 |     4 | True      |
| 5                                    | m1.xlarge | 16384 |  160 |         0 |     8 | True      |
| cd8fe79d-17c6-464a-97bb-09e28bd7ef6d | mg.2      |  1024 |    5 |         0 |     2 | True      |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
[root@Openstack01 ~(keystone_admin)]# openstack flavor create --help
usage: openstack flavor create [-h] [-f {json,shell,table,value,yaml}]
                               [-c COLUMN] [--noindent] [--prefix PREFIX]
                               [--max-width <integer>] [--fit-width]
                               [--print-empty] [--id <id>] [--ram <size-mb>]
                               [--disk <size-gb>] [--ephemeral <size-gb>]
                               [--swap <size-mb>] [--vcpus <vcpus>]
                               [--rxtx-factor <factor>] [--public | --private]
                               [--property <key=value>] [--project <project>]
                               [--description <description>]
                               [--project-domain <project-domain>]
                               <flavor-name>
[root@Openstack01 ~(keystone_admin)]# openstack flavor create x.small --disk 2 --ram 1024 --vcpus 1
+----------------------------+--------------------------------------+
| Field                      | Value                                |
+----------------------------+--------------------------------------+
| OS-FLV-DISABLED:disabled   | False                                |
| OS-FLV-EXT-DATA:ephemeral  | 0                                    |
| disk                       | 2                                    |
| id                         | 7e25178b-d0fe-4a0e-bd15-655e3a28472a |
| name                       | x.small                              |
| os-flavor-access:is_public | True                                 |
| properties                 |                                      |
| ram                        | 1024                                 |
| rxtx_factor                | 1.0                                  |
| swap                       |                                      |
| vcpus                      | 1                                    |
+----------------------------+--------------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack flavor list
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| ID                                   | Name      |   RAM | Disk | Ephemeral | VCPUs | Is Public |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| 1                                    | m1.tiny   |   512 |    1 |         0 |     1 | True      |
| 2                                    | m1.small  |  2048 |   20 |         0 |     1 | True      |
| 3                                    | m1.medium |  4096 |   40 |         0 |     2 | True      |
| 4                                    | m1.large  |  8192 |   80 |         0 |     4 | True      |
| 5                                    | m1.xlarge | 16384 |  160 |         0 |     8 | True      |
| 7e25178b-d0fe-4a0e-bd15-655e3a28472a | x.small   |  1024 |    2 |         0 |     1 | True      |
| cd8fe79d-17c6-464a-97bb-09e28bd7ef6d | mg.2      |  1024 |    5 |         0 |     2 | True      |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
```

### 1.1.5 创建镜像

```apl
[root@Openstack01 ~(keystone_admin)]# openstack image create --disk-format qcow2 --min-disk 2 --min-ram 1024 --public --file=/root/cirros-0.6.2-x86_64-disk.img ubuntu20.04
+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
| Field            | Value                                                                                                                                           |
+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
| container_format | bare                                                                                                                                            |
| created_at       | 2024-07-23T14:59:56Z                                                                                                                            |
| disk_format      | qcow2                                                                                                                                           |
| file             | /v2/images/4ceb01b5-f524-43f2-9347-a048eb930726/file                                                                                            |
| id               | 4ceb01b5-f524-43f2-9347-a048eb930726                                                                                                            |
| min_disk         | 2                                                                                                                                               |
| min_ram          | 1024                                                                                                                                            |
| name             | ubuntu20.04                                                                                                                                     |
| owner            | 65be68c4aad646b6b006b0332c796bfa                                                                                                                |
| properties       | os_hidden='False', owner_specified.openstack.md5='', owner_specified.openstack.object='images/ubuntu20.04', owner_specified.openstack.sha256='' |
| protected        | False                                                                                                                                           |
| schema           | /v2/schemas/image                                                                                                                               |
| status           | queued                                                                                                                                          |
| tags             |                                                                                                                                                 |
| updated_at       | 2024-07-23T14:59:56Z                                                                                                                            |
| visibility       | public                                                                                                                                          |
+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack image list
+--------------------------------------+-------------+--------+
| ID                                   | Name        | Status |
+--------------------------------------+-------------+--------+
| 4ceb01b5-f524-43f2-9347-a048eb930726 | ubuntu20.04 | active |
+--------------------------------------+-------------+--------+

```

### 1.2.1 创建私有网络(切换普通用户)

```
[root@Openstack01 ~(keystone_admin)]# source keystonerc_memeda
[root@Openstack01 ~(keystone_admin)]# openstack network create --help
usage: openstack network create [-h] [-f {json,shell,table,value,yaml}]
                                [-c COLUMN] [--noindent] [--prefix PREFIX]
                                [--max-width <integer>] [--fit-width]
                                [--print-empty] [--share | --no-share]
                                [--enable | --disable] [--project <project>]
                                [--description <description>] [--mtu <mtu>]
                                [--project-domain <project-domain>]
                                [--availability-zone-hint <availability-zone>]
                                [--enable-port-security | --disable-port-security]
                                [--external | --internal]
                                [--default | --no-default]
                                [--qos-policy <qos-policy>]
                                [--transparent-vlan | --no-transparent-vlan]
                                [--provider-network-type <provider-network-type>]
                                [--provider-physical-network <provider-physical-network>]
                                [--provider-segment <provider-segment>]
                                [--dns-domain <dns-domain>]
                                [--tag <tag> | --no-tag]
                                <name>
[root@Openstack01 ~(keystone_memeda)]# openstack network create private
+---------------------------+--------------------------------------+
| Field                     | Value                                |
+---------------------------+--------------------------------------+
| admin_state_up            | UP                                   |
| availability_zone_hints   |                                      |
| availability_zones        |                                      |
| created_at                | 2024-07-23T15:08:03Z                 |
| description               |                                      |
| dns_domain                | None                                 |
| id                        | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 |
| ipv4_address_scope        | None                                 |
| ipv6_address_scope        | None                                 |
| is_default                | False                                |
| is_vlan_transparent       | None                                 |
| mtu                       | 1442                                 |
| name                      | private                              |
| port_security_enabled     | True                                 |
| project_id                | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| provider:network_type     | None                                 |
| provider:physical_network | None                                 |
| provider:segmentation_id  | None                                 |
| qos_policy_id             | None                                 |
| revision_number           | 1                                    |
| router:external           | Internal                             |
| segments                  | None                                 |
| shared                    | False                                |
| status                    | ACTIVE                               |
| subnets                   |                                      |
| tags                      |                                      |
| updated_at                | 2024-07-23T15:08:03Z                 |
+---------------------------+--------------------------------------+

```

### 1.2.2创建私有网络

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack subnet create --help
usage: openstack subnet create [-h] [-f {json,shell,table,value,yaml}]
                               [-c COLUMN] [--noindent] [--prefix PREFIX]
                               [--max-width <integer>] [--fit-width]
                               [--print-empty] [--project <project>]
                               [--project-domain <project-domain>]
                               [--subnet-pool <subnet-pool> | --use-prefix-delegation USE_PREFIX_DELEGATION | --use-default-subnet-pool]
                               [--prefix-length <prefix-length>]
                               [--subnet-range <subnet-range>]
                               [--dhcp | --no-dhcp]
                               [--dns-publish-fixed-ip | --no-dns-publish-fixed-ip]
                               [--gateway <gateway>] [--ip-version {4,6}]
                               [--ipv6-ra-mode {dhcpv6-stateful,dhcpv6-stateless,slaac}]
                               [--ipv6-address-mode {dhcpv6-stateful,dhcpv6-stateless,slaac}]
                               [--network-segment <network-segment>] --network
                               <network> [--description <description>]
                               [--allocation-pool start=<ip-address>,end=<ip-address>]
                               [--dns-nameserver <dns-nameserver>]
                               [--host-route destination=<subnet>,gateway=<ip-address>]
                               [--service-type <service-type>]
                               [--tag <tag> | --no-tag]
                               <name>
[root@Openstack01 ~(keystone_memeda)]# openstack subnet create --subnet-range 192.168.81.0/24 --dhcp --gateway 192.168.81.254 --allocation-pool start=192.168.81.100,end=192.168.81.200  --network private pri_sub
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 192.168.81.100-192.168.81.200        |
| cidr                 | 192.168.81.0/24                      |
| created_at           | 2024-07-23T15:12:12Z                 |
| description          |                                      |
| dns_nameservers      |                                      |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 192.168.81.254                       |
| host_routes          |                                      |
| id                   | 53b94b3d-182a-4ea3-9ad5-195d128f75fc |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | pri_sub                              |
| network_id           | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 |
| prefix_length        | None                                 |
| project_id           | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| revision_number      | 0                                    |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2024-07-23T15:12:12Z                 |
+----------------------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack network list
+--------------------------------------+---------+--------------------------------------+
| ID                                   | Name    | Subnets                              |
+--------------------------------------+---------+--------------------------------------+
| eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | private | 53b94b3d-182a-4ea3-9ad5-195d128f75fc |
+--------------------------------------+---------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack subnet list
+--------------------------------------+---------+--------------------------------------+-----------------+
| ID                                   | Name    | Network                              | Subnet          |
+--------------------------------------+---------+--------------------------------------+-----------------+
| 53b94b3d-182a-4ea3-9ad5-195d128f75fc | pri_sub | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.81.0/24 |
+--------------------------------------+---------+--------------------------------------+-----------------+

```

### 1.3.1创建安全组

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack security group list
+--------------------------------------+---------+------------------------+----------------------------------+------+
| ID                                   | Name    | Description            | Project                          | Tags |
+--------------------------------------+---------+------------------------+----------------------------------+------+
| 8eeac281-3a1d-475f-9b73-53ae815ee5dc | default | Default security group | 1c940c1b0da84f70aa3acf0f0d951fb5 | []   |
+--------------------------------------+---------+------------------------+----------------------------------+------+
[root@Openstack01 ~(keystone_memeda)]# openstack security group create --help
usage: openstack security group create [-h] [-f {json,shell,table,value,yaml}]
                                       [-c COLUMN] [--noindent]
                                       [--prefix PREFIX]
                                       [--max-width <integer>] [--fit-width]
                                       [--print-empty]
                                       [--description <description>]
                                       [--project <project>]
                                       [--stateful | --stateless]
                                       [--project-domain <project-domain>]
                                       [--tag <tag> | --no-tag]
                                       <name>
[root@Openstack01 ~(keystone_memeda)]# openstack security group create sec001
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field           | Value                                                                                                                                                 |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
| created_at      | 2024-07-23T15:16:29Z                                                                                                                                  |
| description     | sec001                                                                                                                                                |
| id              | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d                                                                                                                  |
| name            | sec001                                                                                                                                                |
| project_id      | 1c940c1b0da84f70aa3acf0f0d951fb5                                                                                                                      |
| revision_number | 1                                                                                                                                                     |
| rules           | created_at='2024-07-23T15:16:30Z', direction='egress', ethertype='IPv4', id='63f4631c-be2b-4017-be82-c81816fcc898', updated_at='2024-07-23T15:16:30Z' |
|                 | created_at='2024-07-23T15:16:30Z', direction='egress', ethertype='IPv6', id='af9927ba-ecae-480b-adc6-64d4e1f8b307', updated_at='2024-07-23T15:16:30Z' |
| stateful        | True                                                                                                                                                  |
| tags            | []                                                                                                                                                    |
| updated_at      | 2024-07-23T15:16:30Z                                                                                                                                  |
+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
```

### 1.3.2安全组添加规则

```
[root@Openstack01 ~(keystone_memeda)]# openstack security group rule list
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
| ID                                   | IP Protocol | Ethertype | IP Range  | Port Range | Remote Security Group                | Security Group                       |
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
| 10b38ce5-1fd2-418d-a77b-11a67b793141 | None        | IPv6      | ::/0      |            | 8eeac281-3a1d-475f-9b73-53ae815ee5dc | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 4774cca9-c51b-4054-88c0-b15607f4249a | None        | IPv4      | 0.0.0.0/0 |            | 8eeac281-3a1d-475f-9b73-53ae815ee5dc | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 63f4631c-be2b-4017-be82-c81816fcc898 | None        | IPv4      | 0.0.0.0/0 |            | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| 767d7bc8-5216-4dbe-9e81-5abc847c1d15 | None        | IPv4      | 0.0.0.0/0 |            | None                                 | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 79d261c7-56ed-45c3-a20b-a96950883a48 | None        | IPv6      | ::/0      |            | None                                 | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| af9927ba-ecae-480b-adc6-64d4e1f8b307 | None        | IPv6      | ::/0      |            | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack security group rule create --help
usage: openstack security group rule create [-h]
                                            [-f {json,shell,table,value,yaml}]
                                            [-c COLUMN] [--noindent]
                                            [--prefix PREFIX]
                                            [--max-width <integer>]
                                            [--fit-width] [--print-empty]
                                            [--remote-ip <ip-address> | --remote-group <group>]
                                            [--dst-port <port-range>]
                                            [--protocol <protocol>]
                                            [--description <description>]
                                            [--icmp-type <icmp-type>]
                                            [--icmp-code <icmp-code>]
                                            [--ingress | --egress]
                                            [--ethertype <ethertype>]
                                            [--project <project>]
                                            [--project-domain <project-domain>]
                                            <group>
[root@Openstack01 ~(keystone_memeda)]# openstack security group rule create sec001  --ingress --protocol icmp
+-------------------+--------------------------------------+
| Field             | Value                                |
+-------------------+--------------------------------------+
| created_at        | 2024-07-23T15:20:42Z                 |
| description       |                                      |
| direction         | ingress                              |
| ether_type        | IPv4                                 |
| id                | 5d992cd3-8f49-4cae-998d-100ad5c2a319 |
| name              | None                                 |
| port_range_max    | None                                 |
| port_range_min    | None                                 |
| project_id        | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| protocol          | icmp                                 |
| remote_group_id   | None                                 |
| remote_ip_prefix  | 0.0.0.0/0                            |
| revision_number   | 0                                    |
| security_group_id | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| tags              | []                                   |
| updated_at        | 2024-07-23T15:20:42Z                 |
+-------------------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack security group rule create sec001  --ingress --protocol tcp --dst-port 22:3306
+-------------------+--------------------------------------+
| Field             | Value                                |
+-------------------+--------------------------------------+
| created_at        | 2024-07-23T15:21:40Z                 |
| description       |                                      |
| direction         | ingress                              |
| ether_type        | IPv4                                 |
| id                | 04b4a51b-3f3f-4c28-a61d-5588b437e226 |
| name              | None                                 |
| port_range_max    | 3306                                 |
| port_range_min    | 22                                   |
| project_id        | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| protocol          | tcp                                  |
| remote_group_id   | None                                 |
| remote_ip_prefix  | 0.0.0.0/0                            |
| revision_number   | 0                                    |
| security_group_id | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| tags              | []                                   |
| updated_at        | 2024-07-23T15:21:40Z                 |
+-------------------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack security group rule list
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
| ID                                   | IP Protocol | Ethertype | IP Range  | Port Range | Remote Security Group                | Security Group                       |
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
| 04b4a51b-3f3f-4c28-a61d-5588b437e226 | tcp         | IPv4      | 0.0.0.0/0 | 22:3306    | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| 10b38ce5-1fd2-418d-a77b-11a67b793141 | None        | IPv6      | ::/0      |            | 8eeac281-3a1d-475f-9b73-53ae815ee5dc | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 4774cca9-c51b-4054-88c0-b15607f4249a | None        | IPv4      | 0.0.0.0/0 |            | 8eeac281-3a1d-475f-9b73-53ae815ee5dc | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 5d992cd3-8f49-4cae-998d-100ad5c2a319 | icmp        | IPv4      | 0.0.0.0/0 |            | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| 63f4631c-be2b-4017-be82-c81816fcc898 | None        | IPv4      | 0.0.0.0/0 |            | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
| 767d7bc8-5216-4dbe-9e81-5abc847c1d15 | None        | IPv4      | 0.0.0.0/0 |            | None                                 | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| 79d261c7-56ed-45c3-a20b-a96950883a48 | None        | IPv6      | ::/0      |            | None                                 | 8eeac281-3a1d-475f-9b73-53ae815ee5dc |
| af9927ba-ecae-480b-adc6-64d4e1f8b307 | None        | IPv6      | ::/0      |            | None                                 | 1dfc02ef-7123-4eb7-b867-d476ed4dd51d |
+--------------------------------------+-------------+-----------+-----------+------------+--------------------------------------+--------------------------------------+
```

### 1.4.1 创建KEY密钥对

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack keypair create --help
usage: openstack keypair create [-h] [-f {json,shell,table,value,yaml}]
                                [-c COLUMN] [--noindent] [--prefix PREFIX]
                                [--max-width <integer>] [--fit-width]
                                [--print-empty]
                                [--public-key <file> | --private-key <file>]
                                <name>
[root@Openstack01 ~(keystone_memeda)]# openstack keypair create key001 > key001.pem
[root@Openstack01 ~(keystone_memeda)]# cat key001.pem
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAo/5kWGqRvZ6Z8UlH+F3InA0Sd2vetbOVft8y4tc2zziJus8v
sWnyr0kVd0qxkdgtXL4o5nb2cEgZmNd7Cn9R3Y4ZZU8+eWe/k7msxDFTbGE7ISPM
z5HTw+VR6VxD0wBn8NB7pHojzKGkyFUWtTgAUB9xOMasH7e1rkxkqUHl/chFOpT4
TTBpVIKFZ211h6PRVSCJpmBRw05HiowwUy+nEsQe7G5hCKahdAQfb9Q+tPb8k/UA
XL6JrLYe5OEJ0UW1lS3oXH8aqnoVnDTNJgUDJu6kKbpSYSQCFg50k6/6YqfV/vVx
MtJJ49jW4ixQDl3kxyLhJuLiAm1/w1Y/JKHXTwIDAQABAoIBAGjSWA1zwMg1Miza
LFiCiZHFgUI3/tihezLnM71u1qfJea+gctmx4N9NlZz0b1/Lj+Mx4S6+Z3MJguMB
CLKDAy7cfzsUVdiACiJAkj+tT6d81rCuE2Gx0mvqjlrdELU0EzwH5qAROgS4ZX1v
dd5Ld1e/YT1rL+XuJQDN76GIb5uwey/F12SOZPtI3u0aKwKvYVwr9mmSbV43ndTS
4O6HXNDgzu5eR9RmFo9Hz8nb24Bc8S9P58rmCLVcoy6oo9GoeasvX+oI3he747kg
t6y8j7jhDKkDk+68yyghUGeXY3dFmV7I+tTgrVtxG0LHbN2EJOXsmrqrRV6qi870
/10fAFECgYEAzZ+D+EmFrfEp9tkCTa9rgsPWHTn9CDRg4dElB5OLEz7D4bidvcJH
iQ385Vgz5MeFTK1QKxHfH21I00MCYJN6FzQRJgQc3p4WxVfzfL2NpY5BHb/3k6Xe
EkbgzRnkeKdohOvemVFlzo9VNzd2c1WuiSKjrQ7H458oCZHo2Cj+YfUCgYEAzCvr
yaVx79lUm5LMvUJh0G8oTpdVIMF2F+alckuAxQKL5PYI/pW+q1dVo859Ok586P2a
b/NvISLz2Xdir3w53p9wznYaomuWyScs1iZdmQmrhfwl41kiaBjtCvk3NHHSAc80
EdDm5pgNg3VB3FlX6m/9+72fU4rPxLnAhoQpVbMCgYA744n8du2IjAU88FfLaJxX
qdJjENCx4w+UteWjH0YShOVoiOzop/1N3dUat2Xl7HbWrmP7J2llLd9YKNw4ZLva
pj+YYvpFnKXlNIimfE8VOSmeEJt7VYQorpwrIK96tMesb0aWQS71yql3O6A0V3BO
YNhrPzLZCTIQF39J9iahQQKBgCun1IHIQ2VyhdnB+M8a64lCy06KoyQe2Z5grc2T
gVQeqETrqp6s7Bj80o307+fQsnqrByOa3I8sRxGfqlU1bbZBR0COFkHWWWZnXvnn
OCop3CgI8xz6iRXTBpRLF1e6YpoKcOrCTSzPJEyQfOWdoOO60IbMU83sJ2K8CQN6
LNBrAoGBALleGkstPLV+5+CvtrI0ht3Ibn4h8sCAQY54RoqR8XCB19wT1ST8NRy+
3OlA7Cu3e4SXblL4z1HPgSiTmm9to35re4ViOtow7f401ooYwa2lgFg4SyRYlTWf
mcG19r742LmhmmTcdzOKA18GHy5rMjSIxa+UNytY7op61Y/Tjcqk
-----END RSA PRIVATE KEY-----
```

### 1.5.1发放云主机

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack flavor list
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| ID                                   | Name      |   RAM | Disk | Ephemeral | VCPUs | Is Public |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
| 1                                    | m1.tiny   |   512 |    1 |         0 |     1 | True      |
| 2                                    | m1.small  |  2048 |   20 |         0 |     1 | True      |
| 3                                    | m1.medium |  4096 |   40 |         0 |     2 | True      |
| 4                                    | m1.large  |  8192 |   80 |         0 |     4 | True      |
| 5                                    | m1.xlarge | 16384 |  160 |         0 |     8 | True      |
| 7e25178b-d0fe-4a0e-bd15-655e3a28472a | x.small   |  1024 |    2 |         0 |     1 | True      |
| cd8fe79d-17c6-464a-97bb-09e28bd7ef6d | mg.2      |  1024 |    5 |         0 |     2 | True      |
+--------------------------------------+-----------+-------+------+-----------+-------+-----------+
[root@Openstack01 ~(keystone_memeda)]# openstack image list
+--------------------------------------+-------------+--------+
| ID                                   | Name        | Status |
+--------------------------------------+-------------+--------+
| 4ceb01b5-f524-43f2-9347-a048eb930726 | ubuntu20.04 | active |
+--------------------------------------+-------------+--------+
[root@Openstack01 ~(keystone_memeda)]# openstack network list
+--------------------------------------+---------+--------------------------------------+
| ID                                   | Name    | Subnets                              |
+--------------------------------------+---------+--------------------------------------+
| eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | private | 53b94b3d-182a-4ea3-9ad5-195d128f75fc |
+--------------------------------------+---------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack subnet list
+--------------------------------------+---------+--------------------------------------+-----------------+
| ID                                   | Name    | Network                              | Subnet          |
+--------------------------------------+---------+--------------------------------------+-----------------+
| 53b94b3d-182a-4ea3-9ad5-195d128f75fc | pri_sub | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.81.0/24 |
+--------------------------------------+---------+--------------------------------------+-----------------+
[root@Openstack01 ~(keystone_memeda)]# openstack security group list
+--------------------------------------+---------+------------------------+----------------------------------+------+
| ID                                   | Name    | Description            | Project                          | Tags |
+--------------------------------------+---------+------------------------+----------------------------------+------+
| 1dfc02ef-7123-4eb7-b867-d476ed4dd51d | sec001  | sec001                 | 1c940c1b0da84f70aa3acf0f0d951fb5 | []   |
| 8eeac281-3a1d-475f-9b73-53ae815ee5dc | default | Default security group | 1c940c1b0da84f70aa3acf0f0d951fb5 | []   |
+--------------------------------------+---------+------------------------+----------------------------------+------+
[root@Openstack01 ~(keystone_memeda)]# openstack keypair list
+--------+-------------------------------------------------+
| Name   | Fingerprint                                     |
+--------+-------------------------------------------------+
| key001 | 74:ba:70:e8:3c:75:4e:19:92:1c:a3:6b:03:07:2d:0d |
+--------+-------------------------------------------------+
```

**创建**

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack server create --help
usage: openstack server create [-h] [-f {json,shell,table,value,yaml}]
                               [-c COLUMN] [--noindent] [--prefix PREFIX]
                               [--max-width <integer>] [--fit-width]
                               [--print-empty]
                               (--image <image> | --image-property <key=value> | --volume <volume>)
                               --flavor <flavor>
                               [--security-group <security-group>]
                               [--key-name <key-name>]
                               [--property <key=value>]
                               [--file <dest-filename=source-filename>]
                               [--user-data <user-data>]
                               [--description <description>]
                               [--availability-zone <zone-name>]
                               [--host <host>]
                               [--hypervisor-hostname <hypervisor-hostname>]
                               [--boot-from-volume <volume-size>]
                               [--block-device-mapping <dev-name=mapping>]
                               [--nic <net-id=net-uuid,v4-fixed-ip=ip-addr,v6-fixed-ip=ip-addr,port-id=port-uuid,auto,none>]
                               [--network <network>] [--port <port>]
                               [--hint <key=value>]
                               [--config-drive <config-drive-volume>|True]
                               [--min <count>] [--max <count>] [--wait]
                               <server-name>
[root@Openstack01 ~(keystone_memeda)]# openstack server create --flavor x.small --image ubuntu20.04 --security-group sec001 --key-name key001 --nic net-id=eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 ECS001
+-----------------------------+----------------------------------------------------+
| Field                       | Value                                              |
+-----------------------------+----------------------------------------------------+
| OS-DCF:diskConfig           | MANUAL                                             |
| OS-EXT-AZ:availability_zone |                                                    |
| OS-EXT-STS:power_state      | NOSTATE                                            |
| OS-EXT-STS:task_state       | scheduling                                         |
| OS-EXT-STS:vm_state         | building                                           |
| OS-SRV-USG:launched_at      | None                                               |
| OS-SRV-USG:terminated_at    | None                                               |
| accessIPv4                  |                                                    |
| accessIPv6                  |                                                    |
| addresses                   |                                                    |
| adminPass                   | y9yKWWMh6CUm                                       |
| config_drive                |                                                    |
| created                     | 2024-07-23T15:30:05Z                               |
| flavor                      | x.small (7e25178b-d0fe-4a0e-bd15-655e3a28472a)     |
| hostId                      |                                                    |
| id                          | 85bccd22-9ae0-4752-90cc-da6766930500               |
| image                       | ubuntu20.04 (4ceb01b5-f524-43f2-9347-a048eb930726) |
| key_name                    | key001                                             |
| name                        | ECS001                                             |
| progress                    | 0                                                  |
| project_id                  | 1c940c1b0da84f70aa3acf0f0d951fb5                   |
| properties                  |                                                    |
| security_groups             | name='1dfc02ef-7123-4eb7-b867-d476ed4dd51d'        |
| status                      | BUILD                                              |
| updated                     | 2024-07-23T15:30:05Z                               |
| user_id                     | 97eab00287d64401bd39fc4bbb9b369e                   |
| volumes_attached            |                                                    |
+-----------------------------+----------------------------------------------------+

[root@Openstack01 ~(keystone_memeda)]# openstack server create --flavor x.small --image ubuntu20.04 --security-group sec001 --key-name key001 --network private ECS002
+-----------------------------+----------------------------------------------------+
| Field                       | Value                                              |
+-----------------------------+----------------------------------------------------+
| OS-DCF:diskConfig           | MANUAL                                             |
| OS-EXT-AZ:availability_zone |                                                    |
| OS-EXT-STS:power_state      | NOSTATE                                            |
| OS-EXT-STS:task_state       | scheduling                                         |
| OS-EXT-STS:vm_state         | building                                           |
| OS-SRV-USG:launched_at      | None                                               |
| OS-SRV-USG:terminated_at    | None                                               |
| accessIPv4                  |                                                    |
| accessIPv6                  |                                                    |
| addresses                   |                                                    |
| adminPass                   | U2Qvw8sva5bX                                       |
| config_drive                |                                                    |
| created                     | 2024-07-23T15:32:12Z                               |
| flavor                      | x.small (7e25178b-d0fe-4a0e-bd15-655e3a28472a)     |
| hostId                      |                                                    |
| id                          | 1056b476-ea8a-4c2e-8fc9-4309e9b0c812               |
| image                       | ubuntu20.04 (4ceb01b5-f524-43f2-9347-a048eb930726) |
| key_name                    | key001                                             |
| name                        | ECS002                                             |
| progress                    | 0                                                  |
| project_id                  | 1c940c1b0da84f70aa3acf0f0d951fb5                   |
| properties                  |                                                    |
| security_groups             | name='1dfc02ef-7123-4eb7-b867-d476ed4dd51d'        |
| status                      | BUILD                                              |
| updated                     | 2024-07-23T15:32:12Z                               |
| user_id                     | 97eab00287d64401bd39fc4bbb9b369e                   |
| volumes_attached            |                                                    |
+-----------------------------+----------------------------------------------------+

```

### 1.6.1创建网络（公网）

```APL
[root@Openstack01 ~(keystone_memeda)]# source keystonerc_admin
[root@Openstack01 ~(keystone_admin)]# openstack network create --help
usage: openstack network create [-h] [-f {json,shell,table,value,yaml}]
                                [-c COLUMN] [--noindent] [--prefix PREFIX]
                                [--max-width <integer>] [--fit-width]
                                [--print-empty] [--share | --no-share]
                                [--enable | --disable] [--project <project>]
                                [--description <description>] [--mtu <mtu>]
                                [--project-domain <project-domain>]
                                [--availability-zone-hint <availability-zone>]
                                [--enable-port-security | --disable-port-security]
                                [--external | --internal]
                                [--default | --no-default]
                                [--qos-policy <qos-policy>]
                                [--transparent-vlan | --no-transparent-vlan]
                                [--provider-network-type <provider-network-type>]
                                [--provider-physical-network <provider-physical-network>]
                                [--provider-segment <provider-segment>]
                                [--dns-domain <dns-domain>]
                                [--tag <tag> | --no-tag]
                                <name>
[root@Openstack01 ~(keystone_admin)]# openstack network create public --share --project promemeda --external --provider-network-type flat --provider-physical-network extnet
+---------------------------+--------------------------------------+
| Field                     | Value                                |
+---------------------------+--------------------------------------+
| admin_state_up            | UP                                   |
| availability_zone_hints   |                                      |
| availability_zones        |                                      |
| created_at                | 2024-07-23T15:47:56Z                 |
| description               |                                      |
| dns_domain                | None                                 |
| id                        | aff5cbe2-b12f-49a2-91ad-e960803ea46d |
| ipv4_address_scope        | None                                 |
| ipv6_address_scope        | None                                 |
| is_default                | False                                |
| is_vlan_transparent       | None                                 |
| mtu                       | 1500                                 |
| name                      | public                               |
| port_security_enabled     | True                                 |
| project_id                | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| provider:network_type     | flat                                 |
| provider:physical_network | extnet                               |
| provider:segmentation_id  | None                                 |
| qos_policy_id             | None                                 |
| revision_number           | 1                                    |
| router:external           | External                             |
| segments                  | None                                 |
| shared                    | True                                 |
| status                    | ACTIVE                               |
| subnets                   |                                      |
| tags                      |                                      |
| updated_at                | 2024-07-23T15:47:56Z                 |
+---------------------------+--------------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack network list
+--------------------------------------+---------+----------------------------------------------------------------------------+
| ID                                   | Name    | Subnets                                                                    |
+--------------------------------------+---------+----------------------------------------------------------------------------+
| aff5cbe2-b12f-49a2-91ad-e960803ea46d | public  |                                                                            |
| eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | private | 53b94b3d-182a-4ea3-9ad5-195d128f75fc, e8254f40-2abc-4961-a8c4-02a366c62f30 |
+--------------------------------------+---------+----------------------------------------------------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack subnet create^C
[root@Openstack01 ~(keystone_admin)]# openstack subnet create --subnet-range 192.168.71.0/24 --dhcp --gateway 192.168.71.1 --allocation-pool start=192.168.71.230,end=192.168.71.250  --network public pub_sub
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 192.168.71.230-192.168.71.250        |
| cidr                 | 192.168.71.0/24                      |
| created_at           | 2024-07-23T15:50:19Z                 |
| description          |                                      |
| dns_nameservers      |                                      |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 192.168.71.1                         |
| host_routes          |                                      |
| id                   | 388c0916-02a3-41dc-9c86-42a3e7f88036 |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | pub_sub                              |
| network_id           | aff5cbe2-b12f-49a2-91ad-e960803ea46d |
| prefix_length        | None                                 |
| project_id           | 65be68c4aad646b6b006b0332c796bfa     |
| revision_number      | 0                                    |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2024-07-23T15:50:19Z                 |
+----------------------+--------------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack subnet list
+--------------------------------------+----------+--------------------------------------+-----------------+
| ID                                   | Name     | Network                              | Subnet          |
+--------------------------------------+----------+--------------------------------------+-----------------+
| 388c0916-02a3-41dc-9c86-42a3e7f88036 | pub_sub  | aff5cbe2-b12f-49a2-91ad-e960803ea46d | 192.168.71.0/24 |
| 53b94b3d-182a-4ea3-9ad5-195d128f75fc | pri_sub  | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.81.0/24 |
| e8254f40-2abc-4961-a8c4-02a366c62f30 | pri_sub2 | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.91.0/24 |
+--------------------------------------+----------+--------------------------------------+-----------------+
```

### 1.7.1 创建路由

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack router create --help
usage: openstack router create [-h] [-f {json,shell,table,value,yaml}]
                               [-c COLUMN] [--noindent] [--prefix PREFIX]
                               [--max-width <integer>] [--fit-width]
                               [--print-empty] [--enable | --disable]
                               [--distributed | --centralized]
                               [--ha | --no-ha] [--description <description>]
                               [--project <project>]
                               [--project-domain <project-domain>]
                               [--availability-zone-hint <availability-zone>]
                               [--tag <tag> | --no-tag]
                               <name>
[root@Openstack01 ~(keystone_memeda)]# openstack router create r001
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| admin_state_up          | UP                                   |
| availability_zone_hints |                                      |
| availability_zones      |                                      |
| created_at              | 2024-07-23T15:54:04Z                 |
| description             |                                      |
| external_gateway_info   | null                                 |
| flavor_id               | None                                 |
| id                      | dfcee99b-61d7-42b6-aa9d-15f34c5ef8e3 |
| name                    | r001                                 |
| project_id              | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| revision_number         | 1                                    |
| routes                  |                                      |
| status                  | ACTIVE                               |
| tags                    |                                      |
| updated_at              | 2024-07-23T15:54:04Z                 |
+-------------------------+--------------------------------------+
```

### 1.7.2设置路由网关

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack route set --help
usage: openstack route set [-h] [--name <name>] [--description <description>]
                           [--enable | --disable]
                           [--distributed | --centralized]
                           [--route destination=<subnet>,gateway=<ip-address>]
                           [--no-route] [--ha | --no-ha]
                           [--external-gateway <network>]
                           [--fixed-ip subnet=<subnet>,ip-address=<ip-address>]
                           [--enable-snat | --disable-snat]
                           [--qos-policy <qos-policy> | --no-qos-policy]
                           [--tag <tag>] [--no-tag]
                           <router>
[root@Openstack01 ~(keystone_memeda)]# openstack router list
+--------------------------------------+------+--------+-------+----------------------------------+
| ID                                   | Name | Status | State | Project                          |
+--------------------------------------+------+--------+-------+----------------------------------+
| f060fccf-80b0-4643-bb66-88cd1ca19093 | r001 | ACTIVE | UP    | 1c940c1b0da84f70aa3acf0f0d951fb5 |
+--------------------------------------+------+--------+-------+----------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack router set --external-gateway public r001

```

### 1.8.1 绑定路由内网接口

```
[root@Openstack01 ~(keystone_memeda)]# openstack router add subnet --help
usage: openstack router add subnet [-h] <router> <subnet>

Add a subnet to a router

positional arguments:
  <router>    Router to which subnet will be added (name or ID)
  <subnet>    Subnet to be added (name or ID)

[root@Openstack01 ~(keystone_memeda)]# openstack subnet list
+--------------------------------------+----------+--------------------------------------+-----------------+
| ID                                   | Name     | Network                              | Subnet          |
+--------------------------------------+----------+--------------------------------------+-----------------+
| 388c0916-02a3-41dc-9c86-42a3e7f88036 | pub_sub  | aff5cbe2-b12f-49a2-91ad-e960803ea46d | 192.168.71.0/24 |
| 53b94b3d-182a-4ea3-9ad5-195d128f75fc | pri_sub  | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.81.0/24 |
| e8254f40-2abc-4961-a8c4-02a366c62f30 | pri_sub2 | eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 | 192.168.91.0/24 |
+--------------------------------------+----------+--------------------------------------+-----------------+
[root@Openstack01 ~(keystone_memeda)]# openstack router add subnet r001 pri_sub
```

![image-20240724000300943](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724000300943.png?raw=true)

### 1.9.1绑定EIP并访问

```
[root@Openstack01 ~(keystone_memeda)]# openstack floating ip create public
+---------------------+--------------------------------------+
| Field               | Value                                |
+---------------------+--------------------------------------+
| created_at          | 2024-07-23T16:04:01Z                 |
| description         |                                      |
| dns_domain          | None                                 |
| dns_name            | None                                 |
| fixed_ip_address    | None                                 |
| floating_ip_address | 192.168.71.237                       |
| floating_network_id | aff5cbe2-b12f-49a2-91ad-e960803ea46d |
| id                  | 06f91248-2fe3-4a92-949a-77b78e009816 |
| name                | 192.168.71.237                       |
| port_details        | None                                 |
| port_id             | None                                 |
| project_id          | 1c940c1b0da84f70aa3acf0f0d951fb5     |
| qos_policy_id       | None                                 |
| revision_number     | 0                                    |
| router_id           | None                                 |
| status              | DOWN                                 |
| subnet_id           | None                                 |
| tags                | []                                   |
| updated_at          | 2024-07-23T16:04:01Z                 |
+---------------------+--------------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack floating ip list
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
| ID                                   | Floating IP Address | Fixed IP Address | Port | Floating Network                     | Project                          |
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
| 06f91248-2fe3-4a92-949a-77b78e009816 | 192.168.71.237      | None             | None | aff5cbe2-b12f-49a2-91ad-e960803ea46d | 1c940c1b0da84f70aa3acf0f0d951fb5 |
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack floating ip list
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
| ID                                   | Floating IP Address | Fixed IP Address | Port | Floating Network                     | Project                          |
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
| 06f91248-2fe3-4a92-949a-77b78e009816 | 192.168.71.237      | None             | None | aff5cbe2-b12f-49a2-91ad-e960803ea46d | 1c940c1b0da84f70aa3acf0f0d951fb5 |
+--------------------------------------+---------------------+------------------+------+--------------------------------------+----------------------------------+
[root@Openstack01 ~(keystone_memeda)]# openstack server add floating ip ECS001 192.168.71.237
[root@Openstack01 ~(keystone_memeda)]# openstack server list
+--------------------------------------+--------+--------+----------------------------------------+-------------+---------+
| ID                                   | Name   | Status | Networks                               | Image       | Flavor  |
+--------------------------------------+--------+--------+----------------------------------------+-------------+---------+
| 1056b476-ea8a-4c2e-8fc9-4309e9b0c812 | ECS002 | ACTIVE | private=192.168.81.189                 | ubuntu20.04 | x.small |
| 85bccd22-9ae0-4752-90cc-da6766930500 | ECS001 | ACTIVE | private=192.168.81.144, 192.168.71.237 | ubuntu20.04 | x.small |
+--------------------------------------+--------+--------+----------------------------------------+-------------+---------+

```

![image-20240724000736398](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724000736398.png?raw=true)

## rabbitmq

>- rabbitmq用于实现消息队列的，提升系统的容错性和性能，将各个服务组件进行解耦操作。
>
>- 不至于一个组件出问题，影响其他组件，各自做各自的。默认有两个端口 25672/15672.
>
>- 默认只开启一个25672端口，这个端口就是内部各个节点之间访问使用的端口，不能对外。客户端如果要访问，必须开启15672端口。当开启15672端口后，rabbitmq会提供一个webUI界面。

```apl
[root@Openstack01 ~]# systemctl list-unit-files | grep nova
openstack-nova-api.service                      disabled
openstack-nova-compute.service                  enabled
openstack-nova-conductor.service                enabled
openstack-nova-metadata-api.service             disabled
openstack-nova-novncproxy.service               enabled
openstack-nova-os-compute-api.service           disabled
openstack-nova-scheduler.service                enabled

[root@Openstack01 ~]# rabbitmq-plugins list
Listing plugins with pattern ".*" ...
 Configured: E = explicitly enabled; e = implicitly enabled
 | Status: * = running on rabbit@Openstack01
 |/
[  ] rabbitmq_amqp1_0                  3.8.3
[  ] rabbitmq_auth_backend_cache       3.8.3
[  ] rabbitmq_auth_backend_http        3.8.3
[  ] rabbitmq_auth_backend_ldap        3.8.3
[  ] rabbitmq_auth_backend_oauth2      3.8.3
[  ] rabbitmq_auth_mechanism_ssl       3.8.3
[  ] rabbitmq_consistent_hash_exchange 3.8.3
[  ] rabbitmq_event_exchange           3.8.3
[  ] rabbitmq_federation               3.8.3
[  ] rabbitmq_federation_management    3.8.3
[  ] rabbitmq_jms_topic_exchange       3.8.3
[E*] rabbitmq_management               3.8.3

[root@Openstack01 ~]# rabbitmq-plugins enable rabbitmq_management
Enabling plugins on node rabbit@Openstack01:
rabbitmq_management
The following plugins have been configured:
  rabbitmq_management
  rabbitmq_management_agent
  rabbitmq_web_dispatch
Applying plugin configuration to rabbit@Openstack01...
Plugin configuration unchanged.

```

![image-20240725144433708](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725144433708.png?raw=true)

账户：guest

密码：guest

# Openstack组件详解

## 计算管理Nova

### Nova介绍

![image-20240729171309752](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171309752.png?raw=true)

### Nova在Openstack中的定位

![image-20240729171359131](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171359131.png?raw=true)

### Nova的使命与作用

- 使命：实施服务和相关库，提供对计算资源（包括裸金属、虚拟机和容器）的大规模可扩展、按需、自助访问

![image-20240729171451935](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171451935.png?raw=true)

### Nova架构

![image-20240729171620702](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171620702.png?raw=true)

>- DB：用于数据存储的SQL数据库。
>- API：接收 HTTP 请求、转换命令并通过oslo.messaging队列或 HTTP与其他组件通信的组件。
>- Scheduler：为虚拟机选择合适的物理主机。
>- Compute：虚拟机生命周期和复杂流程控制。
>- Conductor：处理需要协调（构建/调整大小）的请求，充当数据库代理或处理对象转换。
>- Placement：跟踪资源提供者的库存和使用情况。
>- RPC：Remote Procedure Call，远程过程调用，是一个计算机通信协议。该协议允许运行于一台计算机的程序调用另一台计算机的子程序，而程序员无需额外地为这个交互作用编程。
>- API服务器处理REST请求，通常涉及数据库读写，将RPC消息发送到其他Nova服务（可选），并生成对REST调用的响应。
>- RPC消息传递是通过oslo.messaging库完成的，它是消息队列之上的抽象。
>- Nova使用基于消息传递的“无共享”架构，大多数主要的nova组件可以在多个服务器上运行，并且有一个监听RPC消息的管理器。
>
>

#### Nova物理部署实例

![image-20240729171840259](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171840259.png?raw=true)

#### Noava服务运行架构

![image-20240729171948271](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729171948271.png?raw=true)

#### Nova资源池管理架构

![image-20240729172010300](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729172010300.png?raw=true)

#### Nova组件-API

>- Nova-API功能
>  - 对外提供REST接口，接收和处理请求
>  - 对传入参数进行合法性校验和约束限制
>  - 对请求的资源进行配额的校验和预留
>  - 资源的创建，更新，删除查询等
>  - 虚拟机生命周期管理的入口

 ![image-20240730092940642](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730092940642.png?raw=true)

#### Nova组件-Conductor

![image-20240730094314491](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730094314491.png?raw=true)

> 引入nova-conductor
>
> - 安全性考虑。之前每个nova-compute都是直接访问数据库的。如果由于某种原因，某个计算节点被攻陷了，那攻击者就可以获取访问数据库的全部权限，肆意操作数据库。
> - 方便升级。将数据库nova-compute解耦，如果数据库的模式改变，nova-compute就不用升级了
> - 性能上考虑。之前数据库的访问在nova-compute中直接访问且数据库访问是阻塞性的，由于nova-compute只有一个os线程，所以当一个绿色线程去访问数据库的时候会阻塞其他绿色线程，导致绿色线程无法并发。但是nova-conductor是通过rpc 调用，rpc调用是绿色线程友好的，一个rpc call的执行返回前不会阻塞其他绿色线程的执行。这样就会提高了操作的

#### Nova组件-Scheduler

![image-20240730101731294](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730101731294.png?raw=true)

> - Nova-Scheduler:确定将虚拟机分配到那一台物理机，分配过程主要分为两步，过滤和权重；用户创建虚拟机时会提出资源需求。
>   - 例如CPU、内存、磁盘各需要多少，OpenStack这些需要定义在flavor中，用户只需要指定flavor就可以了。
> - 调度过程分为两步：
>   - 通过过滤器选择满足条件的计算节点
>   - 通过权重选择最优的节点。

#### Nova组件-Compute

> - 虚拟机声明周期操作的真正执行者(会调用对应的主机的driver)。
> - 底层对接不通虚拟化平台(KVM/VMware/XEN)
> - 内置周期性任务，完成资源刷新，虚拟机状态同步等 功能。
> - 资源管理模块（resource_tracker)配合插件机制，完成资源的统计。

### Nova工作原理和流程

#### 虚拟机状态介绍

![image-20240730110519785](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730110519785.png?raw=true)

![image-20240730110551521](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730110551521.png?raw=true)

| vm_state | task_state                   | status      | 状态翻译 |
| -------- | ---------------------------- | ----------- | -------- |
| active   | rebooting                    | REBOOT      | 重启     |
| active   | reboot_pending               | REBOOT      | 重启     |
| active   | reboot_started               | REBOOT      | 重启     |
| active   | rebooting_hard               | HARD_REBOOT | 强制重启 |
| active   | reboot_pending_hard          | HARD_REBOOT | 强制重启 |
| active   | reboot_started_hard          | HARD_REBOOT | 强制重启 |
| active   | rebuild_block_device_mapping | REBUILD     | 重建     |
| active   | rebuilding                   | REBUILD     | 重建     |
| active   | rebuild_spawning             | REBUILD     | 重建     |
| active   | migrating                    | MIGRATING   | 迁移中   |
| active   | resize_prep                  | RESIZE      | 调整大小 |
| active   | resize_migrating             | RESIZE      | 调整大小 |
| active   | resize_migrated              | RESIZE      | 调整大小 |
| active   | resize_finish                | RESIZE      | 调整完成 |
| active   | default                      | ACTIVE      | 活跃     |

| vm_state | task_state       | status  | 状态翻译 |
| -------- | ---------------- | ------- | -------- |
| stopped  | resize_prep      | RESIZE  | 调整大小 |
| stopped  | resize_migrating | RESIZE  | 调整大小 |
| stopped  | resize_migrated  | RESIZE  | 调整大小 |
| stopped  | resize_finish    | RESIZE  | 调整完成 |
| stopped  | default          | SHUTOFF | 关闭     |

#### Nova创建虚拟机流程

![image-20240730110644935](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730110644935.png?raw=true)

>- Step1：用户通过Dashboard/CLI 申请创建虚拟机，并以REST API 方式来请求Keystone授权。
>- Step2：keystone通过用户请求认证信息，并生成auth-token返回给对应的认证请求。
>- Step3：界面或命令行通过RESTful API向nova-api发送一个boot instance的请求（携带auth-token）。
>- Step4：nova-api接受请求后向keystone发送认证请求，查看token是否为有效用户和token。
>- Step5：keystone验证token是否有效，如有效则返回有效的认证和对应的角色（注：有些操作需要有角色权限才能操作）。
>- Step6：通过认证后nova-api和数据库通讯。
>- Step7：初始化新建虚拟机的数据库记录。
>- Step8：nova-api通过rpc.call向nova-scheduler请求是否有创建虚拟机的资源（Host ID）。
>- Step9：nova-scheduler进程侦听消息队列，获取nova-api的请求。
>- Step10：nova-scheduler通过查询nova数据库中计算资源的情况，并通过调度算法计算符合虚拟机创建需要的主机。
>- Step11：对于有符合虚拟机创建的主机，nova-scheduler更新数据库中虚拟机对应的物理主机信
>- Step12：nova-scheduler通过rpc.cast向nova-compute发送对应的创建虚拟机请求的消息。
>- Step13：nova-compute会从对应的消息队列中获取创建虚拟机请求的消息。
>- Step14：nova-compute通过rpc.call向nova-conductor请求获取虚拟机消息。
>- Step15：nova-conductor从消息队队列中拿到nova-compute请求消息。
>- Step16：nova-conductor根据消息查询虚拟机对应的信息。
>- Step17：nova-conductor从数据库中获得虚拟机对应信息。
>- Step18：nova-conductor把虚拟机信息通过消息的方式发送到消息队列中。
>- Step19：nova-compute从对应的消息队列中获取虚拟机信息消息。
>- Step20：nova-compute通过keystone的RESTfull API拿到认证的token，并通过HTTP请求glance-api获取创建虚拟机所需要镜像。
>- Step21：glance-api向keystone认证token是否有效，并返回验证结果。
>- Step22：token验证通过，nova-compute获得虚拟机镜像信息（URL）。
>- Step23：nova-compute通过keystone的RESTfull API拿到认证k的token，并通过HTTP请求neutron-server获取创建虚拟机所需要的网络信息。
>- Step24：neutron-server向keystone认证token是否有效，并返回验证结果。
>- Step25：token验证通过，nova-compute获得虚拟机网络信息。
>- Step26：nova-compute通过keystone的RESTfull API拿到认证的token，并通过HTTP请求cinder-api获取创建虚拟机所需要的持久化存储信息。
>- Step27：cinder-api向keystone认证token是否有效，并返回验证结果。
>- Step28：token验证通过，nova-compute获得虚拟机持久化存储信息。
>- Step29：nova-compute根据instance的信息调用配置的虚拟化驱动来创建虚拟机。

#### Nova过滤调度器

![image-20240730111100232](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730111100232.png?raw=true)

### Nova典型操作

![image-20240730111206460](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730111206460.png?raw=true)

#### Nova主要操作对象(1)

![image-20240730111234014](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730111234014.png?raw=true)

![image-20240730111246827](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730111246827.png?raw=true)

## 存储概述Cinder

> **Cinder提供块存储**
>
> - **灰姑娘 Cinderelle**
>   - **用户可以根据业务需求自由选择存储服务。**
>   - **重点介绍块存储服务Cinder和对象存储服务Swift在OpenStack中的定位、作用、与其他服务的交互关系、架构和工作原理。**

### 存储类型

- 临时磁盘来源：
  - 计算节点的本地磁盘。
  - 通过NFS挂载的外部存储（使用此方式创建临时磁盘时，可以在多个计算节点之间迁移虚拟机，因为虚拟机实例的根磁盘位于可被多个物理主机访问的共享存储上）。

![image-20240724201257174](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724201257174.png?raw=true)

**存储类型对比**

![image-20240724003342658](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724003342658.png?raw=true)

### 存储介绍

![image-20240724202422107](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724202422107.png?raw=true)

### Cinder的定位

- cinder的前身是nova中的nova-volume组件，后来才被单独提出来成为一个OpenStack组件，因此cinder的设计架构和nova十分相像，具体体现在它们各个子组件的功能基本都能对应。

![image-20240724202625713](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724202625713.png?raw=true)

### Cinder于其他服务的交互关系

![image-20240724202937596](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724202937596.png?raw=true)

### 块存储服务Cinder

>- **Cinder在虚拟机与具体存储设备之间引入了一层“逻辑存储卷”的抽象，Cinder本身不是一种存储技术，并没有实现对块设备的实际管理和服务**
>- **Cinder只是提供了一个中间的抽象层，为后端不同的存储技术，提供了统一的接口**
>- **不同的块设备服务厂商在Cinder中以驱动的形式实现上述接口与OpenStack进行整合**

###  Cinder简介

>- Cinder Client封装Cinder提供的rest接口，以CLI形式供用户使用。
>- Cinder API对外提供rest API，对操作需求进行解析，对API进行路由寻找相应的处理方法。包含卷的增删改查（包括从源卷、镜像、快照创建）、快照增删改查、备份、volume type管理、挂载/卸载（Nova调用）等。
>- LVM将众多不同的物理存储资源（物理卷、Physical Volume，如磁盘分区）组成卷组。LVM从卷组中创建一个逻辑卷，然后将ext3、ReiserFS等文件系统安装在这个逻辑卷上。
>- 除了LVM，目前Cinder已经以驱动的形式支持众多存储技术或存储厂商的设备作为后端存储，如SAN（Storage Area Network）、Ceph、Sheepdog，以及EMC、华为等厂商的设备。

![image-20240724203936811](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724203936811.png?raw=true)

![image-20240724204013787](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204013787.png?raw=true)

#### Cinder组件-API

- Cinder API对外提供REST API，对操作需求进行解析，并调用处理方法：
  - 卷create/delete/list/show
  - 快照create/delete/list/show
  - 卷attach/detach (Nova调用)
  - 其他
    - Volume types 
    - Quotas
    - Backups

#### Cinder组件-Scheduler

>根据后端的能力进行筛选：Drivers定期报告后端的能力和状态。管理员创建的卷类型（volume type ）。创建卷时，用户指定卷类型。
>
>- Cinder scheduler负责收集后端上报的容量、能力信息，根据设定的算法完成卷到指定cinder-volume的调度
>- Cinder scheduler通过过滤和权重，筛选出合适的后端：

![image-20240724204154776](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204154776.png?raw=true)

#### Cinder组件—Volume

>Cinder默认的后端驱动是LVM。

- Cinder volume多节点部署，使用不同的配置文件、接入不同的后端设备，由各存储厂商插入Driver代码与设备交互，完成设备容量和能力信息收集、卷操作等

![image-20240724204253294](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204253294.png?raw=true)

### Cinder工作原理

>创建卷类型的目的是为了筛选不同的后端存储，例如SSD、SATA、高性能、低性能等，通过创建不同的自定义卷类型，创建卷时自动筛选出合适的后端存储。

![image-20240724204556358](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204556358.png?raw=true)

#### Cinder创建卷流程 Cinder API

![image-20240724204653370](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204653370.png?raw=true)

#### CInder创建卷流程 cinder Scheduler

>和Nova Scheduler类似，Cinder Scheduler也是经过Filter筛选符合条件的后端，然后使用Weigher计算后端进行权重排序，最终选择出最合适的后端存储。

![image-20240724204858719](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204858719.png?raw=true)

#### Cinder创建卷流程-Cinder Volume

![image-20240724204941276](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724204941276.png?raw=true)

### Cinder挂载流程

> - **Nova调用Cinder API创建卷，传递主机的信息，如hostname，iSCSI initiator name，FC WWPNs。**
>
> - **Cinder API将该信息传递给Cinder Volume。**
>
> - **Cinder Volume通过创建卷时保存的host信息找到对应的**
>
> - **Cinder Driver。Cinder Driver通知存储允许该主机访问该卷，并返回该存储的连接信息（如iSCSI iqn，portal，FC Target WWPN，NFS path等）。**
>
> - **Nova调用针对于不同存储类型进行主机识别磁盘的代码（ Cinder 提供了brick模块用于参考）实现识别磁盘或者文件设备。**
>
> - **Nova通知Cinder已经进行了挂载。**
>
> - **Nova将主机的设备信息传递给hypervisor来实现虚拟机挂载磁盘。**

![image-20240724205116399](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240724205116399.png?raw=true)







```apl
[root@Openstack01 ~(keystone_memeda)]# vgs
  Configuration setting "snapshot_autoextend_percent" invalid. It's not part of any section.
  Configuration setting "snapshot_autoextend_threshold" invalid. It's not part of any section.
  VG             #PV #LV #SN Attr   VSize    VFree
  cinder-volumes   1   2   0 wz--n-  <20.60g 1012.00m
  cs               1   3   0 wz--n- <199.00g       0
[root@Openstack01 ~(keystone_memeda)]# lvs
  Configuration setting "snapshot_autoextend_percent" invalid. It's not part of any section.
  Configuration setting "snapshot_autoextend_threshold" invalid. It's not part of any section.
  LV                                          VG             Attr       LSize   Pool                Origin Data%  Meta%  Move Log Cpy%Sync Convert
  cinder-volumes-pool                         cinder-volumes twi-aotz--  19.57g                            1.79   11.04
  volume-295dc8ca-5e61-48ab-9676-4392bcd7f357 cinder-volumes Vwi-a-tz--   5.00g cinder-volumes-pool        7.00
  home                                        cs             -wi-ao---- 125.06g
  root                                        cs             -wi-ao----  70.00g
  swap                                        cs             -wi-ao----   3.93g

```

![image-20240724002335507](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724002335507.png?raw=true)

![image-20240724002402415](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724002402415.png?raw=true)

![image-20240724002428165](D:\桌面\桌面\护网\https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack\image-20240724002428165.png?raw=true)





### 对象存储Swift

### Cinder对接NFS

| 主机           | 服务        |
| -------------- | ----------- |
| 192.168.71.70  | Openatsck01 |
| 192.168.71.71  | Openatsck02 |
| 192.168.71.101 | NFS         |

#### NFS操作

```apl
[root@es02 ~]# df -hT
文件系统                类型      容量  已用  可用 已用% 挂载点
devtmpfs                devtmpfs  1.9G     0  1.9G    0% /dev
tmpfs                   tmpfs     1.9G     0  1.9G    0% /dev/shm
tmpfs                   tmpfs     1.9G   12M  1.9G    1% /run
tmpfs                   tmpfs     1.9G     0  1.9G    0% /sys/fs/cgroup
/dev/mapper/centos-root xfs        46G  1.9G   44G    5% /
/dev/sda1               xfs      1014M  151M  864M   15% /boot
tmpfs                   tmpfs     378M     0  378M    0% /run/user/0
/dev/sdb1               xfs        50G   33M   50G    1% /xyz
[root@es02 ~]# blkid | grep sdb1
/dev/sdb1: UUID="ddd56938-6f03-44a8-8ab4-f19df0f03763" TYPE="xfs"

[root@es02 ~]# yum -y install nfs-utils
[root@es02 ~]# cat /etc/exports
/xyz *(rw)
[root@es02 ~]# systemctl restart nfs
[root@es02 ~]# exportfs -s
/xyz  *(sync,wdelay,hide,no_subtree_check,sec=sys,rw,secure,root_squash,no_all_squash)
[root@es02 ~]# chmod -R 777 /xyz/
```

#### Openstack01 操作

**配置NFS**

```apl
[root@Openstack01 cinder]# mount -t nfs 192.168.71.101:/xyz /mnt
[root@Openstack01 cinder]# cat cindernfs
192.168.71.101:/xyz
[root@Openstack01 cinder]# chown cinder.root cindernfs
[root@Openstack01 cinder]# chmod 640 cindernfs
```

**修改Cinder配置文件**

```apl
[root@Openstack01 cinder]# pwd
/etc/cinder
[root@Openstack01 cinder]# vim cinder.conf

436 enabled_backends=lvm,memeda
5269 [memeda]
5270 nfs_shares_config = /etc/cinder/cindernfs
5271 volume_driver = cinder.volume.drivers.nfs.NfsDriver
5272 volume_backend_name = bkdmemeda
[root@Openstack01 cinder]# systemctl restart openstack-cinder*

[root@Openstack01 cinder(keystone_admin)]# cinder type-create NFS
+--------------------------------------+------+-------------+-----------+
| ID                                   | Name | Description | Is_Public |
+--------------------------------------+------+-------------+-----------+
| 4abcf534-43de-4e47-889a-a24b7dbf2115 | NFS  | -           | True      |
+--------------------------------------+------+-------------+-----------+

```

#### 图形化创建NFS-ECS

![image-20240725164015673](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725164015673.png?raw=true)

![image-20240725164121063](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725164121063.png?raw=true)

**如果未来需求：想让创建的ECS，使用NFS空间。通过镜像，创建一个卷，再通过加载卷去发放云主机即可**

![image-20240725164823867](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725164823867.png?raw=true)

![image-20240725164443240](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725164443240.png?raw=true)

![image-20240725164911282](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725164911282.png?raw=true)

#### 命令行创建NFS-ECS

##### 通过Volume镜像卷创建ECS

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack flavor list;openstack image list;openstack network list;openstack subnet list;openstack security group list;openstack keypair list;openstack volume list
```



```apl
[root@Openstack01 ~(keystone_memeda)]# openstack server create --flavor x.small --volume ubuntu20.04-NFS2 --min 1 --security-group sec001 --nic net-id=eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 volume_ECS03
```

![image-20240725171015627](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725171015627.png?raw=true)

##### 通过image 创建ECS(图形化看不到存储)

>注意：命令行方式创建ecs的时候，如果没有添加参数 --boot-from-volume 5 ，那么创建好的ecs，在界面上看不到创建的卷（没有使用后端对接的卷，而是在ecs所在的主机上创建的本地盘）

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack server create --flavor x.small --image ubuntu20.04 --min 1 --security-group sec001 --nic net-id=eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 image_ECS04
```

>如果带上参数，`--boot-from-volume`

##### 通过image 创建ECS(图形化可以看到存储)

```apl
[root@Openstack01 ~(keystone_memeda)]# openstack server create --flavor x.small --image ubuntu20.04 --min 1 --security-group sec001 --nic net-id=eac2fd4b-ad62-4cfd-a60c-8722c85eaad3 --boot-from-volume 3  image_ECS05
```

![image-20240725171851283](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725171851283.png?raw=true)

## 镜像管理Glance

### Glanche简介

![image-20240725151433240](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725151433240.png?raw=true)

### Glance在Openstack中的定位

> - 目前数据资产包括：
>   - 镜像：Glance镜像服务包括发现、注册和检索VM镜像。Glance有一个RESTful API，允许查询VM镜像元数据以及检索实际镜像。通过Glance提供的VM镜像可以存储在各种位置，从简单的文件系统到Swift等对象存储系统。
>   - 元数据定义：Glance托管一个metadefs目录。这为OpenStack社区提供了一种以编程方式确定可应用于OpenStack资源的各种元数据键名和有效值的方法。我们在这里谈论的只是一个目录，除非使用负责这些资源的服务提供的 API 或客户端工具将键和值应用于各个OpenStack资源，否则键和值实际上不会做任何事情。

![image-20240725151929502](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725151929502.png?raw=true)

### Glance作用

> - 在OpenStack上创建虚拟机时，必须为其选择需要安装的操作系统，glance服务就是为该选择提供不同的操作系统镜像。
>
> - 镜像的元数据保存在数据库中，而镜像本身是通过Glance Store Drivers存放到各种backend store中。

![image-20240725152036943](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152036943.png?raw=true)

### Glance与其他服务的交互

![image-20240725152128869](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152128869.png?raw=true)

### Glance架构

![image-20240725152257509](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152257509.png?raw=true)

#### Glance各组件作用

>- Client：使用Glance服务的应用程序，可以是命令行工具、horizon、nova等。
>- REST API：Glance是一个client-server架构，提供一个REST API，而使用者就是通过REST API来执行关于镜像的各种操作。
>- Glance Domain Controller：是Glance内主要的中间件实现，就相当于一调度员，作用是将Glance内部服务的操作分发到各层（Auth认证、Notifier、Policy策略、Quota、Location及DB数据库连接）具体任务由每个层实现。
>- Registry Layer：属于可选的层，用来组织安全。通过使用这个单独的服务，来控制Glance Domain Controller与Glance DB之间的通信。
>- Glance DB：Glance服务Database Abstraction Layer (DAL) -数据库抽象层。使用一个核心库Glance DB，该库对Glance内部所有依赖数据库的组件来说是共享的。
>- Glance Store：用来组织处理Glance和各种存储后端的交互。所有的镜像文件操作都是通过调用Glance Store库执行的，它负责与外部存储端或本地文件系统的交互。Glance Store提供了一个统一的接口来访问后端存储。

![image-20240725152500716](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152500716.png?raw=true)

![image-20240725152520665](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152520665.png?raw=true)

### Glance工作与案例和流程

#### 镜像-规格

![image-20240725152657858](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152657858.png?raw=true)



磁盘格式

> - 容器格式是指虚拟机镜像是否采用还包含有关实际虚拟机的元数据的文件格式。
>
> - 需要注意的是：容器格式字符串在当前并不会被glance或其他OpenStack组件使用，所以如果你不确定，将容器格式指定为bare是安全的。

![image-20240725152746195](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725152746195.png?raw=true)

##### 状态机

>- queued：没有上传image数据，只有db中的元数据。
>
>- saving：正在上传image data，当注册一个镜像使用POST  /images并且当前携带了一个x-image-meta-location头，这个镜像将不会进入saving状态(镜像的数据已经是可以获得的，不能重传)。
>- active：当镜像数据上传完毕，镜像就可以被使用了(可获得的)，此时处于active状态。
>- deactivated：表示任何非管理员用户都无权访问镜像数据，禁止下载镜像，也禁止像镜像导出和镜像克隆之类的操作（请求镜像数据的操作）。
>- killed：表示上传过程中发生错误，并且镜像是不可读的。
>- deleted：glance已经保存了该镜像的数据，但是该镜像不再可用，处于该状态的镜像将在不久后被自动删除。
>- pending_delete： 与deleted相似，glance还没有清除镜像数据，只是处于该状态的镜像不可恢复。

![image-20240725153211075](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725153211075.png?raw=true)

**状态机转化图**

![image-20240725153818775](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725153818775.png?raw=true)

##### 镜像与实例交互

>- Glance store包含一定数量的镜像，计算节点包含可用的vCPU，内存和本地磁盘资源，Cinder-volume包含一定数量的卷。

![image-20240725154103071](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725154103071.png?raw=true)

---

> - 启动实例时，需要选择一个镜像，规格和任何可选属性。选定的规格提供一个系统盘，标记为vda，另外一个临时盘被标记为vdb，cinder-volume提供的卷被映射到第三个虚拟磁盘并将其称为vdc。
> - 镜像服务将基本镜像从镜像存储复制到本地磁盘。vda是实例访问的第一个磁盘。如果镜像文件越小，则通过网络复制的数据越少，实例启动就会越快。
> - 实例启动时还会创建一块空的临时磁盘vdb，删除实例时将删除此磁盘。
> - 计算节点使用iSCSI 连接到cinder-volume提供的某个卷。该卷被映射到第三个磁盘vdc。计算节点为实例提供vCPU和内存资源后，实例将从根卷vda启动。该实例运行并更改磁盘上的数据（图中红色标示磁盘）。
> - 如果cinder-volume位于单独的网络上，则存储节点配置文件中my_block_storage_ip选项会将镜像流量定向到计算节点。
> -  注意：
>   - 此示例场景中的某些详细信息可能与实际环境不同。例如，可以使用不同类型的后端存储或不同的网络协议。常见的一种场景是vda，vdb存放在SAN存储，而不是本地磁盘上。

![image-20240725154630859](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725154630859.png?raw=true)

---

> - 实例被删除后, 除cinder-volume卷之外的其他资源都会被回收。临时磁盘无论是否加密过，都将会被清空，内存和vCPU资源将会被释放。在这个过程中镜像不会发生任何改变。
> - 注意：
>   - 如果创建实例时选择了“删除实例时删除卷”，则实例删除时，cinder-volume卷也会被删除。

![image-20240725154745319](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725154745319.png?raw=true)

#### Glance镜像制作

##### 直接下载镜像

>镜像的具体下载链接，请参考OpenStack社区网站：https://docs.openstack.org/image-guide/obtain-images.html。

![image-20240725155155744](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725155155744.png?raw=true)

---

##### 手动制作镜像

>Virt-manager是一套图形化的虚拟机管理工具，提供虚拟机管理的基本功能，如开机、挂起、重启、关机、强制关机/重启、迁移等。

![image-20240725155254695](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725155254695.png?raw=true)

##### 镜像转换

![image-20240725155335615](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725155335615.png?raw=true)

### Glance 对接Swift

#### 查看Mysql—Glance存储

```apl
[root@Openstack01 ~]# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 80184
Server version: 10.3.28-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| aodh               |
| cinder             |
| glance             |
| gnocchi            |
| heat               |
| information_schema |
| keystone           |
| mysql              |
| neutron            |
| nova               |
| nova_api           |
| nova_cell0         |
| performance_schema |
| placement          |
| test               |
+--------------------+
15 rows in set (0.012 sec)

MariaDB [(none)]> use glance;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [glance]> desc image_locations;
+------------+-------------+------+-----+---------+----------------+
| Field      | Type        | Null | Key | Default | Extra          |
+------------+-------------+------+-----+---------+----------------+
| id         | int(11)     | NO   | PRI | NULL    | auto_increment |
| image_id   | varchar(36) | NO   | MUL | NULL    |                |
| value      | text        | NO   |     | NULL    |                |
| created_at | datetime    | NO   |     | NULL    |                |
| updated_at | datetime    | YES  |     | NULL    |                |
| deleted_at | datetime    | YES  |     | NULL    |                |
| deleted    | tinyint(1)  | NO   | MUL | NULL    |                |
| meta_data  | text        | YES  |     | NULL    |                |
| status     | varchar(30) | NO   |     | active  |                |
+------------+-------------+------+-----+---------+----------------+
9 rows in set (0.012 sec)

MariaDB [glance]> select id,value,status from image_locations;
+----+--------------------------------------------------------------------+---------+
| id | value                                                              | status  |
+----+--------------------------------------------------------------------+---------+
|  1 | file:///var/lib/glance/images/b4451483-4bf2-4051-af50-8bc428f78555 | deleted |
|  2 | file:///var/lib/glance/images/4ceb01b5-f524-43f2-9347-a048eb930726 | active  |
+----+--------------------------------------------------------------------+---------+
2 rows in set (0.000 sec)

MariaDB [glance]> exit
Bye
[root@Openstack01 ~]# ls /var/lib/glance/images/ -lh
total 21M
-rw-r-----. 1 glance glance 21M Jul 23 22:59 4ceb01b5-f524-43f2-9347-a048eb930726
[root@Openstack01 ~]#

```

![image-20240725173329716](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725173329716.png?raw=true)

#### 配置Glance镜像文件

>现在glance是使用的本地FS空间，现在要把glance对接到swift里面。
>
>操作：找到glance配置文件 /etc/glance/glance-api.conf
>
>修改的所有参数，都在3000行以后。

```apl
3057 stores=file,http,swift glance支持的后端类型
3111 default_store=swift 默认使用的后端类型
3982 swift_store_region = RegionOne  更改Region名称，默认存储区域
4032 swift_store_endpoint_type = publicURL 使用存储端点（访问的url）
4090 swift_store_container = glance 容器前缀名，上传镜像，会以这个名字带上随机字符创建一个容器，在容器里面保存上传的镜像。
4118 swift_store_large_object_size = 5120 单个文件最大不能超过5G大小
4142 swift_store_large_object_chunk_size = 200 大对象按照多大进行切分MB
4160 swift_store_create_container_on_put = true 是否自动创建容器
4182 swift_store_multi_tenant = true 是否启用多租户
4230 swift_store_admin_tenants = services 输入swift用户所在的项目名称
4382 swift_store_auth_version = 2 身份认证服务版本，2和3都表示用keystone
4391 swift_store_auth_address = http://192.168.100.201:5000/v3 身份认证地址，这个地址可以在你的环境变量配置文件里面获取
4399 swift_store_user = swift swift对象存储默认用哪个用户管理swift
4408 swift_store_key = 623967b5afbf4eb0
```

**重启Glance**

```apl
[root@Openstack01 glance]# systemctl restart openstack-glance*
[root@Openstack01 glance]# systemctl status openstack-glance*
● openstack-glance-api.service - OpenStack Image Service (code-named Glance) API server
   Loaded: loaded (/usr/lib/systemd/system/openstack-glance-api.service; enabled; vendor preset: d>
   Active: active (running) since Thu 2024-07-25 19:19:03 CST; 1s ago
 Main PID: 139272 (glance-api)
    Tasks: 5 (limit: 24686)
   Memory: 100.9M
   CGroup: /system.slice/openstack-glance-api.service
           ├─139272 /usr/bin/python3 /usr/bin/glance-api
           ├─139278 /usr/bin/python3 /usr/bin/glance-api
           ├─139279 /usr/bin/python3 /usr/bin/glance-api
           ├─139280 /usr/bin/python3 /usr/bin/glance-api
           └─139281 /usr/bin/python3 /usr/bin/glance-api

Jul 25 19:19:03 Openstack01 systemd[1]: Started OpenStack Image Service (code-named Glance) API se>
[root@Openstack01 glance]#

```

#### 图形化创建Image测试

![image-20240725192519460](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725192519460.png?raw=true)

![image-20240725192803828](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725192803828.png?raw=true)

![image-20240725193205939](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725193205939.png?raw=true)

#### 查看后端Swift存储

![image-20240725193810335](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240725193810335.png?raw=true)

### 配置KVM

#### 安装Cloud-init

```apl
[root@kvm ~]# yum -y install cloud-utils-growpart cloud-init
```



```apl
[root@kvm ~]# virt-sysprep -d q
[root@kvm ~]# virsh list --all
 Id    名称                         状态
----------------------------------------------------
 1     BIOS-centos7.9-52-目标端    running
 2     UEFI-centos7.9-50              running
 -     centos7.9                      关闭
 -     generic                        关闭
 -     UEFI-centos7.9-51              关闭
 -     UEFI-centos7.9-51-目标端    关闭

[root@kvm ~]# virt-sysprep -d generic
[   0.0] Examining the guest ...
[   4.7] Performing "abrt-data" ...
[   4.7] Performing "backup-files" ...
[   5.6] Performing "bash-history" ...
[   5.6] Performing "blkid-tab" ...
[   5.6] Performing "crash-data" ...
[   5.6] Performing "cron-spool" ...
[   5.6] Performing "dhcp-client-state" ...
[   5.6] Performing "dhcp-server-state" ...
[   5.6] Performing "dovecot-data" ...
[   5.7] Performing "logfiles" ...
[   5.7] Performing "machine-id" ...
[   5.7] Performing "mail-spool" ...
[   5.7] Performing "net-hostname" ...
[   5.7] Performing "net-hwaddr" ...
[   5.7] Performing "pacct-log" ...
[   5.7] Performing "package-manager-cache" ...
[   5.8] Performing "pam-data" ...
[   5.8] Performing "passwd-backups" ...
[   5.8] Performing "puppet-data-log" ...
[   5.8] Performing "rh-subscription-manager" ...
[   5.8] Performing "rhn-systemid" ...
[   5.8] Performing "rpm-db" ...
[   5.8] Performing "samba-db-log" ...
[   5.8] Performing "script" ...
[   5.8] Performing "smolt-uuid" ...
[   5.8] Performing "ssh-hostkeys" ...
[   5.8] Performing "ssh-userdir" ...
[   5.8] Performing "sssd-db-log" ...
[   5.8] Performing "tmp-files" ...
[   5.8] Performing "udev-persistent-net" ...
[   5.8] Performing "utmp" ...
[   5.8] Performing "yum-uuid" ...
[   5.8] Performing "customize" ...
[   5.8] Setting a random seed
[   5.9] Setting the machine ID in /etc/machine-id
[   5.9] Performing "lvm-uuids" ...
[root@kvm ~]# virsh domblklist generic
目标     源
------------------------------------------------
hda        /var/lib/libvirt/images/generic.qcow2
hdb        -

[root@kvm ~]# virt-sparsify --compress /var/lib/libvirt/images/generic.qcow2 /data/data_kvm/iso/cenots7.9-sparsify.qcow2
[   0.0] Create overlay file in /tmp to protect source disk
[   0.1] Examine source disk
[   3.7] Fill free space in /dev/centos/root with zero
 100% ⟦▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒⟧ 00:00
[  12.4] Clearing Linux swap on /dev/centos/swap
[  14.1] Fill free space in /dev/sda1 with zero
[  15.6] Copy to destination and make sparse
[  76.1] Sparsify operation completed with no errors.
virt-sparsify: Before deleting the old disk, carefully check that the
target disk boots and works correctly.
[root@kvm ~]# ls /data/data_kvm/iso/
cenots7.9-sparsify.qcow2      qianyi-centos.qcow2
CentOS-7-x86_64-DVD-2009.iso  ubuntu-16.04.7-server-amd64.iso

```

![image-20240726141025769](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141025769.png?raw=true)



![image-20240726141228300](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141228300.png?raw=true)

![image-20240726141244978](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141244978.png?raw=true)

![image-20240726141300720](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141300720.png?raw=true)

![image-20240726141313753](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141313753.png?raw=true)

![image-20240726141338491](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141338491.png?raw=true)

![image-20240726141708616](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141708616.png?raw=true)

![image-20240726142158917](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726142158917.png?raw=true)

![image-20240726141843764](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726141843764.png?raw=true)

## 编排管理heat

> - 本篇将通过编写 yaml [注意读音：耶某] 来自油管文件，使用编排堆栈让 heat 根据文件内容自动创建私网、安全组、密钥对、虚拟路由、网关、接口、EIP、云主机，并为云主机分配 EIP
> - OpenStack 实验采用的版本为 Victoria 版，您可参考下方相关文章 G033 完成 OpenStack 环境搭建
> - OpenStack 基本操作本篇不再赘述，将认为您已掌握基本操作，您可参考 G034/G035 两篇文章完成基本操作学习
> - 为有更好的浏览体验，您可以点击文章左上方目录按钮来显示文章整体目录结构

官方地址：https://docs.openstack.org/heat/latest/

参考：https://docs.openstack.org/heat/latest/template_guide/basic_resources.html#

### 创建公共资源

>用 admin 用户使用图形界面或命令行先把公共资源创建出来

#### 创建租户和用户

![image-20240726143718556](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726143718556.png?raw=true)

![image-20240726143631634](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726143631634.png?raw=true)

#### 创建规格

![image-20240726145958431](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726145958431.png?raw=true)

#### 创建公网

![image-20240726144444396](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726144444396.png?raw=true)

### 编辑模板

> - yaml 缩进不要用 Tab 键，要用 空格！空格！！空格！！！ parameters 段落中 image_name_1 和 public_net 对应的 default 值，需要自行查询公网ID和镜像ID替换下

![image-20240726150533910](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726150533910.png?raw=true)

### 切换普通用户

#### 切换普通用户登录



![image-20240726145254511](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726145254511.png?raw=true)

![image-20240726150712684](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726150712684.png?raw=true)

![image-20240726151121007](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726151121007.png?raw=true)

![image-20240726151021591](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726151021591.png?raw=true)

![image-20240726151137223](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726151137223.png?raw=true)

```apl
heat_template_version: 2018-08-31

description: Simple template to deploy a stack with two virtual machine instances

parameters:
  image_name_1: 
    type: string 
    label: Image ID 
    description: SCOIMAGE Specify an image name for instance1 
    default: 4ceb01b5-f524-43f2-9347-a048eb930726

  public_net:
    type: string
    label: Network ID
    description: SCONETWORK Network to be used for the compute instance
    default: aff5cbe2-b12f-49a2-91ad-e960803ea46d

resources:
  mykey:
    type: OS::Nova::KeyPair
    properties:
      save_private_key: true
      name: mykey

  web_secgroup:
    type: OS::Neutron::SecurityGroup
    properties:
      rules:
        - protocol: tcp
          remote_ip_prefix: 0.0.0.0/0
          port_range_min: 22
          port_range_max: 22
        - protocol: icmp

  private_net:
    type: OS::Neutron::Net
    properties: 
      name: private_net

  private_subnet:
    type: OS::Neutron::Subnet
    properties: 
      network_id: { get_resource: private_net }
      cidr: "192.168.66.0/24"
      ip_version: 4
  
  vrouter:
    type: OS::Neutron::Router
    properties: 
      external_gateway_info: 
        network: { get_param: public_net }

  vrouter_interface:
    type: OS::Neutron::RouterInterface
    properties:
      router_id: { get_resource: vrouter }
      subnet_id: { get_resource: private_subnet }

  instance_port:
    type: OS::Neutron::Port
    properties:
      network: { get_resource: private_net }
      security_groups: 
        - default
        - { get_resource: web_secgroup }
      fixed_ips:
        - subnet_id: { get_resource: private_subnet }
  
  floating_ip:
    type: OS::Neutron::FloatingIP
    properties:
      floating_network_id: { get_param: public_net }

  association:
    type: OS::Neutron::FloatingIPAssociation
    properties:
      floatingip_id: { get_resource: floating_ip }
      port_id: { get_resource: instance_port }

  instance1: 
    type: OS::Nova::Server 
    properties:
      image: { get_param: image_name_1 }
      key_name: { get_resource: mykey }
      flavor: w.smail
      networks:
      - port : { get_resource : instance_port }

outputs:
  private_key:
    description: Private key
    value: { get_attr: [ mykey, private_key ] }
```

## 认证管理Keystone

### Keystone简介

#### 认证服务Kestone

![image-20240729155451746](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729155451746.png?raw=true)

#### Keystone在Openstack中的定位

![image-20240729155520792](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729155520792.png?raw=true)

#### Keystone基本概念

![image-20240729155546727](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729155546727.png?raw=true)

> - Domain：一个域可以对应一个大的机构、一个数据中心，并且必须全局唯一。云的终端用户可以在自己的Domain中创建多个Project、User、Group和Role。具备对多个Project进行统一管理的能力。
> - User：Keystone会通过认证信息（Credential，如密码等）验证用户请求的合法性，通过验证的用户将会分配到一个特定的令牌，该令牌可以被当作后续资源访问的一个通行证，并非全局唯一，只需要在域内唯一即可。
> - Group：用户组是一组User的容器，可以向Group中添加用户，并直接给Group分配角色，在这个Group中的所有用户就拥有了Group所拥有的角色权限。通过引入Group的概念，Keystone实现了对用户组的管理，达到了同时管理一组用户权限的目的。
> - Project：项目是各个服务中的一些可以访问的资源集合。我们需要在创建虚拟机时指定某个项目，在Cinder创建卷时也需要指定具体的项目。用户总是被默认绑定到某些项目上，在用户访问项目的资源前，必须具有对该项目的访问权限，或者说在特定项目下被赋予了特定的角色。项目不必全局唯一，只需要在某个域下唯一即可。
> - Role：一个用户所具有的角色，角色不同意味着被赋予的权限不同，只有知道用户被赋予的角色才能知道该用户是否有权限访问某资源。用户可以被赋予一个域或项目内的角色。一个用户被赋予域的角色意味着他对域内所有的项目都具有相同的角色，而特定项目的角色只具有对特定项目的访问权限。角色可以被继承，在一个项目树下，拥有父项目的访问权限也意味着同时拥有对子项目的访问权限。角色必须全局唯一。
> - Service：服务，如Nova、Swift、Glance、Cinder等。一个服务可以根据User、Tenant和Role确认当前用户是否具有访问其资源的权限。服务会对外暴露一个或多个端点，用户可以通过这些端点访问资源并执行操作。
> - Endpoint：端点，是指一个可以用来访问某个具体服务的网络地址，我们可以将端点理解为服务的访问点。如果我们需要访问一个服务，就必须知道它的Endpoint。一般以一个URL地址来表示一个端点。
> - Token：令牌，令牌是允许访问特定资源的凭证。无论通过何种方式，Keystone的最终目的都是对外提供一个可以访问资源的令牌。
> - Credential：凭证，确认用户身份的数据，如用户的用户名和密码。

![image-20240729160120289](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729160120289.png?raw=true)

#### Keyston在Openstack中的作用

![image-20240729160201519](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729160201519.png?raw=true)

> - Keystone作为OpenStack中一个独立的提供安全认证的模块，主要负责OpenStack用户的身份认证、令牌管理、提供访问资源的服务目录，以及基于用户角色的访问控制。
> - 用户访问系统的用户名和密码是否正确，令牌的发放，服务端点的注册，以及该用户是否具有访问特定资源的权限等都离不开Keystone服务的参与。
> - Identity：身份服务，提供身份验证凭证及有关用户和用户组数据。
> - Token：令牌，Keystone在确认用户的身份后，会给用户提供一个核实身份且可以用于后续资源请求的令牌。
> - Catalog：对外提供一个服务的查询目录，服务目录存储了OpenStack所有服务的Endpoint信息。
> - Policy：安全策略或者访问控制，一个基于规则的身份验证引擎，通过配置文件来定义各种动作与用户角色的匹配关系。
> - Resource：提供关于Domain和Project的数据。
> - Assignment：提供关于Role和Role Assignment的数据，负责角色授权。

### Keystone架构

#### Keystone各组件作用

![image-20240729161106234](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729161106234.png?raw=true)

### Keystone对象模型

![image-20240729163602108](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729163602108.png?raw=true)

> - 用户登录之后通过Keystone进行发送请求登录到一个region中的不通域中，然后便可发送api请求

### Kestone工作原理和流程

![image-20240729170111069](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170111069.png?raw=true)

![image-20240729170130707](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170130707.png?raw=true)

#### 基于UUID令牌

> - 首先是UUID，Universal Unique Identifier通用唯一标识符
> - UUID是一个32 Byte长的随机字符串，不携带任何其他信息，只作为Token ID，发送请求时，将这个Token ID以X-Auth-Token的方式传入。
> - OpenStack API在收到该令牌后，会找Keystone进行令牌校验，并获取相关用户信息。

![image-20240729170236388](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170236388.png?raw=true)

#### 基于PKI令牌认证

> - PKI，Public Key Infrastructure公钥基础设施。
> - PKI的本质是基于数字签名进行验证。Keystone私钥对令牌进行数字签名，各个OpenStack服务的API server用公钥在本地验证该令牌。
> - 具体验证过程就像这张图上显示的，首先用户将用户名和密码发送给Keystone，Keystone使用私钥加密秘钥生成令牌返回给客户端。客户每次向OpenStack 发送调用资源和服务请求时会携带这个Token令牌，OpenStack 服务API会使用本地公钥对令牌进行验证。
> - 和UUID相比，PKI令牌携带更多信息，同时还附上数字签名，以支持本地认证，避免多次找Keystone进行认证。
> - 因为携带的信息较多，所以当OpenStack的规模较大时，Token所占的字节数据就超过了HTTP标准头的大小，有可能导致认证失败。

![image-20240729170327061](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170327061.png?raw=true)

>- 为了解决PKI数据较大问题，出现了另一种验证方式PKIZ。PKIZ在PKI的基础上做了压缩处理，但是压缩效果有限。
>- 一般情况下，压缩后的大小为PKI令牌的90%左右，所以最后发现效果也不是很明显。
>- 在这张图上我们可以看出，验证流程与PKI基本一致。
>- 唯一的差别是在Keystone生成Token并返回给客户端时进行了压缩。

![image-20240729170443065](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170443065.png?raw=true)

#### 基于Fernet令牌

> - UUID，PKI，PKIZ令牌都会持久存放在数据库中，累积的令牌容易导致数据库性能下降，用户需定期清理数据库中的令牌。
> - 为避免该问题，OpenStack目前版本都默认使用Fernet令牌，携带少量的用户信息，采用对称加密，无需存于数据库中，但需定期更换秘钥。
> - Fernet的验证流程第一步，用户将用户名和密码发送给Keystone，Keystone使用秘钥生成临时令牌并返回给客户端。客户每次向OpenStack发送调用资源和服务请求时，会携带这个Token令牌，OpenStack服务API接收到请求后会将Token发送到Keystone进行验证，由Keystone验证其有效性和合法性。验证成功返回信息。
> - 这个过程看似与UUID一样，但是其实是有区别的，UUID由于没有加密和解密过程，Keystone在生成token之后要本地缓存Token，方便后面验证。但是Fernet进行对等验证，无需缓存token，每次验证只需要进行解密验证即可，无需持久化存储，大小也合适，比较适合多数据中心的场景。

![image-20240729170549853](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170549853.png?raw=true)



![image-20240729170705515](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170705515.png?raw=true)

### Keyston实现认证和授权控制

>首先用户发送基本信息给Keystone，一般是用户名和密码。Keystone经过验证后会返回一个Token给用户，用户向Nova发送创建虚拟机请求，并携带Token信息，nova接收到请求后，会拿着Token去Keystone进行验证，验证成功后开始执行创建VM操作，Nova会向Glance发送申请镜像信息并携带Token，会向Neutron发送申请网络信息也会携带Token，Glance和Neutron组件接收到请求后，都会向Keystone验证Token的有效性（图中仅用了一条线表示，请注意理解），验证通过即执行相应的操作，返回完成信息，当VM创建完成后，Nova返回创建成功信息给用户，用户即可使用虚拟机。

![image-20240729170811388](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240729170811388.png?raw=true)

### 多域认证

#### 创建域

```apl
[root@Openstack01 ~]# source keystonerc_admin
[root@Openstack01 ~(keystone_admin)]# openstack domain create domain01
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| enabled     | True                             |
| id          | 72884ed926234bc6aa43f2f0a4918c7d |
| name        | domain01                         |
| options     | {}                               |
| tags        | []                               |
+-------------+----------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack domain list
+----------------------------------+----------+---------+--------------------+
| ID                               | Name     | Enabled | Description        |
+----------------------------------+----------+---------+--------------------+
| 5c758ff6a5a44532bd3b78821e2e8e4c | heat     | True    |                    |
| 72884ed926234bc6aa43f2f0a4918c7d | domain01 | True    |                    |
| default                          | Default  | True    | The default domain |
+----------------------------------+----------+---------+--------------------+

```

### 删除域

```apl
[root@Openstack01 ~(keystone_admin)]# openstack domain show domain01
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| enabled     | False                            |
| id          | 72884ed926234bc6aa43f2f0a4918c7d |
| name        | domain01                         |
| options     | {}                               |
| tags        | []                               |
+-------------+----------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack domain delete domain01
[root@Openstack01 ~(keystone_admin)]# openstack domain create domain01
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| enabled     | True                             |
| id          | 9cfc118bde474bd1a416b227dac72153 |
| name        | domain01                         |
| options     | {}                               |
| tags        | []                               |
+-------------+----------------------------------+

```

### 查询域资源

> 注意：一点创建多个域，那么查询对象资源的时候，一定要注意带上的名称，默认情况下Openstack命令查询的资源都是default下的，如果要查对应的域下资源。

```apl
[root@Openstack01 ~(keystone_admin)]# openstack user list
+----------------------------------+------------+
| ID                               | Name       |
+----------------------------------+------------+
| 773aa440724f4f819e56ca4f762d4ba6 | admin      |
| 0b314236018e416097fe984d0ee6960f | heat_admin |
| a07aece9dc41462e8bd6cdfa7c030ac8 | glance     |
| 57fb2d544ab2474c88caff2b3108f578 | cinder     |
| 12cb7199bbd14c8a938deb80c810257a | nova       |
| c39711fd2e7b48c2a58ac1a53a784dbd | placement  |
| 75175a09427e40af97ca4f11d1c0b8e4 | neutron    |
| 069bef01d66f481d8e393862f00e1449 | swift      |
| c4a1716253d14ca28c50b5c40a262c8b | heat       |
| 2118a703e2ae4a01b0501e080c6ed73a | heat-cfn   |
| 8c5644c9ec484cdbb2cd919c9f9a227f | gnocchi    |
| d221dc0badc54845afddaf49eff7c78b | ceilometer |
| 0a088296bdc440cda0d4db41e84a88a8 | aodh       |
| 97eab00287d64401bd39fc4bbb9b369e | memeda     |
| cf256816878b45be9f8a125086df1f13 | henry      |
+----------------------------------+------------+
[root@Openstack01 ~(keystone_admin)]# openstack user list --domain domain01
```

### 创建项目

```apl
[root@Openstack01 ~(keystone_admin)]# openstack project create abc --domain domain01
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| domain_id   | 9cfc118bde474bd1a416b227dac72153 |
| enabled     | True                             |
| id          | 0d27d3e709de437bb45e3ad4b754a274 |
| is_domain   | False                            |
| name        | abc                              |
| options     | {}                               |
| parent_id   | 9cfc118bde474bd1a416b227dac72153 |
| tags        | []                               |
+-------------+----------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack project list --domain domain01
+----------------------------------+------+
| ID                               | Name |
+----------------------------------+------+
| 0d27d3e709de437bb45e3ad4b754a274 | abc  |
+----------------------------------+------+

```

### 在abc项目下创建一个用户

```apl
[root@Openstack01 ~(keystone_admin)]# openstack user create --project abc --password redhat --domain domain01 abc
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| default_project_id  | 0d27d3e709de437bb45e3ad4b754a274 |
| domain_id           | 9cfc118bde474bd1a416b227dac72153 |
| enabled             | True                             |
| id                  | c79b9ab7ea7c4675afdcb0c63efdf858 |
| name                | abc                              |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
[root@Openstack01 ~(keystone_admin)]# openstack user list --domain domain01
+----------------------------------+------+
| ID                               | Name |
+----------------------------------+------+
| c79b9ab7ea7c4675afdcb0c63efdf858 | abc  |
+----------------------------------+------+

```

#### 为用户分配角色

```apl
[root@Openstack01 ~(keystone_admin)]# openstack project list --domain domain01
+----------------------------------+------+
| ID                               | Name |
+----------------------------------+------+
| 0d27d3e709de437bb45e3ad4b754a274 | abc  |
+----------------------------------+------+
[root@Openstack01 ~(keystone_admin)]# openstack role add --user abc --project 0d27d3e709de437bb45e3ad4b754a274 admin
```

#### 启用多域登录

> 严格区分大小写

```apl
[root@Openstack01 openstack-dashboard(keystone_admin)]# pwd
/etc/openstack-dashboard
[root@Openstack01 openstack-dashboard(keystone_admin)]# vim local_settings

 83 OPENSTACK_KEYSTONE_MULTIDOMAIN_SUPPORT = True
 89 OPENSTACK_KEYSTONE_DEFAULT_DOMAIN = 'Default'

[root@Openstack01 openstack-dashboard(keystone_admin)]# systemctl restart httpd
```

> 区域：domain01
>
> 用户名：abc
>
> 密码：redhat

![image-20240726193859811](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726193859811.png?raw=true)

![image-20240726194128331](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726194128331.png?raw=true)



### 改在目录

```apl
nvme0n2                                        259:3    0    20G  0 disk
├─nvme0n2p1                                    259:7    0    10G  0 part /aaa
└─nvme0n2p2                                    259:8    0    10G  0 part /bbb
[root@Openstack01 node]# df -hT
Filesystem          Type      Size  Used Avail Use% Mounted on
devtmpfs            devtmpfs  3.4G     0  3.4G   0% /dev
tmpfs               tmpfs     3.4G  4.0K  3.4G   1% /dev/shm
tmpfs               tmpfs     3.4G   18M  3.4G   1% /run
tmpfs               tmpfs     3.4G     0  3.4G   0% /sys/fs/cgroup
/dev/mapper/cs-root xfs        70G   28G   43G  40% /
tmpfs               tmpfs     693M     0  693M   0% /run/user/0
/dev/nvme0n1p1      xfs      1014M  188M  827M  19% /boot
/dev/mapper/cs-home xfs       126G  925M  125G   1% /home
/dev/nvme0n2p1      xfs        10G  104M  9.9G   2% /srv/node/aaa
/dev/nvme0n2p2      xfs        10G  104M  9.9G   2% /srv/node/bbb
```

### 卸载swift存储

```apl
[root@Openstack01 ~]# umount /srv/node/swiftloopback/
[root@Openstack01 ~]# vim /etc/fstab
#/srv/loopback-device/swiftloopback     /srv/node/swiftloopback ext4    noatime,nodiratime,nofail,loop,user_xattr       0       0
注释掉
```

```apl
[root@Openstack01 node]# ll
total 0
drwxr-xr-x  2 root  root  6 Jul 26 20:13 aaa
drwxr-xr-x  2 root  root  6 Jul 26 20:13 bbb
drwxr-xr-x. 2 swift swift 6 Jul 11 12:51 swiftloopback
[root@Openstack01 node]# chown swift.swift aaa/ bbb/
[root@Openstack01 node]# ll
total 0
drwxr-xr-x  2 swift swift 6 Jul 26 20:13 aaa
drwxr-xr-x  2 swift swift 6 Jul 26 20:13 bbb
drwxr-xr-x. 2 swift swift 6 Jul 11 12:51 swiftloopback
```

### 创建builder

> 这个builder是为后续创建ring使用的。

```apl
[root@Openstack01 node]# cd /etc/swift/
[root@Openstack01 swift]# ls
account.builder            container.ring.gz      object-server
account.ring.gz            container-server       object-server.conf
account-server             container-server.conf  proxy-server
account-server.conf        internal-client.conf   proxy-server.conf
backups                    object.builder         swift.conf
container.builder          object-expirer.conf
container-reconciler.conf  object.ring.gz
[root@Openstack01 swift]# mv account.builder account.builder.bak
[root@Openstack01 swift]# mv account.ring.gz account.ring.gz.bak
[root@Openstack01 swift]# mv container.builder container.builder.bak
[root@Openstack01 swift]# mv container.ring.gz container.ring.gz.bak
[root@Openstack01 swift]# mv object.builder object.builder.bak
[root@Openstack01 swift]# mv object.ring.gz object.ring.gz.bak
```

#### 创建新的builder

> 12表示2 的12次方，未来将ring切分成多少均等分。
>
> 2表示是副本数
>
> 1表示小时数，代表未来规则一定创建，1小时内不能修改，修改会报错

```apl
[root@Openstack01 swift]# swift-ring-builder container.builder create 12 2 1
[root@Openstack01 swift]# swift-ring-builder account.builder create 12 2 1
[root@Openstack01 swift]# swift-ring-builder object.builder create 12 2 1

```





```apl
[root@Openstack01 swift]# head account-server.conf                                 [DEFAULT]
devices = /srv/node
bind_ip = 192.168.71.70
bind_port = 6002
mount_check = true
user = swift
workers = 2
log_name = account-server
log_facility = LOG_LOCAL2
log_level = INFO

[root@Openstack01 swift]# swift-ring-builder account.builder add z1-192.168.71.70:6002/aaa 100
WARNING: No region specified for z1-192.168.71.70:6002/aaa. Defaulting to region 1.
Device d0r1z1-192.168.71.70:6002R192.168.71.70:6002/aaa_"" with 100.0 weight got id 0

[root@Openstack01 swift]# swift-ring-builder account.builder add z2-192.168.71.70:6002/bbb 100
WARNING: No region specified for z2-192.168.71.70:6002/bbb. Defaulting to region 1.
Device d1r1z2-192.168.71.70:6002R192.168.71.70:6002/bbb_"" with 100.0 weight got id 1

```



```apl
[root@Openstack01 swift]# head container-server.conf                               [DEFAULT]
devices = /srv/node
bind_ip = 192.168.71.70
bind_port = 6001
mount_check = true
user = swift
log_name = container-server
log_facility = LOG_LOCAL2
log_level = INFO
log_address = /dev/log
[root@Openstack01 swift]# swift-ring-builder container.builder add z1-192.168.71.70:6001/aaa 100
WARNING: No region specified for z1-192.168.71.70:6001/aaa. Defaulting to region 1.
Device 0 already uses 192.168.71.70:6001/aaa.
The on-disk ring builder is unchanged.

[root@Openstack01 swift]# swift-ring-builder container.builder add z2-192.168.71.70:6001/bbb 100
WARNING: No region specified for z2-192.168.71.70:6001/bbb. Defaulting to region 1.
Device d1r1z2-192.168.71.70:6001R192.168.71.70:6001/bbb_"" with 100.0 weight got id 1

```



```apl
[root@Openstack01 swift]# head -10 object-server.conf
[DEFAULT]
devices = /srv/node
bind_ip = 192.168.71.70
bind_port = 6000
mount_check = true
servers_per_port = 0
user = swift
log_name = object-server
log_facility = LOG_LOCAL2
log_level = INFO
[root@Openstack01 swift]# swift-ring-builder object.builder add z1-192.168.71.70:6000/aaa 100
WARNING: No region specified for z1-192.168.71.70:6000/aaa. Defaulting to region 1.
Device d0r1z1-192.168.71.70:6000R192.168.71.70:6000/aaa_"" with 100.0 weight got id 0
[root@Openstack01 swift]# swift-ring-builder object.builder add z2-192.168.71.70:6000/bbb 100
WARNING: No region specified for z2-192.168.71.70:6000/bbb. Defaulting to region 1.
Device d1r1z2-192.168.71.70:6000R192.168.71.70:6000/bbb_"" with 100.0 weight got id 1
```



### 再平衡

```apl
[root@Openstack01 swift]# swift-ring-builder account.builder rebalance
Reassigned 8192 (200.00%) partitions. Balance is now 0.00.  Dispersion is now 0.00
[root@Openstack01 swift]# swift-ring-builder container.builder rebalance
Reassigned 8192 (200.00%) partitions. Balance is now 0.00.  Dispersion is now 0.00
[root@Openstack01 swift]# swift-ring-builder object.builder rebalance
Reassigned 8192 (200.00%) partitions. Balance is now 0.00.  Dispersion is now 0.00
[root@Openstack01 swift]#
```



```apl
[root@Openstack01 swift]# ls
account.builder        container-reconciler.conf  object.ring.gz
account.builder.bak    container.ring.gz          object.ring.gz.bak
account.ring.gz        container.ring.gz.bak      object-server
account.ring.gz.bak    container-server           object-server.conf
account-server         container-server.conf      proxy-server
account-server.conf    internal-client.conf       proxy-server.conf
backups                object.builder             swift.conf
container.builder      object.builder.bak
container.builder.bak  object-expirer.conf

```

![image-20240726204506668](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726204506668.png?raw=true)

![image-20240726204746659](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726204746659.png?raw=true)

![image-20240726204836287](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726204836287.png?raw=true)

![image-20240726204845970](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240726204845970.png?raw=true)

```apl
[root@Openstack01 node]# pwd
/srv/node
[root@Openstack01 node]# find . -name '*data*'
./aaa/objects/3684/49f/e6423506a11feb96c6cd294fc1fc549f/1721998069.32546.data
./aaa/objects/3014/e5e/bc69ce078dd9d5c97a3582087b93ae5e/1721998069.45090.data
./bbb/objects/3684/49f/e6423506a11feb96c6cd294fc1fc549f/1721998069.32546.data
./bbb/objects/3014/e5e/bc69ce078dd9d5c97a3582087b93ae5e/1721998069.45090.data
```

## 网络管理Neutron

### Linux网络虚拟化基础

**物理网络与虚拟化网络**

> 物理网络通过Switch交换机机型实现物理主机之间的通讯
>
> 虚拟化网络：通过OVN(sdn)下发控制命令，而OVS接受到控制命令之后，进行底层网路的操作。从而实现控制面和执行面的分离

![image-20240730113252603](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730113252603.png?raw=true)

**Linux网络虚拟化实现技术**

![image-20240730152245493](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730152245493.png?raw=true)

![image-20240730153414414](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730153414414.png?raw=true)

>- TAP/TUN提供了一台主机内用户空间的数据传输机制。它虚拟了一套网络接口，这套接口和物理的接口无任何区别，可以配置IP，可以路由流量，不同的是，它的流量只在主机内流通。
>- TAP/TUN有些许的不同，TUN只操作三层的IP包，而TAP操作二层的以太网帧。
>- Veth-Pair是成对出现的一种虚拟网络设备，一端连接着协议栈，一端连接着彼此，数据从一端出，从另一端进。它的这个特性常常用来连接不同的虚拟网络组件，构建大规模的虚拟网络拓扑，比如连接Linux Bridge、OVS、LXC容器等。一个很常见的案例就是它被用于OpenStack Neutron，构建非常复杂的网络形态。

#### Linux-bridge

![image-20240730153527505](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730153527505.png?raw=true)

> - Linux Bridge结构如上图所示，Bridge设备br0绑定了实际设备eth0与虚拟设备tap0和tap1，但是对于主机的网络协议栈上层来说，只能看到br0，并不会关心桥接的细节。
> - 当这些设备接收到数据包时，会将其提交给br0决定数据包的去向，br0会根据MAC地址与端口的映射关系进行转发。
> - 因为Bridge工作在二层，所以绑定在br0上的从设备eth0、tap0与tap1均不需要再设置IP地址，对于上层路由器来说，它们都位于同一子网，因此只需为br0设置IP地址。因为br0具有自己的IP地址，br0可以被加入路由表，并利用它来发送数据，但是最终实际的发送过程则是由某个从设备来完成。
> - 即使eth0原本具有自己的IP地址，但是在被绑定到br0上后，它的IP地址会失效，用户程序不能接收到这个IP地址的数据。只有目的地址为br0的IP地址的数据包才会被Linux接收。
> - brctl addbr BRIDGE：表示添加BRIDGE。
> - brctl addif BRIDGE DEVICE：表示添加接口到bridge。

#### Open vSwitch

![image-20240730153801772](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730153801772.png?raw=true)

> - Open vSwitch负责连接vNIC与物理网卡，同时桥接同一物理Server内的各个vNIC。其实Linux Bridge已经能够很好地充当这样的角色，为什么我们还需要Open vSwitch？
> - 因为Open vSwitch的引入使得云环境中对虚拟网络的管理及对网络状态和流量的监控变得更容易。
> - 我们可以像配置物理交换机一样，将接入Open vSwitch的各个VM分配到不同的VLAN中以实现网络的隔离。我们也可以在Open vSwitch端口上为VM配置QoS，同时Open vSwitch也支持包括NetFlow、sFlow等很多标准的管理接口和协议，我们可以通过这些接口完成流量监控等工作。
> - Open vSwitch在云环境中的各种虚拟化平台（如Xen与KVM）上实现了分布式的虚拟交换机（Distributed Virtual Switch），一个物理Server上的vSwitch可以透明地与另一个物理Server上的vSwitch连接在一起。

#### Linux网络隔离-Namespace

> - Network Namespace通常与VRF（Virtual Routing Forwarding虚拟路由和转发）一起工作，VRF是一种IP技术，允许路由表的多个实例同时在同一路由器上共存。
> - 使用VETH可以连接两个不同网络命名空间，使用Bridge可以连接多个不同网络命名空间。

![image-20240730155333564](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730155333564.png?raw=true)

![image-20240730155840227](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730155840227.png?raw=true)

### Neutron简介

![image-20240730155940823](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730155940823.png?raw=true)

#### Neutron在Openstack中的定位

> - Neutron是一个Openstack项目，用于在其他Openstack服务(例如nova)管理的接口设备(例如vNIC)之间提供"网络连接即服务"
> - OpenStack Networking （neutron）允许您创建由其他OpenStack服务管理的接口设备并将其连接到网络。可以实施插件以适应不同的网络设备和软件，为OpenStack架构和部署提供灵活性。

![image-20240730160012114](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730160012114.png?raw=true)

#### Neutron作用

> - 实际上，Neutron仅仅是一个管理系统/控制系统，它本身并不能实现任何网络功能，它仅仅是为Linux相关功能做一个配置或者驱动而已。本质上Neutron是借助Linux来实现网络功能的。
> - OpenStack所在的整个物理网络在Neutron中被泛化为网络资源池，通过对物理网络资源进行灵活的划分与管理，Neutron能够为同一物理网络上的每个租户提供独立的虚拟网络环境。

![image-20240730165211158](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730165211158.png?raw=true)

### Neutron概念

![image-20240730165304047](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730165304047.png?raw=true)

#### Network网络

![image-20240730165523423](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730165523423.png?raw=true)

> - Local：与其他网络和节点隔离。Local网络中的虚拟机只能与位于同一节点上同一网络的虚拟机通信，Local网络主要用于单机测试。
> - Flat：无VLAN tagging的网络。Flat网络中虚拟机能与位于同一网络的虚拟机通信，并可以跨多个节点。
> - VLAN：802.1q tagging网络。VLAN是一个二层的广播域，同一VLAN中的虚拟机可以通信，不同VLAN只能通过Router通信。VLAN网络可跨节点，是应用最广泛的网络类型。
> - VXLAN：基于隧道技术的overlay网络。VXLAN网络通过唯一的segmentation ID（也叫 VNI）与其他VXLAN网络区分。VXLAN中数据包会通过VNI封装成UDP包进行传输。因为二层的包通过封装在三层传输，能够克服VLAN和物理网络基础设施的限制。
> - GRE：与VXLAN类似的一种overlay网络，主要区别在于使用IP包而非UDP进行封装。
> - 生产环境中，一般使用的是VLAN、VXLAN或GRE网络。

#### Subnet

![image-20240730170042244](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730170042244.png?raw=true)

#### Port

![image-20240730170609249](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730170609249.png?raw=true)

#### Router

![image-20240730170631335](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730170631335.png?raw=true)

#### Fixed IP

![image-20240730170646255](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730170646255.png?raw=true)

#### Floating IP

![image-20240730171027859](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730171027859.png?raw=true)

#### 物理网络

![image-20240730171050346](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730171050346.png?raw=true)

#### 外网映射-Provider

![image-20240730171126295](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730171126295.png?raw=true)

#### 内部网络Self-service

![image-20240730172327513](https://github.com/liuzhenhua1223/2024-09-image/blob/master/Openstack/image-20240730172327513.png?raw=true)

### Netron架构


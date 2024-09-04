# Elasticserch 

[TOC]



# 第一章 Elasticserch概述

`ES核心`主要是为了查询：文章、视频、图片、网站信息等等

## 数据分类

### 结构化数据

> 可以以二维表表示的数据称为结构化数据，类似execl的表示方式

- 优点：方便管理、方便查询
- 缺点：现有结构，扩展比较难，

![image-20240624100856347](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624100856347.png?raw=true)

### 非机构化数据

> 以key和values进行表示的数据，无法以二维表表示
>
> - 视频、图片、文档等
> - Mongodb、redis

![image-20240624101458997](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624101458997.png?raw=true)

### 半结构化数据

>在生活中，我们搜索的数据并非都是关系型和非关系型，而是两则并行查询，那么由此`半结构化`是一个很好的解决方法，由此ES是一个比较好的选择方案

## 技术选型

### Elasticserch是什么

> `ES核心`
>
> The Elastic Stack, 包括 Elasticsearch、 Kibana、 Beats 和 Logstash（也称为 ELK Stack）。能够安全可靠地获取任何来源、任何格式的数据，然后实时地对数据进行搜索、分析和可视化。
>
> Elaticsearch，简称为 ES， ES 是一个`开源的高扩展的分布式全文搜索引擎`， 是整个 ElasticStack 技术栈的核心。
>
> 它可以近乎实时的存储、检索数据；本身扩展性很好，可以扩展到上百台服务器，处理 PB 级别的数据。

### 全文搜索引擎

> Google，百度类的网站搜索，它们都是根据网页中的关键字生成索引，我们在搜索的时候输入关键字，它们会将该关键字即索引匹配到的所有网页返回；还有常见的项目中应用日志的搜索等等。对于这些非结构化的数据文本，关系型数据库搜索不是能很好的支持。
>
> 一般传统数据库，全文检索都实现的很鸡肋，因为一般也没人用数据库存文本字段。进行全文检索需要扫描整个表，如果数据量大的话即使对 SQL 的语法优化，也收效甚微。建立了索引，但是维护起来也很麻烦，对于 insert 和 update 操作都会重新构建索引。

- 基于以上原因可以分析得出，在一些生产环境中，使用常规的搜索方式，性能是非常差的：

  - 搜索的数据对象是大量的非结构化的文本数据
  - 文件记录量打到数十万或数百万个甚至更多。
  - 支持大量基于交互式文本的查询
  - 需求非常灵活的全文搜索查询
  - 对高度相关的搜索结果的有特殊需求，但是没有可用的关系数据库可以满足。
  - 对不同记录类型、非文本数据操作或安全事务处理的需求相对较少的情况。为了解决结构化数据搜索和非结构化数据搜索性能问题，我们就需要专业，健壮，强大的全文搜索引擎 。

- >这里说到的全文搜索引擎指的是目前广泛应用的主流搜索引擎。它的工作原理是计算机索引程序通过扫描文章中的每一个词，对每一个词建立一个索引，指明该词在文章中出现的次数和位置，当用户查询时，检索程序就根据事先建立的索引进行查找，并将查找的结果反馈给用户的检索方式。这个过程类似于通过字典中的检索字表查字的过程。

### ES应用案例

- GitHub: 2013 年初，抛弃了 Solr，采取 Elasticsearch 来做 PB 级的搜索。 “GitHub 使用Elasticsearch 搜索 20TB 的数据，包括 13 亿文件和 1300 亿行代码”。
- 维基百科：启动以 Elasticsearch 为基础的核心搜索架构
- 百度：目前广泛使用 Elasticsearch 作为文本数据分析，采集百度所有服务器上的各类指标数据及用户自定义数据，通过对各种数据进行多维分析展示，辅助定位分析实例异常或业务层面异常。目前覆盖百度内部 20 多个业务线（包括云分析、网盟、预测、文库、直达号、钱包、 风控等），单集群最大 100 台机器， 200 个 ES 节点，每天导入 30TB+数据。
- 新浪：使用 Elasticsearch 分析处理 32 亿条实时日志。
- 阿里：使用 Elasticsearch 构建日志采集和分析体系。
- Stack Overflow：解决 Bug 问题的网站，全英文，编程人员交流的网站。

# 第二章Elasticserch入门

## 2.1 Elasticersh安装

官网地址：[下载 Elastic 产品 | Elastic](https://www.elastic.co/cn/downloads)

![image-20240624105442007](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624105442007.png?raw=true)

| 目录    | 含义           |
| ------- | -------------- |
| bin     | 可执行脚本目录 |
| config  | 配置目录       |
| jdk     | 内置 JDK 目录  |
| lib     | 类库           |
| logs    | 日志目录       |
| modules | 模块目录       |
| plugins | 插件目录       |

----

**注意：9300端口为Elasticserch集群组件的通讯端口，9200端口为浏览器访问的http协议RESTful端口**

## 2.2 启动ES软件

1. 进入bin目录，执行es.bak文件，执行完成后，浏览器访问 http://localhost:9200

![image-20240624111418157](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624111418157.png?raw=true)

![image-20240624111623168](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624111623168.png?raw=true)

## 2.3 ES基本操作

### 2.3.1 RESTful

> - REST 指的是一组架构约束条件和原则。满足这些约束条件和原则的应用程序或设计就是RESTful。Web 应用程序最重要的REST 原则是，客户端和服务器之间的交互在请求之间是无状态的。从客户端到服务器的每个请求都必须包含理解请求所必需的信息。如果服务器在请求之间的任何时间点重启，客户端不会得到通知。此外，无状态请求可以由任何可用服务器回答，这十分适合云计算之类的环境。客户端可以缓存数据以改进性能。
>
> - 在服务器端，应用程序状态和功能可以分为各种资源。资源是一个有趣的概念实体，它向客户端公开。资源的例子有：应用程序对象、数据库记录、算法等等。每个资源都使用URI (Universal Resource Identifier) 得到一个唯一的地址。所有资源都共享统一的接口，以便在客、户端和服务器之间传输状态。使用的是标准的HTTP 方法，比如GET、PUT、POST 和DELETE。
>
> - 在REST 样式的Web 服务中，每个资源都有一个地址。资源本身都是方法调用的目标，方法列表对所有资源都是一样的。这些方法都是标准方法，包括HTTP GET、POST、PUT、DELETE，还可能包括HEAD 和OPTIONS。简单的理解就是，如果想要访问互联网上的资源，就必须向资源所在的服务器发出请求，请求体中必须包含资源的网络路径，以
>
>   及对资源进行的操作(增删改查)。

**ES允许使用RESTful风格的API进行搜索和分析，并且es遵循于JSON格式**

- **JSON字符串：网络中传递到字符串的格式符合JSON格式**
- JAVAScript Object Notation 特殊标记的javascript对象

```json
var obj  = {"name":"zhangshan","age":30,"info":{"email":"Lzh_888888_1223@163.com"}}
var objs = [obj,obj] 
```

## 2.4Postman客户端工具

Postman是一款强大的网页调试工具，提供功能强大的WebAPI 和HTTP 请求调试。

软件功能强大，界面简洁明晰、操作方便快捷，设计得很人性化。Postman中文版能够发送

任何类型的HTTP 请求(GET, HEAD,POST, PUT..)，不仅能够表单提交，且可以附带任意类型请求体。

官网下载地址：https://www.postman.com/downloads/

## 数据格式

### 正排索引

| id   | content              |
| ---- | -------------------- |
| 1001 | my name is zhang san |
| 1002 | my name is li si     |

### 倒排索引

| keyword | id         |
| ------- | ---------- |
| name    | 1001, 1002 |
| zhang   | 1001       |

- Elasticsearch 是**面向文档型数据库**，一条数据在这里就是一个文档。 为了方便大家理解，我们将 Elasticsearch 里存储文档数据和关系型数据库 MySQL 存储数据的概念进行一个类比

- ES 里的` Index `可以看做一个库，而` Types` 相当于表， `Documents` 则相当于表的行。这里 Types 的概念已经被逐渐弱化， Elasticsearch 6.X 中，一个 index 下已经只能包含一个type， Elasticsearch 7.X 中, Type 的概念已经被删除了。

![image-20240624160625069](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624160625069.png?raw=true)

## 2.5 HTTP操作

启动ES-Postman

![image-20240624161525820](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624161525820.png?raw=true)

### 2.5.1 创建索引

对比关系数据库，创建索引就等于创建数据库

在Postman中，向ES服务器发`PUT`请求：http://127.0.0.1:9200/shopping

- 创建索引

```json
{
    "acknowledged": true,//响应结果
    "shards_acknowledged": true,//分片结果
    "index": "shopping"//索引名称
}
# 注意：创建索引库的分片数默认 1 片，在 7.0.0 之前的 Elasticsearch 版本中，默认 5 片
```

![image-20240624162946932](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624162946932.png?raw=true)

![image-20240624162952436](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624162952436.png?raw=true)

![image-20240624163002960](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624163002960.png?raw=true)

- **重复提交**

```json
{
    "error": {
        "root_cause": [
            {
                "type": "resource_already_exists_exception",
                "reason": "index [shopping/eC4Vo-uYQHiW8zkn-lRYFg] already exists",
                "index_uuid": "eC4Vo-uYQHiW8zkn-lRYFg",
                "index": "shopping"
            }
        ],
        "type": "resource_already_exists_exception",
        "reason": "index [shopping/eC4Vo-uYQHiW8zkn-lRYFg] already exists",
        "index_uuid": "eC4Vo-uYQHiW8zkn-lRYFg",
        "index": "shopping"
    },
    "status": 400
}
```

### 2.查看索引GET

#### 查看shopping

![image-20240624163143268](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624163143268.png?raw=true)

```json
{
    "shopping": {
        "aliases": {},
        "mappings": {},
        "settings": {
            "index": {
                "routing": {
                    "allocation": {
                        "include": {
                            "_tier_preference": "data_content"
                        }
                    }
                },
                "number_of_shards": "1",
                "provided_name": "shopping",
                "creation_date": "1719217452962",
                "number_of_replicas": "1",
                "uuid": "eC4Vo-uYQHiW8zkn-lRYFg",
                "version": {
                    "created": "7100299"
                }
            }
        }
    }
}
```

```json
{
 "shopping"【索引名】: { 
 "aliases"【别名】: {},
 "mappings"【映射】: {},
 "settings"【设置】: {
 "index"【设置 - 索引】: {
 "creation_date"【设置 - 索引 - 创建时间】: "1614265373911",
 "number_of_shards"【设置 - 索引 - 主分片数量】: "1",
 "number_of_replicas"【设置 - 索引 - 副分片数量】: "1",
 "uuid"【设置 - 索引 - 唯一标识】: "eI5wemRERTumxGCc1bAk2A",
 "version"【设置 - 索引 - 版本】: {
 "created": "7080099"
 },
 "provided_name"【设置 - 索引 - 名称】: "shopping"
 }
 }
 }
}
```



#### 查看所有索引

在 Postman 中，向 ES 服务器发 **GET** 请求 ：http://127.0.0.1:9200/_cat/indices?v

#### http://127.0.0.1:9200/_cat/indices?v

![image-20240624163638409](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624163638409.png?raw=true)



这里请求路径中的_cat 表示查看的意思，indices 表示索引，所以整体含义就是查看当前 ES

服务器中的所有索引，就好像 MySQL 中的 show tables 的感觉，服务器响应结果如下

```json
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   shopping eC4Vo-uYQHiW8zkn-lRYFg   1   1          0            0       208b           208b

```

![image-20240624231442806](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624231442806.png?raw=true)

### 3.删除索引 

http://127.0.0.1:9200/shopping

```JSON
{
    "acknowledged": true
}
```

![image-20240624163723489](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624163723489.png?raw=true)

![image-20240624164054178](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624164054178.png?raw=true)

## 文档操作_doc

### 1. 创建文档

> - 索引已经创建好了，接下来我们来创建文档，并添加数据，这里的文档可以类比为关系型数据库中的表数据，添加的数据格式为JSON格式
>
> - 在Postman中，向ES服务器发`POST`请求：请求内容为
>
>   ```json
>   {
>       "title":"小米手机",
>       "category":"小米",
>       "image":"https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
>       "price":3999.00
>   }
>   ```

http://127.0.0.1:9200/shopping/_doc

![image-20240624171317221](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624171317221.png?raw=true)

**注意，此处发送请求方式必须为POST，不能是PUT，否则会发生报错，因为PUT需要幂等，也就是不支持随机ID**

返回结果：



```json
{
    "_index": "shopping", //index 索引
    "_type": "_doc",  //类型-文档
    "_id": "0x1-SZABqL-VLXdJIFH3", //同样的请求，每次请求都会自动生成随机ID，作为数据标识使用。
    "_version": 1,
    "result": "created",
    "_shards": {
        "total": 2,
        "successful": 1,
        "failed": 0
    },
    "_seq_no": 0,
    "_primary_term": 1
}
```

上面的数据创建后，由于没有指定数据唯一性标识（ID），默认情况下，ES 服务器会随机

生成一个。

```json
{
 "_index"【索引】: "shopping",
 "_type"【类型-文档】: "_doc",
 "_id"【唯一标识】: "Xhsa2ncBlvF_7lxyCE9G", #可以类比为 MySQL 中的主键，随机生成
 "_version"【版本】: 1,
 "result"【结果】: "created", #这里的 create 表示创建成功
 "_shards"【分片】: {
 "total"【分片 - 总数】: 2,
 "successful"【分片 - 成功】: 1,
 "failed"【分片 - 失败】: 0
 },
 "_seq_no": 0,
 "_primary_term": 1
}
```

如果想要自定义唯一性标识，需要在创建时指定：http://127.0.0.1:9200/shopping/_doc/**10022**

![image-20240624232142445](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624232142445.png?raw=true)



![image-20240624170441196](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624170441196.png?raw=true)

- **再次使用put提示不能使用put因为PUT不能生成随机唯一性标识**

![image-20240624170748713](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624170748713.png?raw=true)

### 2. 查询文档

#### 查询单个文档

GET：http://127.0.0.1:9200/shopping/_doc/1001

![image-20240624232838609](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624232838609.png?raw=true)

#### 查询所有文档

- 创建一个新的接口进行页面进行查询

![image-20240624234502755](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624234502755.png?raw=true)

### 3. 完全覆盖

#### 全量覆盖PUT

和新增文档一样，输入相同的 URL 地址请求，如果请求体变化，会将原有的数据内容覆盖

在 Postman 中，向 ES 服务器发 **PUT/POST** 请求

![image-20240624234857397](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624234857397.png?raw=true)

#### 局部覆盖POST

**修改数据时，也可以只修改某一给条数据的局部信息**

- 在 Postman 中，向 ES 服务器发 **POST** 请求 
- 新建接口，进行修改1001   titel为华为进行更新
- 更新完毕在进行查看

```json
{
    "doc":{
        "title": "华为手机"
    }
}
```

![image-20240624235307387](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624235307387.png?raw=true)

![image-20240624235326172](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624235326172.png?raw=true)

### 4. 删除文档

删除一个文档不会立即从磁盘上移除，它只是被标记成已删除（逻辑删除）。

在 Postman 中，向 ES 服务器发 **DELETE** 请求DELETE：http://127.0.0.1:9200/shopping/_doc/1001

![image-20240624235702569](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240624235702569.png?raw=true)

## 查询操作

### 条件查询

- 主题查询

  ```http
  GET http://127.0.0.1:9200/shopping/_search?q=category:华为
  ```

![image-20240625001046186](D:/liuzh/AppData/Roaming/Typora/typora-user-images/image-20240625001046186.png)

- BODY查询

  ```json
  {
  "query":{
      "match":{
          "category":"华为"
      }
  }
  }
  ```

  ![image-20240625001726395](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625001726395.png?raw=tru)

- match_all查询所有

- ```json
  {
  "query":{
      "match_all":{
      }
  }
  }
  ```

  ![image-20240625001849648](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625001849648.png?raw=true)

### 分页查询

- 查询第一页，并且显示两条数据的计算公式

  (页码-1) * 每页数据条数

  2-1*1=2 = from=2

```json
{
"query":{
    "match_all":{
    }
},
"from":2,
"size":2
}
```

![image-20240625002513784](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625002513784.png?raw=true)

#### 指定分页查询数据

- 只查询分页中title字段内容

```json
{
"query":{
    "match_all":{
    }
},
"from":2,
"size":2,
"_source":["title"]
}
```

![image-20240625002734418](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625002734418.png?raw=true)

### 查询排序

```json
{
"query":{
    "match_all":{
    }
},
"_source":["title"],
"sort":{
    "price":{
        "order":"desc" //升序从小到大
    }
}
}
```

![image-20240625003359240](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625003359240.png?raw=true)

### 多条件查询

#### 单条件匹配查询must

```json
{
    "query":{
        "bool":{
            "must":[
                {
                    "match": {
                        "category":"华为"
                
                    }
                },
                {
                    "match": {
                        "price":4999
                
                    }
                }
            ]
        }
    }
}
```

![image-20240625004344889](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625004344889.png?raw=true)

#### 多条件匹配查询 should

```json
{
    "query":{
        "bool":{
            "should":[
                {
                    "match": {
                        "category":"华为"
                
                    }
                },
                {
                    "match": {
                        "category":"小米"
                
                    }
                },
                {
                    "match": {
                        "price":4999
                
                    }
                }
            ]
        }
    }
}
```

![image-20240625004840224](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625004840224.png?raw=true)

### 范围查询

```sjon
{
    "query":{
        "bool":{
            "should":[
                {
                    "match": {
                        "category":"华为"
                
                    }
                },
                {
                    "match": {
                        "category":"小米"
                
                    }
                },
                {
                    "match": {
                        "price":4999
                
                    }
                }
            ],
            "filter":{
                "range":{
                    "price":{
                        "gt": 4000
                    }
                }
            }
        }
    }
}
```

![image-20240625005115542](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625005115542.png?raw=true)

### 全文检索

- 当报错文档数据时，ES会将文档数据进行分词拆解操作，并将拆解后的数据进行 倒排存储，因此就算使用文字的一部分查询也能查询到

- ```json
  {
      "query":{
          "match":{
              "category":"米"
          }
      }
  }
  ```

  

  ```sjon
  {
      "query":{
          "match":{
              "category":"小华"
          }
      }
  }
  ```

  

![image-20240625010243206](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625010243206.png?raw=true)

![image-20240625010517985](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625010517985.png?raw=true)

### 完全匹配

```json
{
    "query":{
        "match_phrase":{
            "category":"小华"
        }
    }
}
```

![image-20240625010623613](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625010623613.png?raw=true)

### 高亮查询

```json
{
    "query":{
        "match_phrase":{
            "category":"米"
        }
    },
    "highlight":{
        "fields":{
            "category":{}
        }
    }
}
```

![image-20240625011025268](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625011025268.png?raw=true)

### 聚合查询

```json
{
    "aggs":{
        "price_group":{
            "terms":{
                "field":"price"
            }
        }
    }
}
---------------------------------------
{
    "took": 16,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 8,
            "relation": "eq"
        },
        "max_score": 1.0,
        "hits": [
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "0x1-SZABqL-VLXdJIFH3",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1B2ASZABqL-VLXdJs1EW",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1R2ASZABqL-VLXdJ9FE7",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1h2DSZABqL-VLXdJMFFj",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1002",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1003",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1004",
                "_score": 1.0,
                "_source": {
                    "title": "小米手机",
                    "category": "小米",
                    "image": "https://i1.mifile.cn/f/i/2019/redmi7/sec1.jpg?v=2",
                    "price": 3999.00
                }
            },
            {
                "_index": "shopping",
                "_type": "_doc",
                "_id": "1001",
                "_score": 1.0,
                "_source": {
                    "title": "华为手机",
                    "category": "华为",
                    "images": "http://www.gulixueyuan.com/hw.jpg",
                    "price": 4999.00
                }
            }
        ]
    },
    "aggregations": {
        "price_group": {
            "doc_count_error_upper_bound": 0,
            "sum_other_doc_count": 0,
            "buckets": [
                {
                    "key": 3999.0,
                    "doc_count": 7
                },
                {
                    "key": 4999.0,
                    "doc_count": 1
                }
            ]
        }
    }
}
```

![image-20240625011221613](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625011221613.png?raw=true)

#### 过滤原始数据

```json
{
    "aggs":{
        "price_group":{
            "terms":{
                "field":"price"
            }
        }
    },
    "size":0
}
```

![image-20240625011409211](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625011409211.png?raw=true)

#### 统计平均值

```sjon
{
    "aggs":{
        "price_avg":{
            "avg":{
                "field":"price"
            }
        }
    },
    "size":0
}
```

![image-20240625011508222](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625011508222.png?raw=true)

## 映射关系

PUT：http://127.0.0.1:9200/user

PUT：http://127.0.0.1:9200/user/_mapping

```json
{
    "properties":{
        "name":{
            "type":"text",
            "index":true
        },
        "nsex":{
            "type":"keyword",
            "index":true
        },
        "tel":{
            "type":"keyword",
            "index":false
        }
    }
}
```

GET：http://127.0.0.1:9200/user/_mapping

![image-20240625012349399](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625012349399.png?raw=true)

```json
{
    "query":{
        "match":{
            "name":"zhangsan"
        }
    }
}
```

![image-20240625012758818](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625012758818.png?raw=true)



#### keyword查询

```json
{
    "query":{
        "match":{
           "age":"3"
        }
    }
}
——————————————————如上age字段为keyword，所以必须匹配
{
    "query":{
        "match":{
           "age":"30"
        }
    }
}
```

![image-20240625012925518](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625012925518.png?raw=true)

![](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625012925518.png?raw=true)

#### keywold-false

不支持查询

# 第三章Elasticserch环境

## 创建Maven项目

![1](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/1.gif?raw=true)



![image-20240625145649933](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625145649933.png?raw=true)

### pom.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.atguigu</groupId>
    <artifactId>test</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch</artifactId>
            <version>7.8.0</version>
        </dependency>
        <!-- elasticsearch的客户端 -->
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>elasticsearch-rest-high-level-client</artifactId>
            <version>7.8.0</version>
        </dependency>
        <!-- elasticsearch依赖2.x的log4j -->
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-api</artifactId>
            <version>2.8.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.8.2</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.9</version>
        </dependency>
        <!-- junit单元测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
</project>

```

## 客户端对象

创建 com.atguigu.es.test.Elasticsearch01_Client 类，代码中创建 Elasticsearch 客户端对象

因为早期版本的客户端对象已经不再推荐使用，且在未来版本中会被删除，所以这里我们采

用高级 REST 客户端对象

### com.atguigu.es.test

- ESTest_Client

```json
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;

public class ESTest_Client {
    public static void main(String[] args) throws Exception {

        // 创建ES客户端
        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 关闭ES客户端
        esClient.close();
    }
}

```

`注意：`9200 端口为Elasticserch的Web通讯端口，localhost为启动ES服务的主机名

![image-20240625150648244](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625150648244.png?raw=true)

## 索引操作

### 创建索引

![image-20240625150752044](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625150752044.png?raw=true)



```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;

public class ESTest_Index_Create {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 创建索引
        CreateIndexRequest request = new CreateIndexRequest("user");
        CreateIndexResponse createIndexResponse =
                esClient.indices().create(request, RequestOptions.DEFAULT);

        // 响应状态
        boolean acknowledged = createIndexResponse.isAcknowledged();
        System.out.println("索引操作 ：" + acknowledged);

        esClient.close();
        }
    }
```

![image-20240625152105228](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625152105228.png?raw=true)

### 查询索引

![image-20240625153106230](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625153106230.png?raw=true)

![image-20240625153041860](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625153041860.png?raw=true)

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.CreateIndexRequest;
import org.elasticsearch.client.indices.CreateIndexResponse;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.client.indices.GetIndexResponse;

public class ESTest_Index_Search {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 创建索引
        GetIndexRequest request = new GetIndexRequest("user");
        GetIndexResponse getIndexResponse = esClient.indices().get(request, RequestOptions.DEFAULT);

        // 响应状态
        System.out.println(getIndexResponse.getAliases());
        System.out.println(getIndexResponse.getMappings());
        System.out.println(getIndexResponse.getSettings());

        esClient.close();
        }
    }
```

### 删除索引

![image-20240625154505899](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625154505899.png?raw=true)

![image-20240625154208772](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625154208772.png?raw=true)

![image-20240625154226467](D:/liuzh/AppData/Roaming/Typora/typora-user-images/image-20240625154226467.png)

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexAction;
import org.elasticsearch.action.admin.indices.delete.DeleteIndexRequest;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.support.master.AcknowledgedResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.client.indices.GetIndexResponse;

public class ESTest_Index_Delete {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 查询索引
        DeleteIndexRequest request = new DeleteIndexRequest("user");
        AcknowledgedResponse response = esClient.indices().delete(request, RequestOptions.DEFAULT);

        // 响应状态
        System.out.println(response.isAcknowledged());

        esClient.close();
        }
    }
```

## 数据操作

### 新增数据

```java
package com.atguigu.es.test;

import com.fasterxml.jackson.databind.ObjectMapper;
import org.apache.http.HttpHost;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.client.indices.GetIndexResponse;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Insert {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 插入数据
        IndexRequest request = new IndexRequest();
        request.index("user").id("1001");

        User user = new User();
        user.setName("zhangsan");
        user.setAge(30);
        user.setSex("男");

        // 向ES插入数据，必须将数据转换位JSON格式
        ObjectMapper mapper = new ObjectMapper();
        String userJson = mapper.writeValueAsString(user);
        request.source(userJson, XContentType.JSON);

        IndexResponse response = esClient.index(request, RequestOptions.DEFAULT);
        System.out.println(response.getResult());
        esClient.close();
    }
}
```

![image-20240625161612816](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625161612816.png?raw=true)

![image-20240625162004649](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625162004649.png?raw=true)

### 修改数据

```java
package com.atguigu.es.test;

import com.fasterxml.jackson.databind.ObjectMapper;
import org.apache.http.HttpHost;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.index.IndexResponse;
import org.elasticsearch.action.update.UpdateRequest;
import org.elasticsearch.action.update.UpdateResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Update {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 修改数据
        UpdateRequest request = new UpdateRequest();
        request.index("user").id("1001");
        request.doc(XContentType.JSON,"sex","女");

        UpdateResponse response = esClient.update(request, RequestOptions.DEFAULT);

        System.out.println(response.getResult());
        esClient.close();
    }
}
```

![image-20240625162809600](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625162809600.png?raw=true)

![image-20240625163039781](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625163039781.png?raw=true)

### 查询数据

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.update.UpdateRequest;
import org.elasticsearch.action.update.UpdateResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.client.indices.GetIndexRequest;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Get {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 查询数据
        GetRequest request = new GetRequest();
        request.index("user").id("1001");
        GetResponse response = esClient.get(request, RequestOptions.DEFAULT);

        System.out.println(response.getSourceAsString());

        esClient.close();
    }
}

```

![image-20240625164010002](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625164010002.png?raw=true)

### 删除数据

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.delete.DeleteResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;

public class ESTest_Doc_Delete {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 查询数据
        DeleteRequest request = new DeleteRequest();
        request.index("user").id("1001");
        DeleteResponse response = esClient.delete(request, RequestOptions.DEFAULT);

        System.out.println(response.toString());
        esClient.close();
    }
}
```

![image-20240625165043923](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625165043923.png?raw=true)

## 数据批量操作

### 批量新增

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Insert_Batch {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 批量插入数据
        BulkRequest request = new BulkRequest();

        request.add(new IndexRequest().index("user").id("1001").source(XContentType.JSON,"name","润扬"));
        request.add(new IndexRequest().index("user").id("1002").source(XContentType.JSON,"name","振振"));
        request.add(new IndexRequest().index("user").id("1003").source(XContentType.JSON,"name","振华"));

        BulkResponse responses = esClient.bulk(request, RequestOptions.DEFAULT);
        System.out.println(responses.getTook());
        System.out.println(responses.getItems());
        esClient.close();
    }
}
```

![image-20240625170955137](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625170955137.png?raw=true)

### 批量删除

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.delete.DeleteRequest;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Insert_Batch {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 批量删除数据
        BulkRequest request = new BulkRequest();

        request.add(new DeleteRequest().index("user").id("1001"));
        request.add(new DeleteRequest().index("user").id("1002"));
        request.add(new DeleteRequest().index("user").id("1003"));

        BulkResponse responses = esClient.bulk(request, RequestOptions.DEFAULT);
        System.out.println(responses.getTook());
        System.out.println(responses.getItems());
        esClient.close();
    }
}
```

![image-20240625172618556](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625172618556.png?raw=true)

![image-20240625172547340](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625172547340.png?raw=true)

## 高级查询

### 全量查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.get.GetRequest;
import org.elasticsearch.action.get.GetResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;

public class ESTest_Doc_Insert_Batch {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 批量插入数据
        BulkRequest request = new BulkRequest();

        request.add(new IndexRequest().index("user").id("1001").source(XContentType.JSON,"name","润扬","age",30,"sex","男"));
        request.add(new IndexRequest().index("user").id("1002").source(XContentType.JSON,"name","振振","age",22,"sex","女"));
        request.add(new IndexRequest().index("user").id("1003").source(XContentType.JSON,"name","振华","age",34,"sex","男"));
        request.add(new IndexRequest().index("user").id("1004").source(XContentType.JSON,"name","润扬1","age",10,"sex","男"));
        request.add(new IndexRequest().index("user").id("1005").source(XContentType.JSON,"name","振振2","age",60,"sex","女"));
        request.add(new IndexRequest().index("user").id("1006").source(XContentType.JSON,"name","振华3","age",20,"sex","男"));

        BulkResponse responses = esClient.bulk(request, RequestOptions.DEFAULT);
        System.out.println(responses.getTook());
        System.out.println(responses.getItems());
        esClient.close();
    }
}

```

![image-20240625223216209](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625223216209.png?raw=true)

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 查询索引中全部的数据
        SearchRequest request = new SearchRequest();
        request.indices("user");

        request.source(new SearchSourceBuilder().query(QueryBuilders.matchAllQuery()));
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

![image-20240625230312200](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625230312200.png?raw=true)

### 分页查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

//         分页查询
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder().query(QueryBuilders.matchAllQuery());
        builder.from(0);
        builder.size(2);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

![image-20240625231904857](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625231904857.png?raw=true)



### 条件查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        // 条件查询
        SearchRequest request = new SearchRequest();
        request.indices("user");

        request.source(new SearchSourceBuilder().query(QueryBuilders.termQuery("age",30)));
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

![image-20240625231216221](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625231216221.png?raw=true)

### 查询排序

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        //         查询排序
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder().query(QueryBuilders.matchAllQuery());
        builder.sort("age", SortOrder.DESC);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}
```

![image-20240625232257390](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625232257390.png?raw=true)

### 字段查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

//字段排除
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder().query(QueryBuilders.matchAllQuery());
        String[] exclude = {"age"};
        String[] include = {};
        builder.fetchSource(include,exclude);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

![image-20240625232816944](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625232816944.png?raw=true)

### 组合查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.BoolQueryBuilder;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );


//        范围查询
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder();
        BoolQueryBuilder boolQueryBuilder = QueryBuilders.boolQuery();
        builder.query(boolQueryBuilder);

       boolQueryBuilder.must(QueryBuilders.matchQuery("age",30));
       boolQueryBuilder.must(QueryBuilders.matchQuery("sex","男"));
     // boolQueryBuilder.mustNot(QueryBuilders.matchQuery("sex","男"));
       //查询30或则40
	//        boolQueryBuilder.should(QueryBuilders.matchQuery("age",30));
	//        boolQueryBuilder.should(QueryBuilders.matchQuery("age",40));
        builder.query(boolQueryBuilder);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}
```

![image-20240625234343647](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625234343647.png?raw=true)

![image-20240625234637556](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625234637556.png?raw=true)

![image-20240625234959374](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625234959374.png?raw=true)



### 范围查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.BoolQueryBuilder;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.RangeQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

//        范围查询
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder();
        RangeQueryBuilder rangedQuery = QueryBuilders.rangeQuery("age");

        rangedQuery.gte(30);
        rangedQuery.lte(40);

        builder.query(rangedQuery);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

![image-20240625235337054](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240625235337054.png?raw=true)

### 模糊查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.unit.Fuzziness;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.BoolQueryBuilder;
import org.elasticsearch.index.query.QueryBuilder;
import org.elasticsearch.index.query.QueryBuilders;
import org.elasticsearch.index.query.RangeQueryBuilder;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

//        范围查询
        SearchRequest request = new SearchRequest();
        request.indices("user");
        SearchSourceBuilder builder = new SearchSourceBuilder();
        
        builder.query(QueryBuilders.fuzzyQuery("name","润扬").fuzziness(Fuzziness.ONE));

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();
        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for (SearchHit hit : hits) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}
```

![image-20240626001659219](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626001659219.png?raw=true)

### 高亮查询

```
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.unit.Fuzziness;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.*;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.fetch.subphase.highlight.HighlightBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );

        //高亮查询
        SearchRequest request = new SearchRequest();
        request.indices("user");

        SearchSourceBuilder builder = new SearchSourceBuilder();
        TermsQueryBuilder termsQueryBuilder = QueryBuilders.termsQuery("name", "振华");

        HighlightBuilder highlightBuilder = new HighlightBuilder();
        highlightBuilder.preTags("<font color='red'>");
        highlightBuilder.postTags("</font>");
        highlightBuilder.field("name");

        builder.highlighter(highlightBuilder);
        builder.query(termsQueryBuilder);

        request.source(builder);
        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);

        SearchHits hits = response.getHits();

        System.out.println(hits.getTotalHits());
        System.out.println(response.getTook());

        for ( SearchHit hit : hits ) {
            System.out.println(hit.getSourceAsString());
        }
        esClient.close();
    }
}

```

### 聚合查询

```java
package com.atguigu.es.test;

import org.apache.http.HttpHost;
import org.elasticsearch.action.bulk.BulkRequest;
import org.elasticsearch.action.bulk.BulkResponse;
import org.elasticsearch.action.index.IndexRequest;
import org.elasticsearch.action.search.SearchRequest;
import org.elasticsearch.action.search.SearchResponse;
import org.elasticsearch.client.RequestOptions;
import org.elasticsearch.client.RestClient;
import org.elasticsearch.client.RestHighLevelClient;
import org.elasticsearch.common.unit.Fuzziness;
import org.elasticsearch.common.xcontent.XContentType;
import org.elasticsearch.index.query.*;
import org.elasticsearch.search.SearchHit;
import org.elasticsearch.search.SearchHits;
import org.elasticsearch.search.aggregations.AggregationBuilder;
import org.elasticsearch.search.aggregations.AggregationBuilders;
import org.elasticsearch.search.builder.SearchSourceBuilder;
import org.elasticsearch.search.fetch.subphase.highlight.HighlightBuilder;
import org.elasticsearch.search.sort.SortOrder;

public class ESTest_Doc_Query {
    public static void main(String[] args) throws Exception {

        RestHighLevelClient esClient = new RestHighLevelClient(
                RestClient.builder(new HttpHost("localhost", 9200, "http"))
        );
        //聚合查询
        //查询最大年龄
//        SearchRequest request = new SearchRequest();
//        request.indices("user");
//
//        SearchSourceBuilder builder = new SearchSourceBuilder();
//
//        AggregationBuilder aggregationBuilder = AggregationBuilders.max("maxAge").field("age");
//        builder.aggregation(aggregationBuilder);
//
//        request.source(builder);
//        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);
//
//        SearchHits hits = response.getHits();
//
//        System.out.println(hits.getTotalHits());
//        System.out.println(response.getTook());
//
//        for ( SearchHit hit : hits ) {
//            System.out.println(hit.getSourceAsString());
//        }
//        esClient.close();
        //聚合分组查询
//        SearchRequest request = new SearchRequest();
//        request.indices("user");
//
//        SearchSourceBuilder builder = new SearchSourceBuilder();
//
//        AggregationBuilder aggregationBuilder = AggregationBuilders.terms("ageGroup").field("age");
//        builder.aggregation(aggregationBuilder);
//
//        request.source(builder);
//        SearchResponse response = esClient.search(request, RequestOptions.DEFAULT);
//
//        SearchHits hits = response.getHits();
//
//        System.out.println(hits.getTotalHits());
//        System.out.println(response.getTook());
//
//        for ( SearchHit hit : hits ) {
//            System.out.println(hit.getSourceAsString());
//        }
//        esClient.close();
    }
}

```



# 第四章Elasticserch进阶

## 相关概念

### 4.1.1单机&集群

### 41.2 集群Cluster

### 4.1.3 节点Node

## 4.2 Windows集群

### 4.2.1 部署集群

1. **创建elasticserch文件夹，在内部复制三个ES服务**

![image-20240626092002089](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626092002089.png?raw=true)

2. **修改集群文件目录中每个节点的 config/elasticserch.yaml配置文件**

![image-20240626094840104](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626094840104.png?raw=true)

- **Node-1001节点**

  ```apl
  #节点 1 的配置信息：
  #集群名称，节点之间要保持一致
  cluster.name: my-elasticsearch
  #节点名称，集群内要唯一
  node.name: node-1001
  node.master: true
  node.data: true
  #ip 地址
  network.host: localhost
  #http 端口
  http.port: 1001
  #tcp 监听端口
  transport.tcp.port: 9301
  #discovery.seed_hosts: ["localhost:9301", "localhost:9302","localhost:9303"]
  #discovery.zen.fd.ping_timeout: 1m
  #discovery.zen.fd.ping_retries: 5
  #集群内的可以被选为主节点的节点列表
  #cluster.initial_master_nodes: ["node-1", "node-2","node-3"]
  #跨域配置
  #action.destructive_requires_name: true
  http.cors.enabled: true
  http.cors.allow-origin: "*"
  ```

- **Node-1002节点**

```apl
#节点 2 的配置信息：
#集群名称，节点之间要保持一致
cluster.name: my-elasticsearch
#节点名称，集群内要唯一
node.name: node-1002
node.master: true
node.data: true
#ip 地址
network.host: localhost
#http 端口
http.port: 1002
#tcp 监听端口
transport.tcp.port: 9302
discovery.seed_hosts: ["localhost:9301"]
discovery.zen.fd.ping_timeout: 1m
discovery.zen.fd.ping_retries: 5
#集群内的可以被选为主节点的节点列表
#cluster.initial_master_nodes: ["node-1", "node-2","node-3"]
#跨域配置
#action.destructive_requires_name: true
http.cors.enabled: true
http.cors.allow-origin: "*"
```

- **Node-1003节点**

```apl
#节点 2 的配置信息：
#集群名称，节点之间要保持一致
cluster.name: my-elasticsearch
#节点名称，集群内要唯一
node.name: node-1003
node.master: true
node.data: true
#ip 地址
network.host: localhost
#http 端口
http.port: 1003
#tcp 监听端口
transport.tcp.port: 9303
discovery.seed_hosts: ["localhost:9301"]
discovery.zen.fd.ping_timeout: 1m
discovery.zen.fd.ping_retries: 5
#集群内的可以被选为主节点的节点列表
#cluster.initial_master_nodes: ["node-1", "node-2","node-3"]
#跨域配置
#action.destructive_requires_name: true
http.cors.enabled: true
http.cors.allow-origin: "*"
```

###  4.2.2启动集群

![image-20240626101509115](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626101509115.png?raw=true)

### 4.2.3 测试集群

- 查看集群状态

![image-20240626102815701](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626102815701.png?raw=true)

## Linux单机

### 4.3.1 软件下载

[Elasticsearch 7.10.2 | Elastic](https://www.elastic.co/cn/downloads/past-releases/elasticsearch-7-10-2)

![image-20240626110950703](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626110950703.png?raw=true)

### 4.3.2软件安装

1. **解压软件**

- 将下载的软件解压缩

  ```apl
  #解压缩
  tar -zxvf elasticsearch-7.10.2-linux-x86_64.tar.gz -C /data/
  mv elasticsearch-7.10.2/ es
  ```

2. **创建用户**

   因为安全问题，Elasticserch不允许root用户直接运行，所以需要创建新用户，在root用户中创建新用户

   ```
   useradd es
   passwd es
   
   userdel -r es
   chown -R es:es /data/
   ```

3. 修改配置文件

   ```apl
   vim /data/es/config/elasticsearch.yml
   
   # 加入如下配置
   #集群名称
   cluster.name: cluster-es
   #节点名称，每个节点的名称不能重复
   node.name: node-1 
   #ip 地址，每个节点的地址不能重复
   network.host: linux1
   #是不是有资格主节点
   node.master: true
   node.data: true
   http.port: 9200
   # head 插件需要这打开这两个配置
   http.cors.allow-origin: "*"
   http.cors.enabled: true
   http.max_content_length: 200mb
   #es7.x 之后新增的配置，初始化一个新的集群时需要此配置来选举 master
   cluster.initial_master_nodes: ["node-1"]
   #es7.x 之后新增的配置，节点发现
   discovery.seed_hosts: ["linux1:9300","linux2:9300","linux3:9300"]
   gateway.recover_after_nodes: 2
   network.tcp.keep_alive: true
   network.tcp.no_delay: true
   transport.tcp.compress: true
   #集群内同时启动的数据任务个数，默认是 2 个
   cluster.routing.allocation.cluster_concurrent_rebalance: 16
   #添加或删除节点及负载均衡时并发恢复的线程个数，默认 4 个
   cluster.routing.allocation.node_concurrent_recoveries: 16
   #初始化数据恢复时，并发恢复线程的个数，默认 4 个
   cluster.routing.allocation.node_initial_primaries_recoveries: 16
   ```

4. 修改/etc/security/limits.conf分发文件

   ```apl
   vim /etc/security/limits.conf
   # 在文件末尾中增加下面内容
   es soft nofile 65536
   es hard nofile 65536
   ```

5. 修改/etc/security/limits.d/20-nproc.conf，分发文件

   ```apl
   vim /etc/security/limits.d/20-nproc.conf
   # 在文件末尾中增加下面内容
   es soft nofile 65536
   es hard nofile 65536
   * hard nproc 4096
   # 注：* 带表 Linux 所有用户名称
   ```

6. 修改/etc/sysctl.conf

   ```apl
   # 在文件中增加下面内容
   vm.max_map_count=655360
   ```

7. 重新加载

   ```apl
   sysctl -p
   ```

### 4.3.3启动软件

分别在不同节点上启动 ES 软件

```apl
cd /opt/module/es-cluster
#启动
bin/elasticsearch
#后台启动
bin/elasticsearch -d
```

### 4.4.4 测试集群

![image-20240626153829239](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626153829239.png?raw=true)

## 核心概念

### 4.5.1 索引(index)

- 一个索引就是一个拥有几分相似特征的文档的集合。比如说，你可以有一个客户数据的

  索引，另一个产品目录的索引，还有一个订单数据的索引。一个索引由一个名字来标识（必

  须全部是小写字母），并且当我们要对这个索引中的文档进行索引、搜索、更新和删除的时

  候，都要使用到这个名字。在一个集群中，可以定义任意多的索引。

  能搜索的数据必须索引，这样的好处是可以提高查询速度，比如：新华字典前面的目录

  就是索引的意思，目录可以提高查询速度。

  **Elasticsearch** **索引的精髓：一切设计都是为了提高搜索的性能。**

### 4.5.2 类型（type)

- 在一个索引中，你可以定义一种或多种类型。

  一个类型是你的索引的一个逻辑上的分类/分区，其语义完全由你来定。通常，会为具

  有一组共同字段的文档定义一个类型。不同的版本，类型发生了不同的变化

  ![image-20240626154049776](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626154049776.png?raw=true)

### 4.5.3 字段（Field）

- 相当于是数据表的字段，对文档数据根不通属性进行分类标识

### 4.5.4 映射(Mapping)

- mapping 是处理数据的方式和规则方面做一些限制，如：某个字段的数据类型、默认值、

  分析器、是否被索引等等。这些都是映射里面可以设置的，其它就是处理 ES 里面数据的一

  些使用规则设置也叫做映射，按着最优规则处理数据对性能提高很大，因此才需要建立映射，

  并且需要思考如何建立映射才能对性能更好。

### 4.5.6 分片（Shards）

- 一个索引可以存储超出单个节点硬件限制的大量数据。比如，一个具有 10 亿文档数据

  的索引占据 1TB 的磁盘空间，而任一节点都可能没有这样大的磁盘空间。或者单个节点处

  理搜索请求，响应太慢。为了解决这个问题，Elasticsearch 提供了将索引划分成多份的能力，

  每一份就称之为分片。当你创建一个索引的时候，你可以指定你想要的分片的数量。每个分

  片本身也是一个功能完善并且独立的“索引”，这个“索引”可以被放置到集群中的任何节点

  上。

- 分片很重要，主要有两方面的原因：

  - 允许你水平分割 / 扩展你的内容容量。

  - 允许你在分片之上进行分布式的、并行的操作，进而提高性能/吞吐量。

    至于一个分片怎样分布，它的文档怎样聚合和搜索请求，是完全由 Elasticsearch 管理的，

    对于作为用户的你来说，这些都是透明的，无需过分关心。

**被混淆的概念是，一个 Lucene 索引 我们在 Elasticsearch 称作 分片 。 一个**

**Elasticsearch 索引 是分片的集合。 当 Elasticsearch 在索引中搜索的时候， 他发送查询**

**到每一个属于索引的分片(Lucene 索引)，然后合并每个分片的结果到一个全局的结果集。**

### 4.5.7 副本（Replicas）

- 在一个网络 / 云的环境里，失败随时都可能发生，在某个分片/节点不知怎么的就处于

  离线状态，或者由于任何原因消失了，这种情况下，有一个故障转移机制是非常有用并且是

  强烈推荐的。为此目的，Elasticsearch 允许你创建分片的一份或多份拷贝，这些拷贝叫做复

  制分片(副本)。

- 复制分片之所以重要，有两个主要原因

  - 在分片/节点失败的情况下，提供了高可用性。因为这个原因，注意到复制分片从不与

    原/主要（original/primary）分片置于同一节点上是非常重要的。

  - 扩展你的搜索量/吞吐量，因为搜索可以在所有的副本上并行运行。

  - 总之，每个索引可以被分成多个分片。一个索引也可以被复制 0 次（意思是没有复制）

    或多次。一旦复制了，每个索引就有了主分片（作为复制源的原来的分片）和复制分片（主

    分片的拷贝）之别。分片和复制的数量可以在索引创建的时候指定。在索引创建之后，你可

    以在任何时候动态地改变复制的数量，但是你事后不能改变分片的数量。默认情况下，

    Elasticsearch 中的每个索引被分片 1 个主分片和 1 个复制，这意味着，如果你的集群中至少

    有两个节点，你的索引将会有 1 个主分片和另外 1 个复制分片（1 个完全拷贝），这样的话

    每个索引总共就有 2 个分片，我们需要根据索引需要确定分片个数

### 4.5.8 分配(Allocation)

- 将分片分配给某个节点的过程，包括分配主分片或者副本。如果是副本，还包含从主分

  片复制数据的过程。这个过程是由 master 节点完成的。

## 4.6 分布式集群

### 4.6.1 单节点集群

- 我们在包含一个空节点的集群内创建名为 users 的索引，为了演示目的，我们将分配 3个主分片和一份副本（每个主分片拥有一个副本分片）

  ```apl
  {
   "settings" : {
   "number_of_shards" : 3,
   "number_of_replicas" : 1
   }
  }
  ```

  ![image-20240626171554031](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626171554031.png?raw=true)

  ![image-20240626171601326](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626171601326.png?raw=true)

### 4.6.2 故障转移

- 当集群中只有一个节点在运行时，意味着会有一个单点故障问题——没有冗余。 幸运

  的是，我们只需再启动一个节点即可防止数据丢失。当你在同一台机器上启动了第二个节点

  时，只要它和第一个节点有同样的 cluster.name 配置，它就会自动发现集群并加入到其中。

  但是在不同机器上启动节点的时候，为了加入到同一集群，你需要配置一个可连接到的单播

  主机列表。之所以配置为使用单播发现，以防止节点无意中加入集群。只有在同一台机器上

  运行的节点才会自动组成集群。

- 如果启动了第二个节点，我们的集群将会拥有两个节点的集群 : 所有主分片和副本分

  片都已被分配、

- 我们的集群现在是拥有一个索引的单节点集群。所有 3 个主分片都被分配在 node-1 。

![image-20240626171746522](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626171746522.png?raw=true)

- 通过 elasticsearch-head 插件查看集群情况

![image-20240626172013572](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626172013572.png?raw=true)

![image-20240626172034097](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626172034097.png?raw=true)

- 当前我们的集群是正常运行的，但是在硬件故障时有丢失数据的风险。

### 4.6.3 水平分割

- 当启动了第三个节点，我们的集群将会拥有三个节点的集群 : 为了分散负载而对分片进行重新分配

![image-20240626174900759](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626174900759.png?raw=true)

![image-20240626174931965](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626174931965.png?raw=true)

- 在运行中的集群上是可以动态调整副本分片数目的，我们可以按需伸缩集群。让我们把副本数从默认的 1 增加到 2

```json
{
 "number_of_replicas" : 2
}
```

![image-20240626183922505](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626183922505.png?raw=true)

![image-20240626184005033](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240626184005033.png?raw=true)

### 4.6.4 应对故障

![image-20240627001514670](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627001514670.png?raw=true)

- 我们关闭的节点是一个主节点。而集群必须拥有一个主节点来保证正常工作，所以发生

  的第一件事情就是选举一个新的主节点： Node 2 。在我们关闭 Node 1 的同时也失去了主

  分片 1 和 2 ，并且在缺失主分片的时候索引也不能正常工作。 如果此时来检查集群的状 

  更多 Java –大数据 –前端 –python 人工智能资料下载，可百度访问：尚硅谷官网

  况，我们看到的状态将会为 red ：不是所有主分片都在正常工作。

![image-20240627001645379](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627001645379.png?raw=true)

- 在其它节点上存在着这两个主分片的完整副本， 所以新的主节点立即将这

  些分片在 Node 2 和 Node 3 上对应的副本分片提升为主分片， 此时集群的状态将会为

  yellow。这个提升主分片的过程是瞬间发生的，如同按下一个开关一般。

- **为什么我们集群状态是** **yellow** **而不是** **green** **呢**？

  - 虽然我们拥有所有的三个主分片，但是同时设置了每个主分片需要对应 2 份副本分片，而此

    时只存在一份副本分片。 所以集群不能为 green 的状态，不过我们不必过于担心：如果我

    们同样关闭了 Node 2 ，我们的程序 依然 可以保持在不丢任何数据的情况下运行，因为

    Node 3 为每一个分片都保留着一份副本。

  - 如果我们重新启动 Node 1 ，集群可以将缺失的副本分片再次进行分配，那么集群的状

    态也将恢复成之前的状态。 如果 Node 1 依然拥有着之前的分片，它将尝试去重用它们，

    同时仅从主分片复制发生了修改的数据文件。和之前的集群相比，只是 Master 节点切换了。

## 4.7 路由计算

> - 当索引一个文档的时候，文档会被存储到一个主分片中。 Elasticsearch 如何知道一个
>
>   文档应该存放到哪个分片中呢？
>
> - 当我们创建文档时，它如何决定这个文档应当被存储在分片
>
>   1 还是分片 2 中呢？

- 首先这个过程不是随机的，是根据下面这个公式决定

  ```apl
  shard = hash（routing) % number_of_primary_shards
  ```

  **routing 是一个可变值，默认是文档的_id,也可以设置成一个自定义的值。routing通过hash函数生成一个数字，然后这个数字再处于number_of_primary_shards（主分片的数量）后得到余数。这个分布在0到number_of_primary_shards-1之间的余数，就是我们所寻求的文档所在分片的位置。**

### 4.7.1 路由计算写入数据

> 当张三需要写入数据时，将请求发送给了 node3，并且node3收掉请求后，充当协调节点，然后根据路由计算，将张三的数据写入某个节点的主分区中，然后主分区于其他节点的副本分区同步数据，待追后一个副本完成同步的后，主分区返回给用户说完毕

![image-20240627091659348](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627091659348.png?raw=true)

### 4.7.2路由计算查询数据

> 当张三需要读取数据时，将请求发送给了 node3，并且node3收掉请求后，充当协调节点，然后根据路由计算，将流量进行轮询调度，分配到不通的副本进行查询，并将结果进行返回

![image-20240627110231214.png](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627110231214.png?raw=true)

## 4.8 分配控制

- 假设有一个集群由三个节点组成。 它包含一个叫 emps 的索引，有两个主分片，每个主分片有两个副本分片。相同分片的副本不会放在同一节点。

![image-20240627004523712](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627004523712.png?raw=true)

![image-20240627004548531](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627004548531.png?raw=true)

- 通过 elasticsearch-head 插件查看集群情况，所以我们的集群是一个有三个节点和一个索

  引的集群。

  ![image-20240627004619667](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627004619667.png?raw=true)

### 4.8.1协调节点

- 我们可以发送请求到集群中的任一节点。 每个节点都有能力处理任意请求。 每个节点都知

  道集群中任一文档位置，所以可以直接将请求转发到需要的节点上。

- 例如将所有的请求发送到 Node 1，我们将其称为 **协调节点**(coordinating node)

### 4.8.2写流程

**新建、索引和删除 请求都是 写 操作， 必须在主分片上面完成之后才能被复制到相关**

**的副本分片**

![image-20240627004910513](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627004910513.png?raw=true)

![image-20240627140613767](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627140613767.png?raw=true)

- **新建，索引和删除文档所需要的步骤顺序**

1. 客户端向 Node 1 发送新建、索引或者删除请求。

2. 节点使用文档的 _id 确定文档属于分片 0 。请求会被转发到 Node 3，因为分片 0 的

   主分片目前被分配在 Node 3 上。

3. Node 3 在主分片上面执行请求。如果成功了，它将请求并行转发到 Node 1 和 Node 2 

   的副本分片上。一旦所有的副本分片都报告成功, Node 3 将向协调节点报告成功，协调

   节点向客户端报告成功。

- 在客户端收到成功响应时，文档变更已经在主分片和所有副本分片执行完成，变更是安全的。

  有一些可选的请求参数允许您影响这个过程，可能以数据安全为代价提升性能。这些选项很

  少使用，因为 Elasticsearch 已经很快，但是为了完整起见，请参考下面表格：

| 参数        | 含义                                                         |
| ----------- | ------------------------------------------------------------ |
| consistency | consistency 参数的值可以设为 one （只要主分片状态 ok 就允许执行_写_操作）,all（必须要主分片和所有副本分片的状态没问题才允许执行_写_操作）, 或quorum 。默认值为 quorum , 即大多数的分片副本状态没问题就允许执行_写_操作。当前索引拥有三个副本分片，那规定数量的计算结果即：**int( (primary + 3 replicas) / 2 ) + 1 = 3** |
| timeout     | Elasticsearch 会等待，希望更多的分片出现。默认情况下，它最多等待 1 分钟。 如果你需要，你可以使用 timeout 参数使它更早终止： 100 100 毫秒，30s 是 30 秒 |

>新索引默认有 1 个副本分片，这意味着为满足规定数量应该需要两个活动的分片副本。 但是，这些
>
>默认的设置会阻止我们在单一节点上做任何事情。为了避免这个问题，要求只有当 number_of_replicas 大
>
>于 1 的时候，规定数量才会执行。

###  4.8.3 读流程

>我们可以从主分片或者从其它任意副本分片检索文档

![image-20240627141847845](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627141847845.png?raw=true)

![image-20240627141953680](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627141953680.png?raw=true)

**从主分配或副本分片检索文档的步骤：**

1. 客户端向Node1 发送获取请求。
2. 节点使用文档的_id 来确定文档属于分片0。分片0的副本分片存在于三个节点上，这种情况，将将请求发送到Node02.
3. Node02将文档返回给 Node 1 ，然后将文档返回给客户端。

在处理读取请求时，协调结点在每次请求的时候都会通过轮询所有的副本分片来达到负载均衡。在文档被检索时，已经被索引的文档可能已经存在于主分片上但是还没有复制到副本分片。 在这种情况下，副本分片可能会报告文档不存在，但是主分片可能成功返回文档。 一

旦索引请求成功返回给用户，文档在主分片和副本分片都是可用的。

### 4.8.5更新流程

![image-20240627142821485](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627142821485.png?raw=true)

**部分更新一个文档的步骤**

1. 客户端向Node1 发送更新请求
2. 他将请求转发到主分片所在的Node3.
3. Node3从主分片索引文档，修改_source字段中的JSON，并尝试重新索引主分片的文档。如果文档已经被另一个进程修改，他会重试3次，超过retry_on_conflict此后放弃
4. 如果 Node 3 成功地更新文档，它将新版本的文档并行转发到 Node 1 和 Node 2 上的副本分片，重新建立索引。一旦所有副本分片都返回成功， Node 3 向协调节点也返回成功，协调节点向客户端返回成功。

### 4.8.6 多文档操作流程

#### megt

mget 和 bulk API 的模式类似于单文档模式。区别在于协调节点知道每个文档存在于

哪个分片中。它将整个多文档请求分解成 每个分片 的多文档请求，并且将这些请求并行转

发到每个参与节点。

协调节点一旦收到来自每个节点的应答，就将每个节点的响应收集整理成单个响应，返

回给客户端

>#### `mget` 请求
>
>1. 客户端发送`mget`请求到Node1。
>2. Node1把请求分解，按分片分发到各节点。
>3. 各节点处理请求，把结果返回Node1。
>4. Node1汇总结果，返回给客户端。

![image-20240627143853195](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627143853195.png?raw=true)

**用单个mget请求取回多个文档所需要的步骤顺序**

1. 客户端向Node1发送mget请求。
2. Node 1 为每个分片构建多文档获取请求，然后并行转发这些请求到托管在每个所需的主分片或者副本分片的节点上。一旦收到所有答复， Node 1 构建响应并将其返回给客户端。

#### bulk API

允许在单个批量请求中执行多个创建，索引、删除和更新请求

![image-20240627145127853](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627145127853.png?raw=true)

1. 客户端向Node1 发送bulk请求。
2. Node 1 为每个节点创建一个批量请求，并将这些请求并行转发到每个包含主分片的节点主机。

>#### `bulk` 请求
>
>1. 客户端发送`bulk`请求到Node1。
>2. Node1把请求分解，按分片分发到各节点。
>3. 各节点处理请求，把结果返回Node1。
>4. Node1汇总结果，返回给客户端。

## 4.9 分片原理

> 分片是ES最小的工作单元，文本字段中的每个单词需要被搜索，对数据库意味着需要单个字段有索引多值的能力。最好的支持是一个字段多个值需求的数据结构是倒排索引。

### 4.9.1 倒排索引

- ES使用一种称为倒排索引的结构，它适用于快速的全文搜索。
- 正向索引(forward index),反向索引(inverted index) 更熟悉的名字倒排索引。

所谓的正向索引，就是搜索引擎会将待搜索的文件都对应一个文件 ID，搜索时将这个

ID 和搜索关键字进行对应，形成 K-V 对，然后对关键字进行统计计数

![image-20240627155018707](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627155018707.png?raw=true)

```apl
但是互联网上收录在搜索引擎中的文档的数目是个天文数字，这样的索引结构根本无法满足
实时返回排名结果的要求。所以，搜索引擎会将正向索引重新构建为倒排索引，即把文件
ID对应到关键词的映射转换为关键词到文件ID的映射，每个关键词都对应着一系列的文件，
这些文件中都出现这个关键词。
```

![image-20240627155038546](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627155038546.png?raw=true)

- 个倒排索引由文档中所有不重复词的列表构成，对于其中每个词，有一个包含它的文

  档列表。例如，假设我们有两个文档，每个文档的 content 域包含如下内容：

  - The quick brown fox jumped over the lazy dog
  - Quick brown foxes leap over lazy dogs in summer

- 为了创建倒排索引，我们首先将每个文档的 content 域拆分成单独的 词（我们称它为 词条或 tokens ），创建一个包含所有不重复词条的排序列表，然后列出每个词条出现在哪个文档。结果如下所示：

  ![image-20240627155154871](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627155154871.png?raw=true)

- 比如现在搜素quick brown，我们只需要查找包含每个词条的文档

![image-20240627155335646](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627155335646.png?raw=true)

![image-20240627155511108](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627155511108.png?raw=true)

### 4.9.2 文档搜索

> 早期的全文索引为整个文档集合建立一个很大的倒排索引并将其写入到磁盘。一新的索引就绪，就的就会被替换，这样最近的变化便可以被检索到。

- **倒排索引被写入磁盘后是不可改变：它永久不会修改。**

  - **不需要锁**：如果你从来不更新索引，你就不需要担心多进程同时修改数据的问题。
  - 一旦索引被读入内核的文件系统缓存，便会留在哪里，由于其不变性。只要文件系统缓存中还有足够的空间，那么大部分读请求会直接请求内存，而不会命中磁盘。这提供了很大的性能提升
  - 其它缓存(像 filter 缓存)，在索引的生命周期内始终有效。它们不需要在每次数据改变时被重建，因为数据不会变化。

- 写入单个大的倒排索引允许数据被压缩，减少磁盘 I/O 和 需要被缓存到内存的索引的使用量。

  当然，一个不变的索引也有不好的地方。主要事实是它是不可变的! 你不能修改它。如

  果你需要让一个新的文档 可被搜索，你需要重建整个索引。这要么对一个索引所能包含的数据量造成了很大的限制，要么对索引可被更新的频率造成了很大的限制。


### 4.9.3 动态更新索引

- Elasticserch基于Lucene这个java库引入了 `按段搜索`的概念
- 每一 段 本身都是一个倒排索引， 但索引在 Lucene 中除表示所有段的集合外， 还增加了提交点的概念 — 一个列出了所有已知段的文件

#### 按段搜索

1. 新文档被搜集到内存索引缓存

![image-20240627160418104](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627160418104.png?raw=true)

2. 不时地, 缓存被 提交

   - 一个新的段，一个追加的倒排索引—被写入磁盘

   - 一个新的包含新段名字的 提交点 被写入磁盘

   - 磁盘进行同步 — 所有在文件系统缓存中等待的写入都刷新到磁盘，以确保它们

     被写入物理文件

3. 新的段被开启，让它包含的文档可见以被搜索

4. 内存缓存被清空，等待接收新的文档

>**段的作用**：可以理解为一个段是索引中的一个小文件，每次添加文档都会创建一个新的段，这样可以快速添加新内容，而不必修改已经存在的数据。
>
>**删除文档的标记**：删除文档时，我们并不真的去删除它，而是做个标记说“这个文档被删除了”。这样做的好处是速度快，因为不需要修改原始数据。
>
>**更新文档的操作**：更新文档时，旧文档也不被真的删除，而是标记为删除，同时添加一个新的版本。所以，更新文档的代价其实是“删除+添加”两个操作的成本。
>
>**查询结果的处理**：当我们查询数据时，所有段都会被搜索，虽然被删除的文档也会被找到，但在最终显示结果前，它们会被过滤掉。
>
>

### 4.9.4 近实时查询

> **延迟降低的原因**：按段搜索可以使新文档快速可搜索，但磁盘写入慢的问题仍然存在，因为要确保数据不丢失，必须执行耗时的 `fsync` 操作。
>
> **如何提高速度**：为了提高速度，不是每次都直接写入磁盘，而是先写入一个临时的地方——文件系统缓存。这就像是先把文件放在一个临时文件夹里，等到有空的时候再慢慢搬到磁盘上。
>
> **实际效果**：这样一来，文件已经在缓存中，可以像正常文件一样被搜索。即使数据还没有最终写入磁盘，也能被检索到，从而大大提高了新文档的可搜索速度。

![image-20240627170522639](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627170522639.png?raw=true)

- **新段的写入**：当有新文档需要索引时，Lucene 会将这些文档写入一个新的段中。这个新段会被放在文件系统缓存里，而不是立即写到磁盘上。
- **立即可见**：新段一旦写入缓存，并且被打开，新文档就可以立即被搜索到。这意味着，新文档几乎可以实时地出现在搜索结果中，而不需要等待完整的提交过程。
- **频繁执行**：由于写入缓存的操作非常轻量，这个过程可以频繁执行。即使我们不停地添加新文档，系统性能也不会受到太大影响。

![image-20240627170458090](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627170458090.png?raw=true)

#### Refresh 机制

- **什么是 `refresh`**：在 Elasticsearch 中，`refresh` 是一个让新文档快速可搜索的轻量过程。
- **默认行为**：默认情况下，每个分片每秒会自动执行一次 `refresh` 操作。

#### 近实时搜索

- **为什么是近实时**：因为文档的变化不会立即对搜索可见，需要等待下一次 `refresh` 执行。这通常会在一秒钟内发生，所以 Elasticsearch 被称为“近实时”搜索系统。

#### 用户困惑

- **新文档搜索不到**：新用户可能会困惑，为什么索引了一个文档后，立即搜索却找不到。这是因为文档的变化需要等到下一次 `refresh` 才会变得可见。
- **解决办法**：使用 `refresh` API 手动刷新，比如：`/users/_refresh`。这样可以立即让新文档对搜索可见。

#### 性能考虑

- **性能开销**：尽管 `refresh` 比完整提交轻量很多，但还是有一些性能开销。
- **测试环境 vs 生产环境**：在测试环境中，手动刷新很有用，但在生产环境中，不要每次索引一个文档都手动刷新。这会影响性能。

#### 接受近实时特性

- **理解并接受**：你的应用需要理解并接受 Elasticsearch 的近实时特性，而不是期待所有文档变化立即可见。

**你可能想优化索引速度而不是近实时搜索， 可以通过设置 refresh_interval ， 降低每个索**

**引的刷新频率**

```json
{
 "settings": {
 "refresh_interval": "30s" 
 }
}
```

refresh_interval 可以在既存索引上进行动态更新。 在生产环境中，当你正在建立一个大的新索引时，可以先关闭自动刷新，待开始使用该索引时，再把它们调回来

```json
# 关闭自动刷新
PUT /users/_settings
{ "refresh_interval": -1 } 
# 每一秒刷新
PUT /users/_settings
{ "refresh_interval": "1s" }
```



![image-20240627165758807](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627165758807.png?raw=true)

>
>
>

### 4.9.5 持久化变更

- **确保数据安全**：简单地将数据写入内存或文件系统缓存是不够的，因为这些都在内存中。为了保证数据在断电或程序崩溃后不丢失，必须使用 `fsync` 操作将数据真正写到硬盘上。

  **提交点的重要性**：每次完整提交时，Elasticsearch 会将所有的数据段写到硬盘，并创建一个提交点。这个提交点告诉系统哪些数据段是有效的，确保系统在重新启动时能正确恢复数据。

  **近实时搜索与数据恢复**：每秒钟的刷新操作能让新数据几乎实时被搜索到，但这并不等于数据已经安全写到硬盘上。为了保证数据安全，仍需要定期进行完整提交。

  **事务日志的保护**：为了防止在两次完整提交之间的数据丢失，Elasticsearch 使用 `translog` 记录每次操作。即使系统崩溃，也能通过 `translog` 恢复未完成的操作，确保数据不丢失。

- **整体流程如下**

  1. 一个文档被索引之后，就会被添加到内存缓冲区，并且追加到了 translog，随后立即fulsh到disk translog中

  ![image-20240627173249641](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627173249641.png?raw=true)

  2. 刷新（refresh）使分片每秒被刷新（refresh）一次：
     - 当进行刷新操作时，内存缓冲区中的所有文档会被写入到一个新的段（segment）中。这个过程会将数据从内存缓冲区复制到文件系统的缓存中，并且并没有立即执行 `fsync` 操作来将数据物理写入到硬盘，因此数据暂时保留在文件系统的缓存中。
     - 写入完毕后，新的段会被打开，使其中的文档可以被搜索。这意味着虽然数据还没有被持久化到硬盘，但是它们已经可以被 Elasticsearch 查询到了。
     - 一旦新的段被打开，内存缓冲区中的文档就会被清空，为接受新的写入操作做好准备

![image-20240627173326718](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627173326718.png?raw=true)

3. 这个进程继续工作，更多的文档被添加到内存缓冲区和追加到事务日志

   ![image-20240627173617276](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240627173617276.png?raw=true)

4. **刷新索引**：

   - 定期或根据配置，当事务日志（translog）变得足够大时，Elasticsearch 会触发索引的刷新操作。
   - 在刷新过程中，所有在内存缓冲区中的待索引文档都会被写入到一个新的段（segment）中。这确保了内存中的所有变更都被持久化到磁盘，以便后续搜索能够访问这些文档。

5. **清空缓冲区**：

   - 内存缓冲区中的数据在成功写入到新段后会被清空，以便接受新的索引操作。

6. **写入提交点到硬盘**：

   - 一旦新段的数据被写入磁盘，Elasticsearch 将创建一个提交点（commit point），并将其写入硬盘。这个提交点记录了当前索引状态的快照，包括新创建的段。

   **刷新文件系统缓存**：

   - 文件系统缓存中的数据通过 fsync 操作被刷新到磁盘，以确保数据持久化到物理存储介质。这是为了防止在断电或系统崩溃时数据丢失。

   **删除旧的事务日志**：

   - 当新的事务日志创建完成并已持久化后，旧的事务日志会被删除，以释放磁盘空间并保持系统的高效性能。

   **事务日志的作用**：

   - 事务日志（translog）是一个持久化记录，用来存储所有尚未写入到磁盘的操作。当 Elasticsearch 启动时，它会使用最后一个提交点来恢复已知的段状态，并且会重放事务日志中在最后一次提交后发生的变更操作。
   - 事务日志还允许实时的 CRUD 操作（创建、读取、更新、删除）。在执行查询、更新或删除操作时，Elasticsearch 首先检查事务日志中是否有最近的变更，确保

**实时地获取到文档的最新版本。**

![image-20240628092039732](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240628092039732.png?raw=true)

- **定期自动刷新**：每个分片（shard）可能会每隔一段时间自动刷新，例如每30分钟一次，这有助于确保数据在内存中的变更被持久化到磁盘上的新段中。
- **Translog 大小过大**：当事务日志（translog）变得过大时，Elasticsearch 也会触发刷新操作，以控制日志的大小并确保数据的及时落盘。

重要的是理解以下几点：

- **Flush 的作用**：Flush 操作确保了内存中的待索引数据被写入到磁盘上的新段中，以便后续可以被搜索和访问。
- **Translog 的作用**：事务日志（translog）用于保证数据操作的持久性，确保即使在节点重启或发生故障时，操作不会丢失。默认情况下，translog 每隔5秒会被 fsync 到磁盘，或者在每次写请求（如索引、删除、更新、批量操作）完成后执行。
- **性能和数据一致性权衡**：每次执行 fsync 会带来一些性能损失，因为这涉及将数据从内存中刷写到磁盘。尤其在大量文档的批量导入中，这种损失相对较小。但对于某些场景，可以使用异步的方式来控制 fsync 的频率，以减少性能影响，不过这样可能会在某些情况下导致少量数据丢失。

### 4.9.6 段合并

>- 由于自动刷新流程每秒会创建一个新的段 ，这样会导致短时间内的段数量暴增。而段
>  数目太多会带来较大的麻烦。 每一个段都会消耗文件句柄、内存和 cpu 运行周期。更重要
>   的是，每个搜索请求都必须轮流检查每个段；所以段越多，搜索也就越慢。

- **Elasticsearch 通过在后台进行段合并来解决这个问题。小的段被合并到大的段，然后这些大** **的段再被合并到更大的段。**

- **段合并的时候会将那些旧的已删除文档从文件系统中清除。被删除的文档（或被更新文档的** **旧版本）不会被拷贝到新的大段中。**

- 启动段合并不需要你做任何事。进行索引和搜索时会自动进行。

  **索引过程中的刷新操作**：

  - 当进行索引操作时，Elasticsearch 会将待索引的文档添加到内存缓冲区。
  - 定期或根据配置，这些内存中的文档会被刷新（refresh）到一个新的段（segment）中，并且这个新段会被打开以供搜索使用。

  **段合并过程**：

  - 合并进程会选择一小部分大小相似的段，并在后台将它们合并成更大的段。这个过程不会中断索引和搜索操作，因为合并是在后台异步进行的。
  - 合并的目的是减少段的数量和优化段的大小，以提升性能和减少资源消耗。

  ![image-20240628104253254](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240628104253254.png?raw=true)

  **合并结束后的处理**：

  - 一旦合并操作完成，旧的段会被删除，从而释放资源并优化存储空间。
  - 新的合并后的段会进行刷新（flush），确保所有变更被持久化到磁盘上。
  - 一个新的提交点（commit point）会被创建，其中包含新的大段的信息，同时排除了旧的和较小的段。
  - 新的大段随后被打开，使其能够被搜索引擎使用。

  ![image-20240628104515855](https://github.com/liuzhenhua1223/Image/blob/master/Elastic/image-20240628104515855.png?raw=true)

>合并大的段需要消耗大量的 I/O 和 CPU 资源，如果任其发展会影响搜索性能。Elasticsearch
>
>在默认情况下会对合并流程进行资源限制，所以搜索仍然 有足够的资源很好地执行。

## 4.10 文档分析

### 分析过程包括以下步骤：

1. **字符过滤器（Character Filters）**：
   - 字符过滤器是分析器的第一步，用于在分词之前对文本进行预处理和整理。它们按顺序处理文本，可以执行诸如去除 HTML 标记、转换特定字符等操作。例如，将 "&" 转换为 "and"，或者去除 HTML 标签。
2. **分词器（Tokenizer）**：
   - 分词器将经过字符过滤器处理后的文本分割成单个的词条（tokens）。这些词条通常是搜索引擎实际用来构建索引的基本单位。简单的分词器可能根据空格和标点符号将文本分割成词条。
3. **Token 过滤器（Token Filters）**：
   - 最后，词条通过一系列的 token 过滤器。这些过滤器按顺序处理每个词条，并可以修改、删除或添加词条。它们用于标准化词条，提高搜索的效果和准确性。例如，将词条统一转换为小写（lowercasing），移除停用词（如 "a", "and", "the"），或者扩展词条（如将同义词 "jump" 和 "leap" 视为相同）。

### 作用和优势：

- **提高可搜索性（Recall）**：通过标准化和处理文本，分析器可以提高词条在搜索时的召回率（recall），即能够找到更多与搜索条件匹配的文档。
- **优化索引建立**：分析器的工作能够有效地构建倒排索引，使得搜索操作更加高效和快速。
- **灵活性和可定制性**：Elasticsearch 提供了丰富的字符过滤器和 token 过滤器，可以根据需求进行组合和定制，以适应不同的语言、文本类型或搜索场景。

### 4.10.1 内置分词器

#### 标准分析器（Standard Analyzer）

- **处理过程**：

  - 根据 Unicode 联盟的单词边界规则划分文本。
  - 删除大部分标点符号。
  - 将所有词条转换为小写。

- **词条输出**：

  ```
  vbnet
  复制代码
  set, the, shape, to, semi, transparent, by, calling, set_trans, 5
  ```

  解释：标准分析器将原始字符串按照单词边界划分，转换为小写，并删除大部分标点符号，生成相应的词条集合。

#### 简单分析器（Simple Analyzer）

- **处理过程**：

  - 在非字母字符处分隔文本。
  - 将所有词条转换为小写。

- **词条输出**：

  ```
  vbnet
  复制代码
  set, the, shape, to, semi, transparent, by, calling, set, trans
  ```

  解释：简单分析器按照非字母字符分隔文本，将词条转换为小写，生成相应的词条集合。注意，词条 "set_trans" 在简单分析器中被分为 "set" 和 "trans"。

#### 空格分析器（Whitespace Analyzer）

- **处理过程**：

  - 在空格处分隔文本。

- **词条输出**：

  ```
  scss
  复制代码
  Set, the, shape, to, semi-transparent, by, calling, set_trans(5)
  ```

  解释：空格分析器根据空格字符分隔文本，生成相应的词条集合。词条保持原始大小写和标点。

#### 语言分析器（Language-specific Analyzer，比如英语分析器）

- **处理过程**：

  - 考虑特定语言的语法规则。
  - 删除常见的无用词（停用词）。
  - 提取词干（Stemming）。

- **词条输出**：

  ```
  sql
  复制代码
  set, shape, semi, transpar, call, set_tran, 5
  ```

  解释：英语分析器根据英语语法规则处理文本，删除常见停用词（如 "the", "and"），并将词条转换为它们的词干形式。例如，"transparent" 变为 "transpar"，"calling" 变为 "call"，"set_trans" 变为 "set_tran"。

# 第五章Elasticserch集成

# 第六章Elasticserch优化

# 第七章Elasticserch




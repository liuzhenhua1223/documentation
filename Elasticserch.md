# Elasticserch 

[TOC]



# 第一章 Elasticserch概述

`ES核心`主要是为了查询：文章、视频、图片、网站信息等等

## 数据分类

### 结构化数据

> 可以以二维表表示的数据称为结构化数据，类似execl的表示方式

- 优点：方便管理、方便查询
- 缺点：现有结构，扩展比较难，

![image-20240624100856347](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624100856347.png?raw=true)

### 非机构化数据

> 以key和values进行表示的数据，无法以二维表表示
>
> - 视频、图片、文档等
> - Mongodb、redis

![image-20240624101458997](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624101458997.png?raw=true)

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
>

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
  >

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

![image-20240624105442007](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624105442007.png?raw=true)

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

![image-20240624111418157](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624111418157.png?raw=true)

![image-20240624111623168](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624111623168.png?raw=true)

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

![image-20240624160625069](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624160625069.png?raw=true)

## 2.5 HTTP操作

启动ES-Postman

![image-20240624161525820](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624161525820.png?raw=true)

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

![image-20240624162946932](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624162946932.png?raw=true)

![image-20240624162952436](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624162952436.png?raw=true)

![image-20240624163002960](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624163002960.png?raw=true)

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

![image-20240624163143268](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624163143268.png?raw=true)

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

![image-20240624163638409](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624163638409.png?raw=true)



这里请求路径中的_cat 表示查看的意思，indices 表示索引，所以整体含义就是查看当前 ES

服务器中的所有索引，就好像 MySQL 中的 show tables 的感觉，服务器响应结果如下

```json
health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   shopping eC4Vo-uYQHiW8zkn-lRYFg   1   1          0            0       208b           208b

```

![image-20240624231442806](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624231442806.png?raw=true)

### 3.删除索引 

http://127.0.0.1:9200/shopping

```JSON
{
    "acknowledged": true
}
```

![image-20240624163723489](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624163723489.png?raw=true)

![image-20240624164054178](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624164054178.png?raw=true)

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

![image-20240624171317221](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624171317221.png?raw=true)

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

![image-20240624232142445](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624232142445.png?raw=true)



![image-20240624170441196](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624170441196.png?raw=true)

- **再次使用put提示不能使用put因为PUT不能生成随机唯一性标识**

![image-20240624170748713](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624170748713.png?raw=true)

### 2. 查询文档

#### 查询单个文档

GET：http://127.0.0.1:9200/shopping/_doc/1001

![image-20240624232838609](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624232838609.png?raw=true)

#### 查询所有文档

- 创建一个新的接口进行页面进行查询

![image-20240624234502755](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624234502755.png?raw=true)

### 3. 完全覆盖

#### 全量覆盖PUT

和新增文档一样，输入相同的 URL 地址请求，如果请求体变化，会将原有的数据内容覆盖

在 Postman 中，向 ES 服务器发 **PUT/POST** 请求

![image-20240624234857397](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624234857397.png?raw=true)

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

![image-20240624235307387](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624235307387.png?raw=true)

![image-20240624235326172](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624235326172.png?raw=true)

### 4. 删除文档

删除一个文档不会立即从磁盘上移除，它只是被标记成已删除（逻辑删除）。

在 Postman 中，向 ES 服务器发 **DELETE** 请求DELETE：http://127.0.0.1:9200/shopping/_doc/1001

![image-20240624235702569](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240624235702569.png?raw=true)

## 查询操作

### 条件查询

- 主题查询

  ```http
  GET http://127.0.0.1:9200/shopping/_search?q=category:华为
  ```

![image-20240625001046186](../../../../liuzh/AppData/Roaming/Typora/typora-user-images/image-20240625001046186.png)

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

  ![image-20240625001726395](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625001726395.png?raw=tru)

- match_all查询所有

- ```json
  {
  "query":{
      "match_all":{
      }
  }
  }
  ```

  ![image-20240625001849648](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625001849648.png?raw=true)

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

![image-20240625002513784](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625002513784.png?raw=true)

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

![image-20240625002734418](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625002734418.png?raw=true)

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

![image-20240625003359240](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625003359240.png?raw=true)

### 多条件查询

#### 但条件匹配查询must

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

![image-20240625004344889](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625004344889.png?raw=true)

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

![image-20240625004840224](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625004840224.png?raw=true)

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

![image-20240625005115542](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625005115542.png?raw=true)

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

  

![image-20240625010243206](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625010243206.png?raw=true)

![image-20240625010517985](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625010517985.png?raw=true)

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

![image-20240625010623613](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625010623613.png?raw=true)

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

![image-20240625011025268](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625011025268.png?raw=true)

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

![image-20240625011221613](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625011221613.png?raw=true)

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

![image-20240625011409211](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625011409211.png?raw=true)

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

![image-20240625011508222](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625011508222.png?raw=true)

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

![image-20240625012349399](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625012349399.png?raw=true)

```json
{
    "query":{
        "match":{
            "name":"zhangsan"
        }
    }
}
```

![image-20240625012758818](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625012758818.png?raw=true)



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

![image-20240625012925518](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625012925518.png?raw=true)

![](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625012925518.png?raw=true)

#### keywold-false

不支持查询

# 第三章Elasticserch环境

## 创建Maven项目

![1](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/1.gif?raw=true)



![image-20240625145649933](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625145649933.png?raw=true)

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

![image-20240625150648244](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625150648244.png?raw=true)

## 索引操作

### 创建索引

![image-20240625150752044](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625150752044.png?raw=true)



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

![image-20240625152105228](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625152105228.png?raw=true)

### 查询索引

![image-20240625153106230](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625153106230.png?raw=true)

![image-20240625153041860](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625153041860.png?raw=true)

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

![image-20240625154505899](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625154505899.png?raw=true)

![image-20240625154208772](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625154208772.png?raw=true)

![image-20240625154226467](../../../../liuzh/AppData/Roaming/Typora/typora-user-images/image-20240625154226467.png)

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

![image-20240625161612816](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625161612816.png?raw=true)

![image-20240625162004649](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625162004649.png?raw=true)

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

![image-20240625162809600](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625162809600.png?raw=true)

![image-20240625163039781](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625163039781.png?raw=true)

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

![image-20240625164010002](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625164010002.png?raw=true)

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

![image-20240625165043923](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625165043923.png?raw=true)

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

![image-20240625170955137](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625170955137.png?raw=true)

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

![image-20240625172618556](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625172618556.png?raw=true)

![image-20240625172547340](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625172547340.png?raw=true)

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

![image-20240625223216209](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625223216209.png?raw=true)

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

![image-20240625230312200](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625230312200.png?raw=true)

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

![image-20240625231904857](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625231904857.png?raw=true)



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

![image-20240625231216221](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625231216221.png?raw=true)

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

![image-20240625232257390](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625232257390.png?raw=true)

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

![image-20240625232816944](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625232816944.png?raw=true)

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

![image-20240625234343647](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625234343647.png?raw=true)

![image-20240625234637556](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625234637556.png?raw=true)

![image-20240625234959374](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625234959374.png?raw=true)



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

![image-20240625235337054](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240625235337054.png?raw=true)

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

![image-20240626001659219](https://github.com/liuzhenhua1223/Image/blob/master//Elastic/image-20240626001659219.png?raw=true)

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

# 第五章Elasticserch集成

# 第六章Elasticserch优化

# 第七章Elasticserch




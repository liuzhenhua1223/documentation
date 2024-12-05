# Golang硅谷

# 第一章：Golang开山篇

## 1.1Golang的学习方向

Go语言，我们可以简单的写成Golang

![image-20231014011552514](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014011552514.png?raw=true)

## 1.2Golang的应用领域

### 12.1区块链的应用开发

![image-20231014011618206](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014011618206.png?raw=true)

### 1.2.2后台的服务应用

![image-20231014011640759](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014011640759.png?raw=true)

### 1.2.3云计算/云服务后台应用

![image-20231014011659679](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014011659679.png?raw=true)

## 1.3学习方法介绍

![image-20231014011903641](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014011903641.png?raw=true)

# 第二章Golang概述

## 2.1什么是程序

程序：就是完成某个功能的指令的集合。如下图：

![image-20231014012116060](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014012116060.png?raw=true)

## 2.2Go语言诞生小故事

### 2.2.1 Go语言的核心开发团队-三个大牛

![image-20231014012220965](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014012220965.png?raw=true)

### 2.2.2Google创造Golang的原因

![image-20231014012247658](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014012247658.png?raw=true)

### 2.2.3Golang的发展历程

2007 年，谷歌工程师 Rob Pike, Ken Thompson 和 Robert Griesemer 开始设计一门全新的语言，这是Go 语言的最初原型。

2009 年 11 月 10 日，Google 将 Go 语言以开放源代码的方式向全球发布。2015 年 8 月 19 日，Go 1.5 版发布，本次更新中移除了”最后残余的 C代码
2017 年 2 月17 日，Go 语言 Go 1.8 版发布
2017 年8 月24 日，Go 语言 Go 1.9 版发布。 1.9.2 版本
2018 年2月16 日，Go 语言 Go 1.10 版发布。

## 2.3Golang的语言特点

- 简介

  - Go 语言保证了既能到达静态编译语言的安全和性能，又达到了动态语言开发维护的高效率 ，使用一个表达式来形容 Go 语言：Go = C + Python , 说明 Go 语言既有 C 静态语言程 序的运行速度，又能达到 Python 动态语言的快速开发

  1. 从 C 语言中继承了很多理念，包括表达式语法，控制结构，基础数据类型，调用参数传值，指针等 等，也保留了和 C 语言一样的编译执行方式及弱化的指针 

  - 举一个案例(体验)： //go 语言的指针的使用特点(体验) 

    func testPtr(num *int) {

     *num = 20

    }

  2. 引入包的概念，用于组织程序结构，Go 语言的一个文件都要归属于一个包，而不能单独存在。

![image-20231014100922880](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014100922880.png?raw=true)

3. 垃圾回收机制，内存自动回收，不需开发人员管理

4. 天然并发 (重要特点

   1. 从语言层面支持并发，实现简单

   2. goroutine，轻量级线程，可实现大并发处理，高效利用多核

   3. 基于 CPS 并发模型(Communicating Sequential Processes )实现

   4. 吸收了管道通信机制，形成 Go 语言特有的管道 channel 通过管道 channel , 可以实现不同的 goroute 之间的相互通信。

   5. 函数可以返回多个值。举例

      ```
      //写一个函数，实现同时返回 和，差
      //go 函数支持返回多个值
      func getSumAndSub(n1 int, n2 int) (int, int ) {
      sum := n1 + n2 //go 语句后面不要带分号. sub := n1 - n2
      return sum , sub
      }
      ```

   6. 新的创新：比如切片 slice、延时执行 defer

## 2.8Go语言快速开发入门

### 2.8.1需求

1. 要求开发一个hello.go程序，可以输出hello.world

### 2.8.2开发步骤

1. 开发这个项目是，go的目录结构是怎么处理呢如下图

![image-20231014101513885](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014101513885.png?raw=true)

2. 代码如下

   ![image-20231014102025336](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102025336.png?raw=true)

```cmd
E:\goproject\src\gocode\gw\project01\main>go run hell.go
Hello, World!
```

对上图说明：

(1) go 文件的后缀是 .go 

(2) package main 表示该 hello.go 文件所在的包是 main, 在 go 中，每个文件都必须归属于一个包。 

(3) import “fmt” 表示：引入一个包，包名 fmt, 引入该包后，就可以使用 fmt 包的函数，比如：fmt.Println 

(4) func main() { }

func 是一个关键字，表示一个函数

main 是函数名，是一个主函数，即我们程序的入口。

(5) fmt.Println(“hello”)

表示调用 fmt 包的函数 Println 输出“hello.world"

3. 通过go build 命令对该go文件进行编译，生成.exe文件

​			![image-20231014102337315](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102337315.png?raw=true)

4. 运行hello.exe文件即可
5. 注意：通过 go run 命令可以直接运行hello.go程序[类似执行一个脚本文件的形式]

### 2.8.3linux下如何开发Go程序

说明：linux下开发Go和windows基本是一样的，只是在运行执行的程序时，是以`./文件名方式`

![image-20231014102544804](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102544804.png?raw=true)

### 2.8.6GoGolang执行流程分析

1. 如果是对源码编译后，在执行，Go的执行流程如下图

![image-20231014102728022](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102728022.png?raw=true)

2. 如果我们是对源码直接 执行 go run 源码，Go 的执行流程如下

![image-20231014102740356](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102740356.png?raw=true)

两种执行流程的方式区别

1. 如果我们先编译生成了可执行文件，那么我们可以将该可执行文件拷贝到没有 go 开发环境的机 器上，仍然可以运行
2. 如果我们是直接 go run go 源代码，那么如果要在另外一个机器上这么运行，也需要 go 开发 环境，否则无法执行
3. ) 在编译时，编译器会将程序运行依赖的库文件包含在可执行文件中，所以，可执行文件变大了 很多

### 2.8.7编译和运行说明

1. 有了 go 源文件，通过编译器将其编译成机器可以识别的二进制码文件
2. 在该源文件目录下，通过 go build 对 hello.go 文件进行编译。可以指定生成的可执行文件名，在 windows 下 必须是 .exe 后缀

![image-20231014102913275](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102913275.png?raw=true)

3. 如果程序没有错误，没有任何提示，会在当前目录下会出现一个可执行文件(windows 下是.exe Linux 下是一个可执行文件)，该文件是二进制码文件，也是可以执行的程序。
4. ) 如果程序有错误，编译时，会在错误的那行报错。有助于程序员调试错误

![image-20231014102939749](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102939749.png?raw=true)

5. 运行有两种形式

![image-20231014102959306](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014102959306.png?raw=true)

### 2.8.8Go程序开发的注意事项

1. Go 源件以 "go" 为扩展名 。
2. Go 应用程序的执行入口是 main()函数。 这个是和其它编程语言（比如 java/c
3. Go 语言严格区分大小写。
4. Go 方法由一条条语句构成，每个语句后不需要分号(Go 语言会在每行后自动加分号)，这也体现出 Golang的简洁性
5. Go 编译器是一行行进行编译的，因此我们一行就写一条语句，不能把多条语句写在同一个，否 则报错

![image-20231014104604764](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014104604764.png?raw=true)

6. go 语言定义的变量或者 import 的包如果没有使用到，代码不能编译通过。

​	![image-20231014104636628](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014104636628.png?raw=true)

6. 大括号都是成对出现的，缺一不可

## 2.9Go语言的转义符(escape char)

说明:常用的转义字符有如下:

1. **\t:表示一个制表符，通常使用它可以排版**

2. **\n：换行符**

3. **\\\\:一个\**

4. **\\"一个"**

5. ***

   **\r:一个回测 fmt.Println("天龙八部雪山飞狐\r张飞")**

   ![image-20231014105502023](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014105502023.png?raw=true)

```go
package main
import "fmt" //fmt包中提供格式化，输出，输入的函数
func main() {
	//转义符的使用 \t
	fmt.Println("Hello\tWorld!")
	fmt.Println("lzh\nlzh2")
	fmt.Println("D:\\桌面\\桌面\\笔记")
	fmt.Println("刘振华\"")
	fmt.Println("天龙八部\r振华")
	fmt.Println("天龙八部\r振华九部")
}
```

课堂案例：

要求：用一句话输出如下

![image-20231014105538218](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014105538218.png?raw=true)

```go
package main
import "fmt" //fmt包中提供格式化，输出，输入的函数
func main() {
	//转义符的使用 \t
	fmt.Println("姓名:\t刘振华\n年龄:\t23\n籍贯:\t安阳\n住址\t北京\n")
	fmt.Println("==================")
	fmt.Println("姓名\t年龄\t籍贯\t住址\t\n刘振华\t23\t安阳\t北京")
}
```

![image-20231014110006284](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110006284.png?raw=true)

## 2.10Golang开发常见问题解决方法

### 2.10.1文件名或路径错误

![image-20231014110051659](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110051659.png?raw=true)

### 2.10.2小结提升

学习编程最容易犯的错是语法错误 。Go 要求你必须按照语法规则编写代码。如果你的程序违反了 语法规则，例如：忘记了大括号、引号，或者拼错了单词，Go 编译器都会报语法错误，`要求：尝试 着去看懂编译器会报告的错误信息`

![image-20231014110126527](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110126527.png?raw=true)

## 2.11注释（comment）

### 2.11.1介绍注释

- 用于注解说明解释程序的文字就是注释，注释提高了代码的阅读性； 
- 注释是一个程序员必须要具有的良好编程习惯。将自己的思想通过注释先整理出来，再用代码去 体现。 

### 2.11.2在Golang中注释有两种方式

1. 行注释

   1. 基本语法

      //注释内容

      快捷键ctl+/

      ![image-20231014110258815](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110258815.png?raw=true)

2. 块注释（多行注释）

   1. 基本语法

      /*

      注释内容

      */

      快捷键：alt+shift+a

      ![image-20231014110352069](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110352069.png?raw=true)

## 2.12规范的代码风格

### 2.12.1正确的注释和注释风格

1. Go 官方推荐使用行注释来注释整个方法和语句。
2. 带看 Go源码

### 2.12.2正确的缩进和空白

1. 使用一次 tab 操作，实现缩进,默认整体向右边移动，时候用 shift+tab 整体向左移 
2. 或者使用 gofmt 来进行格式化 

![image-20231014110742252](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110742252.png?raw=true)

3. 运算符两边习惯性加空格：

![image-20231014110848420](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014110848420.png?raw=true)

4. Go 语言的代码风格.

```go
package main
import "fmt"
func main() {
fmt.Println("hello,world!")
}
上面的写法是正确的. package main
import "fmt"
func main()
{
fmt.Println("hello,world!")
}
```

上面的写法不是正确，Go 语言不允许这样编写。 【Go 语言不允许这样写，是错误的！】 Go 设计者思想: 一个问题尽量只有一个解决方法

5. 一行最长不超过 80 个字符，超过的请使用换行展示，尽量保持格式优雅

![image-20231014111135163](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014111135163.png?raw=true)

## 2.13Golang官方编程指南

说明： Golang 官方网站 https://golang.org

![image-20231014111240094](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014111240094.png?raw=true)

## 2.17 本章的知识回顾

- GO语言的SDK是什么

  - SDK 就是软件开发工具包。我们做 Go 开发，首先需要先安装并配置好 sdk.

- Golang 环境变量配置及其作用。

  - GOROOT: 指定 go sdk 安装目
  - Path: 指令 sdk\bin 目录：go.exe godoc.exe gofmt.exe
  - GOPATH: 就是 golang 工作目录：我们的所有项目的源码都这个目录下。

- Golang 程序的编写、编译、运行步骤是什么? 能否一步执行?

  - 编写：就是写源码
  - 编译：go build 源码 =》 生成一个二进制的可执行文件运行：1. 对可执行文件运行 xx.exe ./可执行文件 2. go run 源码

- Golang程序编程写的规则

  - go 文件的后缀 .go

  - go 程序区分大小

  - go 的语句后，不需要带分号

  - go 定义的变量，或者 import 包，必须使用，如果没有使用就会报错

  - go 中，不要把多条语句放在同一行。否则报错

  - go 中的大括号成对出现，而且风格

    - func main() {

      //语句

       }

- 简述：在配置环境、编译、运行各个步骤中常见的错误

  - 对初学者而言，最容易错的地方拼写错误。比如文件名，路径错误。拼写错误

# 第三章Golang变量

## 3.1为什么需要变量

### 3.1.1一个程序就是一个世界

![image-20231014130246005](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130246005.png?raw=true)

### 3.1.2变量是程序的基本组成单位

不论是使用哪种高级程序语言编写程序,变量都是其程序的基本组成单位，比如一个示意图：

![image-20231014130312105](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130312105.png?raw=true)

## 3.2变量的介绍

### 3.2.1变量的概念

变量相当于内存中一个数据存储空间的表示，你可以把变量看做是一个房间的门 牌号，通过门牌号我们可以找到房间，同样的道理，通过变量名可以访问到变量 (值)。

### 3.2.2变量的使用步骤

1. 声明变量（也叫：定义变量）
2. 非变量赋值
3. 使用变量

## 3.3变量快速入门案例

![image-20231014130602844](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130602844.png?raw=true)

### 3.4变量使用注意事项

1. 变量表示内存中的一个存储区域
2. 该区域有自己的名称（变量名）和类型（数据类型）

![image-20231014130655081](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130655081.png?raw=true)

3. Golang 变量使用的三种方

   1. ) 第一种：指定变量类型，声明后若不赋值，使用默认值

   ![image-20231014130742863](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130742863.png?raw=true)

2. 第二种：根据直自行判断定义变量类型（类型推导）

   ![image-20231014130836396](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130836396.png?raw=true)

3. 第三种：省略var，注意 `:=`左侧的变量不应该是已经声明过的，否则会导致编译错误

![image-20231014130952627](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014130952627.png?raw=true)

4. 多变量声明

在编程中，有时我们需要一次性声明多个变量，Golang 也提供这样的语法 举例说明

![image-20231014131111173](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131111173.png?raw=true)

如何一次性声明多个全局变量【在 go 中函数外部定义变量就是全局变量

![image-20231014131208894](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131208894.png?raw=true)

5. 该区域的数据值可以在同一类型范围内不断变化(重点)

![image-20231014131238308](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131238308.png?raw=true)

6. 变量在同一个作用域(在一个函数或者在代码块)内不能重名

![image-20231014131255541](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131255541.png?raw=true)

7. 变量=变量名+值+数据类型，这一点请大家注意，变量的三要素
8. Golang 的变量如果没有赋初值，编译器会使用默认值, 比如 int 默认值 0 string 默认值为空串， 小数默认为 

## 3.5变量的声明，初始化和赋值

![image-20231014131333733](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131333733.png?raw=true)

##  3.6程序中`+`号的使用

1. 当左右两边都是数组类型是，则做加法运算
2. 当左右两边的都是字符串，则做字符串拼接

![image-20231014131929898](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131929898.png?raw=true)

## 3.7 数据类型的基本介绍

![image-20231014131947778](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014131947778.png?raw=true)

## 3.8整数类型

### 3.8.1基本介绍

简单说，就是用于存放整数值的，比如：0-1，2345等等。

### 3.8.2案例演示

### 3.8.3整数的各个类型

![image-20231014132109622](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014132109622.png?raw=true)

![image-20231014132200378](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014132200378.png?raw=true)

int的无符号的类型

![image-20231014132223461](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014132223461.png?raw=true)

![image-20231014172135568](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014172135568.png?raw=true)

int的其他类型的说明

![image-20231014172153414](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014172153414.png?raw=true)

![image-20231014172245365](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014172245365.png?raw=true)

### 整形的使用细节

1. Golang各整数类型分为：有符号和无符号，int uint的大小和系统有关
2. Golang的整形默认声明为int类型

```go
package main
import (
	"fmt"
	"reflect"
)
func main(){
	//整形的使用细节
	var n1 = 100
	//这里我们给介绍一下如何查看某个变量的数据类型
	//fmt.Println()可以用于做格式化输出。
	fmt.Println(n1, "is of type", reflect.TypeOf(n1))
}
```

![image-20231014172611277](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014172611277.png?raw=true)

3. 如何在程序查看某个变量的字（使用较多）

```go
package main
import (
	"fmt"
	// reflect: 反射，用于获取和操作变量的类型信息。
	// "reflect"
	// unsafe: 低级内存操作，允许直接访问内存和数据。
	"unsafe"
)
func main(){
	// //整形的使用细节
	// var n1 = 100
	// //这里我们给介绍一下如何查看某个变量的数据类型
	// //fmt.Println()可以用于做格式化输出。
	// fmt.Println(n1, "is of type", reflect.TypeOf(n1))
	var n2 int64 = 10
	fmt.Println(n2, "is of type",unsafe.Sizeof(n2))
}
```

4. Golang程序中整形变量在使用时，遵守保小不保大的原则，即：在保证正常运行下使用占用空间小的数据类型【如：年龄】

```go
package main
import (
	"fmt"
	// reflect: 反射，用于获取和操作变量的类型信息。
	"reflect"
	// unsafe: 低级内存操作，允许直接访问内存和数据。
	"unsafe"
)
func main(){
	// //整形的使用细节
	// var n1 = 100
	// //这里我们给介绍一下如何查看某个变量的数据类型
	// //fmt.Println()可以用于做格式化输出。
	// fmt.Println(n1, "is of type", reflect.TypeOf(n1))
	var n2 int64 = 10
	fmt.Println(n2, "is of type",unsafe.Sizeof(n2))

	//Golang程序中整形变量在使用时，遵守保小不保大的原则，
	//即:在保证程序正确运行下，尽量使用占用空间小的数据类型
	var age byte = 90
	fmt.Println(age, "is of type", reflect.TypeOf(age))
}
```

![image-20231014174055698](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014174055698.png?raw=true)

5. bit：计算机中的最小存储单位。byte:计算机中基本存储单元。[二进制再详细说] 1byte = 8 bit

## 3.9小数类型/浮点类型

### 3.9.1基本介绍

小数类型就是用于存放小数的，比如：1.2.0.23-1.911

### 3.9.2案例演示

```go
package main
import (
	"fmt"
)
//演示Golang中小数类型使用
func main() {
	var price float32 = 89.21
	fmt.Println(price)
	fmt.Println(price * 100)
}	
```

![image-20231014174358667](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014174358667.png?raw=true)

### 3.9.3小数类型分类

![image-20231014174422163](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014174422163.png?raw=true)

1. 关于浮点数在机器中存放形式的简单说明,浮点数=符号位+指数位+尾数位 说明：浮点数都是有符号的.

```go
package main
import (
	"fmt"
)
//演示Golang中小数类型使用
func main() {
	var price float32 = 89.21
	fmt.Println(price)
	fmt.Println(price * 100)

	var num1 float32 = -0.0093
	var num2 float64 = -72352.023
	fmt.Println(num1, num2)
}	
```

![image-20231014174937883](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014174937883.png?raw=true)

2. 尾数部分可能丢失，造成精度损失。-123.12000

```go
package main
import (
	"fmt"
)
//演示Golang中小数类型使用
func main() {
	var price float32 = 89.21
	fmt.Println(price)
	fmt.Println(price * 100)

	var num1 float32 = -0.0093
	var num2 float64 = -72352.023
	fmt.Println(num1, num2)

	//尾数部分可以丢失，造成精度损失。 -123.0000901
	var num3 float32 = 123.0000901
	var num4 float64 = 123.0000901
	fmt.Println(num3, num4)
}	
```

![image-20231014175246363](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014175246363.png?raw=true)

说明：float64 的精度比 float32 的要准确. 

说明：如果我们要保存一个精度高的数，则应该选用 float64

3. 浮点型的存储分为三部分：符号位+指数位+尾数位 在存储过程中，精度会有丢失

## 3.9.4浮点类型使用细节

1. Golang 浮点类型有固定的范围和字段长度，不受具体 OS(操作系统)的影响。
2. Golang 的浮点型默认声明为 float64类型。

![image-20231014175510166](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014175510166.png?raw=true)

3. 浮点类型常量有两种表示形式

十进制数形式：如5.12 .512（必须要有小数点）

科学计数法形式：5.1234e2 = 5.12 * 10的2次方 5.12E-2=5.12/10的次方

```go
package main
import (
	"fmt"
)
//演示Golang中小数类型使用
func main() {
	var price float32 = 89.21
	fmt.Println(price)
	fmt.Println(price * 100)

	var num1 float32 = -0.0093
	var num2 float64 = -72352.023
	fmt.Println(num1, num2)

	//尾数部分可以丢失，造成精度损失。 -123.0000901
	var num3 float32 = 123.0000901
	var num4 float64 = 123.0000901
	fmt.Println(num3, num4)

	var num5 = 1.1
	fmt.Printf("num5的数据类型是%T\n",num5)

	//十进制数形式
	var num6 = 5.12
	var num7 = .123
	fmt.Println(num6, num7)

	//科学计数法
	num8 := 5.1234e2
	num9 := 5.1234E2
	//上：表示在.后面保留两位
	num10 := 5.1234E-2
	//上：表示在.前面加上2位
	fmt.Println(num8, num9, num10)
}	
```

![image-20231014180101357](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014180101357.png?raw=true)

## 3.10字符类型

### 3.10.1基本介绍

- Golang 中没有专门的字符类型，如果要存储单个字符(字母)，一般使用 byte 来保存
- 字符串就是一串固定长度的字符连接起来的字符序列。Go 的字符串是由单个字节连接起来的。也 就是说对于传统的字符串是由字符组成的，而 Go 的字符串不同，它是由字节组成的。

### 3.10.2 案例演示

```go
package main
import "fmt"
func main() {
	var c1 byte = 'a'
	var c2 byte = '0'

	//当我们直接输出byte值，就是输出了的对应的字符的码值
	// "a" ==》
	fmt.Println("c1",c1)
	fmt.Println("c2",c2)
	//如果我们希望输出对应字符，需要使用格式化输出
	fmt.Printf("c1=%c,c2=%c\n",c1,c2)

	//var c3 byte = "北" //overflow溢出
	var c3 int = '北' //overflow溢出
	fmt.Printf("c3=%c c3对应码值=%d",c3,c3)
}
```

![image-20231014183117397](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014183117397.png?raw=true)

对上面代码说明：

1. 如果我们保存的字符在 ASCII 表的,比如[0-1, a-z,A-Z..]直接可以保存到 byte
2. 如果我们保存的字符对应码值大于 255,这时我们可以考虑使用 int类型保存
3. 如果我们需要安装字符的方式输出，这时我们需要格式化输出，即 fmt.Printf(“%c”,

### 3.10.3 字符类型使用细节

1. ) 字符常量是用单引号('')括起来的单个字符。例如：var c1 byte = 'a' var c2 int = '中' var c3 byte = '9'

2. Go 中允许使用转义字符 '\’来将其后的字符转变为特殊字符型常量。例如：var c3 char = ‘\n’ // '\n'表示换行符

3. Go 语 言 的 字 符 使 用 UTF-8 编 码 ， 如 果 想 查 询 字 符 对 应 的 utf8 码 值 http://www.mytju.com/classcode/tools/encode_utf8.asp

   英文字母-1 个字节 汉字-3 个字节

4. 在 Go 中，字符的本质是一个整数，直接输出时，是该字符对应的 UTF-8 编码的码值

5. 可以直接给某个变量赋一个数字，然后按格式化输出时%c，会输出该数字对应的 unicode 字

![image-20231014193752155](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014193752155.png?raw=true)

6. 字符类型是可以进行运算的，相当于一个整数，因为它对应有Unicod码。

![image-20231014193940072](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014193940072.png?raw=true)

```go
package main
import "fmt"
func main() {
	var c1 byte = 'a'
	var c2 byte = '0'

	//当我们直接输出byte值，就是输出了的对应的字符的码值
	// "a" ==》
	fmt.Println("c1",c1)
	fmt.Println("c2",c2)
	//如果我们希望输出对应字符，需要使用格式化输出
	fmt.Printf("c1=%c,c2=%c\n",c1,c2)

	//var c3 byte = "北" //overflow溢出
	var c3 int = '北' //overflow溢出
	fmt.Printf("c3=%c c3对应码值=%d\n",c3,c3)

	var c4 int = 22269
	fmt.Printf("c4=%c c4对应码值=%d\n",c4,c4)

	var n1 = 10 + 'a'
	fmt.Println("n1=",n1)
}
```

### 3.10.4字符类型本质探讨

1. 字符型 存储到 计算机中，需要将字符对应的码值（整数）找出来

- 存储：字符--->对应码值---->二进制-->存储
- 读取：二进制----> 码值 ----> 字符 --> 读取

2. 字符和码值的对应关系是通过字符编码表决定的(是规定好)
3. Go 语言的编码都统一成了 utf-8。非常的方便，很统一，再也没有编码乱码的困扰了

## 3.11布尔类型

### 3.11.1 基本介绍

1. 布尔类型也叫 bool 类型，bool 类型数据只允许取值 true 和 fals
2. bool 类型占 1 个字节
3. bool 类型适于逻辑运算，一般用于程序流程控制[注：这个后面会详细介绍]：

- if 条件控制语句
- for 循环控制语句

### 3.11.2案例演示

```go
package main
import (
"fmt"
"unsafe"
)

func main() {
var b = false
fmt.Println(b)
//注意事项
//bool类型占用存储空间是1字节
fmt.Println(b,unsafe.Sizeof(b))
}
```

![image-20231014194354482](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194354482.png?raw=true)

## 3.12 string类型

### 3.12.1基本介绍

- 字符串就是一串固定长度的字符连接起来的字符序列。Go 的字符串是由单个字节连接起来的。Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文

### 3.12.2案例演示

![image-20231014194534185](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194534185.png?raw=true)

### 3.12.3string使用注意事项和细节

1. Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本，这样 Golang 统一使用 UTF-8 编码,中文 乱码问题不会再困扰程序员。
2. 字符串一旦赋值了，字符串就不能修改了：在 Go 中字符串是不可变的。

![image-20231014194640110](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194640110.png?raw=true)

3. 字符串的两种表示形式
   - 双引号, 会识别转义字符
   - 反引号，以字符串的原生形式输出，包括换行和特殊字符，可以实现防止攻击、输出源代码等效果

### 案例演示

![image-20231014194812765](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194812765.png?raw=true)

4. 字符串拼接方式

![image-20231014194830233](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194830233.png?raw=true)

5. 当一行字符串太长时，需要使用到多行字符串，可以如下处理

![image-20231014194847918](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014194847918.png?raw=true)

## 3.13基本数据类型的默认值

### 3.13.1 基本介绍

- 在 go 中，数据类型都有一个默认值，当程序员没有赋值时，就会保留默认值，在 go 中，默认值 又叫零值。

### 3.13.2 基本数据类型的默认值如下

![image-20231014201655131](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014201655131.png?raw=true)

案例：

![image-20231014201849891](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014201849891.png?raw=true)

## 3.14 基本数据类型的相互转换

### 3.14.1基本介绍

Golang 和 java / c 不同，Go 在不同类型的变量之间赋值时需要显式转换。也就是说 Golang 中数 据类型不能自动转换。

### 3.14.2基本语法

表达式 T(v) 将值 v 转换为类型 T

T: 就是数据类型，比如 int32，int64，float32 等

v: 就是需要转换的变量

案例演示：

```go
package main
import "fmt"
func main() {
var i int32 = 100
var n1 float32 = float32(i)
var n2 int8 = int8(i)
var n3 int64 = int64(i)
fmt.Println(n1, n2, n3)
}
```

![image-20231014202203675](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014202203675.png?raw=true)

### 3.14.4基本数据类型相互转换的注意事项：

1. Go 中，数据类型的转换可以是从 表示范围小-->表示范围大，也可以 范围大--->范围
2. 被转换的是变量存储的数据(即值)，变量本身的数据类型并没有变化！

![image-20231014202401442](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014202401442.png?raw=true)

3. 在转换中，比如将 int64 转成 int8 【-128---127】 ，编译时不会报错，只是转换的结果是按 溢出处理，和我们希望的结果不一样。 因此在转换时，需要考虑范

![image-20231014202653684](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014202653684.png?raw=true)

### 3.14.5课堂练习

练习1

![image-20231014202912189](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014202912189.png?raw=true)

如何修改上面的代码，就可以正确.

![image-20231014203201145](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014203201145.png?raw=true)

练习2

![image-20231014205838477](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014205838477.png?raw=true)

## 3.15基本数据类型string的转换

### 3.15.1基本介绍

- 在程序开发中，我们经常将基本数据类型转成 string,或者将 string 转成基本数据

### 3.15.2基本类型转string类型

方式 1：fmt.Sprintf("%参数", 表达式) 【个人习惯这个，灵活】

函数的介绍：

![image-20231014210006366](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014210006366.png?raw=true)

参数需要和表达式的数据类型相匹配

fmt.Sprintf().. 会返回转换后的字符串

案例演示：

```go
package main
import "fmt"
func main() {
	var num1 int = 99
	var num2 float32 = 23.456
	var b bool = true
	var mychar byte = 'h'
	var str string //空的str
	//使用第一种方式来转换，fmt.Sprintf方法
	str = fmt.Sprintf("%d",num1)
	fmt.Printf("str type %T str=%q\n",str,str)
	
	str = fmt.Sprintf("%f",num2)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = fmt.Sprintf("%t",b)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = fmt.Sprintf("%c",mychar)
	fmt.Printf("str type %T str=%q\n",str,str)
}
```

![image-20231014210747222](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014210747222.png?raw=true)

方式2：使用strcov包的函数

![image-20231014210812935](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014210812935.png?raw=true)

案例说明：

```go
package main
import (
	"fmt"
	"strconv"
)
func main() {
	var num1 int = 99
	var num2 float32 = 23.456
	var b bool = true
	var mychar byte = 'h'
	var str string //空的str
	//使用第一种方式来转换，fmt.Sprintf方法
	str = fmt.Sprintf("%d",num1)
	fmt.Printf("str type %T str=%q\n",str,str)
	
	str = fmt.Sprintf("%f",num2)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = fmt.Sprintf("%t",b)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = fmt.Sprintf("%c",mychar)
	fmt.Printf("str type %T str=%q\n",str,str)

	var num3 int = 99
	var num4 float64 = 23.456
	var b2 bool = true
	
	str = strconv.FormatInt(int64(num3),10)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = strconv.FormatFloat(num4,'f',10,64)
	fmt.Printf("str type %T str=%q\n",str,str)

	str = strconv.FormatBool(b2)
	fmt.Printf("str type %T str=%q\n",str,str)
}
```

![image-20231014211601204](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014211601204.png?raw=true)

### 3.15.3string类型转基本数据类型

- 使用string类型转基本数据类型

![image-20231014220239006](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014220239006.png?raw=true)

```go
package main
import (
	"fmt"
	"strconv"
)
func main() {
	var str string = "true"
	var b bool
	//说明：
	//1.strconv.ParseBool(str)函数会返回两个值（value bool，err error）
	//2.因为我只想获取value bool，不想获取err所以使用_进行忽略
	b , _ = strconv.ParseBool(str)
	fmt.Printf("b type %T b=%v\n",b,b)

	var str2 string = "12341234"
	var n1 int64
	var n2 int
	n1,_ = strconv.ParseInt(str2,10,64)
	n2 = int(n1)
	fmt.Printf("n1 type %T n1=%v\n",n1,n1)
	fmt.Printf("n2 type %T n1=%v\n",n2,n2)
}
```

![image-20231014221301545](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014221301545.png?raw=true)

### 3.15.4string转基本数据类型的注意事项

- 在将 String 类型转成 基本数据类型时，要确保 String 类型能够转成有效的数据，比如 我们可以 把 "123" , 转成一个整数，但是不能把 "hello" 转成一个整数，如果这样做，Golang 直接将其转成 0 ， 其它类型也是一样的道理. float => 0 bool

![image-20231014221549176](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014221549176.png?raw=true)

## 3.16指针

### 3.16.1基本介绍

1. 基本数据类型，变量存的就是值，也叫值类型

2. 获取变量的地址，用& ：比如：var num int，获取num地址：&num

   1. 分析一下基本数据类型在内存的布局

   

![image-20231014221739938](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014221739938.png?raw=true)

3. 指针类型：指针变量存的是一个地址，这个地址指向的空间的才是值

   比如：var prt *int = &num

   ![image-20231014221851895](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014221851895.png?raw=true)

4. 获取指针类型所指向的值，使用：*，比如：var ptr *int 使用\*ptr获取ptr指向的值

   ```go
   package main
   import (
   	"fmt"
   )
   func main () {
   	var i int = 10
   	fmt.Printf("i的地址   =%v\n", &i)
   
   	//下面的var ptr *int = &i
   	//1.ptr 是一个指针变量
   	//2.ptr 的类型 *int
   	//3.ptr 本身的值&i
   	var ptr *int = &i
   	fmt.Printf("ptr       =%v\n",ptr)
   	fmt.Printf("ptr 的地址=%v\n",&ptr)
   	fmt.Printf("ptr 指向的值=%v\n",*ptr)
   }
   ```

   ![image-20231014222800961](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014222800961.png?raw=true)

5. 一个案例再说明

![image-20231014222840539](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014222840539.png?raw=true)

### 3.16.2案例演示

- 写一个程序，获取一个int变量num的地址，并显示到终端
- 将num的地址赋值给指针ptr，并通过ptr去修改num值

```go
package main
import (
	"fmt"
)
func main () {
	var num int =9
	fmt.Printf("num的地址%v\n",&num)

	var ptr *int = &num
	*ptr = 19
	fmt.Printf("ptr指针的地址:%p\nptr指针的值是:%d \nptr本身的地址%p\n", ptr,*ptr,&ptr)
	fmt.Println(num)
}

```

![image-20231014230208690](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014230208690.png?raw=true)

### 3.16.3指针的课堂练习

![image-20231014230305253](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014230305253.png?raw=true)

### 3.16.4指针的使用细节

- 值类型，都有对应的指针类型， 形式为 *数据类型，比如 int 的对应的指针就是 *int, float32 对应的指针类型就是 *float32, 依次类推
- 值类型包括：基本数据类型 int 系列, float 系列, bool, string 、数组和结构体 struct

## 3.17值类型和引用类型

### 3.17.1值类型和引用类型的说明

- 值类型：基本数据类型 int 系列, float 系列, bool, string 、数组和结构体 struct
- 引用类型：指针、slice 切片、map、管道 chan、interface 等都是引用类型

### 3.17.2 值类型和应用类型的使用特点

1. 值类型：变量直接存储值，内存通常在栈中分配

![image-20231014230526457](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014230526457.png?raw=true)

2. 引用类型：变量存储的是一个地址，这个地址对应的空间才真正存储数据(值)，内存通常在堆 上分配，当没有任何变量引用这个地址时，该地址对应的数据空间就成为一个垃圾，由 GC 来回
3. 内存的栈区和堆区示意图

​	![image-20231014230657236](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014230657236.png?raw=true)

## 3.18标识符的命名规范

1. Golang 对各种变量、方法、函数等命名时使用的字符序列称为标识符
2. 凡是自己可以起名字的地方都叫标识符

### 3.18.2 标识符概念

1. 由26个英文字母大写，0-9，_组成
2. 数字不可用开头。var num int //ok var 3num int //error
3. Golang中严格区分大小写
   - var num int
   - var Num int

- 说明：在Golang中，num和Num是两个不同的变量

4. 标识符不能包括空格

    ![image-20231014231104029](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014231104029.png?raw=true)

5. 下划线"_"本身在Go中是一个特殊的表示符，称为空标识符。可以代表任何其他标识符，但是它对应的值会被忽略(比如:忽略某个返回值)。所以仅能被作为占位符，不能作为标识符使用

​		![image-20231014231238254](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014231238254.png?raw=true)

6. 不能以系统保留关键字作为标识符（一共有 25 个），比如 break，if 等等...

### 3.18.3标识符的案例

hello // ok
hello12 //ok
1hello // error ,不能以数字开头
h-b // error ,不能使用 - x h // error, 不能含有空格

h_4 // ok
_ab // ok
int // ok , 我们要求大家不要这样使用
float32 // ok , 我们要求大家不要这样使用
_ // error
Abc // ok

### 3.18.4表示符命名注意事项

1. 包名：保持 package 的名字和目录保持一致，尽量采取有意义的包名，简短，有意义，不要和 标准库不要冲突 fmt

![image-20231014231402629](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014231402629.png?raw=true)

2. 变量名、函数名、常量名：采用驼峰法 举例： var stuName string = “tom” 形式: xxxYyyyyZzzz ..

 		**var goodPrice float32 = 1234.5**	

3. 如果变量名、函数名、常量名首字母大写，则可以被其他的包访问；如果首字母小写，则只能 在本包中使用 ( 注：可以简单的理解成，首字母大写是公开的，首字母小写是私有的) ,在 golang 没有 public , private

## 3.19 系统保留关键字

![image-20231014231546089](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014231546089.png?raw=true)

## 3.20系统的预定义标识符

![image-20231014231603744](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014231603744.png?raw=true)

# 第四章 运算符

## 运算符的基本介绍

运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等

1) 算术运算符
2) 赋值运算符
3) 比较运算符/关系运算符
4) 逻辑运算符
5) 位运算符
6) 其它运算符

## 4.2算数运算符

算术运算符是对数值类型的变量进行运算的，比如：加减乘除。在 Go 程序中使用的非常多 

### 4.2.1算术运算符的一览表

![image-20231014232601330](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014232601330.png?raw=true)

### 4.2.2案例演示

案例演示算术运算符的使用。
+, - , * , / , %, ++, -- , 重点讲解 /、%
自增：++
自减：--

演示/的使用特点

```go
package main
import (
	"fmt"
)
func main () {
//说明，如果运算的数是整数，那么除后，去掉小数部分，保留整数部分
fmt.Println(10 / 4)

var n1 float32 = 10 / 4
fmt.Println(n1)

//如果我们希望保留小数部分，则需要有浮点数参与运算
var n2 float32 = 10.0 / 4.0
fmt.Println(n2)
}

```

![image-20231014232920089](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014232920089.png?raw=true)

演示%的使用特点

//演示 %的使用

//看一个公式 a%b=a-a/b*a

fmt.Println("10%3=", 10 % 3) // =1
fmt.Println("-10%3=", -10 % 3) // = -10 - (-10) / 3 * 3 = -10 - (-9) = -1
fmt.Println("10%-3=", 10 % -3) // =1
fmt.Println("-10%-3=", -10 % -3) //

++和--的使用

![image-20231014233613217](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014233613217.png?raw=true)

### 4.2.3算术运算符使用注意事项

1. 对于除号 "/"，它的整数除和小数除是有区别的：整数之间做除法时，只保留整数部分而舍弃 小数部分。 例如： x := 19/5 ,结果是
2. 当对一个数取模时，可以等价 a%b=a-a/b*b ， 这样我们可以看到 取模的一个本质运算。

3. Golang 的自增自减只能当做一个独立语言使用时，不能这样使用

![image-20231014233915764](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014233915764.png?raw=true)

4. 

Golang 的++ 和 -- 只能写在变量的后面，不能写在变量的前面，即：只有 a++ a-- 没有 ++a --a

![image-20231014233943354](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014233943354.png?raw=true)

5. Golang 的设计者去掉 c / java 中的 自增自减的容易混淆的写法，让 Golang 更加简洁，统一。(强 制性的) 

### 4.2.4课堂练习 

![image-20231014234123886](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014234123886.png?raw=true)

### 4.2.5课堂练习2

1. 假如还有97天放假，问xx个星期xx天

   ```go
   package main
   import (
   	"fmt"
   )
   func main () {
    var n1 int = 97
    n2 := n1 / 7
    n3 := n1 % 7
    fmt.Println(n2, n3)
   }
   ```

   ![image-20231014234825368](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014234825368.png?raw=true)

2. 定义一个变量保存华氏温度，华氏温度转换摄氏温度的公式为：5/9*(华氏温度-100),请求出华氏 温度对应的摄氏温度。

   ```go
   package main
   import (
   	"fmt"
   )
   func main () {
    var n1 int = 97
    n2 := n1 / 7
    n3 := n1 % 7
    fmt.Println(n2, n3)
   
    var huashi float32 = 132.2
    var sheshi float32 = 5.0 / 9 * (huashi - 100)
    fmt.Println(sheshi)
   }
   ```

   

![image-20231014234929255](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014234929255.png?raw=true)

## 4.3关系运算符(比较运算符)

### 4.3.1基本介绍

1. 关系运算符的结果都是 bool 型，也就是要么是 true，要么是 false
2. 关系表达式 经常用在 if 结构的条件中或循环结构的条件中

### 4.3.2关系运算符一览图

![image-20231014235206097](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014235206097.png?raw=true)

### 4.3.3案例演示

```go
package main
import (
	"fmt"
)
func main () {
//演示关系运算符的使用
var n1 int = 9
var n2 int = 8
fmt.Println(n1 == n2) 
fmt.Println(n1 != n2)
fmt.Println(n1 > n2)
fmt.Println(n1 < n2)
fmt.Println(n1 >= n2)
fmt.Println(n1 <= n2)
flag := n1 > n2
fmt.Println(flag)
}
```

![image-20231014235706841](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231014235706841.png?raw=true)

### 4.3.4关系运算符的细节说明

细节说明

1. 关系运算符的结果都是 bool 型，也就是要么是 true，要么是 false。
2. 关系运算符组成的表达式，我们称为关系表达式： a > b
3. 比较运算符"=="不能误写成 "=" !

## 4.4逻辑运算符

### 4.4.1基本介绍

用于连接多个条件（一般来讲就是关系表达式），最终的结果也是一个 bool 

### 4.4.2逻辑运算的说明

![image-20231015000134074](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015000134074.png?raw=true)

### 4.4.3案例演示

![image-20231015000149817](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015000149817.png?raw=true)

![image-20231015000215611](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015000215611.png?raw=true)

### 4.4.4注意事项和细节说明

1. &&也叫短路与：如果第一个条件为 false，则第二个条件不会判断，最终结果为 false
2. ||也叫短路或：如果第一个条件为 true，则第二个条件不会判断，最终结果为 true
3. 案例演示：

```go
package main
import (
	"fmt"
)
func test() bool{
	fmt.Println("test...")
	return true
}
func main () {
	var i int = 10
	if i < 9 && test() {
		fmt.Println("ok")
	}
	if i > 9 || test() {
		fmt.Println("hello")
	}
}
```

![image-20231015000608606](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015000608606.png?raw=true)

## 赋值运算符

### 4.5.1基本的介绍

赋值运算符就是将某个运算后的值，赋给指定的变量

### 4.5.2赋值运算符的分类

![image-20231015001050318](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015001050318.png?raw=true)

### 4.5.3赋值运算的案例演示：

案例演示赋值运算符的基本使用。

1. 赋值基本案例
2. 有两个变量，a 和 b，要求将其进行交换，最终打印结果
3. += 的使用案
4. 案例

```go
package main
import (
	"fmt"
)
func main() {
//赋值运算符的使用演示
//var i int
//i = 10//基本赋值
//有两个变量，a和b，要将其进行交换，最终打印出来
a := 9
b := 2
fmt.Printf("交换前a=%v,b=%v",a,b)
t := a
a = b
b = t
fmt.Printf("交换后a=%v,b=%v",a,b)
}
```

![image-20231015001538233](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015001538233.png?raw=true)

### 4.5.4赋值运算符的特点

1. 运算顺序从右向左

   ![image-20231015002232214](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015002232214.png?raw=true)

2. 赋值运算符的左边 只能是变量,右边 可以是变量、表达式、

   ![image-20231015002225030](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015002225030.png?raw=true)

   ```go
   package main
   
   import (
       "fmt"
   )
   
   func main() {
       // 交换a和b的值
       a := 9
       b := 2
       fmt.Printf("交换前 a=%v, b=%v\n", a, b)
       a, b = b, a // 使用元组赋值方式交换a和b的值
       fmt.Printf("交换后 a=%v, b=%v\n", a, b)
   
       var c int
       c = a + 3
   	fmt.Println(c)
       // 赋值运算符的左边只能是变量，右边可以是变量、表达式、常量
   
       var d int
       d = a
       d = 8 + 2*8
       d = test() + 90
       d = 890
       fmt.Printf("d=%v\n", d)
   }
   
   func test() int {
       return 10
   }
   
   ```

3. 复合赋值运算符等价于下面的效果

   - 比如：a += 3 等价于 a = a

## 面试题：

有两个变量，a 和 b，要求将其进行交换，但是不允许使用中间变量，最终打印结果

```go
package main

import (
    "fmt"
)

func main() {
    var a = 10
    var b = 20

    a = a + b//30
    b = a - b //10 b=10=a
    a = a - b //20 a=30-20=a=b
    fmt.Println(a, b)
}
```

![image-20231015002729138](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015002729138.png?raw=true)

## 4.6位运算符

![image-20231015002926650](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015002926650.png?raw=true)

## 4.7其他运算符索命

![image-20231015003106640](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003106640.png?raw=true)

```go
package main

import (
    "fmt"
)

func main() {
    a := 100
    fmt.Println("a的地址=",&a)

    var ptr *int = &a
    fmt.Println("ptr指向的值",*ptr)
    fmt.Printf("ptr的地址=%v",ptr)
}
```

![image-20231015003608569](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003608569.png?raw=true)

### 4.7.1课堂案例

![image-20231015003650682](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003650682.png?raw=true)

案例 2：求三个数的最大值

![image-20231015003701402](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003701402.png?raw=true)

## 4.8 特别说明

![image-20231015003726111](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003726111.png?raw=true)

![image-20231015003809488](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003809488.png?raw=true)

## 4.9运算符的优先级

### 4.9.1运算符的优先级的一览表

 ![image-20231015003849247](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015003849247.png?raw=true)

### 4.9.2对上图的说明

1. 运算符有不同的优先级，所谓优先级就是表达式运算中的运算顺序。如右表，上一行运算符总优先于下一行。
2. 只有单目运算符、赋值运算符是从右向左运算的。
3. 梳理了一个大概的优先级

1：括号，++, -- 2: 单目运算
3：算术运算符
4：移位运算
5：关系运算符
6：位运算符
7：逻辑运算符
8：赋值运算符
9：逗号

## 4.10键盘输入语句

### 4.10.1介绍

在编程中，需要接收用户输入的数据，就可以使用键盘输入语句来获取。InputDemo.go

### 4.10.2步骤：

1. 导入fmt包
2. 调用fmt包的fmt.Scanln()或则fmt.Scanf()

![image-20231015004121563](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015004121563.png?raw=true)

​					![image-20231015004142185](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015004142185.png?raw=true)

### 4.10.3案例演示：

要求：可以从控制台接收用户信息，【姓名，年龄，薪水, 是否通过考试 】。

```go
package main

import (
    "fmt"
)

func main() {
 //要求，可以从控制台接收用户信息,【姓名，年龄，薪水，是否通过考试】。
 //方式1 fmt.Scanln
 var name string
 var age byte
 var sal float32
 var isPass bool
 fmt.Println("请输入姓名：")
 fmt.Scanln(&name)
 fmt.Println("请输入年龄：")
 fmt.Scanln(&age)
 fmt.Println("请输入薪水")
 fmt.Scanln(&sal)
 fmt.Println("请输入是否通过考试：")
 fmt.Scanln(&isPass)
 fmt.Printf(" 姓名是：%v \n 年龄是 %v \n 薪水是 %v]n 是否通过考试%v \n",name,age,sal,isPass)
}

```

![image-20231015005846067](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015005846067.png?raw=true)

2. 使用fmt.Scanf()获取

```go
package main

import (
    "fmt"
)

func main() {
 //要求，可以从控制台接收用户信息,【姓名，年龄，薪水，是否通过考试】。
 //方式1 fmt.Scanln
 var name string
 var age byte
 var sal float32
 var isPass bool
//  fmt.Println("请输入姓名：")
//  fmt.Scanln(&name)
//  fmt.Println("请输入年龄：")
//  fmt.Scanln(&age)
//  fmt.Println("请输入薪水")
//  fmt.Scanln(&sal)
//  fmt.Println("请输入是否通过考试：")
//  fmt.Scanln(&isPass)
//  fmt.Printf(" 姓名是：%v \n 年龄是 %v \n 薪水是 %v]n 是否通过考试%v \n",name,age,sal,isPass)

//方式2：fmt.Scanf,可以按执行的格式输入
fmt.Println("请输入你的姓名,年龄,薪水,是否通过考试,使用空格隔开")
fmt.Scanf("%s %d %f %t",&name,&age,&sal,&isPass)
fmt.Printf(" 名字是%v \n 年龄是%v \n 薪水是%v \n 是否通过考试%v \n",name,age,sal,isPass)
}
```

![image-20231015010822105](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015010822105.png?raw=true)

## 4.11进制

对于整数，有四种表达方式：

1. 二进制：0,1 ，满 2 进 1。
   - 在 golang 中，不能直接使用二进制来表示一个整数，它沿用了 c 的特点。
2. 十进制：0-9 ，满 10 进 1。
3. 八进制：0-7 ，满 8 进 1. 以数字 0 开头表示。
4. 十六进制：0-9 及 A-F，满 16 进 1. 以 0x 或 0X 开头表示。
   - 此处的 A-F 不区分大小写

```go
package main

import (
    "fmt"
)

func main() {
 var i int = 5
 //二进制输出
 fmt.Printf("%b \n",i)
 //八进制：0-7，满8进1，以数字0开头表示
 var j int = 011
 fmt.Println("j=",j)

 //0-9及A-F，满16进1，以0x或0X开头表示
 var k int = 0X11 //0X11=> 16 + 1 =17
 fmt.Println("k=",k)
}
```

![image-20231015015659424](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015015659424.png?raw=true)

### 4.11.1进制的图示

![image-20231015011329988](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015011329988.png?raw=true)

### 4.11.2进制转换的介绍

![image-20231015011350737](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015011350737.png?raw=true)

### 4.11.3其他进制转十进制

![image-20231015011447717](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015011447717.png?raw=true)

### 4.11.4二进制如何转十进制

![image-20231015015810217](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015015810217.png?raw=true)

### 4.11.5 八进制转换成十进制

![image-20231015015852874](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015015852874.png?raw=true)

### 4.11.6 16进制转成十进制

![image-20231015020007116](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020007116.png?raw=true)

### 4.11.7其他进制转10进制

课堂练习：请将

二进制： 110001100 转成 十进制
八进制： 02456 转成十进制
十六进制： 0xA45 转成十进制

```
二进制转十进制：将二进制数 110001100 转换为十进制。

二进制数 110001100 可以拆解成：12^8 + 12^7 + 02^6 + 02^5 + 02^4 + 12^3 + 12^2 + 02^1 + 0*2^0。

计算结果为：256 + 128 + 24 = 408。

所以，二进制数 110001100 转换为十进制是 408。

八进制转十进制：将八进制数 02456 转换为十进制。

八进制数 02456 可以拆解成：28^4 + 48^3 + 58^2 + 68^1。

计算结果为：4096 + 1024 + 320 + 48 = 5488。

所以，八进制数 02456 转换为十进制是 5488。

十六进制转十进制：将十六进制数 0xA45 转换为十进制。

十六进制数 0xA45 可以拆解成：1016^2 + 416^1 + 5*16^0。

计算结果为：2560 + 64 + 5 = 2629。

所以，十六进制数 0xA45 转换为十进制是 2629
```

### 4.11.8十进制如何转成其他进制

![image-20231015020501619](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020501619.png?raw=true)

### 4.11.9 十进制如何转二进制

![image-20231015020517741](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020517741.png?raw=true)

### 4.11.10十进制转成八进制

![image-20231015020552708](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020552708.png?raw=true)

### 4.11.11十进制转十六进制

![image-20231015020615001](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020615001.png?raw=true)

## 4.11.2课堂练习

课堂练习：请将
123 转成 二进制
678 转成八进制
8912 转成十六进制

```go
十进制数 123 转换为二进制是 1111011。
十进制数 678 转换为八进制是 1246。
十进制数 8912 转换为十六进制是 0x2310
```

### 4.11.13二进制转换成八进制、十六进制

![image-20231015020820637](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020820637.png?raw=true)

### 4.11.14二进制转换成八进制

![image-20231015020840501](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015020840501.png?raw=true)

### 4.11.15二进制转十六进制

![image-20231015021127835](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015021127835.png?raw=true)

### 4.11.16 八进制、十六进制转成二进制

![image-20231015021302679](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015021302679.png?raw=true)

### 4.11.17 八进制转成二进制

![image-20231015021851175](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015021851175.png?raw=true)

### 4.11.18 十六进制转成二进制

![image-20231015021909899](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015021909899.png?raw=true)

## 4.12位运算

### 4.12.1位运算的思考题

1. 请看下面的代码段，回答 a,b,c,d 结果是多少

   ```go
   package main
   
   import (
       "fmt"
   )
   
   func main() {
   var a int = 1 >> 2
   var b int = -1 >> 2
   var c int = 1 << 2
   var d int = -1 << 2
   fmt.Println(a, b, c, d)
   
   }   
   
   ```

   ![image-20231015022523918](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015022523918.png?raw=true)

```
a: 1 >> 2，这表示将整数 1 向右移动 2 位。右移操作将数值的二进制位向右移动，丢弃最低位，左边用 0 填充。所以 1 右移 2 位后变为 0，所以 a 的值是 0。

b: -1 >> 2，这表示将整数 -1 向右移动 2 位。对于负数，右移操作会保留最高位的符号位，因此 -1 的二进制表示中的所有位都为 1，右移 2 位后，仍然是 11（因为符号位不变），所以 b 的值是 -1。

c: 1 << 2，这表示将整数 1 向左移动 2 位。左移操作将数值的二进制位向左移动，右边用 0 填充。所以 1 左移 2 位后变为 100，所以 c 的值是 4。

d: -1 << 2，这表示将整数 -1 向左移动 2 位。左移操作会将最高位的符号位保留，因此 -1 的二进制表示中的所有位都是 1，左移 2 位后仍然是 11111100，这是一个负数的补码表示，所以 d 的值是 -4。
```

2. 请回答Golang中，下面的表达式运算结果是：

![image-20231015023234340](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015023234340.png?raw=true)

![image-20231015023244896](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015023244896.png?raw=true)

```go
package main

import (
    "fmt"
)

func main() {

fmt.Println(2&3)
fmt.Println(2|3)
fmt.Println(13&7)
fmt.Println(5|4)
fmt.Println(-3^3)
}   
```

![image-20231015023254281](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015023254281.png?raw=true)

### 4.12.2 二进制在运算中的说明

二进制是逢 2 进位的进位制，0、1 是基本算符

现代的电子计算机技术全部采用的是二进制，因为它只使用 0、1 两个数字符号，非常简单方便易于用电子方式实现。计算机内部处理的信息，都是采用二进制数来表示的。二进制（Binary）数用 0 和 1 两个数字及其组合来表示任何数。进位规则是“逢 2 进 1”，数字 1 在不同的位上代表不同的值， 按从右至左的次序，这个值以二倍递增。

在计算机的内部，运行各种运算时，都是以二进制的方式来运行

### 4.12.3原码、反码、补码

![image-20231015023404095](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015023404095.png?raw=true)

### 4.12.4位运算符和移位运算符

Golang 中有 3 个位运算

- 分别是”按位与&、按位或|、按位异或^,它们的运算规则是：
- 按位与& ： 两位全为１，结果为 1，否则为 0
- 按位或| : 两位有一个为 1，结果为 1，否则为 0
- 按位异或 ^ : 两位一个为 0,一个为 1，结果为 1，否则为 

案例练习

比如：2&3=2 2|3=3 2^3=1

![image-20231015023835238](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015023835238.png?raw=true)



- ​	Golang 中有 2 个移位运算符

  - \>>、<< 右移和左移,运算规则

  - 右移运算符 >>：低位溢出,符号位不变,并用符号位补溢出的高位

  - 左移运算符 <<: 符号位不变,低位

案例演示

a :=1 >> 2 // 0000 0001 =>0000 0000

c := 1 << 2 // 0000 0001 ==> 0000

```mariadb
a := 1 >> 2：这是右移操作，将整数 1 向右移动 2 位。二进制表示中的 1 会向右移动两次，因为右移 2 位。每次右移，最低位都会被丢弃，而左边会用 0 填充。所以，00000001 右移 2 位后变成了 00000000，这是二进制 0，所以 a 的值是 0。

c := 1 << 2：这是左移操作，将整数 1 向左移动 2 位。二进制表示中的 1 会向左移动两次，因为左移 2 位。每次左移，右边会用 0 填充。所以，00000001 左移 2 位后变成了 00000100，这是二进制 4，所以 c 的值是 4
```

# 第五章

## 5.1 程序流程控制介绍

- 在程序中，程序运行的流程控制决定程序是如何执行的，是我们必须掌握的，主要有三大流程控 制语句。

1) 顺序控制
2) 分支控制
3) 循环控制

## 5.2 顺序控制

- 程序从上到下逐行地执行，中间没有任何判断和跳转。
- 一个案例说明，必须下面的代码中，没有判断，也没有跳转.因此程序按照默认的流程执行，即顺 序控制。

![image-20231015093607113](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015093607113.png?raw=true)

### 5.2.1顺序控制的一个流程图

![image-20231015093633189](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015093633189.png?raw=true)

### 5.2.2顺序控制举例和注意事项

Golang 中定义变量时采用合法的前向引用。如：

![image-20231015094225101](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094225101.png?raw=true)

## 5.3 分支控制

### 分支控制的基本介绍

分支控制就是让程序有选择执行。有下面三种形式

1. 单分支
2. 双分支

3. 多分支

### 5.3.2单分支控制

基本语法

![image-20231015094353243](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094353243.png?raw=true)

单分支的流程图

流程图可以用图形方式来更加清晰的描述程序执行的流程。

![image-20231015094445953](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094445953.png?raw=true)

单分支的细节说明

![image-20231015094750263](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094750263.png?raw=true)

![image-20231015094758001](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094758001.png?raw=true)

![image-20231015094804406](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094804406.png?raw=true)

### 5.3.3双分支控制

基本语法

![image-20231015094827381](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015094827381.png?raw=true)

应用案例

编写一个程序,可以输入人的年龄,如果该同志的年龄大于 18 岁,则输出 “你年龄大于 18,要对 自己的行为负责!”。否则 ,输出”你的年龄不大这次放过你了.”

```go
package main
import (
	"fmt"
)
func main() {
	var age int 
	fmt.Println("请输入你的年龄")
	fmt.Scanln(&age)
	if age > 18 {
		fmt.Println("年龄大于18岁")
	}else{
		fmt.Println("你的年龄未成年放过你了")
	}
}
```

![image-20231015095849742](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015095849742.png?raw=true)

双分支的流程图的分析

![image-20231015100100869](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015100100869.png?raw=true)

对双分支的总结

从上图看 条件表达式就是 age >1

执行代码块 1 ===> fmt.Println("你的年龄大于 18")

执行代码块 2 ===> fmt.Println("你的年龄

. 强调一下 双分支只会执行其中的一个分支。

### 5.3.4单分支和双分支

![image-20231015100154837](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015100154837.png?raw=true)

![image-20231015100244101](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015100244101.png?raw=true)

![](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015100224867.png?raw=true)

![image-20231015100252293](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015100252293.png?raw=true)

5. 编写程序，声明 2 个 int32 型变量并赋值。判断两数之和，如果大于等于 50，打印“hello world!

```go
package main
import (
	"fmt"
)
func main() {
	var n1 int32 = 10
	var n2 int32 = 50
	if n1 + n2 >= 50{
		fmt.Println("hello world")
	}
}
```

6. 编写程序，声明 2 个 float64 型变量并赋值。判断第一个数大于 10.0，且第 2 个数小于 20.0，打 印两数之和。

```go
package main
import (
	"fmt"
)
func main() {
	var n3 float32 = 11.0
	var n4 float32 = 17.0
	if n3 > 10.0 && n4 <20.0{
		fmt.Println("和=",(n3+n4))
	}
}
```

![image-20231015105533220](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015105533220.png?raw=true)

7. 【选作】定义两个变量int32，判断二者的和，是否能被3又被5整除，打印提升信息

```go
package main
import (
	"fmt"
)
func main() {
    var num1 int32 = 10
	var num2 int32 = 5
	if (num1 + num2) %3 == 0 && (num1 + num2) % 5 == 0 {
		fmt.Println("能被3又能被5整除")
	}
}
```

![image-20231015110018392](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015110018392.png?raw=true)

8. 判断一个年份是否是闰年，闰年的条件是符合下面二者之一：(1)年份能被 4 整除，但不能被 100 整除；(2)能被 400 整除

   ```go
   	var year int = 2023
   	if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0){
   		fmt.Println("是闰年")
   	}
   ```

   

![image-20231015110312846](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015110312846.png?raw=true)

### 5.3.5多分支控制

基本语法

![image-20231015110348857](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015110348857.png?raw=true)

对上面基本语法的说明

1. 多分支的判断流程如下:
   1. 先判断条件表达式 1 是否成立，如果为真，就执行代码块 1
   2. 如果条件表达式 1 如果为假，就去判断条件表达式 2 是否成立， 如果条件表达式 2 为真， 就执行代码块 2
   3. 依次类推.
   4. 如果所有的条件表达式不成立，则执行 else 的语句块。
2. else 不是必须的。
3. 多分支只能有一个执行入口。

- 看一个多分支的流程图(更加清晰)

  ![image-20231015110530757](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015110530757.png?raw=true)

多分支的快速入门案例

岳小鹏参加 Golang 考试，他和父亲岳不群达成承诺： 

如果：

成绩为 100 分时，奖励一辆 BMW；
成绩为(80，99]时，奖励一台 iphone7plus；
当成绩为[60,80]时，奖励一个 iPad；
其它时，什么奖励也没有。
请从键盘输入岳小鹏的期末成绩，并加以判断

```go
package main
import (
	"fmt"
)
func main() {
	var score int
	fmt.Println("请输入成绩")
	fmt.Scanln(&score)

	//多分枝判断
	if score == 100 {
		fmt.Println("奖励一辆BMW")
	}else if score >= 80 && score <= 99 {
		fmt.Println("奖励一个 iPad")
	}else if score >= 60 && score <= 79 {
		fmt.Println("奖励一个 iPad mini")
	}else {
		fmt.Println("没有奖励")
	}
	
}
```

![image-20231015111352338](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015111352338.png?raw=true)

多分支的课堂练习

![image-20231015111442509](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015111442509.png?raw=true)

案例3 

![image-20231015111546027](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015111546027.png?raw=true)

```go
package main
import (
	"fmt"
	"math"
)
func main() {
	var a float64 = 2.0
	var b float64 = 3.0
	var c float64 = 4.0
	m := b * b - 4 * a * c
	//多分支判断
	if m  > 0 {
		n1 :=(-b + math.Sqrt(m)) / (2 * a)
		n2 :=(-b - math.Sqrt(m)) / (2 * a)
		fmt.Println("方程有两个实根", n1, n2)
	}else if m == 0 {
		n1 :=(-b + math.Sqrt(m)) / 2 * a
		fmt.Println("方程有一个实根", n1)
	}else {
		fmt.Println("方程无实根")
	}
}
```

![image-20231015111913755](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015111913755.png?raw=true)

### 5.3.6嵌套分支

在一个分支结构中又完整的嵌套了另一个完整的分支结构，里面的分支的结构称为内层分 支外面的分支结构称为外层分支。

![image-20231015112025979](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015112025979.png?raw=true)

应用案例 

参加百米运动会，如果用时 8 秒以内进入决赛，否则提示淘汰。并且根据性别提示进入男子组或女子组。【可以让学员先练习下】, 输入成绩和性别。

![image-20231015112055925](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015112055925.png?raw=true)

应用案例 2

出票系统：根据淡旺季的月份和年龄，打印票价 [考虑学生先做]

4_10 旺季：
成人（18-60）：60
儿童（<18）:半价
老人（>60）:1/3
淡季：
成人：40
其他：20

![image-20231015112348039](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015112348039.png?raw=true)

## switch分支控制

### 5.4.1 基本的介绍

1. switch 语句用于基于不同条件执行不同动作，每一个 case 分支都是唯一的，从上到下逐一测 试，直到匹配为止。
2. 匹配项后面也不需要再加 break

### 5.4.2基本语法

![image-20231015112535732](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015112535732.png?raw=true)

### 5.4.3switch的流程图

![image-20231015112552518](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015112552518.png?raw=true)

对上图的说明和总结

1. switch 的执行的流程是，先执行表达式，得到值，然后和 case 的表达式进行比较，如果相等， 就匹配到，然后执行对应的 case 的语句块，然后退出 switch 控制
2. 如果 switch 的表达式的值没有和任何的 case 的表达式匹配成功，则执行 default 的语句块。执行后退出 switch 的控制.
3. golang 的 case 后的表达式可以有多个，使用 逗号 间隔.
4. golang 中的 case 语句块不需要写 break , 因为默认会有,即在默认情况下，当程序执行完 case 语 句块后，就直接退出该 switch 控制结构。

### 5.4.4switch快速入门案例

案例：

请编写一个程序，该程序可以接收一个字符，比如: a,b,c,d,e,f,g a表示星期一，b表示星期二 … 根 据用户的输入显示相依的信息.要求使用 switch 语句完成

```go
package main
import (
	"fmt"
)
func main() {
	var key byte
	fmt.Println("请输入一个字符 a,b,c,d,e,f,g")
	fmt.Scanf("%c",&key)

	switch key {
	case 'a':
		fmt.Println("a")
	case 'b':
		fmt.Println("b")
	case 'c':
		fmt.Println("c")
	case 'd':
		fmt.Println("d")
	case 'e':
		fmt.Println("e")
	case 'f':
		fmt.Println("f")
	case 'g':
		fmt.Println("g")
	
	default:
		fmt.Println("输入错误")
	}
}
```

### 5.4.5switch的使用的注意事项和细节

1. case/switch 后是一个表达式( 即：常量值、变量、一个有返回值的函数等都可以)

![image-20231015113205220](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015113205220.png?raw=true)

2. case 后的各个表达式的值的数据类型，必须和 switch 的表达式数据类型一致

![image-20231015113218115](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015113218115.png?raw=true)

3. case 后面可以带多个表达式，使用逗号间隔。比如 case 表达式 1, 表达式 2 ...

![image-20231015113243316](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015113243316.png?raw=true)

4. case 后面的表达式如果是常量值(字面量)，则要求不能重复

![image-20231015113259473](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015113259473.png?raw=true)

5. case 后面不需要带 break , 程序匹配到一个 case 后就会执行对应的代码块，然后退出 switch，如 果一个都匹配不到，则执行 default
6. default 语句不是必须的.
7. switch 后也可以不带表达式，类似 if --else 分支来使用。【案例演示】

```go
package main
import (
	"fmt"
)
func main() {
var age int = 10
switch  {
case age == 10 :
fmt.Println("10")
case age == 20 :
fmt.Println("20")
default:
fmt.Println("default")
}

//case 中也可以对 范围进行判断
var score int = 90
switch {
	case score >= 90 && score <= 100:
		fmt.Println("A")
	case score >= 80 && score < 90 :
		fmt.Println("B")
	case score >= 70 && score < 80 :
		fmt.Println("C")
	case score >= 60 && score < 70 :
		fmt.Println("D")
	default:
		fmt.Println("NO")
}
}
```

![image-20231015113835972](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015113835972.png?raw=true)

8. switch 后也可以直接声明/定义一个变量，分号结束，不推荐。 【案例演示】

![image-20231015114007670](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114007670.png?raw=true)

9. switch 穿透-fallthrough ，如果在 case 语句块后增加 fallthrough ,则会继续执行下一个 case，也 叫 switch 穿透

![image-20231015114107558](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114107558.png?raw=true)

9. Type Switch：switch 语句还可以被用于 type-switch 来判断某个 interface 变量中实际指向的 变量类型 【还没有学 interface, 先体验一把】

![image-20231015114127163](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114127163.png?raw=true)

### 5.4.6switch课堂练习

1. 使用 switch 把小写类型的 char 型转为大写(键盘输入)。只转换 a, b, c, d, e. 其它的输出 “other”。

![image-20231015114319989](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114319989.png?raw=true)

2. 对学生成绩大于 60 分的，输出“合格”。低于 60 分的，输出“不合格”。(注：输入的成绩不 能大于 100)

![image-20231015114340697](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114340697.png?raw=true)

3. 根据用户指定月份，打印该月份所属的季节。3,4,5 春季 6,7,8 夏季 9,10,11 秋季 12, 1, 2

![image-20231015114425625](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231015114425625.png?raw=true)

### 5.4.7switch和if比较

总结了什么情况下使用 switch ,什么情况下使用 if
1) 如果判断的具体数值不多，而且符合整数、浮点数、字符、字符串这几种类型。建议使用 swtich
语句，简洁高效。
2) 其他情况：对区间判断和结果为 bool 类型的判断，使用 if，if 的使用范围更广。

## 5.5 for循环控制

#### 5.5.1基本介绍

听其名而知其意。就是让我们的一段代码循环的执行。

### 5.5.2一个实际的需求

请大家看个案例 [forTest.go]:
编写一个程序, 可以打印 10 句
"你好，尚硅谷!"。请大家想想怎么做?

使用传统的方式实现

![image-20231018142030520](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018142030520.png?raw=true)

for循环的快速入门

```go
package main
import (
	"fmt"
)
func main() {
for i :=1; i<=10; i++ {
	fmt.Println("您好,尚硅谷",i)
}
}
```

![image-20231018142704536](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018142704536.png?raw=true)

### 5.5.3for循环的基本语法

语法格式：

for 循环变量初始化；循环条件；循环变量迭代 {

​	循环操作(语句)

}

**对上面的语法格式说明**

**对 for 循环来说，有四个要素：**

1. 循环变量初始化
2. 循环条件
3. 循环操作(语句),有人也叫循环体。
4. 循环变量迭代

**for循环执行的顺寻说明**

1. 执行循环初始化，比如 `i:=1`

2. 执行循环条件,比如 i<=10
3. 如果循环条件为真，就执行循环操作:比如fmt.Println("......")
4. 执行循环变量迭代，比如 i++
5. 反复执行2，3，4步骤，知道循环条件为false，就退出for循环

#### 5.5.4for循环执行流程分析

![image-20231018143902061](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018143902061.png?raw=true)

对照代码分析for循环的执行过程

![image-20231018144125048](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018144125048.png?raw=true)

#### 5.5.5for循环的使用注意事项和细节讨论

1. 循环条件是返回一个布尔值的表达式

2. for循环的第二种使用方式

   for 循环判断条件 {

   ​	//循环执行语句

   }

   将变量初始化和变量迭代写道其他位置

3. 案例演示

   ![image-20231018144951805](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018144951805.png?raw=true)

   ```go
   //for循环的第二种写法
   j := 1//循环变量初始化
   for j <= 10 { //循环条件
   	fmt.Println("尚硅谷",j)
   	j++//循环变量迭代
   }
   ```

   ![image-20231018145317530](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018145317530.png?raw=true)

3. for循环的第三种使用方式

   ```go
   for {
   //循环执行语句
   }
   ```

   **上面的写法等价 for ; ; {} 是一个无限循环， 通常需要配合 break 语句使用**

4. Golang 提供 for-range 的方式，可以方便遍历字符串和数组(注: 数组的遍历，我们放到讲数组 的时候再讲解) ，案例说明如何遍历字符串。

- 字符串遍历方式1-传统方式



- 字符串遍历方式2-for -range 

  ```go
  str := "abc~ok北京"
  for index, val := range str {
  	fmt.Printf("index=%d, val=%c\n", index, val)
  }
  ```

![image-20231018151546353](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018151546353.png?raw=true)

- 上面代码的细节讨论

- 如果我们的字符串含有中文，那么传统的遍历字符串方式，就是错误，会出现乱码。原因是传统的 对字符串的遍历是按照字节来遍历，而一个汉字在 utf8 编码是对应 3 个字节。

  - 如何解决 需要要将 str 转成 []rune

  ```go
  //字符串遍历方式1-传统方式
  var str string = "hello,world北京"
  str2 := []rune(str) //就是把str转成[]rune
  for i :=0 ;i <len(str2);i++ {
  	fmt.Printf("str[%d]=%c\n",i,str2[i])//使用到下标...
  }
  ```

  - 对应 for-range 遍历方式而言，是按照字符方式遍历。因此如果有字符串有中文，也是 ok

  ```go
  //字符串遍历方式2-for-range
  str := "abc~ok北京"
  for index, val := range str {
  	fmt.Printf("index=%d, val=%c\n", index, val)
  }
  ```

  ### 5.5.6 for 循环的课堂练习

  1. 打印1~100之间所有是9的倍数的整数的个数及总和

     ```go
     package main
     import (
     	"fmt"
     )
     func main() {
     	//1.打印1——100之间所有是9的倍数的整数的个数及总和
     	//2.当一个数%9 == 0就是9 的倍数
     	//3.我们需要声明两个变量count和sum来保存数和总和
     	var max uint64 = 100
     	var min uint64 = 1
     	var count uint64 = 0
     	var sum uint64 = 0
     	for ; min <= max ; min++ {
     		if min%9 == 0 {
     			count++
     			sum += min
     		}
     	}
     	fmt.Printf("count=%v sum=%v\n",count,sum)
     }
     ```

​			![image-20231018153412833](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018153412833.png?raw=true)

2. 完成下面的表达式输出，6是可变的。

```go
	var n int = 6
	for i := 0;i <= n;i++{
		fmt.Printf("%v+%v=%v\n",i,n -i,n)
	}
```

![image-20231018154031768](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018154031768.png?raw=true)

## 5.6 while和do..while的实现

Go语言没有while和do..while，这一点需要同学们注意一下，如果我们需要使用类似其它语 言(比如 java / c 的 while 和 do...while )，可以通过 for 循环来实现其使用效果

### 5.6.1while循环的实现

![image-20231018154138226](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018154138226.png?raw=true)

- 说明上图

  1. for循环是一个无限循环
  2. break语句就是跳出for循环

  使用上面的whilt实现完整输出10句”hello.world"

  ```go
  	//使用上面的whilt实现完整输出10句”hello.world"
  	//循环变量初始化
  	var i int = 1
  	for {
  		if i > 10 { //循环条件
  			break //跳出循环体
  		}else {
  			fmt.Println("hello,world",i)
  			i++ //循环体迭代
  		}
  	}
  ```

  

![image-20231018154437234](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018154437234.png?raw=true)

### 5.6.2do..while的实现

![image-20231018154510065](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018154510065.png?raw=true)

- 对上图说明

  1. 上面的循环是先执行，在判断，因此至少执行一次。

  2. 当循环条件成立后，就会执行 break, break 就是跳出 for 循环，结束循环.

     使用上面的 do...while 实现完成输出 10 句”hello,world”

```go
	//使用上面的 do...while 实现完成输出 10 句”hello,world”
	//循环变量初始化
	var i int = 1
	for {
		fmt.Println("hello,world",i)
		i++ //循环体迭代
		if i > 10 { //循环条件
			break //跳出循环体		
		}
	}
}
```

![image-20231018154953166](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018154953166.png?raw=true)

## 5.7 多重循环控制（重点，难点）

### 5.7.1基本介绍

1. 将一个循环放在另一个循环体内，就形成了嵌套循环。在外边的 for 称为外层循环在里面的 for 循环称为内层循环。`【建议一般使用两层，最多不要超过 3 层】`
2. 实质上，嵌套循环就是把内层循环当成外层循环的循环体。当只有内层循环的循环条件为 false 时，才会完全跳出内层循环，才可结束外层的当次循环，开始下一次的循环。
3. 外层循环次数为 m 次，内层为 n 次，则内层循环体实际上需要执行 m*n 

### 5.7.2应用案例

1. 统计 3 个班成绩情况，每个班有 5 名同学，求出各个班的平均分和所有班级的平均分[学生的成 绩从键盘输入

   - 先易后难
   - 先死后活

   代码：

   ```go
   //求出各个班的平均分和所有班级的平均分[学生的成绩从键盘输入]
   
   //分析实现思路
   //1统计1个班成绩情况，每个班有5名同学，求出该班的平均分[学生的成绩从键盘输入]=》先易后)
   //2.学生数就是5个[先死后活]
   //3.声明一个sum 统计班级的总分
   
   //分析实现思路2
   //1. 统计3个班成绩情况，每个班有5名同学，求出每个班的平均分[学生的成绩从键盘输入]
   //2.j 表示第几个班级
   //3.定义一个变量存放总成绩
   
   //分析实现思路3
   //1.我们可以把代码做活
   //2.定义两个变量，表示班级的个数和班级的人数
   	
   var classNUm int = 3
   var stuNum int = 5
   var totalSum float64 = 0.0
   	for j :=1;j <= classNUm;j++ {
   		sum := 0.0
   		for i := 1;i <= stuNum;i++ {
   			var score float64
   			fmt.Printf("请输入第%d班,第%d个学生的成绩\n",j,i)
   			fmt.Scanln(&score)
   			sum += score
   			}
   		fmt.Printf("第%d个班级的平均分是%v\n",j,sum /float64(stuNum))
   		totalSum += sum
   	}
   	fmt.Printf("所有班级的平均分是%v\n",totalSum / float64(classNUm))
   }	
   ```

   ![image-20231018161907264](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018161907264.png?raw=true)

3. 打印金字塔

使用 for 循环完成下面的案例请编写一个程序，可以接收一个整数,表示层数，打印出金字

- 普通金字塔

```go
package main
import (
	"fmt"
)
var num = 20
func main() {
	for i :=1; i<= num ; i++ {
		for k := 1;k <= num - i ; k++ {
			fmt.Print(" ")
		}
		for j :=1;j <= 2 * i -1 ; j++ {
			fmt.Print("*")
		}
		fmt.Println()
	}
}
```

![image-20231018171158758](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018171158758.png?raw=true)

- 空心金字塔

```go
package main
import (
	"fmt"
)
var num = 20
func main() {
	for i :=1; i<= num ; i++ {
		for k := 1;k <= num - i ; k++ {
			fmt.Print(" ")
		}
		for j :=1;j <= 2 * i -1 ; j++ {
			if j ==1 || j == 2 * i -1||i == num{
			fmt.Print("*")
			}else {
				fmt.Print(" ")
			}
		}
		fmt.Println()
	}
}
```

![image-20231018171220918](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018171220918.png?raw=true)

4. 打印九九乘法表

```go
	num := 9
	for i := 1; i<= num;i++{
		for j := 1;j <=i;j++{
		fmt.Printf("%v * %v = %v\t",j,i,j*i)
	}
	fmt.Println()
}
```

## 5.8 跳转控制语句-break

### 5.8.1看一个具体需求，引出break

随机生成 1-100 的一个数，直到生成了 99 这个数，看看你一共用了几次

分析：编写一个无限循环的控制，然后不停的随机生成数，当生成了 99 时，就退出这个无限循环 ==》break 提示使用 这里我们给大家说一下，如下随机生成 1-100 整数

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	//我们为了生成一个随机数，还需要个rand设置一个种子.
//time.Now()Unix() : 返回一个从197:1:1 的o时e分o秒到现在的秒数
//rand.seed(time.Now( ).Unix())
//如何随机的生成1-100整数
//n := rand.Intn(100) + 1 // [ 10e)//fmt.Println(n)
//随机生成1-1的一个数，直到生成了99这个数，看看你一共用了几次//分析思路:
//编写一个无限循环的控制，然后不停的随机生成数，当生成了99时，就退出这个无限循环==》breal	
	var count int = 0
	for {
		rand.Seed(time.Now().UnixNano())
		n := rand.Intn(100) + 1
		fmt.Println(n)
		count++
		if n == 99 {
			break
		}
	}
	fmt.Printf("生成了99一共用了 %d 次\n", count)
}

```

### 5.8.3基本介绍

break 语句用于终止某个语句块的执行，用于中断当前 for 循环或跳出 switch 语句。

### 5.8.4基本语法

{ ……
break ……
}

### 5.8.5以for循环使用break为例

![image-20231018210853895](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018210853895.png?raw=true)

### 5.8.6break的注意事项和使用细节

1. break 语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块

![image-20231018210948167](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018210948167.png?raw=true)

3. 对上面案例的说明
   - break 默认会跳出最近的 for 循环
   - break 后面可以指定标签，跳出标签对应的 for循环

### 5.8.7课堂练习

1. 100以内的数求和，求出 当和 第一次大于20的当前数

```go
	//1. 100以内的数求和，求出 当和 第一次大于20的当前数
	sum := 0
	for i :=1 ;i <= 100 ;i++ {
		sum += i
		if sum > 20 {
			fmt.Printf("当和第一次大于20的当前数是 %d\n", i)
			break
		}
	}

}
```

```cmd
E:\goproject\src\gocode\gw\project05\damo12>go run main.go
当和第一次大于20的当前数是 6
```

2. 实现登录验证，有三次机会，如果用户名为”张无忌",密码：888 提示登录成功，否则提示还有几次机会，

```go
var name string
var pwd string
var login = 3
for i :=1 ;i <= 3 ;i++ {
	fmt.Printf("请输入用户名:")
	fmt.Scanln(&name)
	fmt.Printf("请输入密码:")
	fmt.Scanln(&pwd)
	if name == "张无忌" && pwd == "888" {
		fmt.Println("登录成功")
		break
		}else {
			login--
			fmt.Printf("用户名或密码错误：还有%v次机会",login)
		}
		}	
	if login == 0 {
		fmt.Println("登录失败")
    }
}
```

![image-20231018212032046](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018212032046.png?raw=true)

### 5.9 跳转控制语句-continue

### 5.9.1基本介绍

continue语句用于结束本次循环，继续执行下一次循环。

continue语句出现在多层签到的循环语句体中时，`可以通过标签指明要跳过的是那一层循环`，这个和前面的break标签使用规则一样

### 5.9.2基本语法

{ ……
continue ……
}

### 5.9.3continue流程图

![image-20231018213327332](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018213327332.png?raw=true)

### 5.9.4案例分析continue的使用

![image-20231018213608409](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018213608409.png?raw=true)

### 5.9.5continue的课堂练习

![image-20231018213649092](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018213649092.png?raw=true)

```go
package main

import (
	"fmt"
	// "math/rand"
	// "time"
)

func main() {
//continue实现打印1-100之内的奇数要求使用for循环+continue
for i := 1; i <= 100; i++ {
	if i % 2 == 0{
		continue
	}
	fmt.Printf("奇数%v\n",i)
}
}
```

![image-20231018213959310](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018213959310.png?raw=true)

- 从键盘读入个数不确定的整数，并判断读入的正数和负数的个数，输入为 0 时结束程序

```go
package main

import (
	"fmt"
	// "math/rand"
	// "time"
)

func main() {
	// 从键盘读入个数不确定的整数，并判断读入的正数和负数的个数，输入为 0 时结束程序
	var z int 
	var f int
	var num int
	for {
		fmt.Println("请输入一个整数")
		fmt.Scanln(&num)
		if num == 0 {
			break
		}
		if num > 0 {
			z++
			continue
		} else {
			f++
		}	
	}
	fmt.Println("正数个数：", z)
	fmt.Println("负数个数：", f)
}
```

```cmd
E:\goproject\src\gocode\gw\project05\damo13>go run main.go
请输入一个整数
1
请输入一个整数
a
请输入一个整数
请输入一个整数
-1
请输入一个整数
0
正数个数： 3
负数个数： 1
```

## 5.10跳转控制语句-goto

### 5.10.1goto基本介绍

1. Go语言的goto语句可以无条件地转移到程序种指定的行
2. goto语句通常与条件语句配合使用。可以来实现条件转移，跳出循环体等功能。
3. 在Go程序设计种`一般不主张使用goto语句`，以免造成程序流程的混乱，使理解和调试程序都困难

### 5.10.2goto基本语法

goto lable

.....

label:statement

### 5.10.3goto的流程图

![image-20231018214700730](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018214700730.png?raw=true)

### 5.10.4快速入门案例

```go
package main

import (
	"fmt"
	// "math/rand"
	// "time"
)

func main() {
	var n int 
	fmt.Println("请输入数值")
	fmt.Scan(&n)
	//演示goto的使用
	fmt.Println("before loop")
	if n > 20 {
		goto out1
	}else if n > 10 && n <= 20{
		goto out2
	}
	fmt.Println("ok2")
	fmt.Println("ok3")
	fmt.Println("ok4")
	out1:
	fmt.Println("ok5")
	out2:
	fmt.Println("ok6")

}

```

![image-20231018215434771](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018215434771.png?raw=true)

## 5.11跳转控制语句-retrun

### 5.11.1介绍：

retrun 使用在方法活函数种，表示跳出所在的方法或函数，在讲解函数的时候，会详细介绍。

```go
package main

import (
	"fmt"
	// "math/rand"
	// "time"
)
func main() {
for i :=0;i <= 10;i++ {
	if i==3{
		return
	}
	fmt.Println("哇哇哇",i)
	}
}
```

```cmd
E:\goproject\src\gocode\gw\project05\damo14>go run main.go
哇哇哇 0
哇哇哇 1
哇哇哇 2
```

![image-20231018215730857](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018215730857.png?raw=true)

说明：

1. 如果return 是在普通的函数，则表示跳出该函数，即不再执行函数中 return 后面代码，也可以 理解成终止函数。

2. 如果 return 是在 main 函数，表示终止 main 函数，也就是说终止程序。

# 第六章 函数、包和错误处理

## 6.1 为什么需要函数

### 6.1.1 请大家完成这样一个需求

输出两个输出，在输入一个运算符得到结果

![image-20231018221421456](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018221421456.png?raw=true)

分析上面代码问题

- 上面的写法是可以完成功能, 但是代码冗余
- 同时不利于代码维护
- 函数可以解决这个问题

## 6.2函数的基本概念

为完成某一功能的程序指令(语句)的集合，称为函数。

在Go种，函数分为：自定义函数、系统函数(查看Go编写手册)

## 6.3函数的基本语法

![image-20231018221721608](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018221735095.png?raw=true)

## 6.4 快速入门案例

使用函数解决前面计算问题

```go
package main
import (
	"fmt"
)
func Cal(n1 float32,n2 float32,Openator byte)float32{
	var res float32
	switch Openator{
		case '+':
			res = n1 + n2
		case '-':
			res = n1 - n2
		case '*':
			res = n1 * n2
		case '/':
			res = n1 / n2
		default:
			fmt.Println("error")
	}
	return res
}
func main(){
	var n1 float32
	var n2 float32
	var Openator byte = '+'
	fmt.Println("请输入n1")
	fmt.Scan(&n1)
	fmt.Print("请输入运算符:\n ")
	// fmt.Scan(&Openator)	
	// fmt.Println(Openator)
	fmt.Println("请输入n2")
	fmt.Scan(&n2)
	Cal(n1,n2,Openator)
	fmt.Println("结果为",Cal(n1,n2,Openator))
}
```

## 6.5 包的引出

1. 在实际的开发中，我们往往需要在不同的文件中，去调用其它文件的定义的函数，比如 main.go 中，去使用 utils.go 文件中的函数，如何实现？ -》包
2. 现在有两个程序员共同开发一个 Go 项目,程序员 xiaoming 希望定义函数 Cal ,程序员 xiaoqiang 也想定义函数也叫 Cal。两个程序员为此还吵了起来,怎么办? -》

## 6.6 包的原理图

包的本质实际上就是创建不同的文件夹，来存放程序文件。 画图说明一下包的原理

![image-20231018225625569](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018225625569.png?raw=true)

![image-20231018225639141](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018225639141.png?raw=true)

## 6.7包的基本概念

说明：go 的每一个文件都是属于一个包的，也就是说 go 是以包的形式来管理文件和项目目录结构 的

## 6.8包的三大作用

区分相同名字的函数、变量等标识符
当程序文件很多时,可以很好的管理项目
控制函数、变量等访问范围，即作用域

## 6.9包的相关说明

- 打包基本语法
  - package 包名
- 引入包的基本语法
  - import “包的路径"

## 6.10包使用的快速入门

包快速入门-Go 相互调用函数，我们将 func Cal 定义到文件 utils.go , 将 utils.go 放到一个包中，当 其它文件需要使用到 utils.go 的方法时，可以 import 该包，就可以使用了. 【为演示：新建项目目录结 构】

![image-20231018230119583](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018230119583.png?raw=true)

1. utils.go文件

   ```go
   package main
   import (
   	"fmt"
   )
   func Cal(n1 float32,n2 float32,Openator byte)float32{
   	var res float32
   	switch Openator{
   		case '+':
   			res = n1 + n2
   		case '-':
   			res = n1 - n2
   		case '*':
   			res = n1 * n2
   		case '/':
   			res = n1 / n2
   		default:
   			fmt.Println("error")
   	}
   	return res
   }
   ```

   

![image-20231018230136308](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018230136308.png?raw=true)

2.main.go文件

```go
package main
import (
	"fmt"
	"gocode/gw/project06/damo1/utils"
)

func main(){
	var n1 float32
	var n2 float32
	var Openator byte = '+'
	fmt.Println("请输入n1")
	fmt.Scan(&n1)
	fmt.Print("请输入运算符:\n ")
	// fmt.Scan(&Openator)	
	// fmt.Println(Openator)
	fmt.Println("请输入n2")
	fmt.Scan(&n2)
	ss := utils.Cal(n1,n2,Openator)
	fmt.Println("结果为",ss)
}
```

![image-20231018231146694](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018231146694.png?raw=true)

## 6.11包使用的注意事项和细节讨论

1. 在给一个文件打包时，该包对应一个文件夹，比如这里的 utils 文件夹对应的包名就是 utils, 文件的包名通常和文件所在的文件夹名一致，一般为小写字母
2. 当一个文件要使用其它包函数或变量时，需要先引入对应的包

- 引入方式1：import "包名"

- 引入方式2：

  import ( 

  "包名"
  "包名"
  )

- package 指令在 文件第一行，然后是 import 指令。

- 在 import 包时，路径从 $GOPATH 的 src 下开始，不用带 src , 编译器会自动从 src 下开始引入

3. 为了让其它包的文件，可以访问到本包的函数，则该函数名的首字母需要大写，类似其它语言 的 

![image-20231018231351077](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018231351077.png?raw=true)

4. 在访问其它包函数，变量时，其语法是 包名.函数名， 比如这里的 main.go 文件中

![image-20231018231500903](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018231500903.png?raw=true)

5. 如果包名较长，Go 支持给包取别名， 注意细节：取别名后，原来的包名就不能使用了

![image-20231018231609456](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018231609456.png?raw=true)

说明: 如果给包取了别名，则需要使用别名来访问该包的函数和变量。

6. 在同一包下，不能有相同的函数名（也不能有相同的全局变量名），否则报重复定义
7. 如果你要编译成一个可执行程序文件，就需要将这个包声明为 main , 即 package main .这个就 是一个语法规范，如果你是写一个库 ，包名可以自定义

![image-20231018231636948](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018231636948.png?raw=true)

## 6.12函数的调用机制

### 6.12.1 通俗易懂的方式的理解

![image-20231018233928345](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018233928345.png?raw=true)

### 6.12.2 函数-调用过程

介绍：为了让大家更好的理解函数调用过程, 看两个案例，并画出示意图，这个很重要

1. 传入一个数+1

```go
package main
import (
	"fmt"
)

	func test(n1 int){
		n1 = n1 + 1
		fmt.Println("test()n1=",n1)
	}
func main () {
 n1 := 10
 //调用test
 test(n1)
 fmt.Println("main()n1=",n1)
}
```

![image-20231018234217697](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018234217697.png?raw=true)

![image-20231018234243203](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018234243203.png?raw=true)

- 在调用一个函数时，会给该函数分配一个新的空间，编译器会通过自身的处理让这个新的空间 和其它的栈的空间区分开来

- 在每个函数对应的栈中，数据空间是独立的，不会混淆

- 当一个函数调用完毕(执行完毕)后，程序会销毁这个函数对应的栈空间。

2. 计算两个数,并返回

```go
package main
import (
	"fmt"
)

func test(n1 int){
	n1 = n1 + 1
	fmt.Println("test()n1=",n1)
}
func gettest(n1 int,n2 int)(int){
	sum := n1 + n2
	fmt.Println("gettest()sum=",sum)
	return sum
}
func main () {
 n1 := 10
 //调用test
 test(n1)
 fmt.Println("main()n1=",n1)
 sum := gettest(10,20)
 fmt.Println("main sum ",sum)
}
```

![image-20231018234701154](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018234701154.png?raw=true)

## 6.12.3 return语句

- 基本语法和说明

![image-20231018234731546](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018234731546.png?raw=true)

- 案例演示

  - 请编写要给函数，可以计算两个数的和和差，并返回结果。

  ```go
  package main
  import (
  	"fmt"
  )
  
  func test(n1 int){
  	n1 = n1 + 1
  	fmt.Println("test()n1=",n1)
  }
  func gettest(n1 int,n2 int)(int){
  	sum := n1 + n2
  	fmt.Println("gettest()sum=",sum)
  	return sum
  }
  func getsub(n1 int,n2 int )(int,int){
  	sum := n1 + n2
  	sub := n1 - n2
  	return sum,sub
  }
  func main () {
   n1 := 10
   //调用test
   test(n1)
   fmt.Println("main()n1=",n1)
   sum := gettest(10,20)
   fmt.Println("main sum ",sum)
   //调用gettest
   fmt.Println("-----------")
   res1,res2 := getsub(1,2)
   fmt.Printf("res1=%v,res2=%v",res1,res2)
  }
  ```

  ![image-20231018235051538](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018235051538.png?raw=true)

- 案例演示2
  - 一个细节说明: 希望忽略某个返回值，则使用 _ 符号表示占位忽略

![image-20231018235505585](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231018235505585.png?raw=true)

## 6.13 函数的递归调用

### 6.13.1基本介绍

一个函数在函数体内又调用了本身，我们称为递归调用

### 6.13.2递归调用快速入门

![image-20231019085120247](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085120247.png?raw=true)

```go
package main
import (
	"fmt"
)
func test(n int ) {
	if n > 2 {
		n--
		test(n)
	}else{
	fmt.Println("n=",n)
	}
}
func main () {
	//看一段代码
	test(4)//通过分析来看一下递归调用的特点
}
```

![image-20231019085138878](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085138878.png?raw=true)

### 6.13.3递归调用的总结

函数递归需要遵守的重要原则：

1. 执行一个函数时，就创建一个新的受保护的独立空间(新函数栈)
2. 函数的局部变量是独立的，不会相互影响
3.  递归必须向退出递归的条件逼近，否则就是无限递归，死龟了:)
4. 当一个函数执行完毕，或者遇到 return，就会返回，遵守谁调用，就将结果返回给谁，同时当函数执行完毕或者返回时，该函数本身也会被系统销毁

### 6.13.4递归课堂练习

题 1：斐波那契数
请使用递归的方式，求出斐波那契数 1,1,2,3,5,8,13... 给你一个整数 n，求出它的斐波那契数是多少？
思路:
1) 当 n == 1 || n ==2 , 返回 1
2) 当 n >= 2, 返回 前面两个数的和 f(n-1) + f(n-2)
代码

![image-20231019085434310](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085434310.png?raw=true)

题 2：求函数值
已知 f(1)=3; f(n) = 2*f(n-1)+1;
请使用递归的思想编程，求出 f(n)的值?
思路：直接使用给出的表达式即可完成

![image-20231019085500305](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085500305.png?raw=true)

练习题 3
题 3：猴子吃桃子问题
有一堆桃子，猴子第一天吃了其中的一半，并再多吃了一个！以后每天猴子都吃其中的一半，然后
再多吃一个。当到第十天时，想再吃时（还没吃），发现只有 1 个桃子了。问题：最初共多少个桃子？
思路分析：
1) 第 10 天只有一个桃子
2) 第 9 天有几个桃子 = (第 10 天桃子数量 + 1) * 2
3) 规律: 第 n 天的桃子数据 peach(n) = (peach(n+1) + 1) * 2
代码:

![image-20231019085519466](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085519466.png?raw=true)

![image-20231019085529630](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085529630.png?raw=true)

## 6.14函数使用的注意事项和细节讨论

1. 函数的形参列表可以是多个，返回值列表也可以是多个。
2. 形参列表和返回值列表的数据类型可以是值类型和引用类型。
3. 函数的命名遵循标识符命名规范，首字母不能是数字，首字母大写该函数可以被本包文件和其 它包文件使用，类似 public , 首字母小写，只能被本包文件使用，其它包文件不能使用，类似 privat
4. 函数中的变量是局部的，函数外不生效【案例说明】

![image-20231019085713587](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085713587.png?raw=true)

5. 基本数据类型和数组默认都是值传递的，即进行值拷贝。在函数内修改，不会影响到原来的值。

![image-20231019085738471](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085738471.png?raw=true)

6. 如果希望函数内的变量能修改函数外的变量(指的是默认以值传递的方式的数据类型)，可以传 入变量的地址&，函数内以指针的方式操作变量。从效果上看类似引用 。

![image-20231019085758492](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085758492.png?raw=true)

7. Go 函数不支持函数重载

![image-20231019085818904](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085818904.png?raw=true)

8. 在 Go 中，函数也是一种数据类型，可以赋值给一个变量，则该变量就是一个函数类型的变量 了。通过该变量可以对函数调用

![image-20231019085854441](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085854441.png?raw=true)

9. 函数既然是一种数据类型，因此在 Go 中，函数可以作为形参，并且调

![image-20231019085913131](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019085913131.png?raw=true)

![image-20231019110723554](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019110723554.png?raw=true)

10. 为了简化数据类型定义，Go支持自定义数据类型

- 基本语法：type 自定义数据类型名 数据类型 // 理解: 相当于一个别
- 案例：type myInt int // 这时 myInt 就等价 int 来使用了.
- 案例：type mySum func (int, int) int // 这时 mySum 就等价 一个 函数类型 func (int, int) int

**举例说明自定义数据类型的使用:**

```go
package main
import (
	"fmt"
)
func main () {
	//给int取了别名，在go中myInt和int虽然都是int类型，但是go认为myint和int两个类型
	type myInt int
	var num1 myInt
	var num2 int
	num1 = 40
	num2 = int(num1) //各位，注意这里依然需要显示转换，go认为myInt和int两个类型
	fmt.Println("num1=",num1,"num2=",num2)
}
```

![image-20231019111150629](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019111150629.png?raw=true)

![image-20231019111200640](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019111200640.png?raw=true)

![image-20231019164500674](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019164500674.png?raw=true)

11. 支持函数返回值命名

```go
package main
import (
	"fmt"
)
func getsub(n1 int,n2 int) (sum int,sub int){
	sub = n1 - n2
	sum = n1 + n2
	return
}
func main () {
	a1,b1 := getsub(10,20)
	fmt.Printf("sub=%v sum=%v",a1,b1)	

}
```

![image-20231019164826033](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019164826033.png?raw=true)

12. 使用_标识符，或略返回值

![image-20231019164913639](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019164913639.png?raw=true)

13. Go支持不可变参数

![image-20231019164930687](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019164930687.png?raw=true)

![image-20231019165624123](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019165624123.png?raw=true)

![image-20231019165632376](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019165632376.png?raw=true)

## 6.15函数的课堂练习

![image-20231019165655017](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019165655017.png?raw=true)

![image-20231019165707591](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019165707591.png?raw=true)

```go
package main
import (
	"fmt"
)
func swap (n1 *int ,n2 *int) {
	t := *n1
	*n1 = *n2
	*n2 = t
}
func main() {
	a := 10
	b := 20
	swap(&a,&b)
	fmt.Printf("a=%v,b=%v",a,b)
}
```

![image-20231019170104310](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019170104310.png?raw=true)

## 6.16 init函数

### 6.16.1基本介绍

- 每一个源文件都可以包含一个 init 函数，该函数会在 main 函数执行前，被 Go 运行框架调用，也 就是说 init 会在 main 函数前被调用。

### 6.16.2 案例说明：

```go
package main
import (
	"fmt"
)
func main () {
	fmt.Println("main()...")
}
func init () {
	fmt.Println("init()...")
}
```

![image-20231019170431698](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019170431698.png?raw=true)

### 6.16.3init函数的注意事项和细节

1. 如果一个文件同事包含全局变量定义，init函数和main函数，则执行的流程`全局变量定义`-`>init`—>`函数`—>`main函数`

```go
package main
import (
	"fmt"
)
var age = test()
//为了看到全局变量是先前被舒适化的，我们这里线些函数
func test() int {
	fmt.Println("test")//1
	return 90
}
//init函数，通常可以在init函数中完成初始化工作
func init () {
	fmt.Println("init")//2
}
func main(){
	fmt.Println("main")//3
}
```

![image-20231019170933019](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019170933019.png?raw=true)

2, init函数最主要的作用，就是完成一些初始化工作。

```go
package utils
import "fmt"
var Age int
var Name string 
func init () {
	fmt.Println("utils 包的init")
	Age = 100
	Name = "tom~"
}
```

![image-20231019171006656](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019171006656.png?raw=true)

```go
package main
import (
	"fmt"
	us "gocode/gw/project06/funcinit/utils"
)

var age = test()
//为了看到全局变量是先前被舒适化的，我们这里线些函数
func test() int {
	fmt.Println("test")//1
	return 90
}
//init函数，通常可以在init函数中完成初始化工作
func init () {
	fmt.Println("init")//2
}
func main(){
	fmt.Println("main")//3
	fmt.Println("Age=",us.Age,"Name=",us.Name)
}
```

![image-20231019171633362](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019171633362.png?raw=true)

3. 细节说明: 面试题：案例如果 main.go 和 utils.go 都含有 变量定义，init 函数时，执行的流程 又是怎么样的呢？

## 6.17匿名函数

### 6.17.1介绍

- Go 支持匿名函数，匿名函数就是没有名字的函数，如果我们某个函数只是希望使用一次，可以考 虑使用匿名函数，匿名函数也可以实现多次调用。

### 6.17.2 匿名函数使用方式

- 在定义匿名函数时就直接调用，这种方式匿名函数只能调用一次。 【案例演示】

  ```go
  package main
  import (
  	"fmt"
  )
  
  func main () {
  	//在定义匿名函数时直接调用，这种方式匿名函数只能用一次
  	//案例演示，求两个数的和，使用匿名函数的方式完成
  	res1 := func (n1 int,n2 int ) int {
  		return n1 + n2
  	}(10,20)
  	fmt.Println(res1)
  }
  ```

![image-20231019172057728](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019172057728.png?raw=true)

### 6.17.3 匿名函数使用方式2

- 将匿名函数赋值给一个变量（函数变量），再通过该变量来调用匿名函数【案例演示】

```go
package main
import (
	"fmt"
)

func main () {
	//在定义匿名函数时直接调用，这种方式匿名函数只能用一次
	//案例演示，求两个数的和，使用匿名函数的方式完成
	res1 := func (n1 int,n2 int ) int {
		return n1 + n2
	}
	res2 := res1(10,30)
	res3 := res1(90,30)
	fmt.Println("res2=",res2)
	fmt.Println("res3=",res3)
}
```

![image-20231019172321087](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019172321087.png?raw=true)

### 6.17.4全局匿名函数

- 如果将匿名函数赋给一个全局变量，那么这个匿名函数，就成为一个全局匿名函数，可以在程序 有效。

```go
package main
import (
	"fmt"
)
var (
	//fun1就是一个全局匿名函数
	Funl = func (n1 int,n2 int) int {
		return n1 * n2
	}
)
func main () {
	//在定义匿名函数时直接调用，这种方式匿名函数只能用一次
	//案例演示，求两个数的和，使用匿名函数的方式完成
	res1 := func (n1 int,n2 int ) int {
		return n1 + n2
	}
	res2 := res1(10,30)
	res3 := res1(90,30)
	fmt.Println("res2=",res2)
	fmt.Println("res3=",res3)


	res4 := Funl(4,9)
	fmt.Println("res4",res4)
}
```

## 6.18闭包

### 6.18.1 介绍

- 基本介绍：闭包就是一个函数和与其相关的引用环境组合的一个整体（实体）

### 6.18.2 案例演示

```go
package main
import (
	"fmt"
)
var (
	//fun1就是一个全局匿名函数
	Funl = func (n1 int,n2 int) int {
		return n1 * n2
	}
)
func  Addupper() func (int) int {
	var n int = 10
	return func (x int ) int {
		n = n + x
		return n 
	}
}
func main () {
	f := Addupper()
	fmt.Println(f(1))//11
	fmt.Println(f(2))//13
	fmt.Println(f(3))//16
}
```

```apl
这段代码定义了一个函数 Addupper，它没有参数，返回一个函数，这个返回的函数也接受一个整数参数，然后返回一个整数。

在 Addupper 函数中，有以下关键点：

var n int = 10 定义了一个整数变量 n，并初始化为 10。

return func(x int) int { ... } 返回一个匿名函数。这个匿名函数接受一个整数参数 x，然后执行以下操作：

n = n + x：将函数内部的 n 变量与传入的参数 x 相加，并将结果赋值给 n。这样，n 的值在每次调用这个匿名函数时都会增加。

return n：返回增加后的 n 的值。

在 main 函数中，通过 f := Addupper() 调用了 Addupper 函数，将返回的函数保存在变量 f 中。然后，你可以使用变量 f 来调用这个返回的函数，传递一个整数参数给它。

示例中的输出解释如下：

fmt.Println(f(1))：调用 f，并传递参数 1 给它。n 的初始值是 10，所以 n 变成 11，返回 11。

fmt.Println(f(2))：再次调用 f，并传递参数 2 给它。n 现在是 11，所以 n 变成 13，返回 13。

fmt.Println(f(3))：继续调用 f，并传递参数 3 给它。n 现在是 13，所以 n 变成 16，返回 16。

这个代码演示了闭包的概念，匿名函数可以访问并修改外部函数中定义的变量，这里的 n 就是一个外部变量。
```

```cmd
E:\goproject\src\gocode\gw\project06\damo10>go run main.go
11
13
16
```

对上面代码的说明和总结

-  AddUpper 是一个函数，返回的数据类型是 fun (int) in
- 闭包的说明

![image-20231019210056466](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231019210056466.png?raw=true)

返回的是一个匿名函数, 但是这个匿名函数引用到函数外的 n ,因此这个匿名函数就和 n 形成一 个整体，构成闭包。

3. 大家可以这样理解: 闭包是类, 函数是操作，n 是字段。函数和它使用到 n 构成闭包。
4. 当我们反复的调用 f 函数时，因为 n 是初始化一次，因此每调用一次就进行累计。
5. 我们要搞清楚闭包的关键，就是要分析出返回的函数它使用(引用)到哪些变量，因为函数和它引 用到的变量共同构成闭包。
6. 对上面代码的一个修改，加深对闭包的理解

```go
package main 
import (
	"fmt"
)
func AddUpper() func (int) int {
	var n int = 10
	var str = "hello"
	return func (x int) int {
		n = n + x
		str += string(36)
		fmt.Println("str",str)
		return n 
	}
}
func main () {
	f := AddUpper()
	fmt.Println(f(1))
	fmt.Println(f(2))
	fmt.Println(f(3))
}
```

### 6.18.3闭包的最佳实践

- 请编写一个程序，具体要求如下：

1. 编写一个函数 makeSuffix(suffix string) 可以接收一个文件后缀名(比如.jpg)，并返回一个闭包
2. 调用闭包，可以传入一个文件名，如果该文件名没有指定的后缀(比如.jpg) ,则返回 文件名.jpg , 果已经有.jpg 后缀，则返回原文件名。
3. 要求使用闭包的方式完成
4. strings.HasSuffix , 该函数可以判断某个字符串是否有指定的后缀。

```go
package main

import (
	"fmt"
	"strings"
)
//func(string)。这就是匿名函数的参数。 func(string) 表示匿名函数接受一个 string 类型的参数
func makeSuffix(suffix string) func(string) string {
	return func(name string) string {
		if !strings.HasSuffix(name, suffix) {
			return name + suffix
		}
		return name
	}
}

func main() {
	f2 := makeSuffix(".jpg")
	fmt.Println("文件处理后=", f2("example")) // 传递文件名给 f2
	fmt.Println("文件处理后=", f2("image.jpg")) // 传递文件名给 f2
}
```

```cmd
E:\goproject\src\gocode\gw\project06\damo11>go run main.go
文件处理后= example.jpg
文件处理后= image.jpg
```

- 上面代码的总结和说明:
  - 返回的匿名函数和 makeSuffix (suffix string) 的 suffix 变量 组合成一个闭包,因为 返回的函数引用 到 suffix 这个变量
  - 我们体会一下闭包的好处，如果使用传统的方法，也可以轻松实现这个功能，但是传统方法需要每 次都传入 后缀名，比如 .jpg ,而闭包因为可以保留上次引用的某个值，所以我们传入一次就可以反复 使用。大家可以仔细的体会一把！

## 6.19函数的defer

### 6.19.1为什么需要defer

- 在函数中，程序员经常需要创建资源（比如:数据库连接、文件句柄、锁等），为了在函数执行完毕后，即使的释放资源，GO设计则提供defer(延时机制)

### 6.19.2快速入门案例

```go
package main

import (
	"fmt"
	_"strings"
)
func sum(n1 int,n2 int) int {
	//当执行defer时，暂时不执行，会将defer后面的语句压入到独立的栈(defer栈)
	//当函数执行完毕后，再从defer栈，按照先入后出的方式出栈，执行
	defer fmt.Println("ok1 n1=",n1)
	defer fmt.Println("ok2 n2=",n2)
	res := n1 + n2
	fmt.Println("ok3 res=",res)
	return res
}
func main() {
	res := sum(10,20)
	fmt.Println("res=",res)
}
```

![image-20231020093039781](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020093039781.png?raw=true)

### 6.19.3defer的注意事项和细节

1. 当go 执行到一个 defer 时，不会立即执行 defer 后的语句，而是将 defer 后的语句压入到一个栈 中[我为了讲课方便，暂时称该栈为 defer 栈], 然后继续执行函数下一个语句。
2. 当函数执行完毕后，在从 defer 栈中，依次从栈顶取出语句执行(注：遵守栈 先入后出的机制)
3. 在 defer 将语句放入到栈时，也会将相关的值拷贝同时入栈。请看一段代码：

```go
package main

import (
	"fmt"
	_"strings"
)
func sum(n1 int,n2 int) int {
	//当执行defer时，暂时不执行，会将defer后面的语句压入到独立的栈(defer栈)
	//当函数执行完毕后，再从defer栈，按照先入后出的方式出栈，执行
	defer fmt.Println("ok1 n1=",n1)
	defer fmt.Println("ok2 n2=",n2)
	n1++
	n2++
	res := n1 + n2
	fmt.Println("ok3 res=",res)
	return res
}
func main() {
	res := sum(10,20)
	fmt.Println("res=",res)
}
```

![image-20231020094715045](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020094715045.png?raw=true)

### 6.19.4defer的最佳实践

- defer 最主要的价值是在，当函数执行完毕后，可以及时的释放函数创建的资源。看下模拟代码。。

![image-20231020094816175](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020094816175.png?raw=true)

1. 在 golang 编程中的通常做法是，创建资源后，比如(打开了文件，获取了数据库的链接，或者是 锁资源)， 可以执行 defer file.Close() defer connect.Close()
2. 在 defer 后，可以继续使用创建资源
3. 当函数完毕后，系统会依次从 defer 栈中，取出语句，关闭资源.
4. 这种机制，非常简洁，程序员不用再为在什么时机关闭资源而烦心。

### 6.20函数参数传递方式

### 6.20.1基本介绍

- 我们在讲解函数注意事项和使用细节时，已经讲过值类型和引用类型了，这里我们再系统总结一 下，因为这是重难点，值类型参数默认就是值传递，而引用类型参数默认就是引用传递。

### 6.20.2两种传递方式

1. 值传递
2. 引用传递

其实，不管是值传递还是引用传递，传递给函数的都是变量的副本，不同的是，值传递的是值的 拷贝，引用传递的是地址的拷贝，一般来说，地址拷贝效率高，因为数据量小，而值拷贝决定拷贝的 数据大小，数据越大，效率越低。

### 6.20.3值类型和引用类型

1. **值类型**：基本数据类型int 系列，float系列，bool，string、数组和结构体stunct
2. **引用类型**：指针、slice切片、map、管道chan、interface等都是引用类型

### 6.20.4值传递和引用传递使用特点

![image-20231020095356468](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020095356468.png?raw=true)

3. 如果希望函数内的变量能修改函数外的变量，可以传入变量的地址&，函数内以指针的方式操 作变量。从效果上看类似引用 。这个案例在前面详解函数使用注意事项的

![image-20231020100300664](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020100300664.png?raw=true)

## 6.21变量作用域

1. 函数内部声明/定义的变量叫局部变量，作用域仅限于函数内部

![image-20231020100541007](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020100541007.png?raw=true)

2. 函数外部声明/定义的变量叫全局变量，作用域在整个包都有效，如果其首字母为大写，则作用 域在整个程序有效

```go
package main

import (
	"fmt"
	_"strings"
)
var age int = 50
var Name string = "jack~"
func test () {
	//age 和name的作用域就是只在test函数内部
	age := 10
	Name := "tom~"
	fmt.Println("age1=",age)//10
	fmt.Println("Name1=",Name)//tom
}
func main() {
	fmt.Println("age2",age)
	fmt.Println("name2",Name)
	test()
}
```

![image-20231020100857555](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020100857555.png?raw=true)

3. 如果变量是在一个代码块，比如 for / if 中，那么这个变量的的作用域就在该代码块

![image-20231020103138400](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020103138400.png?raw=true)

### 6.21.1变量作用域的课堂练习

```go
package main

import (
	"fmt"
	_"strings"
)
var name = "tom"//全局变量
func test01() {
	fmt.Println(name)//tom tom
}
func test02() { //编译器采用就近原则
	name := "jack"
	fmt.Println(name) //jack
}
func main() {
	fmt.Println(name) //tom
	test01()//tom
	test02()//jack
	test01()//tom
}
```

![image-20231020104003673](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020104003673.png?raw=true)

![image-20231020104142305](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020104142305.png?raw=true)

## 6.22函数课堂练习（综合）

1. 函数可以没有返回值案例，编写一个函数,从终端输入一个整数打印出对应的金子塔

分析思路：就是将原来写的打印金字塔的案例，使用函数的方式封装，在需要打印时，直接调用 即可。

```go
package main

import (
	"fmt"
)

func test(totallevel int) {
	for i := 1; i <= totallevel; i++ {
		// 打印空格
		for k := 1; k <= totallevel-i; k++ {
			fmt.Print(" ")
		}
		// 打印星号
		for j := 1; j <= 2*i-1; j++ {
			fmt.Print("*")
		}
		// 换行
		fmt.Println()
	}
}

func main() {
	var n int
	fmt.Println("请输入打印金字塔的层数")
	fmt.Scanln(&n)
	test(n)
}

```

2. 编写一个函数,从终端输入一个整数(1—9),打印出对应的乘法表

分析思路：就是将原来写的调用九九乘法表的案例，使用函数的方式封装，在需要打印时，直接调 用即可 代码

```go
package main

import (
	"fmt"
)

func test(totallevel int) {
	for i := 1; i <= totallevel; i++ {
		// 打印空格
		for k := 1; k <= totallevel-i; k++ {
			fmt.Print(" ")
		}
		// 打印星号
		for j := 1; j <= 2*i-1; j++ {
			fmt.Print("*")
		}
		// 换行
		fmt.Println()
	}
}

func test2(num int ) {
	for i := 1;i <= num;i++{
		for j := 1;j <= i;j++{
			fmt.Printf("%v * %v = %v \t",j,i,j * i)	
		}
		fmt.Println()
	}
}
func main() {
	var n int
	fmt.Println("请输入打印金字塔的层数")
	fmt.Scanln(&n)
	test(n)

	var num int
	fmt.Println("请输入九九乘法表的对应数")
	fmt.Scanln(&num)
	test2(num)
}
```

![image-20231020110027939](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020110027939.png?raw=true)

3. 编写函数,对给定的一个二维数组(3×3)转置，这个题讲数组的时候再完成

![image-20231020110051569](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020110051569.png?raw=true)

## 6.23字符串常用的系统函数

- 说明：字符串在我们程序开发中，使用的是非常多的，常用的函数需要掌握【看手册或官方指南】

1. 统计字符串的长度，按字节 `len(str)`![image-20231020142926383](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020142926383.png?raw=true)

   ```go
   	//统计字符串的长度，按字节len(str)
   	//golang的编码统一为utf-8（ascii的字符（字母和数字）占一个字节
   	// ，汉字占用3哥字节）
   	str := "hello北"
   	fmt.Println("str len=",len(str))
   ```

2. 字符串遍历，同事处理有中文的问题 r :=[]rune(str)

```go
	str2 := "hello北京"
	//字符串遍历，同事处理中文的问题r:=[]rune(str2)
	r := []rune(str2)
	for i :=0;i < len(r);i++ {
		fmt.Printf("字符=%c\n",r[i])
	}
```

3. 字符串转整数：n,err :=strconv.Atoi("12")

```go
n,err :=strconv.Atoi("111")
if err !=nil{
	fmt.Println("转换错误",err)
}else{a
	fmt.Println("转成的结果是",n)
}
```

4. 整数转字符串 str = strconv.Itoa(12345)

```go
	n1 :=strconv.Itoa(222)
	fmt.Printf("str=%v,str=%T",n1,n1)
```

5. 字符串转 []byte: 	var bytes = []byte("+-*/%")

```go
	var bytes = []byte("+-*/%")
	fmt.Printf("bytest=%v",bytes)
```

6. []byte 转 字符串 	str3 := string([]byte{43,45,42,47,37})

```go
	str3 := string([]byte{43,45,42,47,37})
	fmt.Println(str3)
```

7. 10进制转2、8、16进制：str =strconv.FormatInt(123,2)//2->8,16

```go
	sep := strconv.FormatInt(123,2)
	fmt.Printf("123对应的二进制是=%v\n",sep)

	sep2 := strconv.FormatInt(123,8)
	fmt.Printf("123对应的二进制是=%v\n",sep2)
	
	sep3 := strconv.FormatInt(123,16)
	fmt.Printf("123对应的二进制是=%v\n",sep3)
```

8. 查找子串是否在指定的字符串中: strings.Contains("seafood", "foo") //t

```go
//查找子串是否在指定的字符串中，string。contains("seafood","foo")//true
	b := strings.Contains("seafood","sea")
	fmt.Printf("b=%v\n",b)
}
```

9. 统计一个字符串有几个指定的子串： strings.Count("ceheese",

```go
//统计一个字符串有几个指定的子串
	onf := strings.Count("appssow","s")
	fmt.Printf("onf=%v\n",onf)
```

10. 不区分大小写的字符串比较(==是区分字母大小写的): fmt.Println(strings.EqualFold("abc", "Abc")) // trune

    ```go
    // 不区分大小写的字符串比较(==是区分字母大小写的): fmt.Println(strings.EqualFold("abc", "Abc")) // trune
    	noAb := strings.EqualFold("abc","ABC")
    	fmt.Printf("noAb=%v\n",noAb)
    	fmt.Println("结果",strings.EqualFold("abc", "Abc"))
    	fmt.Println("结果","abc" == "ABC")
    ```

11. 返回子串在字符串第一次出现的 index 值，如果没有返回-1 : strings.Index("NLT_abc", 

```go
// 返回子串在字符串第一次出现的 index 值，如果没有返回-1 : strings.Index("NLT_abc", 
index := strings.Index("NLT_abcxjfosnkos","abc")//4
fmt.Printf("index=%v",index)
```

12. 返回子串在字符串最后一次出现的 index，如没有返回-1 : strings.LastIndex("go golang", "go")

```go
//返回子串在字符串最后一次出现的 index，如没有返回-1 : strings.LastIndex("go golang", "go")
index2 := strings.LastIndex("go sgolang","go")
fmt.Printf("index2=%v",index2)
```

13. 将指定的子串替换成 另外一个子串: strings.Replace("go go hello", "go", "go 语言", n) n 可以指 定你希望替换几个，如果 n=-1 表示全部替换

```go
//将指定的子串替换成 另外一个子串: strings.Replace("go go hello", "go", "go 语言", n) n 可以指
// 定你希望替换几个，如果 n=-1 表示全部替换
st2 := "go go hello"
st3 := strings.Replace(st2,"go","北京",-1)
fmt.Printf("st2=%v st3=%v",st2,st3)
```

14. 按 照 指 定 的 某 个 字 符 ， 为 分 割 标 识 ， 将 一 个 字 符 串 拆 分 成 字 符 串 数 组 ： strings.Split("hello,wrold,ok", ","

```go
//按 照 指 定 的 某 个 字 符 ， 为 分 割 标 识 ， 将 一 个 字 符 串 拆 分 成 字 符 串 数 组 ：
// strings.Split("hello,wrold,ok", ","
strArr := strings.Split("hello,world,ok",",")
for i := 0 ;i < len(strArr);i++ {
	fmt.Printf("str[%v]=%v\n",i,strArr[i])
}
fmt.Printf("strArr=%v\n",strArr)
}
```

15. 将字符串的字母进行大小写的转换: strings.ToLower("Go") // go strings.ToUpper("Go") // GO

```go
a1 := "goLang Hello"
a1 = strings.ToLower(a1)
fmt.Printf("str=%v\n",a1)
a1 = strings.ToUpper(a1)
fmt.Printf("str=%v\n",a1)
}
```

16. 将字符串左右两边的空格去掉： strings.TrimSpace(" tn a lone gopher ntrn "

```go
b1 := strings.TrimSpace("  tn  a lone goa   ")
fmt.Printf("b1=%v",b1)
}
```

17) 将字符串左右两边指定的字符去掉 ： strings.Trim("! hello! ", " !") // ["hello"] //将左右两边 ! 和 " "去掉

```go
//将字符串左右两边的空格去掉： strings.TrimSpace(" tn a lone gopher ntrn "
b1 := strings.Trim("!!@  tn  a lone goa   !!","!")
fmt.Printf("b1=%v",b1)
```

18. 将字符串左边指定的字符去掉 ： strings.TrimLeft("! hello! ", " !") // ["hello"] //将左边 ! 和 " "去掉
19. 将字符串右边指定的字符去掉 ：strings.TrimRight("! hello! ", " !") // ["hello"] //将右边 ! 和 " "去掉

```go
// 将字符串左边指定的字符去掉 ： strings.TrimLeft("! hello! ", " !") // ["hello"] //将左边 ! 和 " "去掉
c1 := strings.TrimLeft("!hello!","!")
fmt.Println(c1)
c1 = strings.TrimRight("!hello!","!")
fmt.Println(c1)
```

20. 判断字符串是否以指定的字符串开头: strings.HasPrefix("ftp://192.168.10.1", "ftp") // true

```go
d1 := strings.HasPrefix("ftp://127.0.0.1","ftp")//true
fmt.Printf("d1=%v\n",d1)
```

21) 判断字符串是否以指定的字符串结束: strings.HasSuffix("NLT_abc.jpg", "abc") //false

```go
d1 = strings.HasSuffix("ftp://127.0.0.1.obs","obs")//true
fmt.Printf("d1=%v\n",d1)
```

#### 总代码

```go
package main

import (
	"fmt"
	"strconv"
	"strings"
)

func main () {
	//统计字符串的长度，按字节len(str)
	//golang的编码统一为utf-8（ascii的字符（字母和数字）占一个字节
	// ，汉字占用3哥字节）
	str := "hello北"
	fmt.Println("str len=",len(str))

	str2 := "hello北京"
	//字符串遍历，同事处理中文的问题r:=[]rune(str2)
	r := []rune(str2)
	for i :=0;i < len(r);i++ {
		fmt.Printf("字符=%c\n",r[i])
	}

	n,err :=strconv.Atoi("111")
	if err !=nil{
		fmt.Println("转换错误",err)
	}else{
		fmt.Println("转成的结果是",n)
	}

	n1 :=strconv.Itoa(222)
	fmt.Printf("str=%v,str=%T",n1,n1)

fmt.Println()
	var bytes = []byte("+-*/%")
	fmt.Printf("bytest=%v",bytes)

fmt.Println()
	str3 := string([]byte{43,45,42,47,37})
	fmt.Println(str3)

fmt.Println()
	//10进制转2、8、16进制：str =strconv.FormatInt(123,2)//2->8,16
	sep := strconv.FormatInt(123,2)
	fmt.Printf("123对应的二进制是=%v\n",sep)

	sep2 := strconv.FormatInt(123,8)
	fmt.Printf("123对应的二进制是=%v\n",sep2)
	
	sep3 := strconv.FormatInt(123,16)
	fmt.Printf("123对应的二进制是=%v\n",sep3)

fmt.Println()
//查找子串是否在指定的字符串中，string。contains("seafood","foo")//true
	b := strings.Contains("seafood","sea")
	fmt.Printf("b=%v\n",b)

fmt.Println()
//统计一个字符串有几个指定的子串
	onf := strings.Count("appssow","s")
	fmt.Printf("onf=%v\n",onf)

fmt.Println ()
// 不区分大小写的字符串比较(==是区分字母大小写的): fmt.Println(strings.EqualFold("abc", "Abc")) // trune
	noAb := strings.EqualFold("abc","ABC")
	fmt.Printf("noAb=%v\n",noAb)
	fmt.Println("结果",strings.EqualFold("abc", "Abc"))
	fmt.Println("结果","abc" == "ABC")

fmt.Println()
// 返回子串在字符串第一次出现的 index 值，如果没有返回-1 : strings.Index("NLT_abc", 
	index := strings.Index("NLT_abcxjfosnkos","abc")//4
	fmt.Printf("index=%v",index)

fmt.Println()
//返回子串在字符串最后一次出现的 index，如没有返回-1 : strings.LastIndex("go golang", "go")
	index2 := strings.LastIndex("go sgolang","go")
	fmt.Printf("index2=%v",index2)

fmt.Println()
fmt.Println()
//将指定的子串替换成 另外一个子串: strings.Replace("go go hello", "go", "go 语言", n) n 可以指
// 定你希望替换几个，如果 n=-1 表示全部替换
st2 := "go go hello"
st3 := strings.Replace(st2,"go","北京",-1)
fmt.Printf("st2=%v st3=%v",st2,st3)

fmt.Println()
//按 照 指 定 的 某 个 字 符 ， 为 分 割 标 识 ， 将 一 个 字 符 串 拆 分 成 字 符 串 数 组 ：
// strings.Split("hello,wrold,ok", ","
strArr := strings.Split("hello,world,ok",",")
for i := 0 ;i < len(strArr);i++ {
	fmt.Printf("str[%v]=%v\n",i,strArr[i])
}
fmt.Printf("strArr=%v\n",strArr)

fmt.Println()
a1 := "goLang Hello"
a1 = strings.ToLower(a1)
fmt.Printf("str=%v\n",a1)
a1 = strings.ToUpper(a1)
fmt.Printf("str=%v\n",a1)

//将字符串左右两边的空格去掉： strings.TrimSpace(" tn a lone gopher ntrn "
b1 := strings.Trim("!!@  tn  a lone goa   !!","!")
fmt.Printf("b1=%v",b1)

fmt.Println()
fmt.Println()
// 将字符串左边指定的字符去掉 ： strings.TrimLeft("! hello! ", " !") // ["hello"] //将左边 ! 和 " "去掉
c1 := strings.TrimLeft("!hello!","!")
fmt.Println(c1)
c1 = strings.TrimRight("!hello!","!")
fmt.Println(c1)

d1 := strings.HasPrefix("ftp://127.0.0.1","ftp")//true
fmt.Printf("d1=%v\n",d1)
d1 = strings.HasSuffix("ftp://127.0.0.1.obs","obs")//true
fmt.Printf("d1=%v\n",d1)
}
```

## 6.24时间和日期相关函数

### 6.24.1基本的介绍

- 说明：在编程中，程序员会经常使用到日期相关的函数，比如：统计某段代码执行花费的时间等 等。

1. 时间和日期相关函数，需要导入time包

![image-20231020161438809](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020161438809.png?raw=true)

2. time.Time类型，用于表示时间

```go
package main

import (
	"fmt"
	"time"
)

func main (){
	//看看日期和时间相关函数和方法使用
	//1.获取当前时间
	now := time.Now()
	fmt.Printf("now=%v now type=%T",now,now)
}
```

![image-20231020161652760](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020161652760.png?raw=true)

4. 格式化日期和时间

- 方式1：就是使用Printf或则SPrintf

```go
func main (){
	//看看日期和时间相关函数和方法使用
	//1.获取当前时间
	now := time.Now()
	fmt.Printf("now=%v now type=%T\n",now,now)

	//2.通过now可以获取到年月日，分十秒
	fmt.Printf("年=%v\n",now.Year())
	fmt.Printf("月=%v\n",int(now.Month()))
	fmt.Printf("日=%v\n",now.Day())
	fmt.Printf("分=%v\n",now.Hour())
	fmt.Printf("时=%v\n",now.Minute())
	fmt.Printf("秒=%v\n",now.Second())

	fmt.Printf("当前年月日 %d-%d-%d %d:%d:%d\n",now.Year(),now.Month(),now.Day(),now.Hour(),now.Minute(),now.Second())
	dateStr := fmt.Sprintf("当前年月日 %d-%d-%d %d:%d:%d\n",now.Year(),now.Month(),now.Day(),now.Hour(),now.Minute(),now.Second())
	fmt.Printf(dateStr)
```

![image-20231020162800333](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020162800333.png?raw=true)

方式二：使用time.Format()方法完成:

```go
	//格式化时间的第二章方式：
	fmt.Printf(now.Format("2006-01-02 15:04:05"))
	fmt.Println()
	fmt.Printf(now.Format("2006-01-02"))
	fmt.Println()
	fmt.Printf(now.Format("15:04:05"))
```

对上面代码的说明:

 "2006/01/02 15:04:05" 这个字符串的各个数字是固定的，必须是这样写。
"2006/01/02 15:04:05" 这个字符串各个数字可以自由的组合，这样可以按程序需求来返回时间
和日期

```go
package main

import (
	"fmt"
	"time"
)

func main (){
	//看看日期和时间相关函数和方法使用
	//1.获取当前时间
	now := time.Now()
	fmt.Printf("now=%v now type=%T\n",now,now)

	//2.通过now可以获取到年月日，分十秒
	fmt.Printf("年=%v\n",now.Year())
	fmt.Printf("月=%v\n",int(now.Month()))
	fmt.Printf("日=%v\n",now.Day())
	fmt.Printf("分=%v\n",now.Hour())
	fmt.Printf("时=%v\n",now.Minute())
	fmt.Printf("秒=%v\n",now.Second())

	fmt.Printf("当前年月日 %d-%d-%d %d:%d:%d\n",now.Year(),now.Month(),now.Day(),now.Hour(),now.Minute(),now.Second())
	dateStr := fmt.Sprintf("当前年月日 %d-%d-%d %d:%d:%d\n",now.Year(),now.Month(),now.Day(),now.Hour(),now.Minute(),now.Second())
	fmt.Printf(dateStr)

	//格式化时间的第二章方式：
	fmt.Printf(now.Format("2006-01-02 15:04:05"))
	fmt.Println()
	fmt.Printf(now.Format("2006-01-02"))
	fmt.Println()
	fmt.Printf(now.Format("15:04:05"))
}
```

![image-20231020163214802](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020163214802.png?raw=true)

5. 时间的常量

![image-20231020163231496](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020163231496.png?raw=true)

- 常量的作用:在程序中可用于获取指定时间单位的时间，比如想得到 100 毫秒 100 * time. Millisecond

6. 结合 Sleep 来使用一下时间常量

```go
i := 0
	for {
		i++
		fmt.Println(i)
		time.Sleep(time.Millisecond * 100)
		if i == 100 {
			break
		}
	}
```

7. time 的 Unix 和 UnixNano 的方

![image-20231020164505030](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020164505030.png?raw=true)

```go
//unix和unixNano的使用
	fmt.Printf("unix时间戳=%v unixnano时间戳=%v\n",now.Unix(),now.UnixNano())
```

### 6.24.2时间和日期的课堂练习题

- 编写一段代码来统计 函数test03执行的时间

```go
package main
import (
	"fmt"
	"time"
	"strconv"
)
func test03() {
	str := ""
	for i := 0;i < 100000;i++{
		str +="hello" + strconv.Itoa(i)
		}
}
func main () {
	//在执行test03前，先获取到当前unix时间戳
	start := time.Now().Unix()
	test03()
	end := time.Now().Unix()
	fmt.Printf("执行test03()耗时时间为%v秒\n",end-start)
}
```

![image-20231020170354815](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020170354815.png?raw=true)

## 6.25内置函数

### 6.25.1说明：

- Golang 设计者为了编程方便，提供了一些函数，这些函数可以直接使用，我们称为 Go 的内置函 数。文档：https://studygolang.com/pkgdoc -> builtin

1. len：用来求长度，比如 string、array、slice、map、chann

2. new：用来分配内存，主要用来分配值类型，比如 int、float32,struct...返回的是指针

   举例说明 new 的使用

```go
package main
import (
	"fmt"
	_"time"
	_"strconv"
)
func main () {
	num1 := 100
	fmt.Printf("num1的类型%T,num2的值=%v,num1的地址%v\n",num1,num1,&num1)

fmt.Println()
	num2 := new(int)//*int
	//num2的类型%T => *int
	//num2的值 = 地址0xc00000e0b8（这个地址是系统分配的）
	//num2的地址%v = 地址 
	*num2 = 100
	fmt.Printf("num2的类型%T,num2的值=%v,num2的地址%v,指针指向的地址=%v\n",num2,num2,&num2,*num2)
}
```

上面代码对应的内存分析图

![image-20231020172014226](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020172014226.png?raw=true)

3. make:用来分配内存，主要用来分配引用类型，比如 channel、map、slice。这个我们后面讲解。

## 6.26错误处理

### 6.26.1看一段代码，因此错误处理

```go
package main
import (
	"fmt"
	_"time"
	_"strconv"
)
func test() {
	num1 := 10
	num2 := 0
	res := num1 / num2
	fmt.Println("res=",res)
}
func main (){
	//测试
	test()
	fmt.Println("main()下面的代码...")
}
```

![image-20231020172334070](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020172334070.png?raw=true)

1. 在默认情况下，当发生错误后(panic),程序就会退出（崩溃）
2. 如果我们希望：当发生错误后，可以捕获到错误，并进行处理，保证程序可以继续执行。还可 以在捕获到错误后，给管理员一个提示(邮件,短信。。。）
3. 这里引出我们要将的错误处理机制

### 6.26.2基本说明

1. Go 语言追求简洁优雅，所以，Go 语言不支持传统的 try…catch…finally 这种处理。
2. Go 中引入的处理方式为：defer, panic, recover
3. 这几个异常的使用场景可以这么简单描述：Go 中可以抛出一个 panic 的异常，然后在 defer 中 通过 recover 捕获这个异常，然后正常处理

### 2.26.3使用defer+reconver来处理错误

```go
package main
import (
	"fmt"
	"time"
	_"strconv"
)
func test () {
	//使用defer+reconver来捕获和处理异常
	defer func() {
		err := recover()
		if err !=nil {
			fmt.Println("err=",err)
		}
	}()
	num1 := 10
	num2 := 1
	res := num1 / num2
	fmt.Println("res=",res)
}
func main () {
	test()
	for {
		fmt.Println("main()下面的代码")
		time.Sleep(time.Second)
	}
}
```

![image-20231020173542985](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020173542985.png?raw=true)

### 6.26.4错误处理的好处

- 进行错误处理后，程序不会轻易挂掉，如果加入预警代码，就可以让程序更加的健壮。看一个 

  案例演示：

![image-20231020173714309](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020173714309.png?raw=true)

### 6.26.5自定义错误

### 6.26.6自定义错误的介绍

- Go 程序中，也支持自定义错误， 使用 errors.New 和 panic 内置函数。

1. errors.New("错误说明") , 会返回一个 error 类型的值，表示一个错误
2. panic 内置函数 ,接收一个 interface{}类型的值（也就是任何值了）作为参数。可以接收 error 类 型的变量，输出错误信息，并退出程序.

### 6.26.7案例说明

```go
package main
import (
	"fmt"
	"errors"
	_"time"
	_"strconv"
)
//函数去读取以配置文件init.conf的信息
//如果文件名传入不正确，我们就返回一个自定义的错误
func readConf(name string)(err error){
	if name == "config.ini"{
	return nil
	}else {
		// 返回一个自定义错误
		return errors.New("读取文件错误..")
	}
}
func test02() {
	// config.ini
	// config2.ini
	err := readConf("config2.ini")
	if err != nil {
		//如果读取文件发送错误，就输出这个错误，并终止程序
		panic(err)
	}
	fmt.Println("test02()继续执行...")
}
func main (){
	test02()
	fmt.Println("main()下面的代码")
}
```

![image-20231020175152589](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231020175152589.png?raw=true)

# 第七章 数字与切片

## 7.1为什么需要数组

- 看一个问题
  - 一个养鸡场有 6 只鸡，它们的体重分别是 3kg,5kg,1kg,3.4kg,2kg,50kg 。请问这六只鸡的总体重是 多少?平均体重是多少? 请你编一个程序。=》数组

- 传统的方法解决
  - ![image-20231114173125749](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114173125749.png?raw=true)

- 对上面代码的说明
  1) 使用传统的方法不利于数据的管理和维护
  2) 传统的方法不够灵活，因此我们引出需要学习的新的数据类型=>数组

## 7.2数组介绍

数组可以存放多个同一类型数据。数组也是一种数据类型，在 Go 中，数组是值类型

## 7.3数组的快速入门

我们使用数组的方法来解决养鸡场的问题。

```go
package main
import "fmt"
func main() {
	//使用数组方式来解决问题
	//定义一个数组
	var hens [7]float64
	//2.给每个元素赋值，元素的下标是从0开始的0-5
	hens[0] = 1.0
	hens[1] = 2.0
	hens[2] = 3.0
	hens[3] = 4.0
	hens[4] = 5.0
	hens[5] = 6.0
	hens[6] = 7.0
	//3.遍历数组求出的总体重
	totalWegith := 0.0
	for i := 0; i < 7; i++ {
		totalWegith += hens[i]
	}
	fmt.Println("总体重为\t", totalWegith)
	//4.求出平均体重
	av := fmt.Sprintf("%.2f", totalWegith / float64(len(hens)))
	fmt.Printf("平均体重为\t%v",av)
}
```

```cmd
E:\goproject\src\gocode\gw\project07\damo01>go run main.go
总体重为         28
平均体重为      4.00
```

对上面代码总结：

1. 使用数组来解决问题，程序的可维护性增加
2. 而且方法代码更加清除，也容易扩容。

## 7.4数组定义和内存布局

- **数组的定义**
  - var 数组名 [数组大小] 数组类型
  - var a [5] int
  - 赋初值 a[0] = 1 a [1] = 30....
- **数组在内存布局(重要)**

![image-20231114204655251](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114204655251.png?raw=true)

上图总结:

1. 数组的地址可以通过数组名来获取 &intArr
2. 数组的第一个元素的地址，就是数组的首地址
3. 数组的各个元素的地址间隔是依据数组的类型决定，比如 int64 -> 8 int32->4...

![image-20231114204839364](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114204839364.png?raw=true)

```go
package main
import "fmt"
func main() {
var intArr [3] int //int占8个字节
//当我们定义完数组后，其实数组的各个元素有默认值0
fmt.Println(intArr)
intArr[0] = 10
intArr[1] = 20
intArr[2] = 30
fmt.Println(intArr)
fmt.Printf("intArr的地址=%p intArr[0]地址%p intArr[1]地址%p intArr[2]地址%p",
&intArr,&intArr[0],&intArr[1],&intArr[2])
}
```

```cmd
E:\goproject\src\gocode\gw\project07\damo01>go run main.go
[0 0 0]
[10 20 30]
intArr的地址=0xc0000a4060 intArr[0]地址0xc0000a4060 intArr[1]地址0xc0000a4068 intArr[2]地址0xc0000a4070
```

## 7.5数组的使用

- 访问数组元素
  - 数组名 [下标] 比如: 你要使用a数组的第三个元素 a[2]
- 快速入门案例
  - 从终端循环输入5个成绩，保存到float64数组，并输出

```go
package main
import "fmt"
func main() {
//从终端循环输入5个成绩，保存到float64数组，并输出，
var score [5] float64
for i := 0; i < len(score);i++ {
	fmt.Printf("请输入第%d个元素的值\n",i+1)
	fmt.Scanln(&score[i])
}
//变量数组打印
for i :=0;i <len (score);i++{
	fmt.Printf("score[%d]=%v\n",i,score[i])
}
}
```

四种初始化数组的方式

![image-20231114222828547](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114222828547.png?raw=true)

```go
package main
import "fmt"
func main() {
//四种初始化数组的方式
var numArr01 [3]int = [3]int{1,2,3}
fmt.Println(numArr01)

var numArr02 = [3]int{5,6,7}
fmt.Println(numArr02)
//这里的[...]是规定的写法
var numArr03 = [...]int{7,8,9}
fmt.Println(numArr03)
var numArr04 = [...]int{1:100,3:200}
fmt.Println(numArr04)

//类型推导
strArr05 := [...] string{1:"tom",0:"jack",2:"mary"}
fmt.Println("strArr05=",strArr05)
}
```

```go
E:\goproject\src\gocode\gw\project07\damo05>go run main.go
[1 2 3]
[5 6 7]
[7 8 9]
[0 100 0 200]
strArr05= [jack tom mary]
```

## 7.6数组的遍历

### 7.6.1方式 1-常规遍历:

参考7.6

### 7.6.2方式2-for-range结构遍历

这是 Go 语言一种独有的结构，可以用来遍历访问数组的元素。

for-range的基本语法

![image-20231114223056520](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114223056520.png?raw=true)

for-range案例

![image-20231114223836778](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114223836778.png?raw=true)

```go
package main
import "fmt"
func main() {
//演示for-range遍历数组
heroes := [...]string{"松江","吴用","卢俊义"}
//使用常规的方式遍历，我不写了..
for i,v := range heroes {
	fmt.Printf("i=%v v=%v\n",i,v)
}
for _,v := range heroes {
	fmt.Printf("元素的值=%v\n",v)
}
}
```

```cmd
E:\goproject\src\gocode\gw\project07\damo06>go run main.go
i=0 v=松江
i=1 v=吴用
i=2 v=卢俊义
元素的值=松江
元素的值=吴用
元素的值=卢俊义
```

## 7.7数组使用的注意事项和细节

1. 数组是多个相同类型数据的组合,一个数组一旦声明/定义了,其长度是固定的, 不能动态变化![image-20231114224132500](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114224132500.png?raw=true)

```go
package main
import "fmt"
func main() {
//数组是多个相同类型数据的组合，一个数组一旦声明/定义了，其长度是固定的，不能动态变化。
var arr01 [3]int
arr01[0] = 1
arr01[1] = 2
arr01[2] = 1.1
arr01[3] = 890
fmt.Println(arr01)
}
```

2. var arr[]int 这时arr就是一个slice切片，切片后面专门讲解

3. 数组中的元素可以是任何数据类型，包括值类型和引用类型，但是不能混用。

4. 数组创建后，如果没有赋值，有默认值(零值)

   - 数值类型数组：默认值为0

   - 字符串数组：默认值为""
   - bool数组：默认值为false

![image-20231114224842925](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114224842925.png?raw=true)

```go
var arr02 [3]float32
var arr03 [3]string
var arr04 [3]bool
fmt.Printf("arr02=%v arr03=%v arr04=%v\n",arr02,arr03,arr04)
```

```cmd
arr02=[0 0 0] arr03=[  ] arr04=[false false false]
```

5. 使用数组的步骤
   1. 声明数组并开辟空间
   2. 给数组各个元素赋值(默认零值)
   3. 使用数组
6. 数组的下标是从0开始的

![image-20231114225025021](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114225025021.png?raw=true)

7. 数组下标必须在指定范围内使用，否则报 panic：数组越界，比如 var arr [5]int 则有效下标为 0-4

8. Go 的数组属值类型， 在默认情况下是值传递， 因此会进行值拷贝。数组间不会相互影

   ![image-20231114225437122](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114225437122.png?raw=true)

9. 如想在其它函数中，去修改原来的数组，可以使用引用传递(指针方式)

![image-20231114225446674](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114225446674.png?raw=true)

10. 长度是数组类型的一部分，在传递函数参数时 需要考虑数组的长度，看下面案例

    ![image-20231114225529389](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114225529389.png?raw=true)

## 7.8 数组的应用案例

1. ) 创建一个 byte 类型的 26 个元素的数组，分别 放置'A'-'Z‘。使用 for 循环访问所有元素并打印 出来。提示：字符数据运算 'A'+1 -> 'B'

   ![image-20231114230522178](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114230522178.png?raw=true)

```go
package main
import "fmt"
func main() {
//1）创建一个byte类型的26个元素的数组，分别放置A-Z
//使用for循环访问所有元素并打印出来，提升：字符数据运算'A' +1 ->'B'
//思路
//1.声明一个数组var myChars [26]byte
//2.使用for循环，利用 字符可以进行运算的特点来赋值'A' +1 -> 'B'
//3.使用for循环打印即可
//代码
var myChars [26]byte
for i := 0; i < 26; i++ {
	myChars[i] = 'A' + byte(i)
	fmt.Printf("%c ", myChars[i])
}
// for i := 0; i < 26; i++ {
//	fmt.Printf("%c ", myChars[i])
// 	}
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo08>go run main.go
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```

2. 请求出一个数组的最大值，并得到对应的下标。

   ![image-20231114233522054](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231114233522054.png?raw=true)

```go
package main
import "fmt"
func main() {
//请求出一个数组最大值，并得到对应的下标
//思路
//1.声明一个数组var intArr[5] = [...] int {1,-1,9,90,11}
//2.假定一个元素就是最大值,下标就0
//3.然后从第二个元素开始循环比较，如果发现有更大，则交换
fmt.Println()
var intArr[6]int = [...]int{1,-1,9,90,11,100}
maxVal := intArr[0]
maxValIndex := 0
for i := 1; i < len(intArr); i++ {
	if maxVal < intArr[i] {
		maxVal = intArr[i]
		maxValIndex = i
	}
}
fmt.Println("最大值是",maxVal,"下标是",maxValIndex)
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo09>go run main.go

最大值是 100 下标是 5
```

## 7.9为什么需要切片

- 先看一个需求：我们需要一个数组用于保存学生的成绩，但是学生的个数是不确定的，请问怎么 办？解决方案：-》使用切片。

## 7.10切片的基本介绍

1. 切片的英文是slice

2. 切片是数组的一个引用，因此切片是引用类型，在进行传递时，遵守引用传递的机制。

3. 切片的使用和数组类似，遍历切片、访问切片的元素和求切片长度len(slice)都一样。

4. 切片的长度是可以变化的，因此切片是一个可以动态变化数组。

5. 切片定义的基本语法:

   var 切片名 [] 类型

   比如: var  a [] int

## 7.11快速入门

演示一个切片的基本使用：

```go
package main
import "fmt"
func main() {
//演示切片的基本使用
var intArr [5] int = [...]int{1,22,33,55,99}
//声明/定义一个切片
//slice := intArr[1:3]
//1. slice 就是切片名
//2. intArr[1:3] 表示slice 引用到intArr这个数组
//3. 引用intArr数组的起始下标为1，最后的下标为3(但是不包含3)
slice := intArr[1:3]
fmt.Println("intArr=",intArr)
fmt.Println("slice 的元素是 =",slice)
fmt.Println("slice 的元素个数=",len(slice))
fmt.Println("slice 的容量=",cap(slice))
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo10>go run main.go
intArr= [1 22 33 55 99]
slice 的元素是 = [22 33]
slice 的元素个数= 2
slice 的容量= 4
```

## 7.12切片在内存中形式(重要)

- 基本的介绍

  - 为了让大家更加深入的理解切片，我们画图分析一下切片在内存中是如何布局的，这是一个非常重要的知识点:(以前面的案例来分析)

- 画出前面的切片内存布局

  ![image-20231115094735344](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115094735344.png?raw=true)

对上面的分析图总结

1. slice的确是一个引用类型

2. slice从底层来说，其实就是一个数据结构struct结构体

   type slice struct{

   ptr *[2]int

   len int

   cap int

   }

## 7.13切片的使用

- 方式1
  - 第一种方式：定义一个切片，然后让切片去引用一个已经创建好的数组，比如前面的案例就是这样的。

![image-20231115095301446](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115095301446.png?raw=true)

- 方式2
  - 第二种方式：通过make来创建切片
  - 基本语法：var 切片名 []type = make([]type,len,[cap])
  - 参数说明: type: 就是数据类型 len : 大小 cap ：指定切片容量，可选， 如果你分配了 cap,则要 求 cap>=len.

案例演示：

![image-20231115095607426](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115095607426.png?raw=true)

对上面代码的小结：

1. 通过make方式创建切片可以制定切片的大小容量
2. 如果没有给切片的各个元素赋值，那么就会使用默认值[int,float=> 0 string =>''' bool => false]
3. 通过make方式创建的切片对应的数组是由make底层维护，对外不可见，即只能通过slice去访问各个元素。

- 方式3
  - 第3种方式：定义一个切片，直接就指定具体数组，使用原理类似make的方式

案例演示：

![image-20231115104127752](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115104127752.png?raw=true)

**方式1和方式2的区别**

![image-20231115104156100](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115104156100.png?raw=true)

## 7.14切片的遍历

切片的遍历和数组一样，也有两种方式

- for循环常规方式遍历

- for-range结构遍历切片

```go
package main
import "fmt"
func main() {
	//使用常规的for循环遍历切片
	var arr [5]int = [...]int{10,20,30,40,50}
	slice := arr[1:4]//20,30,40
	for i :=0;i <len(slice);i++{
		fmt.Println(i,slice[i])
	}
	fmt.Println()
	
	// 使用for-range 方式遍历切片
	for i,v := range slice{
		fmt.Println(i,v)
	}
	fmt.Println()
	
	//使用for-range 方式遍历map
	var m map[string]int = make(map[string]int)
	m["a"] = 20
	m["b"] = 30
	m["c"] = 40
	for k,v := range m{
		fmt.Println(k,v)
	}
	fmt.Println()	
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo11>go run main.go
0 20
1 30
2 40

0 20
1 30
2 40

a 20
b 30
c 40
```

## 7.15切片的使用的注意事项和细节讨论

1. 切片初始化时 var slice = arr[startIndex:endIndex]

说明：从arr数组下标为startIndex，取到 下标为 endIndex的元素(不含arr[endIndex])。

2. 切片初始化时，忍让不能越界，范围在[0-len(arr)]之间，但是可以动态增长。

   var slice = arr[0:end] 可以简写 var slice = arr[:end]

   var slice = arr[start:len(arr)]可以简写: var slice = arr[start:]

   var slice = arr[0:len(arr)]可以简写成：var slice = arr[:]

3. cap是一个内置函数，用于统计切片的容量，即最大可用存放多少个元素

4. 切片定义完后，还不能使用，因为本身是一个空的，需要让其引用到一个数组，或则make一个空间供切片来使用

5. 切片可以继续切片

   ![image-20231115111015402](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115111015402.png?raw=true)

6. 用 append 内置函数，可以对切片进行动态追加![image-20231115111719580](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115111719580.png?raw=true)

   ```go
   package main
   import "fmt"
   func main() {
   //通过append内置函数，可以对切片进行动态追加
   var slice3 []int = []int{100,200,300}
   slice3 = append(slice3,400,500)
   fmt.Println(slice3)
   //通过append将切片slice3追加给slice3
   slice3 = append(slice3,slice3...)
   fmt.Println(slice3)
   fmt.Println(len(slice3))
   fmt.Println(cap(slice3))
   }	
   ```

   ```cmd
   E:\goproject\src\gocode\gw\project07\damo12>go run main.go
   [100 200 300 400 500]
   [100 200 300 400 500 100 200 300 400 500]
   10
   12
   ```

   ![image-20231115111811372](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115111811372.png?raw=true)

**切片 append 操作的底层原理分析:**

**切片 append 操作的本质就是对数组扩容**

**go 底层会创建一下新的数组 newArr(安装扩容后大小)**

**将 slice 原来包含的元素拷贝到新的数组 newArr**

**slice 重新引用到 newArr**

**注意 newArr 是在底层来维护的，程序员不可见.** 

7. 切片的拷贝操作

   - 切片使用copy内置函数完成拷贝，举例说明

   ```go
   package main
   import "fmt"
   func main() {
   //切片的拷贝操作
   //切片使用copy内置函数拷贝，举例说明
   fmt.Println()
   var slice4 []int = []int{1,2,3,4,5}
   var slice5 = make ([]int,10)
   copy(slice5,slice4)
   fmt.Println(slice4)//12345
   fmt.Println(slice5)//1234500000
   }	
   ```

```cmd
E:\goproject\src\gocode\gw\project07\damo13>go run main.go

[1 2 3 4 5]
[1 2 3 4 5 0 0 0 0 0]
```

代码说明

1. copy（paral，para2）参数的数据类型的切片
2. 按照上面的代码来看，slice4和slice5的数据空间是独立，相互不影响，也就是说slice4[0]=999,slice5[0]仍然是1

8. 拷贝注意事项

![image-20231115112846911](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115112846911.png?raw=true)

## 7.16string和slice

1. string底层是一个byte数组，因此string也可以进行切片处理，案例演示：

   ```go
   package main
   import "fmt"
   func main() {
   //string底层是一个byte数组，因此string也可以进行切片处理
   str :="hello@atguigu"
   //使用切片获取到 atguigu
   slice :=str[6:]
   fmt.Println(slice)
   }	
   ```

   ```cmd
   E:\goproject\src\gocode\gw\project07\damo14>go run main.go
   atguigu
   ```

2. string和七篇在内存的形式，以“abcd”画出内存示意图

   ![image-20231115113202685](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115113202685.png?raw=true)

3. string是不可变的，也就是说不能通过str[0]='z'方式来修改字符串

   ![image-20231115113906700](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115113906700.png?raw=true)

4. 如果需要修改字符串，可以先将string->[]byte /或则[]rune ->修改 ->重新转成string![image-20231115114854018](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115114854018.png?raw=true)

```go
package main
import "fmt"
func main() {
//string底层是一个byte数组，因此string也可以进行切片处理
str :="hello@atguigu"
//使用切片获取到 atguigu
slice :=str[6:]
fmt.Println(slice)

arr1 := []byte(str)
arr1[0] = 'z'
str = string(arr1)
fmt.Println("str=",str)
//细节，我们转成[]byte后，可以处理英文和数字，但是不能处理中文
//原因[]byte字节来处理，面一个汉字，是3个字节，因此会出现乱码
//解决方法，将string转成[]rune即可，因为[]rune是按照字节处理，兼容汉字
arr02 := []rune(str)
arr02[0] = '北'
str = string(arr02)
fmt.Println("str=",str)
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo14>go run main.go
atguigu
str= zello@atguigu
str= 北ello@atguigu
```

## 7.17切片的课堂练习

说明：编写一个函数fbn(n int),要求完成

1. 可以接收一个n int
2. 能够将斐波那契的数列放到切片中
3. 提示, 斐波那契的数列形式

arr[0] = 1; arr[1] = 1; arr[2]=2; arr[3] = 3; arr[4]=5; arr[5]=8

```go
package main
import "fmt"
func fbn(n int)([]uint64){
	//声明一个切片，切片大小n
	fbnSlice := make([]uint64,n)
	//第一个数和第二个数的斐波那契为1
	fbnSlice[0] = 1
	fbnSlice[1] = 1
	//进行for循环来存放斐波那契的数列
	for i :=2;i < n;i++{
		fbnSlice[i] = fbnSlice[i-1] + fbnSlice[i-2]
	}
	return fbnSlice
}
func main() {
/* 
	1. 可以接收一个n int
	2.能够将斐波那契的数列放到切片种
	3.提升，斐波那契的数列形式：
	arr[0] = 1; arr[1] = 1; arr[2]=2; arr[3] = 3; arr[4]=5; arr[5]=8

	思路
	1.声明一个函数fbn(n int) ([]unint64)
	2.编程fbn(n int)进行for循环来存放斐波那契的数列 0=》1 1 =》 1
*/
fnbSlice := fbn(20)
fmt.Println(fnbSlice)
}	
```

```cmd
E:\goproject\src\gocode\gw\project07\damo15>go run main.go
[1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765]
```

## 第八章排序和查找

### 8.1排序的基本介绍

![image-20231115141913400](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115141913400.png?raw=true)

### 8.2冒泡排序的思路分析

![image-20231115142417333](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115142417333.png?raw=true)

### 8.3冒泡排序实现

```go
package main

import "fmt"

// 冒泡排序
//接受一个指向包含5个整数的数组的指针
func BubbleSort(arr *[5]int) {
	//打印排序前的数组
	fmt.Println("排序前：", *arr)
	
	//定义一个临时变量
	temp := 0

	// 冒泡排序..一步一步推导出来的
	//外层循环，控制比较和交换的轮数 i= 4，一共循环4次
	for i := 0; i < len(*arr)-1; i++ { 
		//外层循环 'i'控制比较和交换的轮数，'len(*arr)'表示数组的长度。
		//len(*arr):表示由多少个数需要比较一共5个数（0-4）所有i=4
		//len(*arr -1 -i)：表示：这是内层循环，用于遍历未排序部分的数组元素。
			//在每一轮中，内层循环会比较相邻的元素，如果前一个元素比后一个元素大，
			// 则交换它们的位置。因为每一轮外层循环都会确保当前最大的元素已经在正
			// 确的位置，所以不需要变量已经遍历过的数。
		for j := 0; j < len(*arr)-1-i; j++ {
			//比较相邻的两个元素的大小，如果前一个元素大于后一个元素，就交互他们的位置
			if (*arr)[j] > (*arr)[j+1] { // 修正此处的索引
				temp = (*arr)[j]
				(*arr)[j] = (*arr)[j+1]
				(*arr)[j+1] = temp
			}
		}
		// 内层循环结束后，打印当前轮次的排序结果。
		fmt.Println("排序后：", *arr)
	}
}

func main() {
	//声明数组元素，并将地址传递给冒泡指针
	arr := [5]int{5, 4, 3, 2, 1} // 注意这里的数组元素顺序
	BubbleSort(&arr)
}

```

```cmd
E:\goproject\src\gocode\gw\project08\damo01>go run main.go
排序前： [5 4 3 2 1]
排序后： [4 3 2 1 5]
排序后： [3 2 1 4 5]
排序后： [2 1 3 4 5]
排序后： [1 2 3 4 5]
```

### 8.4课后练习

### 8.5查找

- 介绍：

  - 在Golang中，我们常用的查找有两种：
    1. 顺序查找
    2. 二分查找

- 案例演示：

  1. 有一个数列：白眉鹰王、金毛狮王、紫衫龙王、青翼蝠王

     猜数游戏：从键盘中任意输入一个名称，判断数列中是否包含此名称【顺序查找】

  代码：

  ```go
  package main
  import "fmt"
  func main() {
  	names :=[4]string{"白眉鹰王","金毛狮忘忘","紫衫龙王","青翼龙王"}
  	var heroName = ""
  	fmt.Println("请输入英雄的名字：")
  	fmt.Scanln(&heroName)
  
  	//顺序查找：第一种方式
  	for i := 0 ; i < len(names); i++ {
  		if heroName == names[i] {
  			fmt.Printf("英雄已找到，名字为%v位置%v",heroName,i+1)
  			break
          }else if i == len(names)-1 {
  			fmt.Printf("英雄未找到，名字为：%s\n",heroName)
  		}
      }
  	fmt.Println("\n----------------------------------------")
  	//顺序查找：第二种方式
  	index := -1
  	for i := 0 ; i < len(names); i++ {
  		if heroName == names[i] {
  			index = i
  			break
  		}
  	}
  	if index != -1 {
  		fmt.Printf("英雄已找到，名字为%v位置%v",heroName,index+1)
  	}else {
  		fmt.Printf("英雄未找到，名字为：%s\n",heroName)
  	}
  
  }
  ```

  ```cmd
  E:\goproject\src\gocode\gw\project08\damo02>go run main.go
  请输入英雄的名字：
  紫衫龙王
  英雄已找到，名字为紫衫龙王位置3
  ----------------------------------------
  英雄未找到，名字为：紫衫龙王
  ```

  2. 请对一个有序数组进行二分查找 {1,8, 10, 89, 1000, 1234} ，输入一个数看看该数组是否存 在此数，并且求出下标，如果没有就提示"没有这个数"。【会使用到递归】

  二分查找的思路分析：

  ![image-20231115161351940](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115161351940.png?raw=true)

```go
package main
import ( "fmt"
)
//二分查找的函数
/*
二分查找的思路: 比如我们要查找的数是 findVal
1. arr 是一个有序数组，并且是从小到大排序
2. 先找到 中间的下标 middle = (leftIndex + rightIndex) / 2, 然后让 中间下标的值和 findVal 进行
比较
2.1 如果 arr[middle] > findVal , 就应该向 leftIndex ---- (middle - 1)
2.2 如果 arr[middle] < findVal , 就应该向 middel+1---- rightIndex
2.3 如果 arr[middle] == findVal ， 就找到
2.4 上面的 2.1 2.2 2.3 的逻辑会递归执行
3. 想一下，怎么样的情况下，就说明找不到[分析出退出递归的条件!!]
if leftIndex > rightIndex {
// 找不到.. return .. }
*/
func BinaryFind(arr *[6]int, leftIndex int, rightIndex int, findVal int) {
//判断 leftIndex 是否大于 rightIndex
if leftIndex > rightIndex {
fmt.Println("找不到")
return
}
//先找到 中间的下标
middle := (leftIndex + rightIndex) / 2
if (*arr)[middle] > findVal {
//说明我们要查找的数，应该在 leftIndex --- middel-1
BinaryFind(arr, leftIndex, middle - 1, findVal)
} else if (*arr)[middle] < findVal {
//说明我们要查找的数，应该在 middel+1 --- rightIndex
BinaryFind(arr, middle + 1, rightIndex, findVal)
} else {
//找到了
fmt.Printf("找到了，下标为%v \n", middle)
}
} 
func main() {
arr := [6]int{1,8,10, 89, 1000, 1234}
//测试一把
BinaryFind(&arr, 0, len(arr) - 1,1000)
}
```

```cmd
E:\goproject\src\gocode\gw\project08\damo03>go run main.go
找到了，下标为4
```

## 8.6二维i数组的介绍

多维数组我们只介绍二维数组

## 8.7二维数组的应用场景

比如我们开发了一个五子棋游戏，棋盘就是需要二维数组表示。

![image-20231115164449186](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115164449186.png?raw=true)

## 8.8二维数组快速入门

快速入门案例：

- 请用二维数组输出如下图形

  0 0 0 0 0 0 

  0 0 1 0 0 0

   0 2 0 3 0 0

   0 0 0 0 0 0

```go
package main
import "fmt"
func main() {
//二维数组的演示案例
/* 
0 0 0 0 0 0 

0 0 1 0 0 0

0 2 0 0 0 0

0 0 3 0 0 0 
 */
 //定义 / 声明二维数组
 var arr [4][6]int
 //赋初始值
 arr[1][2] = 1
 arr[2][1] = 2
 arr[3][2] = 3
	//遍历二维数组，按照要求输出图形
	for i :=0;i <4;i++{
		for j :=0;j <6;j++{
			fmt.Print(arr[i][j], " ")
        }
		fmt.Println()
		}
}
```

```cmd
E:\goproject\src\gocode\gw\project08\damo04>go run main.go
0 0 0 0 0 0
0 0 1 0 0 0
0 2 0 0 0 0
0 0 3 0 0 0
```

## 8.9使用方式1：先声明/定义，再赋值

- 语法：var 数组名 [大小] [大小] 类型

- 比如：var arr [2] [3] int ,再赋值

- 使用演示

- 二维数组再内存的存在形式(重点)

  ![image-20231115170032551](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115170032551.png?raw=true)

## 8.10使用方式2：直接初始化

- 声明：var 数组名 [大小] [大小] 类型 = [大小] [大小]类型{{初值},{初值}}

- 赋值(有默认值，比如 int 类型的就是0)

- 使用演示

  ```cmd
  package main
  import "fmt"
  func main() {
  fmt.Println()
  var arr3 [2][3]int = [2][3]int{{1,2,3},{4,5,6}}
  fmt.Println("arr3=",arr3)
  }
  ```

  ```cmd
  E:\goproject\src\gocode\gw\project08\damo05>go run main.go
  
  arr3= [[1 2 3] [4 5 6]]
  ```

- 说明：二维数组在声明/定义时也对应有四种写法[和一维数组类似]

  - var 数组名 [大小][大小]类型 = [大小][大小]类型{{初值..},{初值..}}
  - var 数组名 [大小][大小]类型 = [...][大小]类型{{初值..},{初值..}}
  - var 数组名 = [大小][大小]类型{{初值..},{初值..}}

## 8.11二维数组的遍历

- 双层for循环完成遍历
- for-range方式完成遍历

案例演示：

```go
package main
import "fmt"
func main() {
var arr3 = [2][3]int{{1,2,3},{4,5,6}}
//for循环来遍历
for i := 0 ;i < len(arr3);i++ {
	for j := 0; j < len(arr3[i]); j++ {
	fmt.Println(arr3[i][j])
			}
		}
	fmt.Println("---------------------------------")
//for-range来遍历二维数组
for i ,v := range arr3 {
	for j,v2 := range v {
		fmt.Printf("arr3[%v][%v]=%v\t",i,j,v2)
        }
		fmt.Println("  ")
}
}
```

```cmd
E:\goproject\src\gocode\gw\project08\damo06>go run main.go
1
2
3
4
5
6
---------------------------------
arr3[0][0]=1    arr3[0][1]=2    arr3[0][2]=3
arr3[1][0]=4    arr3[1][1]=5    arr3[1][2]=6
```

## 8.12二维数组的应用案例

- 要求如下：

  - 定义二维数组，用于保存三个班，每个班五名学生成绩，
  - 并求出每个班级平均分，以及所有班级平均分

- 代码：

  ```go
  package main
  
  import "fmt"
  
  func main() {
  	// 定义二维数组，用于保存三个班，每个班无名同学成绩。
  	// 并求出每个班级平均分，以及所有班级平均分。
  
  	// 1.定义一个二维数组
  	var scores [3][5]float64
  	// 2.循环的输入成绩
  	for i := 0; i < len(scores); i++ {
  		for j := 0; j < len(scores[i]); j++ {
  			fmt.Printf("请输入第%d班的第%d个学生的成绩\n", i+1, j+1)
  			fmt.Scanln(&scores[i][j])  // 修改这一行
  		}
  	}
  
  	// 3.遍历出成绩后的二维数组，统计平均分
  	totalSum := 0.0 // 定义一个变量，用于累计所有班级的总分
  
  	for i := 0; i < len(scores); i++ {
  		sum := 0.0
  		for j := 0; j < len(scores[i]); j++ {
  			sum += scores[i][j]
  		}
  		totalSum += sum
  		fmt.Printf("第%d班级的总分为%v,平均分为%v\n", i+1, sum, sum/float64(len(scores[i])))
  	}
  
  	fmt.Printf("所有班级总分%v,所有班级平均分%v\n", totalSum, totalSum/float64(len(scores)))
  }
  
  ```

  ```cmd
  E:\goproject\src\gocode\gw\project08\damo07>go run main.go
  请输入第1班的第1个学生的成绩
  10
  请输入第1班的第2个学生的成绩
  10
  请输入第1班的第3个学生的成绩
  10
  请输入第1班的第4个学生的成绩
  10
  请输入第1班的第5个学生的成绩
  10
  请输入第2班的第1个学生的成绩
  10
  请输入第2班的第2个学生的成绩
  10
  请输入第2班的第3个学生的成绩
  10
  请输入第2班的第4个学生的成绩
  10
  请输入第2班的第5个学生的成绩
  10
  请输入第3班的第1个学生的成绩
  10
  请输入第3班的第2个学生的成绩
  10
  请输入第3班的第3个学生的成绩
  10
  请输入第3班的第4个学生的成绩
  10
  请输入第3班的第5个学生的成绩
  10
  第1班级的总分为50,平均分为10
  第2班级的总分为50,平均分为10
  第3班级的总分为50,平均分为10
  所有班级总分150,所有班级平均分50
  ```

# 第九章map

## 9.1 map的基本介绍

map是key-value数据结构，又称为字段或者关联数组。类似其他编程语言的集合，在编程中是经常使用到

## 9.2map的声明

### 9.2.1基本语法

var map 变量名 map[keytype] valuetype

- key 可以是什么类型
  - golang中的map，的key可以是很多种类型，比如bool、数字、string、指针、channel，还可以是只包含前面几个类型的接口，结构体、数组
  - **通常key为int，string**
  - 注意：slice，map还有function不可以，因为这几个没法用 ==来判断
- valuetype 可以是什么类型
  - valuetype的类型和key基本一样
  - 通常为：数字(整数，浮点数),string,map,struct

### 9.2.2map声明的举例

- map声明的举例
  - var a map[string]string
  - var a map[string]int
  - var a map[int]string
  - var a map[string]map[string]string
  - 注意：声明是不会分配内存的，初始化需要make，分配内存后才能赋值和使用。

案例演示：

```go
package main
import "fmt"
func main() {
//map的声明和注意事项
var a map[string]string
//在使用map前，需要先make，make的作用就是给map分配数据空间
a = make(map[string]string,10)
a["no1"] = "宋江"
a["no2"] = "吴用"
a["no3"] = "卢俊义"
a["no4"] = "武松"
a["no4"] = "公孙胜"
fmt.Println(a)
}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo08>go run main.go
map[no1:宋江 no2:吴用 no3:卢俊义 no4:公孙胜]
```

- 对上面代码的说明
  - map在使用前一定要make
  - map的key是不能重复，如果重复了，则以最后这个key-value为准
  - map的value是可以相同的
  - map的key-value是无序
  - make内置函数数目

![image-20231115212739774](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115212739774.png?raw=true)

## 9.3map的使用

- 方式1

![image-20231115214401091](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115214401091.png?raw=true)

- 方式2

![image-20231115214456840](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115214456840.png?raw=true)

- 方式3

  ![image-20231115214921279](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115214921279.png?raw=true)

```go
package main
import "fmt"
func main() {
//map的声明和注意事项
a := map[string]string{
"no1": "宋江",
"no2": "吴用",
"no3": "卢俊义",
"no4": "武松",
// "no4": "公孙胜",报错不能重复key
}
a["no4"] = "公孙胜"
fmt.Println(a)
}	
```

- map使用的课堂案例
  - 课堂练习：演示一个key-value的value是map的案例
  - 比如：我们要存放3个学生信息，每个学生又name和sex信息
  - 思路：map[string]map[string]string

代码：

```go
package main
import "fmt"
func main() {
//案例
studentMap := make(map[string]map[string]string)
studentMap["stu01"] = make(map[string]string,3)
studentMap["stu01"]["name"] = "张三"
studentMap["stu01"]["age"] = "20"
studentMap["stu01"]["sex"] = "男"
studentMap["stu01"]["address"] = "北京长安街"

studentMap["stu02"] = make(map[string]string,1)//map初始容量1，值为4个则自动扩容
studentMap["stu02"]["name"] = "李四"
studentMap["stu02"]["age"] = "21"
studentMap["stu02"]["sex"] = "女"
studentMap["stu02"]["address"] = "北京长安街"

fmt.Println(studentMap)
fmt.Println()
fmt.Println(studentMap["stu01"])
fmt.Println(studentMap["stu02"])
}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo09>go run main.go
map[stu01:map[address:北京长安街 age:20 name:张三 sex:男] stu02:map[address: 北京长安街 age:21 name:李四 sex:女]]

map[address:北京长安街 age:20 name:张三 sex:男]
map[address:北京长安街 age:21 name:李四 sex:女]
```

## 9.4map的增删改查操作

### map增加和更新：

- map["key"] = value//如果key还没有，就是增加，如果key存在就是修改。

### map删除：

- 说明：

- delete(map,"key"),delete是一个内置函数，如果key存在，就是删除该key-value，如果key不存在，不操作，但是也不会报错

  ![image-20231115225715391](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115225715391.png?raw=true)

案例演示：

![image-20231115230656599](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115230656599.png?raw=true)

```go
package main
import "fmt"
func main() {
//案例
studentMap := make(map[string]map[string]string)
studentMap["stu01"] = make(map[string]string,3)
studentMap["stu01"]["name"] = "张三"
studentMap["stu01"]["age"] = "20"
studentMap["stu01"]["sex"] = "男"
studentMap["stu01"]["address"] = "北京长安街"

delete(studentMap["stu01"],"age")

studentMap["stu02"] = make(map[string]string,1)//map初始容量1，值为4个则自动扩容
studentMap["stu02"]["name"] = "李四"
studentMap["stu02"]["age"] = "21"
studentMap["stu02"]["sex"] = "女"
studentMap["stu02"]["address"] = "北京长安街"

delete(studentMap["stu02"],"age")

fmt.Println(studentMap)
fmt.Println()
fmt.Println(studentMap["stu01"])
fmt.Println(studentMap["stu02"])
}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo09>go run main.go
map[stu01:map[address:北京长安街 name:张三 sex:男] stu02:map[address:北京长安街 name:李四 sex:女]]

map[address:北京长安街 name:张三 sex:男]
map[address:北京长安街 name:李四 sex:女]
```

- 细节说明
  - 如果我们要删除map的所有key，没有一个专门的方法一次删除，可以遍历一个key，逐个删除或者 map=make(...) make一个新 的，让原来的称为垃圾，给gc回收

```go
//如果希望一次性删除所有的key
//1.扁你所有的key，如何逐一删除[遍历]
//2.直接make一个新空间
studentMap = make(map[string]map[string]string)
fmt.Println(studentMap)
```

```cmd
map[]
```

### map查找

- 案例演示：

  - ```go
    package main
    import "fmt"
    func main() {
    //案例
    studentMap := make(map[string]map[string]string)
    studentMap["stu01"] = make(map[string]string,3)
    studentMap["stu01"]["name"] = "张三"
    studentMap["stu01"]["age"] = "20"
    studentMap["stu01"]["sex"] = "男"
    studentMap["stu01"]["address"] = "北京长安街"
    
    delete(studentMap["stu01"],"age")
    
    studentMap["stu02"] = make(map[string]string,1)//map初始容量1，值为4个则自动扩容
    studentMap["stu02"]["name"] = "李四"
    studentMap["stu02"]["age"] = "21"
    studentMap["stu02"]["sex"] = "女"
    studentMap["stu02"]["address"] = "北京长安街"
    
    delete(studentMap["stu02"],"age")
    
    fmt.Println(studentMap)
    fmt.Println()
    fmt.Println(studentMap["stu01"])
    fmt.Println(studentMap["stu02"])
    
    // //如果希望一次性删除所有的key
    // //1.扁你所有的key，如何逐一删除[遍历]
    // //2.直接make一个新空间
    // studentMap = make(map[string]map[string]string)
    // fmt.Println(studentMap)
    
    //演示map的查找
    val , ok := studentMap["stu01"]
    if ok {
    	fmt.Printf("stu01的值是%v\n",val)
    	}else {
    		fmt.Printf("stu01的值不存在\n")
    	}
    }	
    ```

    ```cmd
    E:\goproject\src\gocode\gw\project08\damo09>go run main.go
    map[stu01:map[address:北京长安街 name:张三 sex:男] stu02:map[address:北京长安街 name:李四 sex:女]]
    
    map[address:北京长安街 name:张三 sex:男]
    map[address:北京长安街 name:李四 sex:女]
    stu01的值是map[address:北京长安街 name:张三 sex:男]
    ```

    说明：如果 studentMap 这个 map 中存在 "stu01" ， 那么 findRes 就会返回 true,否则返回 false

- 9.5map遍历：

  - 案例演示相对复杂的map遍历，该map的value又是一个map

  - 说明：map的遍历使用for-range的结构遍历

  - ```go
    package main
    import "fmt"
    func main() {
    //案例
    studentMap := make(map[string]map[string]string)
    studentMap["stu01"] = make(map[string]string,3)
    studentMap["stu01"]["name"] = "张三"
    studentMap["stu01"]["age"] = "20"
    studentMap["stu01"]["sex"] = "男"
    studentMap["stu01"]["address"] = "北京长安街"
    
    for k ,v := range studentMap {
    	fmt.Printf("k=%v\n",k)
    	for k2,v2 := range v {
    		fmt.Printf("k2=%v,v2=%v\n",k2,v2)
    		}
    		fmt.Println()
    }	
    }
    ```

    ```cmd
    E:\goproject\src\gocode\gw\project08\damo09>go run main.go
    k=stu01
    k2=name,v2=张三
    k2=age,v2=20
    k2=sex,v2=男
    k2=address,v2=北京长安街
    ```

### map的长度

![image-20231115232056428](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231115232056428.png?raw=true)

## 9.6map切片

### 9.6.1基本介绍

切片的数据类型如果是 map，则我们称为 slice of map，map 切片，这样使用则 map 个数就可以动 态变化了。

### 9.6.2案例演示

要求：使用一个 map 来记录 monster 的信息 name 和 age, 也就是说一个 monster 对应一个 map,并 且妖怪的个数可以动态的增加=>map 切片

```go
package main
import "fmt"
func main() {
//演示map切片的使用
// 要求：使用一个 map 来记录 monster 的信息 name 和 age, 也就是说一个 
// monster 对应一个 map,并 且妖怪的个数可以动态的增加=>map 切片

//1. 声明一个map切片
var monsters []map[string]string
//2. 初始化
monsters = make([]map[string]string, 2)
//3. 增加第一个妖怪信息
if monsters[0] == nil {
	monsters[0] = make(map[string]string,2)
	monsters[0]["name"] = "牛魔王"
	monsters[0]["age"] = "1000"
}

if monsters[1] == nil {
	monsters[1] = make(map[string]string,2)
	monsters[1]["name"] = "红孩儿"
	monsters[1]["age"] = "100"
}
//写法越界
// if monsters[2] == nil {
// 	monsters[2] = make(map[string]string,2)
// 	monsters[2]["name"] = "狐狸精"
// 	monsters[2]["age"] = "300"
// }
newMonster := map[string]string{
	"name": "黑熊精",
	"age": "10000",
}
monsters = append(monsters, newMonster)
fmt.Println(monsters)
}
```

```cmd
E:\goproject\src\gocode\gw\project08\damo10>go run main.go
[map[age:1000 name:牛魔王] map[age:100 name:红孩儿] map[age:10000 name:黑熊 精]]
```

## 9.7map排序

### 9.7.1基本介绍

1. golang中没有一个专门的方法针对map的key进行排序
2. golang中的map默认是无序的，注意也不是按照添加的顺序存放的，你每次遍历，得到的输出可以能不一样
3. golang中map的排序，是先将key进行排序，然后根据key值遍历输出即可

### 9.7.2案例演示

```go
package main
import (
	"fmt"
	"sort"
)
func main() {
//map的排序
map1 := make(map[int]int,10)
map1[10] = 100
map1[1] = 13
map1[2] = 56
map1[4] = 90
map1[8] = 90
fmt.Println(map1)
//如果按照map的key的顺序进行排序输出
//1.先将map的key放入到切片中
//2.对切片排序
//3.遍历切片，然后按照key来输出map的值
var keys []int
for k ,_ := range map1 {
	keys = append(keys,k)
	}
	sort.Ints(keys)
	fmt.Println(keys)
	for s,v := range keys {
		fmt.Printf("map[%v]=%v\n",s,map1[v])
	}
}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo11>go run main.go
map[1:13 2:56 4:90 8:90 10:100]
[1 2 4 8 10]
map[1]=13
map[2]=56
map[4]=90
map[8]=90
map[10]=100
```

## 9.8map使用细节

1. map是引用类型，遵守引用类型传递的机制，在一个函数接收map，修改后，会直接修改原来的map【案例演示】

```go
package main
import "fmt"
func modify(map1 map[int]int){
	map1[10] = 9000
}
func main() {
	//map是引用类型，遵守引用类型传递的机制，在一个函数接收map。
	//修改后，会直接修改原来的map
	map1 := make(map[int]int)
	map1[1] = 100
	map1[2] = 99
	map1[10] = 1
	map1[20] = 2
	modify(map1)
	//看看结果，map1[10] = 900,说明map是引用类型
	fmt.Println(map1)
}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo12>go run main.go
map[1:100 2:99 10:9000 20:2]
```

2. map 的容量达到后，再想 map 增加元素，会自动扩容，并不会发生 panic，也就是说 map 能动 态的增长 键值对(key-value)
3. map 的 value 也经常使用 struct 类型，更适合管理复杂的数据(比前面 value 是一个 map更好比如 value 为 Student 结构体 【案例演示，因为还没有学结构体，体验一下即可】

```go
package main
import "fmt"
type Stu struct {
	Name string
	Age int
	Address string
}
func main() {
//map的value 也经常使用struct类型，
//更适合管理复杂的数据(比前面value是一个map更好)
//比如value为Student结构体
//1.map的key为学生的学号，是唯一的
//2.map的value为结构体，包含学生的 名称，年龄，地址
students := make(map[string]Stu,10)
//创建2个学生
stu1 := Stu{"张三", 20, "北京"}
stu2 := Stu{"李四", 22, "上海"}
students["no1"] = stu1
students["no2"] = stu2
fmt.Println(students)
//遍历各个学生信息
for k,v := range students {
	fmt.Printf("学生的编号是%v \n",k)
	fmt.Printf("学生的名字是%v \n",v.Name)
	fmt.Printf("学生的年龄是%v \n",v.Age)
	fmt.Printf("学生的地址是%v \n",v.Address)
	fmt.Println()
}	
}
```

```go
E:\goproject\src\gocode\gw\project08\damo13>go run main.go
map[no1:{张三 20 北京} no2:{李四 22 上海}]
学生的编号是no1
学生的名字是张三
学生的年龄是20
学生的地址是北京

学生的编号是no2
学生的名字是李四
学生的年龄是22
学生的地址是上海
```

## 9.9map课堂练习题

- 课堂练习：
  - 使用map[string]map[string]string的map配型
  - key：表示用户名，是唯一的，不可用重复
  - key：表示用户名，就将其密码修改”888888“，如果不存在就增加这个用户信息，(包括昵称 nickname和密码pwd)。
  - 编写一个函数 modifyUser()

```go
package main
import "fmt"
/*
1)使用 map[string]map[string]sting 的 map 类型
2)key: 表示用户名，是唯一的，不可以重复
3)如果某个用户名存在，就将其密码修改"888888"，如果不存在就增加这个用户信息, （包括昵称 nickname 和 密码 pwd）。
4)编写一个函数 modifyUser(users map[string]map[string]sting, name string) 完成上述功能
*/
func modifyUser(users map[string]map[string]string, name string){
	//判断users中是否有name
	//v,ok :=user[name]
	if users[name] != nil{
		//有这个用户
		users[name]["pwd"] = "888888"
	}else {
		//没有这个用户
		users[name] = make(map[string]string)
		users[name]["pwd"] = "888888"
		users[name]["nickname"] = "匿名"+ name//示意
	}
}
func main() {
	users := make(map[string]map[string]string)
	users["smith"] = make(map[string]string,2)
	users["smith"]["pwd"] = "999999"
	users["smith"]["nickname"] = "小花猫"

	modifyUser(users,"小花猫")
	modifyUser(users,"mary")
	modifyUser(users,"smith")
	fmt.Println(users)

}	
```

```cmd
E:\goproject\src\gocode\gw\project08\damo14>go run main.go
map[mary:map[nickname:匿名mary pwd:888888] smith:map[nickname:小花猫 pwd:888888] 小花猫:map[nickname:匿名小花猫 pwd:888888]]
```

# 第10章面向对象编程(上)

## 10.1结构体

### 10.1.1看一个问题

![image-20231116111307228](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116111307228.png?raw=true)

### 10.1.2使用现有技术解决

1. 单独的定义变量解决

- 代码演示：

  ![image-20231116111449515](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116111449515.png?raw=true)

2. 使用数组解决

- 代码演示：

  ![image-20231116111523079](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116111523079.png?raw=true)

### 10.1.3现有技术解决的缺点分析

1. 使用变量或者数组来解决养猫的问题，不利于数据的管理和维护。因为名字，年龄，颜色都是属于一只猫，但是这里是分开保存。
2. 如果我们希望对一只猫的属性(名字、年龄、颜色)进行操作(绑定方法),也不好处理
3. 引出我们要讲解的结束-》结构体。

### 10.1.14一个程序就是一个世界，有很多对象(变量)

![image-20231116111824597](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116111824597.png?raw=true)

### 10.1.5Golang语言面向对象编程说明

1. Golang也支持面向对象编程(OOP),但是和传统的面向对象编程有区别，并不是纯粹的面向对 象语言。所以我们说 Golang 支持面向对象编程特性是比较准确的。
2. Golang没有类(class)，Go语言结构体(struct)和其他编程语言的类(class)有同等的地位，你可以理解Golang是基于struct来实现OOP特性的。
3. Golang面向对象编程非常简洁，去掉了传统OOP语言的继承、方法重载、构造函数和析构函 数、隐藏的 this 指针等等
4. Golang仍然与面向对象编程的继承，封装和多态的特性，只是实现的方式和其它 OOP 语言不 一样，比如继承 ：Golang 没有 extends 关键字，继承是通过匿名字段来实现。
5. Golang 面向对象(OOP)很优雅，OOP 本身就是语言类型系统(type system)的一部分，通过接口 (interface)关联，耦合性低，也非常灵活。后面同学们会充分体会到这个特点。也就是说在 Golang 中面 向接口编程是非常重要的特性。

### 10.1.6结构体与结构体变量(实例/对象)的关系示意图

![image-20231116141520596](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116141520596.png?raw=true)

- 对上图的说明

  - 将一类事物的特性提取出来(比如猫类),形成一个新的数据类型,就是一个结构体。
  - 通过这个结构体，我们可以创建多个变量(实例/对象)
  - 事物可以以猫类，也可以是Person，Fish或是某个工具类。。。

  ![image-20231116141717317](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116141717317.png?raw=true)

### 10.1.7快速入门-面向对象的方式(struct)解决养猫问题

- 代码演示：

  ![image-20231116142612783](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116142612783.png?raw=true)

  ### 10.1.8结构体和结构体变量(实例)的区别和联系

  通过上面的案例和讲解我们可以看出:

  1. 结构体是自定义的数据类型，代表一类事物。
  2. 结构体变量(实例)是具体，实际的，代表一个具体变量

  ### 10.1.9 结构体变量(实例)在内存的布局(重要!)

  ![image-20231116142858901](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116142858901.png?raw=true)

  ### 10.1.10如何声明结构体

- 基本语法

  - type 结构体名称struct {

    ​	field1 type

    ​	field2 type

    }

- 举例:
  - type Student struct {
    Name string //字段
    Age int //字段
    Score float32
    }

### 字段/属性

- 基本介绍

  1. 从概念或叫法上看： 结构体字段 = 属性 = field （即授课中，统一叫字段)

  2. 字段是结构体的一个组成部分，一般是基本数据类型、数组,也可是引用类型。比如我们前面定 义猫结构体 的 Name string 就是属性

- 注意事项和细节说明

  1. 字段声明语法同变量，示例：字段名 字段类型

  2. 字段的类型可以为：基本类型、数组或引用类型

  3. 在创建一个结构体变量后，如果没有给字段赋值，都对应一个零值(默认值)，规则同前面讲的 一样:

     布尔类型是false，数值是0，字符串是""。

     数组类型的默认值和他的元素类型相关，比如score[3]int则为[0,0,0]

     [指针，slice，和 map 的零值都是 nil ，即还没有分配空间]()

案例演示:

```go
package main

import "fmt"
//定义一个cat结构体，将cat各个字段/属性信息，放入到Cat结构体进行管理

//如果结构体的字段类型是:指针，slice，和map的零值都是nil，即还没有分配空间
//如果需要使用这样的字段，需要先make，才能使用。
type Person struct{
	Nmae string
	Age int
	scores [5]float64 
	ptr *int //指针
	slice []int //切片
	map1 map[string]string//map
}

func main() {
	//定义结构体变量
		var p1 Person
		fmt.Println(p1)
		
		if p1.ptr == nil {
			fmt.Println("ok1")
		}
		
		if p1.slice == nil {
			fmt.Println("ok2")
		}

		if p1.map1 == nil {
			fmt.Println("ok3")
		}

		//使用slice，再次说明，一定要make
		p1.slice = make([]int, 5)
		p1.slice[0] = 100 //ok

		//使用map，一定要先make
		p1.map1 = make(map[string]string)
		p1.map1["name"] = "tom"
		p1.map1["age"] = "18"
		fmt.Println(p1)

	}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo01>go run main.go
{ 0 [0 0 0 0 0] <nil> [] map[]}
ok1
ok2
ok3
{ 0 [0 0 0 0 0] <nil> [100 0 0 0 0] map[age:18 name:tom]}
```

4. 不同结构体变量的字段是独立，互不影响，一个结构体变量字段的更改，不影响另外一个, 结构体 是值类型。

![image-20231116150525681](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116150525681.png?raw=true)

![image-20231116150542943](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116150542943.png?raw=true)

### 10.1.12创建结构体变量和访问结构体字段

- 方式1-直接声明
  - 案例演示：var person Person
- 方式2-{ }
  - 案例演示：var person Person = Person{ }![image-20231116152053615](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116152053615.png?raw=true)

- 方式3-&

  - 案例: var person *Person = new (Person)

    ![image-20231116152131454](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116152131454.png?raw=true)

- 方式4-{ }

  - 案例：var person *Person = &Person { }

    ![image-20231116153350720](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116153350720.png?raw=true)

```go
package main

import "fmt"
//定义一个cat结构体，将cat各个字段/属性信息，放入到Cat结构体进行管理

//如果结构体的字段类型是:指针，slice，和map的零值都是nil，即还没有分配空间
//如果需要使用这样的字段，需要先make，才能使用。
type Person struct{
	Name string
	Age int

}

func main() {
	//方式2
	p2 := Person{"mary",20}
	fmt.Println(p2)
	//方式3-&
	//案例: var person *Person = new (Person)
	var p3 *Person = new(Person)
	(*p3).Name = "smith"
	p3.Name = "tom"

	(*p3).Age = 30
	p3.Age = 100
	fmt.Println(*p3)
	
	//方式4-{ }
	//案例： var person *Person = &Person{}
	//下面的语句，也可以直接给字符赋值
	//var person *Person = &Person{"mary",60}
	var person *Person = &Person{}
	//因为person是一个指针，因此标准的访问字段的方法
	//（*person).Name = "scott"
	//go的设计为了程序员使用方便，也可以person.name = "scott"
	//原因和上面一样，底层会对person.Name= "scoot"进行处理会加上(*person)
	(*person).Name = "scott"
	person.Name = "~~scoot"

	(*person).Age = 30
	person.Age = 100
	fmt.Println(*person)
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo02>go run main.go
{mary 20}
{tom 100}
{~~scoot 100}
```

- 说明：
  - 第三种和第4种方式返回的是 **结构体指针**。
  - 结构体指针访问字段的标准方式应该是：(*结构体指针).字段名 ，比如 (*person).Name = "tom"
  - 但 go 做了一个简化，也支持 结构体指针.字段名, 比如 person.Name = "tom"。更加符合程序员 使用的习惯，go 编译器底层 对 person.Name 做了转化 (*person).Name。

### 10.1.13 struct类型的内存分配机制

- 看一个思考题

  - 我们定义一个Person结构体(包括 名字,年龄)。

    ![image-20231116153735217](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116153735217.png?raw=true)

输出的结构体是：p2.Name = tom p1.Name= 小明

- 基本说明
  - ![image-20231116153928196](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116153928196.png?raw=true)

- 结构体在内存种示意图
  - ![image-20231116154001218](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116154001218.png?raw=true)

- 代码演示：

  ```go
  package main
  
  import "fmt"
  //定义一个cat结构体，将cat各个字段/属性信息，放入到Cat结构体进行管理
  
  //如果结构体的字段类型是:指针，slice，和map的零值都是nil，即还没有分配空间
  //如果需要使用这样的字段，需要先make，才能使用。
  type Person struct{
  	Name string
  	Age int
  
  }
  
  func main() {
  	var p1 Person
  	p1.Age=10
  	p1.Name= "小明"
  	/* p2 被赋值为 &p1，表示 p2 指向了 p1 的内存地址。
  	因此，通过 p2 可以访问和修改 p1 的字段值，因为 p2 
  	指向了 p1 的存储位置。这样的操作使得你可以通过指针
  	间接地操作结构体的字段。 */
  	
  	var p2 *Person = &p1 //这里是关键-->画出示意图
  	
  	fmt.Println((*p2).Age)
  	fmt.Println(p2.Age)
  	p2.Name = "tom"
  	fmt.Printf("p2.Name = %v p1.Name%v\n",p2.Name,p1.Name)
  	fmt.Printf("p2.Name = %v p1.Name%v\n",(*p2).Name,p1.Name)
  
  	fmt.Printf("p1的地址%p\n",&p1)
  	fmt.Printf("p2的地址本身%p p2值的地址%p\n",&p2,p2)
  }
  ```

  输出的结构是：

  ```cmd
  E:\goproject\src\gocode\gw\project010\damo03>go run main.go
  10
  10
  p2.Name = tom p1.Nametom
  p2.Name = tom p1.Nametom
  p1的地址0xc000008078
  p2的地址本身0xc00000a028 p2值的地址0xc000008078
  ```

  ![image-20231116165202267](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116165202267.png?raw=true)

### 10.1.14结构体使用注意事项和细节

1. 结构体的所有字段在内存种是连续的

```go
package main
import "fmt"
//结构体
type Point struct {
	x int
	y int
}
//结构体
type Rect struct {
	leftup,rightDown Point
}
//结构体
type Rect2 struct {
	leftup,rightDown *Point
}
func main() {
	r1 := Rect {Point{1,2},Point{3,4}}
	//r1有四个int，在内存中是连续分布
	//打印地址
	fmt.Printf("r1.leftup.x地址=%p\nr1.leftup.y 地址=%p\nr1.rightDown.x 地址=%p\nr1.rightDown.y 地址=%p\n",
&r1.leftup.x,&r1.leftup.y,&r1.rightDown.x,&r1.rightDown.y)
	fmt.Println("")

	r2 := Rect2 {&Point{20,30},&Point{40,50}}
	fmt.Printf("r1.leftup.x地址=%p\nr1.leftup.y 地址=%p\n",
&r2.leftup.x,&r2.leftup.y)
	fmt.Printf("r1.leftup.x地址=%p\nr1.leftup.y 地址=%p\n",
&r2.rightDown.x,&r2.rightDown.y)
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo04>go run main.go
r1.leftup.x地址=0xc0000161a0
r1.leftup.y 地址=0xc0000161a8
r1.rightDown.x 地址=0xc0000161b0
r1.rightDown.y 地址=0xc0000161b8

r1.leftup.x地址=0xc00000e0f0
r1.leftup.y 地址=0xc00000e0f8
r1.leftup.x地址=0xc00000e100
r1.leftup.y 地址=0xc00000e108
```

![image-20231116220600092](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116220600092.png?raw=true)

2. 结构体是用户单独定义的类型，和其它类型进行转换时需要有完全相同的字段(名字、个数和类 型)

```go
package main
import "fmt"
type A struct {
	Num int
}
type B struct {
	Num int 
}

func main() {
	var a A 
	var b B
	a = A(b)
	fmt.Println(a,b)
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo05>go run main.go
{0} {0}
```

3. 结构体进行 type 重新定义(相当于取别名)，Golang 认为是新的数据类型，但是相互间可以强转

![image-20231116220840672](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116220840672.png?raw=true)

4. struct 的每个字段上，可以写上一个 tag, 该 tag 可以通过反射机制获取，常见的使用场景就是序 列化和反序列化。

- 序列化使用场景

  - ![image-20231116220929971](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116220929971.png?raw=true)

  - 举例

    

```go
package main
import (
	"fmt"
	"encoding/json"
)
type Monster struct {
	Name string 
	Age int
	Skill string
}

func main() {
	//创建一个monster变量
	Monster := Monster{"小怪兽", 10, "打怪"}
	//2.将Monster变量序列化json格式字串
	//json Marshl 函数中使用反射，这个讲解反射，我们会详细介绍
	jsonStr,err := json.Marshal(Monster)
	if err != nil {
		fmt.Println("序列化失败",err)
	}
	fmt.Println("jsonStr",string(jsonStr))
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo05>go run main.go
jsonStr {"Name":"小怪兽","Age":10,"Skill":"打怪"}
```

## 10.2方法

### 10.2.1基本介绍

- **在某些情况下，我们要需要声明(定义)方法。比如 Person 结构体:除了有一些字段外( 年龄，性别...)Person 结构体还有一些行为比如:可以说话、跑步..,通过学习，还可以做算术题。这时就要用方法 才能完成。**
- **Golang 中的方法是作用在指定的数据类型上的(即：和指定的数据类型绑定)，因此自定义类型， 都可以有方法，而不仅仅是 struc**

### 10.2.2 方法的声明和调用

**type A struct {**
**Num int**
**}**
**func (a A) test() {**
**fmt.Println(a.Num)**
**}**

- 对上面的语法说明
  1. func ( a A) test () {} 表示A结构体有一方法，方法名为test
  2. (a A) 体现test方法是和A类型绑定的
- 举例说明

```go
package main
import "fmt"

type Person struct {
	Name string
}
//给Person类型绑定一方法
func (p Person) test(){
	fmt.Println("test()name=",p.Name)
}
func main() {
var p Person
p.Name = "zhangsan"
p.test()//调用方法
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo06>go run main.go
test()name= zhangsan
```

- 对上面的总结

  1. test方法和Person类型绑定

  2. test方法法只能通过 Person 类型的变量来调用，而不能直接调用，也不能使用其它类型变量来调 用

     ![image-20231116222804609](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116222804609.png?raw=true)

  3. func (p Person) test() {}... p 表示哪个 Person 变量调用，这个 p 就是它的副本, 这点和函数传参非 常相似。

  4. p 这个名字，有程序员指定，不是固定, 比如修改成 person 也是可以

     ![image-20231116223047594](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116223047594.png?raw=true)

### 10.2.3方法快速入门

1. 给Person结构体添加speak方法，输入 xxx是一个好人

![image-20231116223201197](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116223201197.png?raw=true)

2. 给Person结构体添加jisuan方法，可以计算从1+..+1000的结果，说明方法体内可以函数一样，进行各种运算

![image-20231116223449251](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116223449251.png?raw=true)

3. 给 Person 结构体 jisuan2 方法,该方法可以接收一个数 n，计算从 1+..+n 的结

![image-20231116225817917](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116225817917.png?raw=true)

4.  给 Person 结构体添加 getSum 方法,可以计算两个数的和，并返回结果

![image-20231116225835722](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116225835722.png?raw=true)

5. 方法调用

![image-20231116225848177](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116225848177.png?raw=true)

```go
package main
import "fmt"

type Person struct {
	Name string
}
//给Person类型绑定一方法
// func (p Person) test(){
// 	fmt.Println("test()name=",p.Name)
// }
func (p Person) speak(){
	fmt.Println(p.Name,"是一个goodman~")
}
func (p Person) jisuan() {
	res := 0
	for i := 1;i <= 1000; i++ {
		res += i
	}
	fmt.Println(p.Name,"计算结果是",res)
}
//给Person结构体jisuan2 方法，该方法可以接收一个参数n，计算从1+..+n的结果
func (p Person) jisuan2(n int) {
	res := 0
	for i := 1;i <= n; i++ {
		res += i
	}
	fmt.Println(p.Name,"计算结果是",res)
}
func (p Person) getSum(n1 int,n2 int) int {
	return n1 + n2
}
func main() {
	var p Person
p.speak()
p.jisuan()
p.jisuan2(20)
res := p.getSum(10,20)
fmt.Println(res)
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo07>go run main.go
 是一个goodman~
 计算结果是 500500
 计算结果是 210
30
```

### 10.2.4 方法的调用和传递机制原理:（重要!)

- 说明
  - 方法的调用和传参机制和函数基本一样，不一样的地方是方法调用时，会将调用方法的变量，当做 实参也传递给方法。下面我们举例说明。
- 案例1：
  - 画出前面 getSum 方法的执行过程+说明
  - ![image-20231116230018595](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116230018595.png?raw=true)

- 说明：
  1. 在通过一个变量去调用方法时，其调用机制和函数一样
  2. 不一样的地方时，变量调用方法时，该变量本身也会作为一个参数传递到方法(如果变量是值类 型，则进行值拷贝，如果变量是引用类型，则进行地质拷贝
- 案例2
  - 编写一个程序，如下要求
    1. 声明一个结构体 Circle, 字段为 radiu
    2. 声明一个方法 area 和 Circle 绑定，可以返回面积。
    3. 提示：画出 area 执行过程+说

```go
package main
import "fmt"
type Circle struct {
	redius float64
}
//2.声明一个方法area和Circle绑定，可以返回面积
func (c Circle) area() float64 {
	return 3.14 * c.redius * c.redius
}
func main() {
	var c Circle
	c.redius = 4.0
	res := c.area()
	fmt.Println("面积是=",res)
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo08>go run main.go
面积是= 50.24
```

![image-20231116231127335](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116231127335.png?raw=true)

### 10.2.5 方法的声明(定义)

func (recevier type) methodName (参数列表) (返回值列表){

​	方法体

​	 retrun  返回值

}

1. **参数列表：表示方法输入**
2. **recevier type : 表示这个方法和 type 这个类型进行绑定，或者说该方法作用于 type 类型**
3. **receiver type : type 可以是结构体，也可以其它的自定义类型**
4. **receiver : 就是 type 类型的一个变量(实例)，比如 ：Person 结构体 的一个变量(实例）**
5. **返回值列表：表示返回的值，可以多个**
6.  **方法主体：表示为了实现某一功能代码块**
7. **return 语句不是必须的**

### 10.2.6方法的注意事项和细节

1. **结构体类型是值类型，在方法调用中，遵守值类型的传递机制，是值拷贝传递方式**
2. **如程序员希望在方法中，修改结构体变量的值，可以通过结构体指针的方式来处理**![image-20231116232027398](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231116232027398.png?raw=true)

```go
package main
import "fmt"
type Circle struct {
	redius float64
}
//2.声明一个方法area和Circle绑定，可以返回面积
func (c Circle) area() float64 {
	return 3.14 * c.redius * c.redius
}
func (c *Circle) area2() float64 {
	return 3.14 * (*c).redius * (*c).redius
}
func main() {
	var c Circle
	c.redius = 4.0
	res := c.area()
	fmt.Println("面积是=",res)

	c.redius = 6.0
	res2 := (&c).area2()
	fmt.Println("面积是=",res2)
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo08>go run main.go
面积是= 50.24
面积是= 113.03999999999999
```

3. Golang 中的方法作用在指定的数据类型上的(即：和指定的数据类型绑定)，因此自定义类型， 都可以有方法，而不仅仅是 struct， 比如 int , float32 等都可以有方

```go
package main
import "fmt"

type integer int
func (i integer) print() {
	fmt.Println("i=",i)
}
//编写一个方法，可以改变i的值
func (i *integer) change() {
	*i = *i + 1
}
func main() {
	var i integer = 10
	i.print()
	i.change()
	fmt.Println("i=",i)
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo09>go run main.go
i= 10
i= 11
```

4. 方法的访问范围控制的规则，和函数一样。方法名首字母小写，只能在本包访问，方法首字母 大写，可以在本包和其它包访问。[讲解]
5. 如果一个类型实现了 String()这个方法，那么 fmt.Println 默认会调用这个变量的 String()进行输 出

### 10.2.7方法的课堂练习

1.  编写结构体(MethodUtils)，编程一个方法，方法不需要参数，在方法中打印一个 10*8 的矩形， 在 main 方法中调用该方法。

   ```go
   package main
   import (
   	"fmt"
   )
   type methodUtils struct {
   
   }
   func (mu methodUtils) Print() {
   	for i :=1 ;i <=10; i++{
   		for j :=1 ;j <= 8;j++{
   			fmt.Print("*")
   		}
   		fmt.Println()
   	}
   }
   func main() {
   var mu methodUtils
   mu.Print()
   }	
   ```

   ```cmd
   E:\goproject\src\gocode\gw\project010\damo11>go run main.go
   *****
   *****
   *****
   *****
   *****
   ```

2. 编写一个方法，提供m和n两个参数，方法中打印一个m*n的矩形

   ```go
   package main
   import (
   	"fmt"
   )
   type methodUtils struct {
   
   }
   func (mu methodUtils) Print(m int,n int) {
   	for i :=1 ;i <=m; i++{
   		for j :=1 ;j <= n;j++{
   			fmt.Print("*")
   		}
   		fmt.Println()
   	}
   }
   func main() {
   var mu methodUtils
   mu.Print(5,5)
   }	
   ```

   ```cmd
   E:\goproject\src\gocode\gw\project010\damo11>go run main.go
   *****
   *****
   *****
   *****
   *****
   ```

3. 编写一个方法算该矩形的面积(可以接收长 len，和宽 width)， 将其作为方法返回值。在 main 方法中调用该方法，接收返回的面积值并打印。

```go
package main
import (
	"fmt"
)
type methodUtils struct {

}
func (mu methodUtils) Print(len float64,width float64) float64{
	return len * width
		}
func main() {
var mu methodUtils
	a := mu.Print(2.3,8.7)
	fmt.Println("面积为=",a)
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo11>go run main.go
面积为= 20.009999999999998
```

4. 判断一个数是奇数还是偶数

```go
package main
import (
	"fmt"
)
type methodUtils struct {

}
func (mu methodUtils) JudgeNum(num int) {
	if num % 2 == 0 {
		fmt.Println(num,"是偶数")
	}else {
		fmt.Println(num,"是奇数")
	}
}
func main() {
var mu methodUtils
	mu.JudgeNum(5)

}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo11>go run main.go
5 是奇数
```

5. 根据行、列、字符打印 对应行数和列数的字符，比如：行：3，列：2，字符*,则打印相应的效 果

### 10.2.8方法的课后练习题

1. 在MethodUtils结构体编个方法，从键盘接收整数(1-9),打印对应乘法表:

![image-20231117153845293](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231117153845293.png?raw=true)

![image-20231117153858048](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231117153858048.png?raw=true)

### 10.2.9 方法和函数区别

1. 调用方式不一样

   函数的调用方式: 函数名(实参列表)

   方法的调用方式: 变量.方法名(实参列表)

2. 对于普通函数，接收者为值类型时，不能将指针类型的数据直接传递，反之亦然![image-20231117154357818](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231117154357818.png?raw=true)

![image-20231117154343102](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231117154343102.png?raw=true)

3. 对于方法（如 struct 的方法），接收者为值类型时，可以直接用指针类型的变量调用方法，反 过来同样也可以

```go
package main
import "fmt"
type Person struct {
	Name string
}
//函数
//对于pu
func test01(p Person){
	fmt.Println(p.Name)
}

func test02(p *Person){
	fmt.Println(p.Name)
}
//d对于方法
func (p Person) test03(){
	p.Name = "jack"
	fmt.Printf("test03(%v)",p.Name)//jack
}

func (p *Person) test04(){
	p.Name = "jack"
	fmt.Printf("test04(%v)",p.Name)//mary
}

func main() {
	p := Person{"tom"}
	test01(p)
	test02(&p)
fmt.Println()
	p.test03()
	fmt.Println("\nmain()p.name=",p.Name)
	(&p).test03()//从形式上是传入地址，但是本质仍然是值拷贝
	fmt.Println("\nmain()p.name=",p.Name)
fmt.Println()
	p.test04()
	fmt.Println("\nmain()p.name=",p.Name)
	(&p).test04()
	fmt.Println("\nmain()p.name=",p.Name)
	
}
```

```cmd
E:\goproject\src\gocode\gw\project010\damo13>go run main.go
tom
tom

test03(jack)
main()p.name= tom
test03(jack)
main()p.name= tom

test04(jack)
main()p.name= jack
test04(jack)
main()p.name= jack
```

总结：

1. 不管调用形式如何，真正决定是值拷贝还是地址拷贝，看这个方法是和哪个类型绑定.
2. 如果是和值类型，比如 (p Person) , 则是值拷贝， 如果和指针类型，比如是 (p *Person) 则 是地址拷贝。

## 10.3面向对象编程应用实例

### 10.3.1步骤

1. 声明(定义)结构体，确定结构体名
2. 编写结构体的字段
3. 编写结构体的方法

### 10.3.2学生案例：

1. 编写一个 Student 结构体，包含 name、gender、age、id、score 字段，分别为 string、string、int、 int、float64 类型。
2. 结构体中声明一个 say 方法，返回 string 类型，方法返回信息中包含所有字段值。
3. 在 main 方法中，创建 Student 结构体实例(变量)，并访问 say 方法，并将调用结果打印输出
4. 代码：

```go
package main
import "fmt"
/*
学生案例：
编写一个 Student 结构体，包含 name、gender、age、id、score 字段，分别为 string、string、int、int、
float64 类型。
结构体中声明一个 say 方法，返回 string 类型，方法返回信息中包含所有字段值。
在 main 方法中，创建 Student 结构体实例(变量)，并访问 say 方法，并将调用结果打印输出。
*/
type Student struct {
	name string
	gender string
	age int
	id int
	score float64
}
func (student *Student) say() string {
	infoStr := fmt.Sprintf("student的信息 name=[%v] gender=[%v] age=[%v] id=[%v] score=[%v]",
		student.name, student.gender, student.age, student.id, student.score)
	return infoStr
}
func main() {
	//测试
	//创建一个Studeng实例变量
	var stu = Student{
		name : "tom",
		gender : "male",
		age : 20,
		id : 1000,
		score : 90.23,
		}
		fmt.Println(stu.say())
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo14>go run main.go
student的信息 name=[tom] gender=[male] age=[20] id=[1000] score=[90.23]
```

### 10.3.3小狗案例

1) 编写一个 Dog 结构体，包含 name、age、weight 字段
2) 结构体中声明一个 say 方法，返回 string 类型，方法返回信息中包含所有字段值。
3) 在 main 方法中，创建 Dog 结构体实例(变量)，并访问 say 方法，将调用结果打印输出。

```go
package main
import "fmt"
/* 
1) 编写一个 Dog 结构体，包含 name、age、weight 字段
2) 结构体中声明一个 say 方法，返回 string 类型，方法返回信息中包含所有字段值。
3) 在 main 方法中，创建 Dog 结构体实例(变量)，并访问 say 方法，将调用结果打印输出。
 */
type Dog struct {
	name string
	age int
	weight int
}
func (d Dog) say() string {
	return fmt.Sprintf("name:%s,age:%d,weight:%d",d.name,d.age,d.weight)
}
 func main() {
	var c Dog
	c.name = "Tom"
	c.age = 10
	c.weight = 100
	fmt.Println(c.say())
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo15>go run main.go
name:Tom,age:10,weight:100
```

### 10.3.4盒子案例

1.  编程创建一个 Box 结构体，在其中声明三个字段表示一个立方体的长、宽和高，长宽高要从终 端获取
2. 声明一个方法获取立方体的体积。
3. 创建一个 Box 结构体变量，打印给定尺寸的立方体的体积

代码：

```go
package main
import "fmt"
/* 
1. 编程创建一个 Box 结构体，在其中声明三个字段表示一个立方体的长、宽和高，长宽高要从终 端获取
2. 声明一个方法获取立方体的体积。
3. 创建一个 Box 结构体变量，打印给定尺寸的立方体的体积
*/
type Box struct {
	len float64
	width float64
	height float64
}
func (box *Box) getVolume() float64 {
	return box.len * box.width * box.height
}
 func main() {
var box Box
box.len = 1.1
box.width = 2.2
box.height = 3.3
volume := box.getVolume()
fmt.Printf("体积为=%.2f",volume)
}	
```

```cmd
E:\goproject\src\gocode\gw\project010\damo16>go run main.go
体积为=7.99
```

### 10.3.5 景区门票案例

1. 一个景区根据游人的年龄收取不同价格的门票，比如年龄大于 18，收费 20 元，其它情况门票免 费.
2. 请编写 Visitor 结构体，根据年龄段决定能够购买的门票价格并输出

代码：

```go
package main
import "fmt"
//景区门票案例
 type Visitor struct {
	Name string
	Age int
 }
 func ( v *Visitor) showPrice() {
	if v.Age >= 90 || v.Age <= 8 {
		fmt.Println("考虑到安全,老人和小朋友不可以")
		return
	}
	if v.Age >= 18 {
		fmt.Printf ("游客名字:%v \n年龄:%v\n 收费20\n",v.Name,v.Age)
	}else{
		fmt.Printf ("游客名字:%v \n年龄:%v\n 免费哦\n",v.Name,v.Age)
	}

 }
 
func main() {
	var v Visitor
	for {
		fmt.Println("请输入你的名字")
		fmt.Scanln(&v.Name)
		if v.Name == "n" {
			fmt.Println("退出程序")
			break
		}
		fmt.Println("请输入你的年龄")
		fmt.Scanln(&v.Age)
		v.showPrice()
	}
}	
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo12>go run main.go
请输入你的名字
指针
请输入你的年龄
8
考虑到安全,老人和小朋友不可以
请输入你的名字
释放
请输入你的年龄
25
游客名字:释放
年龄:25
 收费20
请输入你的名字
n
退出程序

```

## 10.4 创建结构体变量时指定字段值

- 说明

  - Golang在创建结构体实例(变量)时，可以直接指定字段的值

- 方式1

  - ![image-20231120105112841](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120105112841.png?raw=true)

  - ```go
    package main
    
    import "fmt"
    
    type Stu struct {
    	Name string
    	Age  int
    }
    
    
    func main() {
    	
    // 在全局范围声明结构体变量，使用 var 关键字
    var stu1 = Stu{"小明", 19}
    stu2 := Stu{"小红", 18}
    
    // 在创建结构体变量时，把字段名和字段值写在一起
    var stu3 = Stu{
    	Name: "小张",
    	Age:  20,
    }
    
    stu4 := Stu{
    	Age:  21,
    	Name: "小李",
    }
    	// 在 main 函数内部打印结构体变量
    	fmt.Println(stu1, stu2, stu3, stu4)
    }
    
    ```

    ```cmd
    E:\go\goproject\src\gocode\gw\project010\damo13>go run main.go
    {小明 19} {小红 18} {小张 20} {小李 21}
    ```

- 方式2

  - ![image-20231120105923201](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120105923201.png?raw=true)

  - ```go
    package main
    
    import "fmt"
    
    type Stu struct {
    	Name string
    	Age  int
    }
    
    
    func main() {
    	
    // 在全局范围声明结构体变量，使用 var 关键字
    var stu1 = Stu{"小明", 19}
    stu2 := Stu{"小红", 18}
    
    // 在创建结构体变量时，把字段名和字段值写在一起
    var stu3 = Stu{
    	Name: "小张",
    	Age:  20,
    }
    
    stu4 := Stu{
    	Age:  21,
    	Name: "小李",
    }
    	// 在 main 函数内部打印结构体变量
    	fmt.Println(stu1, stu2, stu3, stu4)
    
    //方式2/ 返回结构体的指针类型(!!!)
    var stu5 *Stu = &Stu{"小王",30}
    stu6 := &Stu{"小刘",29}
    
    //在创建结构体指针变量时，把字段名和字段值写在一起，这种写法，就不依赖字段的定义顺序。
    var stu7 = &Stu {
    	Name : "小李",
    	Age : 49,
    }
    stu8 := &Stu{
    	Age : 23,
    	Name: "释放",
    }
    fmt.Println(*stu5, *stu6, *stu7, *stu8)
    }
    ```

    ```cmd
    E:\go\goproject\src\gocode\gw\project010\damo13>go run main.go
    {小明 19} {小红 18} {小张 20} {小李 21}
    {小王 30} {小刘 29} {小李 49} {释放 23}
    ```

## 10.5 工厂模式

### 10.5.1 说明

- Golang 的结构体没有构造函数，通常可以使用工厂模式来解决这个问题。

### 10.5.2 看一个需求

- 一个结构体的声明是这个样的

  package model

  type Student struct {

  Name string.....

  }

- 因为这里的 Student 的首字母 S 是大写的，如果我们想在其它包创建 Student 的实例(比如 main 包)， 引入 model 包后，就可以直接创建 Student 结构体的变量(实例)。`但是问题来了，如果首字母是小写的， 比如 是 type student struct {....} 就不不行了，怎么办---> 工厂模式来解决.`

### 10.5.3 工厂模式来解决问题

- 使用工厂模式实现跨包创建结构体实例(变量)的案例：

  如果 model 包的 结构体变量首字母大写，引入后，直接使用, 没有问题

  ![image-20231120111844882](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120111844882.png?raw=true)

![image-20231120111939307](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120111939307.png?raw=true)

```cmd
E:\go\goproject\src\gocode\gw\project010\damo14>go run main.go
{tom 90}
```

- 如果 model 包的 结构体变量首字母小写，引入后，不能直接使用, 可以工厂模式解决

  ![image-20231120113124850](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120113124850.png?raw=true)

```go
package main

import (
	"fmt"
	"gocode/gw/project010/damo14/os"
)

func main() {
//创建要给Studeng实例
// var stu = model.Student{
// 	Name : "tom",
// 	Score : 90,
// }
//定义studeng结构体，通过工厂模式解决
var stu2 = model.NewStudent("jerry", 100)
fmt.Println(*stu2)

}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo14>go run main.go
{jerry 100}
```

- 如果 model 包的 student 的结构体的字段 Score 改成 score，我们还能正常访问 吗？又应该如何解决这个问题呢？
  - ![image-20231120144611466](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120144611466.png?raw=true)

```go
package model
type student struct {
	Name string
	score float32
}
//接收一个字符串和一个数字，并且退出的值为地址，并且将地址以指针：值的方式传递
func NewStudent(n string,s float32) *student{
	return &student{
		Name : n,
		score : s,
    }
}
func (s *student)GetName() string{
	return s.score
}
```

```go
package main

import (
	"fmt"
	"gocode/gw/project010/damo14/os"
)

func main() {
//创建要给Studeng实例
// var stu = model.Student{
// 	Name : "tom",
// 	Score : 90,
// }
//定义studeng结构体，通过工厂模式解决
var stu2 = model.NewStudent("jerry", 100)
fmt.Println(*stu2)
fmt.Println(stu2.GetName())
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo14>go run main.go
# gocode/gw/project010/damo14/os
os\model.go:14:9: cannot use s.score (variable of type float32) as string value in return statement

```

# 第11章面向对象编程(下)

## 11.2面向对象编程思想-抽象

### 11.2.1抽象的介绍

- 我们在前面去定义一个结构体时候，实际上就是把一类事物的共有的属性(字段)和行为(方法)提取 出来，形成一个物理模型(结构体)。这种研究问题的方法称为抽象。

![image-20231120144801386](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120144801386.png?raw=true)

### 11.2.2代码实现

```go
package main

import "fmt"

// 定义一个结构体 Account
type Account struct {
	AccountNo string
	Pwd       string
	Balance   float64
}

// 存款
func (a *Account) Deposit(money float64, pwd string) {
	// 看下输入的密码是否正确
	if pwd != a.Pwd {
		fmt.Println("您输入的密码不正确")
		return
	}
	// 看看存款金额是否正确
	if money < 0 {
		fmt.Println("存款金额不能为负数")
		return
	}
	a.Balance += money
	fmt.Println("存款成功")
}

// 取款
func (a *Account) Withdraw(money float64, pwd string) {
	// 看一下输入的密码是否正确
	if pwd != a.Pwd {
		fmt.Println("您输入的密码不正确")
		return
	}
	// 看看取款金额是否正确
	if money < 0 || money > a.Balance {
		fmt.Println("您输入的金额不正确")
		return
	}
	a.Balance -= money
	fmt.Println("取款成功")
}

func (a *Account) ShowBalance(pwd string) {
	if pwd != a.Pwd {
		fmt.Println("您输入的密码不正确")
		return
	}
	fmt.Printf("您的账号为=%v 您的余额为=%v\n", a.AccountNo, a.Balance)
}

func main() {
	// 测试一把
	account := Account{
		AccountNo: "gs123",
		Pwd:       "666666",
		Balance:   1003.2,
	}

	// 这里可以做得更加灵活，让用户通过控制台输入命令...
	// 菜单.... account.Query("666666")
	account.Deposit(200.0, "666666")
	account.Withdraw(150.0, "666666")
	account.ShowBalance("666666")
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo16>go run main.go
存款成功
取款成功
您的账号为=gs123 您的余额为=1053.2
```

## 11.3 面向对象编程三大特性-封装

### 11.3.1 基本介绍

- Golang 仍然有面向对象编程的继承，封装和多态的特性，只是实现的方式和其它 OOP 语言不一 样，下面我们一一为同学们进行详细的讲解 Golang 的三大特性是如何实现的。

### 11.3.2 封装介绍

- 封装(encapsulation)就是把抽象出的字段和对字段的操作封装在一起,数据被保护在内部,程序的其 它包只有通过被授权的操作(方法),才能对字段进行操作

### 11.3.3 封装的理解和好处

1. 隐藏实现细节
2. 提可以对数据进行验证，保证安全合理(Age)

### 11.3.4如何体现封装

1. 对结构体中的属性进行封装
2. 通过方法，包实现封装

### 11.3.5封装的实现步骤

1. 将结构体、字段(属性)的首字母小写(不能导出了，其它包不能使用，类似 private)
2. 给结构体所在包提供一个工厂模式的函数，首字母大写。类似一个构造函数
3. 提供一个首字母大写的 Set 方法(类似其它语言的 public)，用于对属性判断并赋

func (var 结构体类型名) Set Xxx(参数列表)(返回值列表) {

​	//加入数据验证的业务逻辑

​	var 字段 = 参数

}

4. 提供一个首字母大写的 Get 方法(类似其它语言的 public)，用于获取属性的值

func ( var 结构体类型名)Get Xxx() {

​	retrun var.age;

}

`特别说明`:在Golang 开发中并没有特别强调封装，这点并不像 Java. 所以提醒学过 java 的朋友， 不用总是用 java 的语法特性来看待 Golang, Golang 本身对面向对象的特性做了简化的

### 11.3.6快速入门案例

- 看一个案例

  - 请大家看一个程序(person.go),不能随便查看人的年龄,工资等隐私，并对输入的年龄进行合理的验 证。设计: model 包(person.go) main 包(main.go 调用Person结构体)

- 代码实现

  ![image-20231120172010530](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120172010530.png?raw=true)

  - model/Person.go

  - ```go
    package model
    
    import "fmt"
    
    // 定义一个结构体 Account
    type person struct {
    	Name string
    	age int
    	sal float64
    }
    
    //写一个工厂模式函数，相当于构造函数
    func NewPerson(name string) *person {
    	return &person{
    		Name : name,
    	}
    }
    
    //为了访问age和 sal 我们编写一对SetXxx的方法和GetXxx方法
    func (p *person) SetAge(age int) {
    	if age > 0 && age < 150 {
    		p.age = age
    	}else{
    		fmt.Println("年龄范围不正确")
    		//给程序员一个默认值
    	}
    }
    
    func (p *person) GetAge() int {
    	return p.age
    }
    
    func (p *person) SetSal(sal float64){
    	if sal >= 3000 && sal <= 300000 {
    		p.sal = sal
    	}else {
    		fmt.Println("工资范围不正确")
    		//给程序员一个默认值
    	}
    }
    
    func (p *person) GetSal() float64 {
    	return p.sal
    }
    func main() {
    
    }
    ```

    main/main.go

    ```go
    package main
    import (
    	"fmt"
    	"gocode/gw/project010/damo17"
    )
    func main() {
    	p := model.NewPerson("张三")
    	p.SetAge(18)
    	p.SetSal(50000)
    	fmt.Println(*p)
    	fmt.Println(p.Name, "age=",p.GetAge(), "sal=", p.GetSal())
    }
    
    ```

    ```cmd
    E:\go\goproject\src\gocode\gw\project010\damo17\main>go run main.go
    {张三 18 50000}
    张三 age= 18 sal= 50000
    ```

### 11.3.7练习

- 要求
  1. 创建程序,在 model 包中定义 Account 结构体：在 main 函数中体会 Golang 的封装性。
  2. Account 结构体要求具有字段：账号（长度在 6-10 之间）、余额(必须>20)、密码（必须是六）
  3. 通过 SetXxx 的方法给 Account 的字段赋值。(同学们自己完成
  4. 在 main 函数中测

![image-20231120214143838](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120214143838.png?raw=true)

main

```go
package main
import (
	"fmt"
	"gocode/gw/project010/damo17"
)
func main() {
	//创建一个account变量
	account :=model.NewAccount("jzh11111","0000000",4000)
	if account != nil {
		fmt.Println("创建成功=",*account)
	}else{
	fmt.Println("创建失败")
	}
}

```

model.go

```go
package model

import "fmt"

//定义一个结构体account
type account struct {
	accountNo string
	pwd string
	balance float64
}
//工厂模式的函数-构造函数
func NewAccount(accountNo string, pwd string, balance float64) *account {

	if len(accountNo) < 6 || len(accountNo) > 10 {	
		fmt.Println("账号长度不正确")
		return nil
	}
	if len(pwd) < 6 {
		fmt.Println("密码长度不对")
		return nil
	}

	if balance < 20 {
		fmt.Println("余额不足")
		return nil
	}
	return &account{
		accountNo : accountNo,
		pwd : pwd,
		balance : balance,
	}
}
//方法
//1.存款
func ( a *account) Deposit(money float64,pwd string) {
	if pwd != a.pwd {
	fmt.Println("密码不对")
	}
//看看存款金额是否正确
	if money < 0 {
		fmt.Println("存款金额不对")
	return
	}
	a.balance += money
	fmt.Println("存款成功")
}

//2取款
func (a *account) Withdraw(money float64,pwd string) {
	if pwd != a.pwd {
	fmt.Println("密码不对")
	return
	}
//看看取款金额是否正确
	if money < 0 {
		fmt.Println("存款金额不对")
	return
	}
	a.balance -= money
	fmt.Println("取款成功")
}
//查询余额
func (a *account) Balance(pwd string) {
	if pwd != a.pwd {
	fmt.Println("密码不对")
	return
	}
	fmt.Println("余额为",a.balance)
}

```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo17\main>go run main.go
创建成功= {jzh11111 0000000 4000}
```

## 11.4面向对象编程三塔特性-继承

- 一个小问题,看个学生考试系统的程序 extends01.go，提出代码复用的问题

![image-20231120214253290](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120214253290.png?raw=true)

```go
package main

import "fmt"

//编写一个学生考试系统
//小学生
type Pupil struct {
	Name string
	Age int
	Score int
	}
//显示他的成绩
func (p *Pupil) ShowScore() {
	fmt.Printf("学生名=%v 年龄=%v 成绩=%v\n", p.Name, p.Age, p.Score)
}
func (p *Pupil) SetScore(score int) {
	//业务判断
	p.Score = score
	}
func (p *Pupil) testing() {
	fmt.Println("小学生正在考试中...")
}

//大学生
type Graduate struct {
	Name string
	Age int
	Score int
	}
//显示他的成绩
func (g *Graduate) ShowScore() {
	fmt.Printf("学生名=%v 年龄=%v 成绩=%v\n", g.Name, g.Age, g.Score)	
}
	
func (g *Graduate) SetScore(score int) {
	//业务判断
	g.Score = score
}

func (g *Graduate) testing() {
	fmt.Println("大学生正在考试中...")
}
//代码冗余高中生.....

func main() {
	//测试
	var pupil = &Pupil{
	Name :"tom", Age : 10, }
	pupil.testing()
	pupil.SetScore(90)
	pupil.ShowScore()
fmt.Println("-------------------------")
	var graduate = &Graduate{
		Name :"mary", Age : 20, }
		graduate.testing()
		graduate.SetScore(90)
		graduate.ShowScore()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo18>go run main.go
小学生正在考试中...
学生名=tom 年龄=10 成绩=90
-------------------------
大学生正在考试中...
学生名=mary 年龄=20 成绩=90
```

-  对上面代码的小结
  1. Pupil 和 Graduate 两个结构体的字段和方法几乎，但是我们却写了相同的代码， 代码复用性不
  2. 出现代码冗余，而且代码不利于维护，同时也不利于功能的扩展。
  3. 解决方法-通过继承方式来解决

### 11.4.2继承基本介绍和示意图

- 继承可以解决代码复用,让我们的编程更加靠近人类思维。
- 当多个结构体存在相同的属性(字段)和方法时,可以从这些结构体中抽象出结构体(比如刚才的Student),在该结构体中定义这些相同的属性和方法。
- 其它的结构体不需要重新定义这些属性(字段)和方法，只需嵌套一个 Student 匿名结构体即可。 
  - ![image-20231120225631463](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120225631463.png?raw=true)

​	`也就是说：在 Golang 中，如果一个 struct 嵌套了另一个匿名结构体，那么这个结构体可以直接访 问匿名结构体的字段和方法，从而实现了继承特性。`

### 11.4.3嵌套匿名结构体的基本语法

```go
type Goods struct {
Name string
Price int
}

type Book struct {
Goods //这里就是嵌套匿名结构体 Goods
Writer string
}
```

### 11.4.4快速入门案例

- 我们对 extends01.go 改进，使用嵌套匿名结构体的方式来实现继承特性,请大家注意体会这样编程的好处

![image-20231120225816586](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120225816586.png?raw=true)

```go
package main

import "fmt"

//编写一个学生考试系统
//小学生
type Student struct {
	Name string
	Age int
	Score int
	}

//将Pupil和Graduate共有的方法也绑定到*Student
func (stu *Student) ShowInfo() {
	fmt.Printf("学生名=%v 年龄=%v 成绩=%v\n", stu.Name, stu.Age, stu.Score)
}
func (stu *Student) SetScore(score int) {
	stu.Score = score
}

//小学生
type Pupil struct {
	Student //嵌入了Student匿名函数
}

//显示他的成绩

//这时Pupil结构体特有的方法，保留
func (p *Pupil)testing(){
	fmt.Println("小学生正在考试中")
}
// 大学生
type Graduate struct {
	Student //嵌入了Studeng匿名结构体
}
//显示他的成绩
//这时Graduate结构体特有的方法，保留
func (p *Graduate) testing() {
	fmt.Println("大学生正在考试中.....")
	}

func main (){
//当我们对结构体嵌入了匿名结构体使用方法会发生变化
pupil := &Pupil{}
pupil.Student.Name = "tom~" 
pupil.Student.Age = 8
pupil.testing()
pupil.Student.SetScore(70)
pupil.Student.ShowInfo()

graduate := &Graduate{}
graduate.Student.Name = "mary~" 
graduate.Student.Age = 28
graduate.testing()
graduate.Student.SetScore(90)
graduate.Student.ShowInfo()

}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo18>go run main.go
小学生正在考试中
学生名=tom~ 年龄=8 成绩=70
大学生正在考试中.....
学生名=mary~ 年龄=28 成绩=90
```

### 11.4.5继承编程带来的便利

1. 代码的复用性提高了
2. 代码的扩展性和维护性提高了

### 11.4.6继承深入讨论

1. 结构体可以使用嵌套匿名结构体所有的字段和方法，即：首字母大写或者小写的字段、方法， 都可以使用。【举例说明】

```go
package main

import "fmt"

type A struct {
	Name string
	age  int
}

func (a *A) SayOK() {
	fmt.Println("OK")
}

func (a *A) SayHi() {
	fmt.Println("Hi")
}

type B struct {
	A
}

func main() {
	var b B
	b.A.Name = "123"
	b.A.age = 19
	b.A.SayHi()
	b.A.SayOK()
}

```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo19>go run main.go
Hi
OK
```

2. 匿名结构体字段访问可以简化，如图

![image-20231120232014976](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120232014976.png?raw=true)

- 对上面的代码小结
  1. 当我们直接通过 b 访问字段或方法时，其执行流程如下比如 b.Nam
  2. 编译器会先看 b 对应的类型有没有 Name, 如果有，则直接调用 B 类型的 Name 字段
  3. 如果没有就去看 B 中嵌入的匿名结构体 A 有没有声明 Name 字段，如果有就调用,如果没有 继续查找..如果都找不到就报错.

3. 当结构体和匿名结构体有相同的字段或者方法时，编译器采用就近访问原则访问，如希望访问 匿名结构体的字段和方法，可以通过匿名结构体名来区分【举例说明】

   ![image-20231120232146277](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120232146277.png?raw=true)

4. 结构体嵌入两个(或多个)匿名结构体，如两个匿名结构体有相同的字段和方法(同时结构体本身没有同名的字段和方法)，在访问时，就必须明确指定匿名结构体名字，否则编译报错。【举例说明】

​		![image-20231120232643423](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120232643423.png?raw=true)

5. 如果一个 struct 嵌套了一个有名结构体，这种模式就是组合，如果是组合关系，那么在访问组合 的结构体的字段或方法时，必须带上结构体的名字

![image-20231120232738585](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120232738585.png?raw=true)

6. 嵌套匿名结构体后，也可以在创建结构体变量(实例)时，直接指定各个匿名结构体字段的值

```go
package main

import "fmt"

type Goods struct {
	Name  string
	Price float64
}

type Brand struct {
	Name    string
	Address string
}

type TV struct {
	Goods
	Brand
}

type TV2 struct {
	*Goods
	*Brand
}

func main() {
	tv := TV{Goods{"Tv", 1000},Brand{"TCL", "Shanghai"},}

	tv2 := TV2{
		&Goods{
			Price: 5000.12,
			Name:  "电视剧002",
		},
		&Brand{
			Name:    "TCL",
			Address: "Shanghai",
		},
	}

	fmt.Println(tv)
	fmt.Println(tv2)

	tv3 := TV2{&Goods{"Tv", 1000}, &Brand{"TCL", "Shanghai"}}
	tv4 := TV2{
		&Goods{
			Price: 5000.12,
			Name:  "电视剧002",
		},
		&Brand{
			Name:    "TCL",
			Address: "Shanghai",
		},
	}

	fmt.Println("tv3", *tv3.Goods, *tv3.Brand)
	fmt.Println("tv4", *tv4.Goods, *tv4.Brand)
}

```

```cmd

E:\go\goproject\src\gocode\gw\project010\damo20>go run main.go
{{Tv 1000} {TCL Shanghai}}
{0xc000008048 0xc00005c3a0}
tv3 {Tv 1000} {TCL Shanghai}
tv4 {电视剧002 5000.12} {TCL Shanghai}
```

### 11.4.7练习

结构体的匿名字段是基本数据类型，如何访问, 下面代码输出什么

```go
package main

import "fmt"

type Monster struct {
	Name string
	Age  int
}

type E struct {
	Monster
	int
	n int
}

func main() {
	// 演示一下匿名字段基本数据类型的使用
	var e E
	e.Name = "狐狸精"
	e.Age = 300
	e.int = 20
	e.n = 40
	fmt.Println("e=", e)
}

```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo21>go run main.go
e= {{狐狸精 300} 20 40}
```

说明

1. 如果一个结构体有 int 类型的匿名字段，就不能第二个。
2. 如果需要有多个 int 的字段，则必须给 int 字段指定名字

### 11.4.8面向对象编程-多重继承

- 多重继承说明
  - 如`一个 struct 嵌套了多个匿名结构体`，那么该结构体可以直接访问嵌套的匿名结构体的字段和方 法，`从而实现了多重继承。`

- 案例演示
  - 通过一个案例来说明多重继承使用
  - ![image-20231120234718834](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120234718834.png?raw=true)

-  多重继承细节说明

  1. 如嵌入的匿名结构体有相同的字段名或者方法名，则在访问时，需要通过匿名结构体类型名来 区分。【案例演示】

  - ![image-20231120234748279](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231120234748279.png?raw=true)

  2. 为了保证代码的简洁性，建议大家尽量不使用多重继承

## 11.5 接口(interface)

### 11.5.1 基本介绍

- 按顺序,我们应该讲解多态,但是在讲解多态前,我们需要讲解接口(interface)，因为在 Golang 中 多态 特性主要是通过接口来体现的。

### 11.5.2为什么有结构

![image-20231121171031765](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121171031765.png?raw=true)

### 11.5.3接口快速入门

- 这样的设计需求在 Golang 编程中也是会大量存在的,我曾经说过,一个程序就是一个世界,在现实世 界存在的情况，在程序中也会出现。我们用程序来模拟一下前面的应用场景。

代码

```go
package main

import "fmt"

//声明定义一个接口
type Usb interface {
	//声明了两个没有实现的方法
	Start()
	Stop()
}

type Phone struct {

}
//让Phone实现Usb接口方法
func (p Phone) Start() {
	fmt.Println("手机开始工作")
}
func (p Phone) Stop() {
	fmt.Println("手机停止工作")
}

type Camera struct {

}
//让Camer 实现 Usb接口的方法
func (c Camera) Start() {
	fmt.Println("相机开始工作")
}
func (c Camera) Stop() {
	fmt.Println("相机停止工作")
}

//计算机
type Computer struct {

}
//编写一个方法Working方法，接收一个Usb接口类型变量
//只要实现了Usb接口(所谓实现Usb接口，就是指实现了 Usb 接口声明所有方法）
func (c Computer) Working(usb Usb) {
	usb.Start()
	usb.Stop()
}
func main () {
	//测试
	//先创建结构体变量
	computer := Computer{}
	phone := Phone{}
	camera := Camera{}
	//关键点
	computer.Working(phone)
	computer.Working(camera)
}

```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo22>go run main.go
手机开始工作
手机停止工作
相机开始工作
相机停止工作
```

### 11.5.4 接口概念的再说明

- interface 类型可以定义一组方法，但是这些不需要实现。并且 interface 不能包含任何变量。到某个 自定义类型(比如结构体 Phone)要使用的时候,在根据具体情况把这些方法写出来(实现)。

### 11.5.5基本语法

![image-20231121215652934](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121215652934.png?raw=true)

1. 接口里的所有方法都没有方法体，即接口的方法都是没有实现的方法。接口体现了程序设计的 多态和高内聚低偶合的思想。
2. Golang 中的接口，不需要显式的实现。只要一个变量，含有接口类型中的所有方法，那么这个 变量就实现这个接口。因此，Golang 中没有 implement 这样的关键字

### 11.5.6接口使用的应用场景

![image-20231121215831034](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121215831034.png?raw=true)

### 11.5.7注意事项和细节

1. 接口本身不能创建实例,但是可以指向一个实现了该接口的自定义类型的变量(实例)

```go
package main

import "fmt"

type Interface interface {
	Say()
}

type Stu struct {
	Name string
}

func (stu Stu) Say() {
	fmt.Println("stu say()")
}

func main() {
	var stu Stu // 结构体变量，实现了 Say() 方法，因此实现了 Interface
	var a Interface = stu
	a.Say() // 调用 Interface 接口的 Say() 方法

	// 直接通过 stu 变量访问 Name 字段
	fmt.Println(stu.Name)
}
```

```
E:\go\goproject\src\gocode\gw\project010\damo23>go run main.go
stu say()
```

2. 接口中所有的方法都没有方法体,即都是没有实现的方法。
3. 在 Golang 中，一个自定义类型需要将某个接口的所有方法都实现，我们说这个自定义类型实现 了该接口。
4. 一个自定义类型只有实现了某个接口，才能将该自定义类型的实例(变量)赋给接口类型
5. 只要是自定义数据类型，就可以实现接口，不仅仅是结构体类型。![image-20231121222633446](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121222633446.png?raw=true)

```go
package main

import "fmt"

type Interface interface {
	Say()
}

type Stu struct {
	Name string
}

type integer int

func (i integer) Say() {
	fmt.Println("integer say()", i)
}

func (stu Stu) Say() {
	fmt.Println("stu say()")
}

func main() {
	var stu Stu // 结构体变量，实现了 Say() 方法，因此实现了 Interface
	var a Interface = stu
	a.Say() // 调用 Interface 接口的 Say() 方法

	// 直接通过 stu 变量访问 Name 字段
	fmt.Println(stu.Name)

	var i integer = 100
	var b Interface = i // 将整数类型转换为接口类型
	b.Say()
}

```

6. 一个自定义类型可以实现多个接口

```go
package main

import "fmt"

type Interface interface {
	Say()
}

type Binterface interface {
	Hello()
}
type Monster struct {

}
func (m Monster) Hello() {
	fmt.Println("Monster Hello()")
}

type Monster2 struct {

}
func (m Monster) Say() {
	fmt.Println("Monster Say()")
}

type Stu struct {
	Name string
}

type integer int

func (i integer) Say() {
	fmt.Println("integer say()", i)
}

func (stu Stu) Say() {
	fmt.Println("stu say()")
}

func main() {
	var stu Stu // 结构体变量，实现了 Say() 方法，因此实现了 Interface
	var a Interface = stu
	a.Say() // 调用 Interface 接口的 Say() 方法

	// 直接通过 stu 变量访问 Name 字段
	fmt.Println(stu.Name)

	var i integer = 100
	var b Interface = i // 将整数类型转换为接口类型
	b.Say()

	var monster Monster
	var a2 Interface = monster
	var a3 Binterface = monster
	a2.Say()
	a3.Hello()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo23>go run main.go
stu say()

integer say() 100
Monster Say()
Monster Hello()
```

7. Golang接口中不能有任何变量

![image-20231121223055458](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121223055458.png?raw=true)

8. 一个接口(比如 A 接口)可以继承多个别的接口(比如 B,C 接口)，这时如果要实现 A 接口，也必 须将 B,C接口的方法也全部实现。

```go
package main

import "fmt"

type Interface interface {
	test01()
}

type Binterface interface {
	test02()
}

type Cinterface interface {
	Interface
	Binterface
	test03()
}
type Stu struct {

}
func (stu Stu) test01() {
	fmt.Println("test01")
}

func (stu Stu) test02() {
	fmt.Println("test02")
}

func (stu Stu) test03() {
	fmt.Println("test03")
}

func main() {
	var stu Stu
	var a  Cinterface = stu
	a.test01()
	a.test02()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo23>go run main.go
test01
test02
```

9. interface 类型默认是一个指针(引用类型)，如果没有对 interface 初始化就使用，那么会输出 nil
10. 空接口 interface{} 没有任何方法，所以所有类型都实现了空接口, 即我们可以把任何一个变量 赋给空接口

![image-20231121224054105](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121224054105.png?raw=true)

### 11.5.8课堂练习

![image-20231121224210072](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121224210072.png?raw=true)![image-20231121224216988](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121224216988.png?raw=true)

![image-20231121224223694](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231121224223694.png?raw=true)

### 11.5.9接口编程的最佳实践

```go
package main

import (
	"fmt"
	"sort"
	"math/rand"
)

// 1. 声明 Hero 结构体
type Hero struct {
	Name string
	Age  int
}

	// 2. 声明一个 Hero 结构体切片类型
		/* HeroSlice实现了`sort.Interface`接口，这是为了让sort包能够对
		HeroSlice进行排序。
		Len（）：返回切片长度
		less：定义了排序标准，这里按照Age字段进行升序排序
		Swap：用于交换切片中的两个元素。 */
type HeroSlice []Hero
		// 3. 实现 sort.Interface 接口
		func (hs HeroSlice) Len() int {
			return len(hs)
		}
		// Less 方法决定使用什么标准进行排序
		// 这里按照 Hero 的年龄从小到大排序
		func (hs HeroSlice) Less(i, j int) bool {
			return hs[i].Age < hs[j].Age
		}
		func (hs HeroSlice) Swap(i, j int) {
			temp := hs[i]
			hs[i] = hs[j]
			hs[j] = temp
		//等价于hs[i],hs[j] = hs[j],hs[i]
		}

func main() {
	//创建一个整数切片 intSlice，包含元素 0, -1, 10, 7, 90。然后
	//使用 sort.Ints 函数对切片进行排序，最后打印排序后的结果。
	var intSlice = []int{0, -1, 100, 7, 90}
	fmt.Println(intSlice)
	//使用sort。Ints进行排序
	sort.Ints(intSlice)
	//查看排序后的切片
	fmt.Println(intSlice)
fmt.Println("\n\n--------------------------------")
	/* 创建一个 HeroSlice 类型的切片 heroes，循环10次，每次生成一个
	  Hero 结构体对象，并将其追加到 heroes 切片中。Name 字段使用 
	  fmt.Sprintf 格式化字符串生成，Age 字段使用 rand.Intn(100)
	  生成一个 0 到 99 的随机整数。创建一个 HeroSlice 类型的切片
	  heroes，循环10次，每次生成一个 Hero 结构体对象，并将其追加
	  到 heroes 切片中。Name 字段使用 fmt.Sprintf 格式化字符串
	  生成，Age 字段使用 rand.Intn(100) 生成一个 0 到 99 的随机整数。 */
	var heroes HeroSlice
	for i := 0; i < 10; i++ {
		hero := Hero{
			Name: fmt.Sprintf("hero%d", i),
			Age:  rand.Intn(100),
		}
		// 将 hero 追加到 heroes 切片
		heroes = append(heroes, hero)
	}

	// 查看排序前的顺序
	fmt.Println("排序前顺序:")
	for _, v := range heroes {
		fmt.Println(v)
	}

	// 根据年龄字段对 heroes 切片进行排序
	sort.Sort(heroes)

	// 查看排序后的顺序
	fmt.Println("排序后顺序:")
	for _, v := range heroes {
		fmt.Println(v)
	}
	i := 10
	j := 20
	i, j = j, i
	fmt.Println("i=", i, "j=", j) // i=20 j = 10
}
```

```cmd
[0 -1 100 7 90]
[-1 0 7 90 100]


--------------------------------
排序前顺序:
{hero0 61}
{hero1 86}
{hero2 0}
{hero3 61}
{hero4 36}
{hero5 71}
{hero6 46}
{hero7 62}
{hero8 32}
{hero9 50}
排序后顺序:
{hero2 0}
{hero8 32}
{hero4 36}
{hero6 46}
{hero9 50}
{hero0 61}
{hero3 61}
{hero7 62}
{hero5 71}
{hero1 86}
i= 20 j= 10
```

- 接口编程的课后练习

  - //1.声明Studeng结构体

    type Studeng 结构体 {

    ​	Name string

    ​	Age int

    ​	Score float64

    }

    //将 Studeng的切片，安Score从大到小排序

### 11.5.10实现结构 vs 继承

- 大家听到现在，可能对实现接口和继承比较迷茫了

![image-20231122145841271](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231122145841271.png?raw=true)

```go
package main

import (
	"fmt"
)
//Monkey结构体
type Monkey struct {
	Name string
}
//声明接口
type BirdAble interface {
	Flying()
}
type FisHAble interface {
	Swimming()
}

func (this *Monkey) climbing() {
	fmt.Println(this.Name,"生来会爬树")
}
//LittleMonkey结构体
type LittleMonkey struct {
	Monkey //继承
}

func (this *LittleMonkey) Flying() {
	fmt.Println(this.Name,"会飞")
}
func (this *LittleMonkey) Swimming() {
	fmt.Println(this.Name,"会游泳")
}

func main () {
	//创建一个LittleMonkey实例
	monkey := &LittleMonkey{
		Monkey {
			Name : "悟空",
		},
	}
	monkey.climbing()
	monkey.Flying()
	monkey.Swimming()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo26>go run main.go
悟空 生来会爬树
悟空 会飞
悟空 会游泳
```

- 对上面代码的小结
  1. 当 A 结构体继承了 B 结构体，那么 A 结构就自动的继承了 B 结构体的字段和方法，并且可以直 接使用
  2. 当 A 结构体需要扩展功能，同时不希望去破坏继承关系，则可以去实现某个接口即可，因此我 们可以认为：实现接口是对继承机制的补充.
- 实现接口可以看作是对 继承的一种补充

![image-20231122150858957](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231122150858957.png?raw=true)

- 接口和继承解决的解决的问题不同

  继承的价值主要在于：解决代码的复用性和可维护性。 

  接口的价值主要在于：设计，设计好各种规范(方法)，让其它自定义类型去实现这些方法。

- 接口比继承更加灵活 Person Student BirdAble LittleM

  ​	接口比继承更加灵活，继承是满足 is - a 的关系，而接口只需满足 like - a 的关系。

- 接口在一定程度上实现代码解耦

## 11.6 面向对象编程-多态

### 11.6.1基本介绍

- 变量(实例)具有多种形态。面向对象的第三大特征，在 Go 语言，多态特征是通过接口实现的。可 以按照统一的接口来调用不同的实现。这时接口变量就呈现不同的形态。

### 11.6.2 快速入门

- 在前面的 Usb 接口案例，Usb usb ，既可以接收手机变量，又可以接收相机变量，就体现了 Usb 接 口 多态特性。[点明]

![image-20231122151158006](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231122151158006.png?raw=true)

## 11.6.3 接口体现多态的两种形式

- 多态参数
  - 在前面的Usb接口案例，Usb usb，既可以接收手机变量，又可以接收相机变量，就体现了Usb接口 多态。
- 多态数组
  - 演示一个案例：给Usb数组中，存放Phone 结构体 和 Camera 结构体变量

```go
package main

import (
	"fmt"
)
//声明/定义一个接口
type Usb interface {
	//声明了两个没有实现的方法
	Start()
	Stop()
}

type Phone struct {
	name string
}
//让Phone 实现了Usb接口的方法
func (p Phone) Start() {
	fmt.Println("手机开始工作")
}
func (p Phone) Stop() {
	fmt.Println("手机停止工作")
}

type Camera struct {
	name string
}
//让Camera 实现 Usb 接口的方法
func (c Camera) Start() {
	fmt.Println("相机开始工作")
}
func (c Camera) Stop() {
	fmt.Println("相机停止工作")
}

func main(){
	//定义一个USB接口数组，可以存放Phone和Camera的结构体变量
	//这里就体现出多态数组
	var usbArr [3]Usb
	usbArr[0] = Phone{"小米"}
	usbArr[1] = Phone{"三星"}
	usbArr[2] = Camera{"佳能"}
	fmt.Println(usbArr)
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo27>go run main.go
[{小米} {三星} {佳能}]
```

## 11.7 类型断言

### 11.7.1由一个具体的需要，引出了类型断言，

![image-20231122152455692](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231122152455692.png?raw=true)

### 11.7.2基本介绍

- 类型断言，由于接口是一般类型，不知道具体类型，如果要转成具体类型，就需要使用类型断言， 具体的如下
  - ![image-20231122152518478](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231122152518478.png?raw=true)

- 对上面代码的说明：
  - 在进行类型断言时，如果类型不匹配，就会报 panic, 因此进行类型断言时，要确保原来的空接口 指向的就是断言的类型.
- 如何在进行断言时，带上检测机制，如果成功就 ok,否则也不要报 pani

```go
package main

import (
	"fmt"
)

func main(){
//类型断言的其他案例
var x interface {}
var b2 float32 = 1.1
x = b2 //空接口，可以接收任意类型
// x=>float32[使用类型断言]
y := x.(float32)
fmt.Printf("y 的类型是%T 值是=%v",y,y)
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo28>go run main.go
y 的类型是float32 值是=1.1
```

### 11.7.3类型断言的最佳实践1

- 在前面的Usb接口案例做改进：
  - 给Phone结构体增加一个特有的方法call(),当Usb接口接收的是Phone变量时，还需要调用call

```go
//1.导包
	package main

	import (
		"fmt"
	)

//2.声明/定义一个接口
	type Usb interface {
		//声明了两个没有实现的方法
		Start()
		Stop()
	}
//3.定义Phone结构体
	type Phone struct {
		name string
	}

//4.让Phone 实现Usb接口的方法
	/* Phone 结构体实现了Usb接口Start和Stop方法
	同时，Phone结构体还有一个额外的方法Call */
	func (p Phone) Start () {
		fmt.Println("手机开始工作")
	}
	func (p Phone) Stop () {
		fmt.Println ("手机停止工作")
	}
	func (p Phone) Call () {
		fmt.Println("手机 在打电话..")
	}

//5.定义Camera结构体
	type Camera struct {
	name string
	}

//6.让Camera 实现 Usb接口方法
	//Camera 结构体实现了 Usb 接口的 Start 和 Stop 方法
	func (c Camera) Start () {
		fmt.Println("相机开始工作")
	}
	func (c Camera) Stop () {
		fmt.Println ("相机停止工作")
	}
//7.定义Computer结构体
	type Computer struct {
	}
//8.Computer中的Working方法：
	/*如果 usb 是 Phone 类型，那么 ok 将为 true，并且通过类型断言
	  phone, ok := usb.(Phone) 将 usb 转换为 Phone 类型。然后，
	  你调用了 phone.Call() 方法，这是 Phone 类型的特有方法。
      无论 usb 是什么类型，都会调用 usb.Start() 和 usb.Stop() 方
	  法，因为这两个方法是 Usb 接口中声明的。*/
	func (computer Computer) Working(usb Usb){
	usb.Start()
	if phone,ok := usb.(Phone); ok{
		phone.Call()
	}
	usb.Stop()
	}

func main(){
	//定义一个Usb接口数组，可以存放Phone和Camera的结构体变量
	//这里就体现出多态数组
	var usbArr[3]Usb
	usbArr[0] = Phone{"vivo"}
	usbArr[1] = Phone{"小米"}
	usbArr[2] = Camera{"尼康"}
	//遍历 usbArr
	//Phone 还有一个特有的方法 call()，请遍历 Usb 数组，如果是 Phone 变量，
	//除了调用 Usb 接口声明的方法外，还需要调用 Phone 特有方法 call. =》类型断
	var computer Computer
	for _,v :=range usbArr{
		computer.Working(v)
		fmt.Println()
	}
	fmt.Println(usbArr)
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo29>go run main.go
手机开始工作
手机 在打电话..
手机停止工作

手机开始工作
手机 在打电话..
手机停止工作

相机开始工作
相机停止工作

[{vivo} {小米} {尼康}]
```

### 11.7.4类型断言的最佳实践2

写一函数，循环判断传入的类型：

```go
package main
import "fmt"

type Student struct {

}
//9.编写一个函数，可以判断输入的参数是什么类型
func TypeJudge(items... interface{}) {
	for index,x := range items{
		switch x.(type) {
		case bool:
			fmt.Printf("第%v个参数是 bool 类型，值是%v\n",index,x)
		case float32:
			fmt.Printf("第%v个参数是 float32 类型，值是%v\n",index,x)
		case float64:
			fmt.Printf("第%v个参数是 float64 类型，值是%v\n",index,x)
		case int,int32,int64:
			fmt.Printf("第%v个参数是 整数 类型，值是%v\n",index,x)
		case string:
			fmt.Printf("第%v个参数是 string 类型，值是%v\n",index,x)
		case Student:
			fmt.Printf("第%v个参数是 Studeng 类型，值是%v\n",index,x)
		case *Student:
			fmt.Printf("第%v个参数是 Studeng 类型，值是%v\n",index,x)
		default:
			fmt.Printf("第%v个参数是 未知类型，值是%v\n",index,x)
	}	
}
}
func main () {
	var n1 float32 = 1.2
	var n2 float64 = 2.2
	var n3 int64 = 30
	var name string = "tom"
	address := "北京"
	n4  := 3000
	stu1 := Student{}
	stu2 := &Student{}
	TypeJudge(n1,n2,n3,name,address,n4,stu1,stu2)
}
```

```cmd
E:\go\goproject\src\gocode\gw\project010\damo30>go run main.go
第0个参数是 float32 类型，值是1.2
第1个参数是 float64 类型，值是2.2
第2个参数是 整数 类型，值是30
第3个参数是 string 类型，值是tom
第4个参数是 string 类型，值是北京
第5个参数是 整数 类型，值是3000
第6个参数是 Studeng 类型，值是{}
第7个参数是 Studeng 类型，值是&{}
```

# 第12章 项目1-家庭收支记账软件项目

## 12.1项目开发流程说明

![image-20231123095700398](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123095700398.png?raw=true)

## 12.2项目需求说明

1. 模拟实现基于文本界面的《家庭记账软件》
2. 该软件能够记录家庭的收入、支出，并能够打印收支明细表

## 12.3项目的界面

![image-20231123095747626](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123095747626.png?raw=true)

![image-20231123095759440](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123095759440.png?raw=true)

![image-20231123095808960](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123095808960.png?raw=true)

其它的界面，我们就直接参考 项目效果图.txt

### 12.4项目代码实现

### 12.4.1实现基本功能（先使用面向过程，后面改成面向对象）

#### 功能1：先完成可以显示主菜单，并且可以退出

- 思路分析：

  更加给出的界面完成，主菜单的显示, 当用户输入 4 时，就退出该程序![image-20231123104532604](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123104532604.png?raw=true)

#### 功能2：完成收入登记

还需要定义变量来记录余额(balance)、每次收支的金额(money), 每次收支的说明(note)

- 思路分析

  因为需要显示明细，我们定义一个变量details string来记录

  还需要定义变量来记录余额(balance),每次收支的金额(money),每次收支的说明（note)

  ![image-20231123104550236](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123104550236.png?raw=true)

#### 功能3：完成了登记支出的功能

- 思路分析：

  登记支出的功能和登录收入的功能类似。

  ![image-20231123104602128](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123104602128.png?raw=true)

### 12.4.2 项目代码实现改进

1. 用户退出时，给出提示“你确定要退出吗?y/n",必须输入正确y/n，否则循环输入指令，直到输入y或者n

   ![image-20231123105550593](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123105550593.png?raw=true)

2. 当没有任何收支明细时，提示”当前没有收支明细..来一笔吧!"![image-20231123110944542](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123110944542.png?raw=true)

   ![image-20231123111051641](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123111051641.png?raw=true)

3. 在支出时，判断余额是否够，并给出相应的提示

   ![image-20231123112223530](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123112223530.png?raw=true)

```go
package main 
import (
	"fmt"
)

func main () {
	//声明一个变量，保存接收用户输入的选项
	key := ""
	//声明一个变量，控制是否退出for
	loop := true
	//定义账户的余额【】
	balance := 10000.0
	// 每次收支的金额
	money := 0.0
	//每次收支的说明
	note := ""
	//定义个变量，记录是否有收支的行为
	flag := false
	//收支的详细使用字符串来记录
	//当有收支时，只需要对details 进行拼接处理即可
	details := "收支\t账户金额\t收支金额\t说 明\n"
	//显示这个主菜单
	for {
		fmt.Println("----------家庭收支记账软件----------")
		fmt.Println("          1. 收支明细")
		fmt.Println("          2. 登记收入")
		fmt.Println("          3. 登记指出")
		fmt.Println("          4. 退出软件")
		fmt.Print("请选择(1-4)")
		fmt.Scanln(&key)
		switch key {
			case "1":
				fmt.Println("----------当前收支明细记录----------\n")
				if flag {
					fmt.Println(details)
				}else{
					fmt.Println("当前没有收支明细...来一笔吧!")
					}
			case "2":
				fmt.Println("本次收入金额")
				fmt.Scanln(&money)
				balance += money
				fmt.Println("本次收入说明")
				fmt.Scanln(&note)
				//进行引用"收支\t账户金额\t收支金额\t说 明\n"
				details += fmt.Sprintf("\n收入\t%v\t\t%v\t%v", balance, money, note)
				flag = true
			case "3":
				fmt.Println("登记指出")
				fmt.Println("本次支出金额")
				fmt.Scanln(&money)
				if money > balance {
					fmt.Printf("余额不足:%v无法支出 \n当前余额:%v\n",money,balance)
					break
				}
				balance -= money
				fmt.Println("本次支出说明")
				fmt.Scanln(&note)
				//进行引用"收支\t账户金额\t收支金额\t说 明\n"
				details += fmt.Sprintf("\n收入\t%v\t\t%v\t%v", balance, money, note)
			case "4","exit":
				fmt.Println("你确定要退出吗?y/n")
				choice := ""
				for {
					fmt.Scanln(&choice)
					if choice == "y" || choice == "n" {
						break
					}
					fmt.Println("你输入的有误，请重新输入  y/n")
				}
				if choice == "y" {
				loop = false
				}
			default:
				fmt.Println("输入错误，请重新输入")
			}
		if !loop {
			break
			}
		}
		fmt.Println("退出程序")
}
```

```cmd
E:\go\goproject\src\gocode\gw\project12\damo01>go run main.go
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

当前没有收支明细...来一笔吧!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)2
本次收入金额
1000
本次收入说明
红包来啦!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

收支    账户金额        收支金额        说 明

收入    11000           1000    红包来啦!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)3
登记指出
本次支出金额
20
本次支出说明
买烟
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

收支    账户金额        收支金额        说 明

收入    11000           1000    红包来啦!
收入    10980           20      买烟
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)4
你确定要退出吗?y/n
y
退出程序
```



### 项目转为面向对象

将面 向 过 程 的 代 码 修 改 成 面 向 对 象 的 方 法 ， 编 写 myFamilyAccount.go ， 并 使 用 testMyFamilyAccount.go 去完成测

- 思路分析：

  - 把记账软件的功能，封装到一个结构体中，然后调用该结构体方法，来实现记账，显示明细。结构体的名字 FamilyAcount.

  - 在通过在main方法中，创建一个结构体FamilyAccount，实现记账即可

- 代码实现

  - 代码不需要重写，只需要重写组织一下

  ![image-20231123152403802](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123152403802.png?raw=true)

utils/utils.go

```go
package utils
import (
	"fmt"
)

type FamilyAccount struct {
	//声明一个变量，保存接收用户输入的选项
	key string
	//声明一个变量，控制是否退出for
	loop bool
	//定义账户的余额【】
	balance float64
	// 每次收支的金额
	money float64
	//每次收支的说明
	note string
	//定义个变量，记录是否有收支的行为
	flag  bool
	//收支的详细使用字符串来记录
	//当有收支时，只需要对details 进行拼接处理即可
	details string
	//显示这个主菜单
}
//编写工厂函数的构造方法，返回一个*FamilyAccount实例
func NewFamilyAccount() *FamilyAccount{
	return &FamilyAccount{
		key: "1",
		loop: true,
		balance: 00.00,
		money: 0,
		note: "",
		flag: false,
		details: "收支\t 账户金额\t 收支金额\t说   明",
	}
}

//将显示明细写一个方法
func (this *FamilyAccount) ShowDetails() {
	fmt.Println("----------当前收支明细记录----------\n")
	if this.flag {
		fmt.Println(this.details)
	}else{
		fmt.Println("当前没有收支明细...来一笔吧!")
		}
}
//将登记收入写成一个方法，和*FamilyAccount绑定
func (this *FamilyAccount) income() {
	fmt.Println("本次收入金额")
	fmt.Scanln(&this.money)
	this.balance += this.money
	fmt.Println("本次收入说明")
	fmt.Scanln(&this.note)
	//进行引用"收支\t账户金额\t收支金额\t说 明\n"
	this.details += fmt.Sprintf("\n收入\t%v\t\t%v\t%v",this.balance,this.money,this.note)
	this.flag = true
}
//将登记支出写成一个方法，和*FamilyAccount绑定
func (this *FamilyAccount) pay() {
	fmt.Println("登记指出")
	fmt.Println("本次支出金额")
	fmt.Scanln(&this.money)
	if this.money > this.balance {
		fmt.Printf("余额不足:%v无法支出 \n当前余额:%v\n",this.money,this.balance)
		// break
	this.flag = true
	}
	this.balance -= this.money
	fmt.Println("本次支出说明")
	fmt.Scanln(&this.note)
	//进行引用"收支\t账户金额\t收支金额\t说 明\n"
	this.details += fmt.Sprintf("\n收入\t%v\t\t%v\t%v", this.balance,this.money,this.note)
}
//将退出系统写成一个方法，和*FamilyAccount绑定
func (this *FamilyAccount) Exit() {
	fmt.Println("你确定要退出吗?y/n")
				choice := ""
				for {
					fmt.Scanln(&choice)
					if choice == "y" || choice == "n" {
						break
					}
					fmt.Println("你输入的有误，请重新输入  y/n")
				}
				if choice == "y" {
				this.loop = false
				}
			}
//显示主菜单
func (this *FamilyAccount) MainMenu() {
	for {
		fmt.Println("----------家庭收支记账软件----------")
		fmt.Println("          1. 收支明细")
		fmt.Println("          2. 登记收入")
		fmt.Println("          3. 登记指出")
		fmt.Println("          4. 退出软件")
		fmt.Print("请选择(1-4)")
		fmt.Scanln(&this.key)
		switch this.key {
			case "1":
				this.ShowDetails()
			case "2":
				this.income()
			case "3":
				this.pay()
			case "4","exit":
				this.Exit()
			default:
				fmt.Println("输入错误，请重新输入")
			}
		if !this.loop {
			break
			}
		}
		fmt.Println("退出程序")
	}
```

familyaccount/main/main.go

```go
package main
import (
	"gocode/gw/project12/utils"
	"fmt"
)
func main() {
	fmt.Println("这个是面向对象的方式完成~~")
	utils.NewFamilyAccount().MainMenu()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project12\damo01>go run main.go
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

当前没有收支明细...来一笔吧!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)2
本次收入金额
1000
本次收入说明
红包来啦!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

收支    账户金额        收支金额        说 明

收入    11000           1000    红包来啦!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)3
登记指出
本次支出金额
20
本次支出说明
买烟
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)1
----------当前收支明细记录----------

收支    账户金额        收支金额        说 明

收入    11000           1000    红包来啦!
收入    10980           20      买烟
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记指出
          4. 退出软件
请选择(1-4)4
你确定要退出吗?y/n
y
退出程序
```

### 12.4.3 对项目的扩展功能的练习

- 对上面的项目完成一个转账功能
- 在使用该软件前，有一个登录功能，只有输入正确的用户名和密码才能操作。

familyaccount/utils

```
package utils

import (
	"fmt"
	"strings"
)

type FamilyAccount struct {
	// 声明一个变量，保存接收用户输入的选项
	key string
	// 声明一个变量，控制是否退出for
	loop bool
	// 定义账户的余额
	balance float64
	// 每次收支的金额
	money float64
	// 每次收支的说明
	note string
	// 定义个变量，记录是否有收支的行为
	flag bool
	// 收支的详细使用字符串来记录
	// 当有收支时，只需要对 details 进行拼接处理即可
	details string
	// 用户名和密码
	username string
	password string
	// 登录状态
	loginStatus bool
}

// 编写工厂函数的构造方法，返回一个 *FamilyAccount 实例
func NewFamilyAccount(username, password string) *FamilyAccount {
	return &FamilyAccount{
		key:         "1",
		loop:        true,
		balance:     0.00,
		money:       0,
		note:        "",
		flag:        false,
		details:     "收支\t账户金额\t收支金额\t说明",
		username:    username,
		password:    password,
		loginStatus: false,
	}
}

// 登录功能
func (this *FamilyAccount) login() {
	fmt.Println("请输入用户名:")
	fmt.Scanln(&this.username)
	fmt.Println("请输入密码:")
	fmt.Scanln(&this.password)
	if this.username == "刘振华" && this.password == "123.com" {
		fmt.Println("登录成功！")
		this.loginStatus = true
	} else {
		fmt.Println("用户名或密码错误，退出程序！")
		this.loop = false
	}
}

// 将显示明细写一个方法
func (this *FamilyAccount) ShowDetails() {
	fmt.Println("----------当前收支明细记录----------\n")
	if this.flag {
		fmt.Println(this.details)
	} else {
		fmt.Println("当前没有收支明细...来一笔吧!")
	}
}

// 将登记收入写成一个方法，和 *FamilyAccount 绑定
func (this *FamilyAccount) income() {
	if !this.loginStatus {
		fmt.Println("请先登录！")
		return
	}

	fmt.Println("本次收入金额")
	fmt.Scanln(&this.money)
	this.balance += this.money
	fmt.Println("本次收入说明")
	fmt.Scanln(&this.note)
	// 进行引用"收支\t账户金额\t收支金额\t说明\n"
	this.details += fmt.Sprintf("\n收入\t%v\t\t%v\t%v", this.balance, this.money, this.note)
	this.flag = true
}

// 将登记支出写成一个方法，和 *FamilyAccount 绑定
func (this *FamilyAccount) pay() {
	if !this.loginStatus {
		fmt.Println("请先登录！")
		return
	}

	fmt.Println("登记支出")
	fmt.Println("本次支出金额")
	fmt.Scanln(&this.money)
	if this.money > this.balance {
		fmt.Printf("余额不足:%v无法支出 \n当前余额:%v\n", this.money, this.balance)
		// break
		this.flag = true
	}
	this.balance -= this.money
	fmt.Println("本次支出说明")
	fmt.Scanln(&this.note)
	// 进行引用"收支\t账户金额\t收支金额\t说明\n"
	this.details += fmt.Sprintf("\n支出\t%v\t\t%v\t%v", this.balance, this.money, this.note)
}

// 转账功能
func (this *FamilyAccount) transfer() {
	if !this.loginStatus {
		fmt.Println("请先登录！")
		return
	}

	var targetAccount string
	fmt.Println("请输入对方账户:")
	fmt.Scanln(&targetAccount)
	if targetAccount == "" {
		fmt.Println("对方账户不能为空")
		return
	}

	var transferAmount float64
	fmt.Println("请输入转账金额:")
	fmt.Scanln(&transferAmount)
	if transferAmount <= 0 {
		fmt.Println("转账金额必须大于0")
		return
	}

	// 检查余额是否足够
	if transferAmount > this.balance {
		fmt.Printf("余额不足:%v无法转账 \n当前余额:%v\n", transferAmount, this.balance)
		return
	}

	// 执行转账
	this.balance -= transferAmount
	// 记录转账详情
	transferNote := fmt.Sprintf("\n转账\t%v\t\t%v\t%v", this.balance, transferAmount, "转账给"+targetAccount)
	this.details += transferNote
	fmt.Printf("转账成功！余额：%v\n", this.balance)
}

// 将退出系统写成一个方法，和 *FamilyAccount 绑定
func (this *FamilyAccount) Exit() {
	fmt.Println("你确定要退出吗?y/n")
	choice := ""
	for {
		fmt.Scanln(&choice)
		if strings.ToLower(choice) == "y" || strings.ToLower(choice) == "n" {
			break
		}
		fmt.Println("你输入的有误，请重新输入  y/n")
	}
	if strings.ToLower(choice) == "y" {
		this.loop = false
	}
}

// 显示主菜单
func (this *FamilyAccount) MainMenu() {
    for {
        if !this.loop {
            break
        }

        // 如果未登录，先执行登录操作
        if !this.loginStatus {
            this.login()
            // 如果登录失败，退出程序
            if !this.loginStatus { //或则this.flag {
                break
            }
        }

        fmt.Println("----------家庭收支记账软件----------")
        fmt.Println("          1. 收支明细")
        fmt.Println("          2. 登记收入")
        fmt.Println("          3. 登记支出")
        fmt.Println("          4. 转账功能")
        fmt.Println("          5. 退出软件")
        fmt.Print("请选择(1-5): ")
        fmt.Scanln(&this.key)

        switch this.key {
        case "1":
            this.ShowDetails()
        case "2":
            this.income()
        case "3":
            this.pay()
        case "4":
            this.transfer()
        case "5", "exit":
            this.Exit()
            if !this.loop {
                break
            }
        default:
            fmt.Println("输入错误，请重新输入")
        }
    }
    fmt.Println("退出程序")
}
```

familyaccount/main

```go
package main

import (
	"fmt"
	"gocode/gw/project12/utils"
)

func main() {
	fmt.Println("这个是面向对象的方式完成~~")
	// Provide your username and password when creating a new FamilyAccount
	utils.NewFamilyAccount("your_username", "your_password").MainMenu()
}
```

```cmd
E:\go\goproject\src\gocode\gw\project12\familyaccount\main>go run main.go
这个是面向对象的方式完成~~
请输入用户名:
liuzhenhua
请输入密码:
123.com
用户名或密码错误，退出程序！
退出程序

E:\go\goproject\src\gocode\gw\project12\familyaccount\main>go run main.go
这个是面向对象的方式完成~~
请输入用户名:
刘振华
请输入密码:
123.com
登录成功！
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 1
----------当前收支明细记录----------

当前没有收支明细...来一笔吧!
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 2
本次收入金额
1000
本次收入说明
买帽子
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 1
----------当前收支明细记录----------

收支    账户金额        收支金额        说明
收入    1000            1000    买帽子
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 3
登记支出
本次支出金额
500
本次支出说明
买烟
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 4
请输入对方账户:
刘润阳
请输入转账金额:
500
转账成功！余额：0
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
请选择(1-5): 1
----------当前收支明细记录----------

收支    账户金额        收支金额        说明
收入    1000            1000    买帽子
支出    500             500     买烟
转账    0               500     转账给刘润阳
----------家庭收支记账软件----------
          1. 收支明细
          2. 登记收入
          3. 登记支出
          4. 转账功能
          5. 退出软件
```

# 第13章项目2-客户信息关系系统

## 13.1项目需求分析

1. 模拟实现基于文本界面的《客户信息管理软件》
2. 该软件能够实现对客户对象的插入、修改和删除（用切片实现），并能够打印客户明细表

## 13.2项目的界面设计

- 主菜单界面

  ![image-20231123164622602](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164622602.png?raw=true)

- 添加客户界面

  ![image-20231123164642483](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164642483.png?raw=true)

- 修改客户界面

  ![image-20231123164657428](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164657428.png?raw=true)

- 删除客户界面

  ![image-20231123164708331](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164708331.png?raw=true)

- 客户列表界面

  ![image-20231123164727362](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164727362.png?raw=true)

## 13.3客户关系管理系统和程序框架图

![image-20231123164808564](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123164808564.png?raw=true)

## 13.4项目功能实现-显示主菜单和完成退出软件功能

- 功能的说明
  - 当用户运行程序时，可用看到主菜单，当输入5时，可用退出该软件
- 思路分析
  - 编写customerView，另外可以把customer.go和custerService.go写上

![image-20231123172904157](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123172904157.png?raw=true)

- 代码实现

  - customerManage/model/customer.go

    ```go
    package model
    //声明一个Customer结构体，表示一个客户信息
    type Customer struct {
    	Id int
    	Name string
    	Gender string
    	Age int
    	Phone string
    	Email string
    }
    //使用工厂模式，返回一个Customer的实例
    func NewCustomer(id int, name string, gender string,
    	 age int, phone string, email string) *Customer {
    	return &Customer{
    		Id : id,
    		Name : name,
    		Gender : gender,
    		Age : age,
    		Phone : phone,
    		Email : email,	
    	}
    }
    ```

  - customerManage/service/customerService.go

    ```go
    package service
    import (
    	"gocode/gw/project12/customerManage/model"
    )
    //该CustomerService，完成对Customer的操作，包括
    //增删改查
    type 该CustomerService struct {
    	customers []model.Customer
    	//声明一个字段，表示当前切片含有多少个用户
    	//该字段后面，还可以作为新客户的id+1
    	customerNum int
    }
    ```

  - customerManage/view/customerView.go

    ```go
    package main
    import (
    	"fmt"
    )
    type customerView struct {
    	//定义必要字段
    	key string //接收用户输入
    	loop bool //表示是否循环的显示主菜单
    }
    //显示主菜单
    func (this *customerView) mainMenu() {
    	for {
    		fmt.Println("--------客户信息管理软件--------")
    		fmt.Println("        1.添 加 客 户")
    		fmt.Println("        2.修 改 客 户")
    		fmt.Println("        3.删 除 客 户")
    		fmt.Println("        4.客 户 列 表")
    		fmt.Println("        5.退    出")
    		fmt.Println("请选择(1-5):")
    		fmt.Scanln(&this.key)
    		switch this.key {
    		case "1":
    			fmt.Println("添 加 客 户")
    		case "2":
    			fmt.Println("修 改 客 户")
    		case "3":
    			fmt.Println("删 除 客 户")
    		case "4":
    			fmt.Println("客 户 列 表")
    		case "5":
    			this.loop = false
    		default:
    			fmt.Println("输入错误，请重新输入")
    		}
    		if !this.loop {
    			break
    		}	
    	}
    	fmt.Println("你退出了客户关系管理系统...")
    }
    func main () {
    	//在main函数中，创建一个customerView，并运行显示主菜单
    	customerView := customerView{
    		key :"",
    		loop :true,
    	}
    	//显示主菜单
    	customerView.mainMenu()
    }
    ```

    ```cmd
    E:\go\goproject\src\gocode\gw\project12\customerManage\view>go run customerView.go
    --------客户信息管理软件--------
            1.添 加 客 户
            2.修 改 客 户
            3.删 除 客 户
            4.客 户 列 表
            5.退    出
    请选择(1-5):
    ```

## 13.5项目功能实现-完成显示客户列表的功能

- 功能说明

  ![image-20231123221151775](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123221151775.png?raw=true)

- 思路分析

  ![image-20231123221215109](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123221215109.png?raw=true)

- 代码实现

customerManager/model/customer.go



## 13.6项目功能实现-添加用户的功能

- 功能说明

  ![image-20231123224036324](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123224036324.png?raw=true)

- 思路分析
  - ![image-20231123224058223](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123224058223.png?raw=true)

## 13.7项目功能实现-完成删除用户的功能

- 功能说明

  ![image-20231123225907660](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123225907660.png?raw=true)

- 思路分析![image-20231123225922851](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231123225922851.png?raw=true)

## 13.8项目功能实现-完善退出确认功能

- 功能说明：
  - 要求用户在退出时提示"确认是否退出(Y/N)"，用户必须输入y/n，否则循环提示。
- 思路分析
  - 需要编写customerView.go
- 代码实现



## 13.9客户关系管理系统

![image-20231124095700290](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231124095700290.png?raw=true)

# 第十四章文件操作

## 14.1文件的基本介绍

- 文件的概念

  - 文件，对我们并不陌生，文件是数据源(保存数据的地方)的一种，比如大家经常使用的word文档.txt文件，execl文件。文件最主要的作用就是保护数据，它既可以保存一张图片，也可以保存视频，声音等。

- 输入流和输出流

  ![image-20231124100025440](https://github.com/liuzhenhua1223/Image/blob/master/CCEimage/image-20231124100025440.png?raw=true)

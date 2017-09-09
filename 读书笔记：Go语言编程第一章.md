# Go语言初始
## 1.1Go语言简史
虽然Go语言的历史很短，但是只要记住一点就够了，它是由google发起的，有好几个大牛编写的就可以了。

---

> 
Go语言的主要作者。
 肯·汤普逊（Ken Thompson，http://en.wikipedia.org/wiki/Ken_Thompson）：设计了B语言
>
和C语言，创建了Unix和Plan 9操作系统，1983年图灵奖得主，Go语言的共同作者。
 罗布·派克（Rob Pike，http://en.wikipedia.org/wiki/Rob_Pike）：Unix小组的成员，参与Plan
9和Inferno操作系统，参与 Limbo和Go语言的研发，《Unix编程环境》作者之一。
>
 罗伯特·格里泽默（Robert Griesemer）：曾协助制作Java的HotSpot编译器和Chrome浏览
器的JavaScript引擎V8。
>
 拉斯· 考克斯（Russ Cox，http://swtch.com/~rsc/）：参与Plan 9操作系统的开发，Google Code
Search项目负责人。
>
 伊安·泰勒（Ian Lance Taylor）：GCC社区的活跃人物，gold连接器和GCC过程间优化LTO
的主要设计者，Zembu公司的创始人。
>
 布拉德·菲茨帕特里克（Brad Fitzpatrick，http://en.wikipedia.org/wiki/Brad_Fitzpatrick）：
LiveJournal的创始人，著名开源项目memcached的作者。

## 1.2Go语言的特性
虽然到目前为止还不知道为啥有这些特性，但勉强先记录一下吧
- 自动回收机制（GC）
- 丰富的内置类型（切片、map等）
- 函数多返回值（这个点比较使用）
- 错误处理
- 匿名函数和闭包（一直听说但一直没真正理解，后续重点学习并尝试使用）
- 类型与接口（貌似和类对象等有关的功能吧，不了解重点学习）
- 并发编程（作为希望在服务器方向编程的我，这个貌似也是重点哦）
- 反射
- 语言交互性（听说有cgo，可以直接写c代码，作为一个C程序我喜欢）

## 1.3第一个Go程序

```
package main

import "fmt"

func main(){
	fmt.Printf("hello world.你好，世界！")
}

```
作为一个通用的起点，我也尝试写了一个“hello world”，
看起来很简单啊！
知识点：
- package 指定此文件的包名。
- import 要引用的包名。此文件中需要引入fmt包中的Printf函数，故需要引入此包名。与C语言不同之处在于**如果不引用此包的函数则不能引用此包，编译器会报错**。有一个原因就是Go工程的依赖关系不用通过makefile等工程管理工具实现，自身通过文件中的引用关系就能够确定依赖关系。所以此处也不能随便引用一个包名
- func命名一个函数的关键字，前边提到的函数可以有多个返回值，通过返回值列表返回
```
func 函数名(参数列表)(返回值列表) {
// 函数体
}
```
- main函数一个程序中只能有一个，且main函数不能有返回值和参数，参数通过os.Args传递。
- 代码块注释包括/* 注释块 */， //注释行

### 1.3.2编译准备环境
多说无益，现在Go语言的安装包已经足够强大，直接下载windows版本安装即可，根本就不是自己手动设置环境变量了。
-检查是否安装好go环境命令：go version

```
C:\Users\my>go version
go version go1.9 windows/amd64
```
## 1.3.3 编译程序
1. go的编译命令进入go文件同级目录
2. 执行go run xxx.go即可

```
E:\001\GoStudy>go run TestGo.go
hello world.
```
## 1.4 开发工具选择
我使用的是pyCharm+go插件，其他的大家还是自行百度好啦！
不过此处多罗嗦一句：
1. 下载安装pyCharm后，进入到File->settings->Plugins
2. 选择Browse Repositories
3. 选择Manage Repositories 添加 https://plugins.jetbrains.com/plugins/alpha/5047
4. 再搜索Go插件，安装即可。（记住第3步很重要，否则提示下载失败）

## 1.5 工程管理
简单点说就是：Go语言不用你去关心依赖关系等，只要你写的程序中import引用关系正确，Go就自动帮你指定了依赖关系，不用做特殊的Makefile的文件啦！这点貌似很实用。
Go语言编程书中显示的工程结构记录一下：

```

<calcproj>
├─<src>
    ├─<calc>
        ├─calc.go
    ├─<simplemath>
        ├─add.go
        ├─add_test.go
        ├─sqrt.go
        ├─sqrt_test.go
├─<bin>
├─<pkg>＃包将被安装到此处

```
## 1.6问题追踪调试

据说go语言编程编译后的程序能够直接通过gdb调试，还未做实验，值得期待！


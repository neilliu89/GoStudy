# 第2章 顺序编程

## 2.1 变量
说到变量，首先要想到与变量相关的几个名词：
- 变量声明
- 变量赋值
- 变量初始化

此书也是从这几方面描述的，那我就来学习一下吧！
### 2.1.1 变量的声明
C语言的变量声明

```
int a, b, c;
```
GO 语言的变量声明

```
var v1 int
var v2 string
var v3 [10]int // 数组
var v4 []int // 数组切片
var v5 struct {
f int
}
var v6 *int // 指针
var v7 map[string]int // map，key为string类型，value为int类型
var v8 func(a int) int
```
> 特点
- var作为变量声明的关键字
- 变量类型放在了变量之后
- 声明语句没有分号结尾
- 为了方便声明多个变量Go语言也做了一些处理如下：
```
var (
v1 int
v2 string
)
```
- 可以省去多个var的定义，但换行是必不可少的，因为他是默认以换行作为结束的
- 同一行中多个相同类型变量声明如下：

```
var v1, v2, v3 int
```
### 2.1.2 变量初始化
变量初始化一般都是和变量的声明放在一起初始化
如C语言：

```
int a1 = 2；
int b1 = 3；
```
与C语言相比Go语言有个好处就是可以省去变量类型，Go语言可以根据你的赋值语句右边的值来决定变量类型。


```
var str1 string = "000" // 正确的使用方式1
var str2 = "123" // 正确的使用方式2，编译器可以自动推导出v2的类型
str3 := "321" // 正确的使用方式3，编译器可以自动推导出v3的类型

```
- **如果是被声明过的变量是不能使用第3种方式进行初始化的**

```
var str1 string
str1 := "1223"  //提示在：=符号左边不是一个新的变量
```
### 2.1.3 变量赋值
变量赋值和变量初始化还是有一定区别的。变量先声明，之后再赋值就是变量赋值
- 值得一提的是变量能够多重赋值，即同时赋值几个变量如下：

```
var str1 string = "000"
var str2 = "123"
str1, str2 = str2 , str1
fmt.Printf(str1)
fmt.Printf(str2)
//打印结果
//123000
```
- 从例子中可以看出str1与str2交换数据，不需要临时变量了，可以直接互换，这或许就是多重赋值的好处吧，其他的方便之处还有待总结。

### 2.1.4 匿名变量
匿名变量顾名思义就是没有名字
举例：

```
func getName()(firstName, secondName string){
	firstName = "ly"
	secondName = "ulysses"
	return "ly", "ulysses"
}
func main(){
	var str1 string
	_, str1 = getName()
	fmt.Printf(str1)
}

```
- **_**符号表示的就是一个匿名变量，函数在返回时可能返回多个返回值，但有些返回值可能根本不需要，那么我们不必非要定义一个变量存储，而是可以用匿名变量存储
- 匿名变量能够被赋值，但不能在后续作为表达式或者打印输出。

## 2.2 常量
常量在C语言中是用const定义的，初始化之后不可以被改动的值
- Go语言中常量是指在编译期间就已经知道不可改变的值

### 2.2.1 字面常量
第一次听说这个概念
- Go语言中字面常量是没有类型的，与C语言定义常量有所不同，当然C语言中没有字面常量一说。
- 只要这个常量在相应的类型范围内，则可以认为是这个类型的常量。

### 2.2.2 常量定义
- const关键字，用来给常量定义名称使用如：

```
const Pi float64 = 3.14159265358979323846
const zero = 0.0 // 无类型浮点常量
const (
size int64 = 1024
eof = -1 // 无类型整型常量
)
const u, v float32 = 0, 3 // u = 0.0, v = 3.0，常量的多重赋值
const a, b, c = 3, 4, "foo"
// a = 3, b = 4, c = "foo", 无类型整型和字符串常量
```
- 常量类型不一定非要指定

### 2.2.3预定义常量
- Go中的预定义常量包括true 、false、iota
- iota可被编译器修改的常量，在每个const关键字出现之后被重置

```
const ( // iota被重设为0
c0 = iota // c0 == 0
c1 // c1 == 1
c2 // c2 == 2
)
const (
a = 1 <<iota // a == 1 (iota在每个const开头被重设为0)
b // b == 2
c // c == 4
)
```
### 2.2.4枚举
- Go语言中没有枚举关键字
- 连续的定义几个相关联的const就可以认为是枚举类型，其实在C语言中我们通常可以用宏定义代替枚举类型也是可以的。

```
const (
Sunday = iota
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
numberOfDays // 这个常量没有导出
)
```
- 此处有个知识点：除numberOfDays外其他的const都能被模块外部引用，而numberOfDays不能，因为他是以小写字母开头。
- 凡是以大写字母开头的全局变量或者函数或者常量才能被外部模块访问，否则都是模块内部才能访问。
- 


## 2.3 类型
- 基础类型
    - 布尔类型： bool 。
    - 整型： int8 、 byte 、 int16 、 int 、 uint 、 uintptr 等。
    - 浮点类型： float32 、 float64 。
    - 复数类型： complex64 、 complex128 。
    - 字符串： string 。
    - 字符类型： rune 。
    - 错误类型： error 。
- 复合类型
    - 指针（pointer）
    - 数组（array）
    - 切片（slice）
    - 字典（map）
    - 通道（chan）
    - 结构体（struct）
    - 接口（interface）

### 2.3.1 布尔类型

- 布尔类型与C语言有些区别不能和其他类型强转 bool类型的值只能是true false

```
var b bool
b = 1 // 编译错误
b = bool(1) // 编译错误
```
### 2.3.2 整型


| 类型           | 字节   | 范围                                       |
| ------------ | ---- | ---------------------------------------- |
| int8         | 1    | 128 ~ 127                                |
| uint8（即byte） | 1    | 0 ~ 255                                  |
| int16        | 2    | 32 768 ~ 32 767                          |
| uint16       | 2    | 0 ~ 65 535                               |
| int32        | 4    | 2 147 483 648 ~ 2 147 483 647            |
| uint32       | 4    | 0 ~ 4 294 967 295                        |
| int64        | 8    | 9 223 372 036 854 775 808 ~ 9 223 372 036 854 775 807 |
| uint64       | 8    | 0 ~ 18 446 744 073 709 551 615           |
| int          | 平台相关 | 平台相关                                     |
| uint         | 平台相关 | 平台相关                                     |
| uintptr      | 同指针  | 在32位平台下为4字节，64位平台下为8字节                   |

- int与int32等认为是不同的类型，不能直接转换，需要使用强制类型转换

```
var value2 int32
value1 := 64 // value1将会被自动推导为int类型
value2 = value1 // 编译错误
value2 = int32(value1) // 编译通过
```
- 尽量不要进行强转，因为可能出现数据被截断和值溢出
- 数值运算(+-*%) 与比较运算(== != >= <= > <)与C语言语法一致，**但不同类型之间不能同步比较运算符进行比较**
- ​
```
var i32 int32 = 1
i := 2
if i != i32 {
	fmt.Printf("error")
}
//invalid operation: i != i32 (mismatched types int and int32)
```
- 位运算支持如下语法

| 运算     | 含义   | 样例                 |
| ------ | ---- | ------------------ |
| x << y | 左移   | 124 << 2 // 结果为496 |
| x >> y | 右移   | 124 >> 2 // 结果为31  |
| x ^ y  | 异或   | 124 ^ 2 // 结果为126  |
| x & y  | 与    | 124 & 2 // 结果为0    |
| x \| y | 或    | 124 \| 2 // 结果为126 |
| ==^x== | 取反   | ^2 // 结果为3         |
### 2.3.3 浮点型
- Go中没有double类型，浮点型float32相当于float类型，float64相当于double类型
- **浮点类型不能使用==判断是否相等**，应该使用如下方法：

```
import "math"
// p为用户自定义的比较精度，比如0.00001
func IsEqual(f1, f2, p float64) bool {
return math.Abs(f1- f2) < p
}

Go语言编程书籍中使用Fdim函数，但我的版本中没有此函数，存在Dim函数但与预期不同
```
- Printf函数接受一个str参数后边是不定参，如果参数过多会出现%!(EXTRA 多余参数 )的字符
- bool类型打印为%t
### 2.3.4 复数类型
用不到就不写啦
-  如果以后遇到，查阅math/cmplx 标准库

### 2.3.5 字符类型
- Go中支持两种字符类型
- byte 就是uint8 ，代表UTF-8的单个字节
- rune代表单个Unicode字符
- Go提供Unicode与UTF-8的转换

### 2.3.6 字符串
- 字符串是Go语言中的基本类型，与C语言不同
- 字符串被赋值之后每个元素的值是不能被单独改变的，但数组的每个元素是可以被单独改变

```
var str5 string
str5 = "helloworld"
str5 = "xxx"    
str5[2] = '1'   //编译错误cannot assign to str5[2]
fmt.Printf(str5)
```
1. 字符串操作

| 运 算    | 含 义   | 样 例                            |
| ------ | ----- | ------------------------------ |
| x + y  | 字符串连接 | "Hello" + "123" // 结果为Hello123 |
| len(s) | 字符串长度 | len("Hello") // 结果为5           |
| s[i]   | 取字符   | "Hello" [1] // 结果为'e'          |

2. 字符串遍历

- 以字节遍历
```
var str5 string
str5 = "hello中国"
n := len(str5)
for i:=0; i< n; i++{
	fmt.Println(i, str5[i])
}

//输出
0 104
1 101
2 108
3 108
4 111
5 228
6 184
7 173
8 229
9 155
10 189
```
    - 一个中文字符占3个字节
- 以Unicode字符进行遍历

```
var str5 string
str5 = "hello中国"

for i, ch := range str5{
	fmt.Println(i, ch)
}

0 104
1 101
2 108
3 108
4 111
5 20013
8 22269

```
- for range应该是固定用法，遍历str中的所有字符

### 2.3.7 数组
- 数组定义形式
```
ar1 := [5] int{1,2,3,4}
var ar2 [2] string
var ar3 [2] struct {}
var ar4 [2] *float32
var ar5 [2][4] int
var ar6 [2][2][3] float64
ar7 := [...] int{1,2,3,3}   //根据初始值来指定数组长度
fmt.Println(ar1)
fmt.Println(ar2)
fmt.Println(ar3)
fmt.Println(ar4)
fmt.Println(ar5)
fmt.Println(ar6)
fmt.Println(ar7)
//打印结果依次如下：
[1 2 3 4 0]
[ ]
[{} {}]
[<nil> <nil>]
[[0 0 0 0] [0 0 0 0]]
[[[0 0 0] [0 0 0]] [[0 0 0] [0 0 0]]]
```
- 指针默认初始化nil
- float32 float64 默认是0
- 定义采用右结合的方式，方便理解
- 数组中对应的元素个数也是类型的一部分，即拥有不同元素个数的数组是不能比较的

```

```

1. 数组访问
- 通过获取数组元素个数来进行for循环，len函数。
- 数组的长度定义之后不可变更

```
ar1 := [5] int{1,2,3,4}
ar1len := len(ar1)

for i := 0; i< ar1len; i++{
	fmt.Printf("%d,", ar1[i])
}

输出：1,2,3,4,0,
```
- 通过range关键字访问，range可以返回容器的下标索引以及索引对应的内容，如果熟悉python的同学知道和python的range类似 

```
ar1 := [5] int{1,2,3,4}
for i, v := range ar1{
		fmt.Printf("%d, %d \n", i, v)
	}
}
输出：
0, 1 
1, 2 
2, 3 
3, 4 
4, 0 
```

2. 值类型
- 在Go语言中，所有的值类型在参数传递时，都是传递的副本而不是本身
  举例：

```
func changeArray(ar [5]int) {
	ar[0] = 100
	fmt.Println(ar)
}
func main{
    ar1 := [5] int{1,2,3,4}
    
    changeArray(ar1)
    fmt.Println(ar1)
}
输出：
[100 2 3 4 0]
[1 2 3 4 0]
```

### 2.3.8数组切片
数组切片数据结构抽象为如下：
- 一个指向原生数组的指针
- 数组切片中的元素的个数
- 数组切片已分配的存储空间

1. 通过数组创建切片
- 使用数组创建切片对应的切片存储空间不能指定
- 通过例子查看已数组创建切片方式，查看创建的切片的存储空间

```
ar1 := [5] int{1,2,3,4}
var slice1 []int = ar1[:4]
var slice2 []int = ar1[:]
var slice3 []int = ar1[2:]
fmt.Println(slice1, len(slice1), cap(slice1))
fmt.Println(slice2, len(slice2), cap(slice2))
fmt.Println(slice3, len(slice3), cap(slice3))
输出：
[1 2 3 4] 4 5
[1 2 3 4 0] 5 5
[3 4 0] 3 3     //此处的切片存储空间为3，可以推测切片的存储空间为指定数组的其实位置到数组结束的位置大小

```
2. 直接创建切片
- 通过内置函数make创建切片，创建时可以指定创建切片的元素个数以及切片的容量
- 创建数组时[]中存在数值指定数组元素个数，而切片不能填写数值
```
slice4 := make([]int, 5)        //未指定容量，则容量与元素个数相同
slice4 = make([]int, 5, 10)     //指定元素个数为5，容量为10
slice5 := []int{1,2,3,4,5}      //不使用make，直接赋值也是可以创建slice的
fmt.Println(slice4, len(slice4), cap(slice4))
fmt.Println(slice5, len(slice5), cap(slice5))
```
3. 元素的遍历 
- 遍历方式与数组遍历方式相同存在两种方式，不在赘述
4. 动态增减元素
- 如果初始创建了容量为10的数组，则在向slice中添加元素时超过了容量大小，则系统会自动分配一个新的空间，此空间大小为原空间大小的2倍
- append函数可以向slice中添加元素

```
slice4 = make([]int, 5, 10)
slice5 := []int{1,2,3,4,5}
slice4 = append(slice4, 4,5,6)
fmt.Println(slice4, len(slice4), cap(slice4))
slice5 = append(slice5, slice4...)      //append只能接受slice中元素相同类型，且是一个不定长参数，所以需要使用...将slice4打散
fmt.Println(slice5, len(slice5), cap(slice5)) 
输出：
[0 0 0 0 0 4 5 6] 8 10
[1 2 3 4 5 0 0 0 0 0 4 5 6] 13 14   //资源不够每次分配2倍实在添加个数在两倍之后容量能存储的情况下
```
5. 基于切片的切片
- 原则：新切片的返回只要不超过原切片的范围都是可以获取切片元素的，只是超出元素个数的内容被赋值为0

```
slice4 := make([]int, 5, 10)
slice4[4] = 1
slice5 := slice4[3:8]
fmt.Println(slice4, len(slice4), cap(slice4))
fmt.Println(slice5, len(slice5), cap(slice5))
输出
[0 0 0 0 1] 5 10    //slice4 1之后没有元素
[0 1 0 0 0] 5 7     //能够取到slice4之后的容量，并将此位置初始化为0
```

6. 内容复制
- 内容复制原则：不会复制超过切片元素个数的长度

```
slice1 := []int{1, 2, 3, 4, 5}
slice2 := []int{5, 4, 3}
copy(slice2, slice1) // 只会复制slice1的前3个元素到slice2中
copy(slice1, slice2) // 只会复制slice2的3个元素到slice1的前3个位置
```

### 2.3.9 map
- 简单说就是键值对key：value，key必须是基本类型，value可以是任何类型
- 其他注意事项通过例子学习
```
type Person struct{
	ID string
	Name string
	Address string
}

var personDB map[string] Person //map的声明
personDB = make(map[string] Person)     //map初始化，除了用make之外也能直接初始化
//m1:=map[int]string{1:"a",2:"b",3:"c",4:"d",5:"e"}

personDB["12345"] = Person{"12345", "Tom", "101"}   //向map中添加元素
personDB["54321"] = Person{"54321", "Mot", "001"}

person, ok := personDB["12345"]                     //查询map中的元素，通过key
if ok{
	fmt.Println("Found Person " , ok, person.Name)
	delete(personDB, "12345")                       //删除map中指定key的元素，personDB必须不能为nil，即执行过make
}else{
	fmt.Println("Can not find person with ID 12345")
}
```
## 2.4流程控制
### 2.4.1 条件语句
- 关键字 if 、else 和else if
- 与C语言不同条件语句不需要使用括号将条件包含起来 () ；
- 无论语句体内有几条语句，花括号 {} 都是必须存在的；这点在很多
  公司的编程规范中也对C程序这样要求
- 左花括号 { 必须与 if 或者 else 处于同一行
- 在 if 之后，条件语句之前，**可以添加变量初始化语句**，使用;间隔
- **此句错误答案是可以的**：~~在有返回值的函数中，不允许将“最终的” return 语句包含在 if...else... 结构中，
  否则会编译失败：~~

```
i := 10
fmt.Println(example(i))

func example(x int) int {
	if x == 0 {
		return 5
	} else {
		return x
	}
}
输出：
10
```
### 2.4.2 选择语句
- 关键字 switch 、case 、fallthrough、select（不懂channel再了解）
- 左花括号 { 必须与 switch 处于同一行；
- 条件表达式不限制为常量或者整数，比C语言方便很多
- 单个 case 中，可以出现多个结果选项 ，例如：
```
switch {
    case 0 <= Num && Num <= 3:
        fmt.Printf("0-3")
    case 4 <= Num && Num <= 6:
        fmt.Printf("4-6")
    case 7 <= Num && Num <= 9:
        fmt.Printf("7-9")
}
```
- 与C语言等规则相反，Go语言不需要用 break 来明确退出一个 case。只有在 case 中明确添加 fallthrough 关键字，才会继续执行紧跟的下一个 case 
- 可以不设定 switch 之后的条件表达式，在此种情况下，整个 switch 结构与多个
  if...else... 的逻辑作用等同

### 2.4.3 循环语句
- 关键字 for range break continue
- Go中无while和do while，可以使用for实现，例如

```
sum := 0
for {   //与while功能一样
    sum++
    if sum > 100 {
        break
    }
}
```
- 与条件判断一样，for后边的表达式也不需要用（）括起来
- Go不支持多个以逗号分隔的赋值语句，但是可以使用Go的多重赋值实现例如

```
for i:= 10, j := 20; i < 15; i++,j++{
	fmt.Printf("%d, %d", i, j)
}
//syntax error: i := 10, j used as value

for i,j := 10, 20; i < 15; i,j = i+1, j+1{
	fmt.Printf("%d, %d", i, j)
}
输出
10, 2011, 2112, 2213, 2314, 24
```
- break、continue与C语言语法相同，但是支持跳转到指定的label 位置的循环处
  -
```
JLOOP:
for i:=1; i < 10; i++ {
	for j:=i+1; j < 10; j++ {
		break JLOOP
	}
}
```
- **break对应的跳出循环的标签一定要在for循环之上，且紧跟for语句，否则提示语法错误，标签未使用**

```
JLOOP:  //未紧跟for语句
sum := 100
for i:=1; i < 10; i++ {
	for j:=i+1; j < 10; j++ {
		break JLOOP
	}
}
JLOOP://未在for语句之前
```

### 2.4.4 跳转语句
- 关键字 goto
- 跳转指定标签位置
- ​

## 2.5 函数
- 函数的组成 关键字func 函数名称 参数列表 返回值 函数体和返回语句

### 2.5.1 函数的定义
### 2.5.2 函数调用
- 函数调用以大写字母开头的函数能够被外部调用，小写字母为内部函数

### 2.5.3 不定参数
- 可以接受不定参数形如：
- ...int 此处的...被称为语法糖
```
func printInt(args ...int){
	for i, v := range args{
		fmt.Println(i, v)
	}
}
```
- 如果想传入任何参数则使用interface关键字，虽然不懂接口是什么意思
- ​
```
func printInterface(args ... interface{}){
	for i, v := range args{
		fmt.Println(i, v)
	}
}
```
### 2.5.4 多返回值
- Go语言函数可以有多个返回值，如果调用者不需要这个返回值则可以使用匿名变量省略掉
- ​
```
func (file *File) Read(b []byte) (n int, err Error)
n, _ := f.Read(buf)
```
### 2.5.5 匿名函数与闭包
1. 匿名函数
- 看了好多遍但还是不知道具体的应用场景**以后遇到了在重新学习**
- 匿名函数如下：
```
func(a, b int, z float64) bool {
return a*b <int(z)
}
```
- 匿名函数可以直接调用，也可以赋值给变量
2. 闭包
  姑且先记录下来，虽然还不是很理解
---
- 基本概念
  闭包是可以包含自由（未绑定到特定对象）变量的代码块，这些变量不在这个代码块内或者
  任何全局上下文中定义，而是在定义代码块的环境中定义。要执行的代码块（由于自由变量包含
  在代码块中，所以这些自由变量以及它们引用的对象没有被释放）为自由变量提供绑定的计算环
  境（作用域）。
- 闭包的价值
  闭包的价值在于可以作为函数对象或者匿名函数，对于类型系统而言，这意味着不仅要表示
  数据还要表示代码。支持闭包的多数语言都将函数作为第一级对象，就是说这些函数可以存储到
  变量中作为参数传递给其他函数，最重要的是能够被函数动态创建和返回。
- Go语言中的闭包
  Go语言中的闭包同样也会引用到函数外的变量。闭包的实现确保只要闭包还被使用，那么
  被闭包引用的变量会一直存在

## 2.6 错误处理
**涉及到接口知识，后续再学习**


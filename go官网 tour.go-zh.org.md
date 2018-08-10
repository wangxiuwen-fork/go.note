

https://go-zh.org/doc/  1.Go编程语言

https://tour.go-zh.org/welco	me/1    2.go指南 中文教程

https://go-zh.org/doc/effective_go.html#   3. 实效 Go 编程

https://go-zh.org/ref/spec 4.Go编程语言规范 



`GOPATH` 环境变量指定了你的工作空间位置。它或许是你在开发Go代码时， 唯一需要设置的环境变量 

Go的可执行命令是静态链接的；在运行Go程序时，包对象无需存在。 

 

```go
//Go 的基本类型有 https://tour.go-zh.org/basics/11
bool
string
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr
byte // uint8 的别名
rune // int32 的别名
   // 表示一个 Unicode 码点
float32 float64
complex64 complex128
```

零值 https://tour.go-zh.org/basics/12
没有明确初始值的变量声明会被赋予它们的 零值。
零值是：
数值类型为 0，
布尔类型为 false，
字符串为 ""（空字符串）。



 defer 栈  后进先出  defer 语句会将函数推迟到外层函数返回之后执行。 

Go 切片：用法和本质  https://blog.go-zh.org/go-slices-usage-and-internals

切片 https://tour.go-zh.org/moretypes/7

#### 延伸阅读

[实效 Go 编程](https://go-zh.org/doc/effective_go.html) 包含了对 [切片](https://go-zh.org/doc/effective_go.html#切片)和 [数组](https://go-zh.org/doc/effective_go.html#数组)更深入的探讨； [Go 编程语言规范](https://go-zh.org/ref/spec)对 [切片类型](https://go-zh.org/ref/spec#Slice_types)和 [数组类型](https://go-zh.org/ref/spec#Array_types) 以及操作他们的内建函数（[len/cap](https://go-zh.org/ref/spec#Length_and_capacity)， [make](https://go-zh.org/ref/spec#Making_slices_maps_and_channels)和 [copy/append](https://go-zh.org/ref/spec#Appending_and_copying_slices)） 进行了定义。
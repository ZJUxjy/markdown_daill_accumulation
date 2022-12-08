# 变量
标准变量初始化格式
```go
var num int = 1
//var var_name var_type = ..
```
简化格式
```go
num:=1
```
编译器推导格式
```go
var num=1
```
多个变量同时初始化
```go
name, age :="Tom", 18
```
go语言中变量初始化但未被使用会报错

### 变量交换

```go
a:=1
b:=2
a,b=b,a
```
就可以进行交换

### 匿名变量

```go
func ReturnData() (int, int) { 
	return 10,20  
}
```

# 字符串
## 字符串拼接

1. 直接加
```
a+b
```
2.字节缓冲
```go
var c bytes.Buffer
c.WriteString(a)
c.WriteString(b)
ans:=c.String()
```

# 常量组

```go
const(
a=3.14
b
c
d=10
)
```
常量组不提供初始值，会直接用上行的值

# 映射

## map
```go
var mymap = map[string]int  {
   "jan":10,
   "jade":1,
}
fmt.Println(mymap)
//得到 map[jade:1 jan:10]
```

也可以使用make()函数进行初始化
```go
var mymap = make(map[string]int)  
mymap["jade"]=1
mymap["jan"]=10
fmt.Println(mymap)
//得到 map[jade:1 jan:10]
fmt.Println("map长度为：",len(mymap))
//得   map长度为： 2
```
遍历
```go
for k,v:=range mymap{
   fmt.Println(k,v)
}
//jade 1
//jan 10
```

## sync.Map
在1.9中提供了一个线程安全的map `sync.Map`，不用加锁就可以保证并发安全执行。

无须使用make创建

# 函数变量

匿名函数
```
func (参数列表) (返回参数列表) { 函数体 }
```
将匿名函数赋给变量
```go
f1 := func(data string){
	fmt.Println("Hello "+data)
}
f1("world!")
```

定义匿名函数同时进行调用
```go
func(data string){ 
	fmt.Println("Hello "+data) 
}("world!")
```
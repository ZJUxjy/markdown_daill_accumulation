# 函数模板

用例：
```
template <typename T>
void Swap(T &a,T&b){
    T &temp;
    temp = a;
    b=a;
    a=temp;
}
```

显示实例化：
```
//自定义结构体
struct job
{
    char name[40];
    double salary;
    int floor;
};
//显式实例化
template<> void Swap(job &j1,job &j2);
```
对于函数重载、函数模板和函数模板重载，选择函数的策略：
>1. 创建候选函数列表，包含于被调用函数的同名函数与模板函数
>2. 使用候选函数列表创建可行函数列表。
>3. 确定是否有最佳可行函数，若无则调用出错

匹配优先级：
>1. 完全匹配，常规函数优先于模板函数
>2. 提升转换，char->int，float->double
>3. 标准转换，int->char，long->double
>4. 用户定义的转换

---

# 可变参数模板

### c语言以宏方式实现可变参数
```
/*
用宏的方式
*/
#define add_1(a) a
#define add_2(a,b) a + b
#define add_3(a,b,c) a + add_2(b,c)

#define add(...)  PASTE(add_ ,GET_ARG_COUNT(__VA_ARGS__)) (__VA_ARGS__)
```

### c++可变参数
...在参数前面，代表定义参数包
...在参数后面，代表展开的语义

```cpp
//下面的args是一个参数包
template<class ...Args>
void ShowList(Args... args)
{
	cout << sizeof...(args) << endl; //获取参数包中参数的个数
}
```

递归展开参数包：
```cpp
//展开函数
template<class T, class ...Args>
void ShowList(T value, Args... args)
{
	cout << value << " "; //打印分离出的第一个参数
	ShowList(args...);    //递归调用，将参数包继续向下传
}
```

增加一个无参的递归终止函数
```cpp
//递归终止函数
void ShowList()
{
	cout << endl;
}
//展开函数
template<class T, class ...Args>
void ShowList(T value, Args... args)
{
	cout << value << " "; //打印分离出的第一个参数
	ShowList(args...);    //递归调用，将参数包继续向下传
}
```


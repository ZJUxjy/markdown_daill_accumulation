# std::function
>一个函数包装模板，可以包装*函数、函数指针、类成员函数指针*或*任意类型的函数对象*。
std::function对象可以被拷贝和转移，并且可以使用指定的调用特征来直接调用目标元素。当std::function对象未包裹任何实际的可调用元素，调用该std::function对象将抛出std::bad_function_call异常。

---

# 实际应用


引用头文件
```cpp
#include <iostream>
#include <functional>
using namespace std;
```

```cpp
//包装普通函数 || pack normal func
int normal_func(int i,int j) { return i-j; }
function<int(int,int)> f_normal = normal_func;
```

```cpp
//包装模板函数 || pack template func
template <class T>
T template_func(T i,T j) { return i-j; }
template <class T>
function<T(T,T)> f_template = template_func<T>;
```

```cpp
//包装lambda
auto lambda_func = [](int i,int j) { return i-j; };
function<int(int,int)> f_lambda = lambda_func;
```

```cpp
//包装参数模板lambda
template <class T>
T lambda_template_func = [](T i,T j) { return i-j; };
template <class T>
function<T(T,T)> f_template_lambda = lambda_template_func<T>;
```

```cpp
//包装函数对象
struct func_struct {
    int operator()(int i,int j) { return i-j; }
};
function<int(int,int)> f_struct = func_struct();
```

```cpp
//包装类静态成员函数
class func_static_struct {
public:
    static int func(int i, int j) { return i - j; }
};
function<int(int,int)> f_static_struct = &func_static_struct::func;
```

```cpp
//包装类对象成员函数
class func_struct_func {
public:
    int func(int i, int j) { return i - j; }
};
func_struct_func m;
function<int(int, int)> f_struct_func = 
	bind(&func_struct_func::func, &m, placeholders::_1, placeholders::_2);
```


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
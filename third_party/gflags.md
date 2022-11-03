# gflags
gflags是一种命令行解析工具，用于解析命令行可执行文件时传入的参数，

1. 定义flag
	用glfags定义一个flag：
```c
#include <gflags/gflags.h>
DEFINE_bool(big_menu, true, "Include 'advanced' options in the menu listing");
DEFINE_string(languages, "english,french,german",
              "comma-separated list of languages to offer in the 'lang' menu");
```
>DEFINE_string：C++string类型
>DEFINE_int32：32位整形
>DEFINE_int64：64位整形
>DEFINE_uint64：64位无符号整形
>DEFINE_double：double类型
>DEFINE_bool：bool类型

2. flags变量
用DEFINE宏定义的flag都可以像普通的变量一样进行调用，定义的变量是以FLAGS_为前缀，
3. 在其他文件中调用flag变量
````cpp
DECLARE_bool(big_menu); 
````
功能等价于
```cpp
extern FLAGS_big_menu; 
```

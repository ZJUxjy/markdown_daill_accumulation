
项目目录结构
```
├─.vscode
├─build
├─install
│  ├─bin
│  ├─include
│  └─lib
└─src
```
src下是源文件
```
PS C:\Users\94806\Documents\code\cmake\src> ls
    Directory: C:\Users\94806\Documents\code\cmake\src

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---          2022/11/15    16:53            397 CMakeLists.txt
-a---          2022/11/15    15:05            103 main.cpp
-a---          2022/11/15    15:09           4008 mylib.cpp
-a---          2022/11/15    15:09            700 mylib.hpp
```

cmake:
```
    Directory: C:\Users\94806\Documents\code\cmake

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----          2022/11/15    15:02                .vscode
d----          2022/11/15    16:55                build
d----          2022/11/15    11:50                install
d----          2022/11/15    11:17                src
-a---          2022/11/15    16:53            244 CMakeLists.txt
```

---

# 编译单个文件到可执行文件


首先在CMakeLists.txt中需要有
`cmake_minimum_required(VERSION 3.5 FATAL_ERROR)`
这句话指定了所需最小版本cmake，低于这个版本报错。

然后声明项目名称，支持的编程语言
```
project(test LANGUAGES CXX)
```

然后指示CMake创建一个新目标：可执行文件
```
add_executable(hello_world hello_world.cpp)
```
在hello_world.cpp同级目录下执行：
```
mkdir build
cd build
cmake ..
```

顺利的话，可以在build中找到可执行文件。

 **NOTE**: *_CMake语言不区分大小写，但是参数区分大小写_*

```
cmake -Bbuild
```
-Bbuild告诉cmake在当前目录下build文件夹下生成所有文件

## 切换生成器

```
cmake -G Ninja ..
```
使用-G切换生成器

## 静态库动态库

```
add_library(mylib 
mylib.hpp 
mylib.cpp)
```
windows下默认静态，当然也可以显式指出：
```
add_library(mylib STATIC
mylib.hpp 
mylib.cpp)
```

## 将库与可执行文件链接

```
target_link_libraries(main mylib)
```
如果不进行链接，会报no sympol。。。的错误。

## 进行编译

接下来是进行编译，
```bash
cmake --build build --config=Release --target=install
```

编译后的install：
```bash
install
├─bin
│      main.exe
│      mylib_shared.dll
│
├─include
│      mylib.hpp
│
└─lib
        mylib.lib
```

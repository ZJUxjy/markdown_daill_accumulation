`CMAKE_INSTALL_PREFIX` 


# 变量

下面这句设置了一个逻辑变量，值为OFF
```
set(USE_LIBRARY OFF)
```
把它的值打印出来：
```
message(STATUS "Compile sources into a library? ${USE_LIBRARY}")
```

下面展示了利用变量控制是编译成库+可执行文件还是 直接编译成一个可执行文件：
```cmake
set(USE_LIBRARY ON)
list(APPEND _sources mylib.hpp mylib.cpp)
if(USE_LIBRARY)
    add_library(mylib ${_sources})
    add_executable(main main.cpp)
    target_link_libraries(main mylib)
else()
add_executable(main main.cpp ${_sources})
endif()
```

---

## 向用户显示选项

将上面的`set(USE_LIBRARY ON)`替换为`option(USE_LIBRARY "Compile sources into a library?" OFF)`(默认 OFF)

编译时设置为ON
```
cmake -D USE_LIBRARY=ON
```

---

## 指定编译器


`cmake -D CMAKE_CXX_COMPILER=clang++ `

指定msvc编译器编译：
`cmake .. -G"Visual Studio 12 2017 Win64"`



---

## 切换构建类型

`cmake -D CMAKE_BUILD_TYPE=Debug ..`

同时构建Release和Debug：
`cmake -D CMAKE_CONFIGURATION_TYPES="Release;Debug"`

---

## 检测操作系统

```
if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
	message(STATUS "Configuring on/for Linux")
```

对目标系统进行预处理

cpp代码：

```c++
#include <cstdlib>
#include <iostream>
#include <string>

std::string say_hello() {
#ifdef IS_WINDOWS
  return std::string("Hello from Windows!");
#elif IS_LINUX
  return std::string("Hello from Linux!");
#elif IS_MACOS
  return std::string("Hello from macOS!");
#else
  return std::string("Hello from an unknown system!");
#endif
}

int main() {
  std::cout << say_hello() << std::endl;
  return EXIT_SUCCESS;
}
```

通过定义以下目标编译定义，让预处理器知道系统名称:

   ```cmake
   if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
     target_compile_definitions(hello-world PUBLIC "IS_LINUX")
   endif()
   if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
     target_compile_definitions(hello-world PUBLIC "IS_MACOS")
   endif()
   if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
     target_compile_definitions(hello-world PUBLIC "IS_WINDOWS")
   endif()
   ```


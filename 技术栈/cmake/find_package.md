
1. 首先，定义CMake最低版本和项目名称。注意，这里不需要任何语言支持:

   ```cmake
   cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
   project(recipe-01 LANGUAGES NONE)
   ```

2. 然后，使用`find_package`命令找到Python解释器:

   ```cmake
   find_package(PythonInterp REQUIRED)
   ```

3. 然后，执行Python命令并捕获它的输出和返回值:

   ```cmake
   execute_process(
     COMMAND
     	${PYTHON_EXECUTABLE} "-c" "print('Hello, world!')"
     RESULT_VARIABLE _status
     OUTPUT_VARIABLE _hello_world
     ERROR_QUIET
     OUTPUT_STRIP_TRAILING_WHITESPACE
     )
   ```

4. 最后，打印Python命令的返回值和输出:

   ```cmake
   message(STATUS "RESULT_VARIABLE is: ${_status}")
   message(STATUS "OUTPUT_VARIABLE is: ${_hello_world}")
   ```

## 工作原理

`find_package`是用于发现和设置包的CMake模块的命令。这些模块包含CMake命令，用于标识系统标准位置中的包。CMake模块文件称为` Find<name>.cmake`，当调用`find_package(<name>)`时，模块中的命令将会运行。

---

可以强制CMake，查找特定版本的包。例如，要求Python解释器的版本大于或等于2.7：`find_package(PythonInterp 2.7)`

可以强制满足依赖关系:

```cmake
find_package(PythonInterp REQUIRED)
```


---

软件包没有安装在标准位置时，CMake无法正确定位它们。用户可以使用CLI的`-D`参数传递相应的选项，告诉CMake查看特定的位置。Python解释器可以使用以下配置:

```shell
$ cmake -D PYTHON_EXECUTABLE=/custom/location/python ..
```

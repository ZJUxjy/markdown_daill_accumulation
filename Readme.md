此分支需要qt5依赖，目前仅支持ubuntu环境下gcc进行编译
[qt download)](https://download.qt.io/)

构建：CMakeLists.txt中`set(CMAKE_PREFIX_PATH $ENV{QTDIR})`这句指出了qt路径，可以将`$ENV{QTDIR}`替换为本地的qt绝对路径或者像我一样在系统ENV下创建一个QTDIR的系统变量。这是我本地的QTDIR路径：
```cmake
QTDIR=/home/jingyao/Qt5.12.0/5.12.0/gcc_64
```

将
```cmake
set(CMAKE_PREFIX_PATH $ENV{QTDIR})
```
替换为绝对路径：
```cmake
set(CMAKE_PREFIX_PATH /home/jingyao/Qt5.12.0/5.12.0/gcc_64)
```
是一样的效果。

---

编译：
```bash
bash scripts/build_ubuntu_x86_64.sh
```

编译后生成的内容都在build文件夹下。
```
ls build/
CMakeCache.txt  cmake_install.cmake    CPM_modules             _deps                 Makefile                qt_cmake          qt_cmake_debug
CMakeFiles      compile_commands.json  cpm-package-lock.cmake  install_manifest.txt  pg_cpm_functions.cmake  qt_cmake_autogen
```
qt_cmake即为生成的可执行程序。

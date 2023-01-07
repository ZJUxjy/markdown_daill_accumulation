
编译中报错：
```
# undefined reference to symbol 'pthread_create@@GLIBC_2.2.5'
```
解决：
cmake中添加：
```
SET（CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread")
```
就行了
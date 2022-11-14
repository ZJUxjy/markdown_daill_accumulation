# 如何使用protoc将proto文件转换成.h和.cc文件

```
protoc -I=D:\work\proto --cpp_out=D:\work\proto log.proto 
```
-I后面是proto的位置，--cpp_out [^注释1] 表示输出到哪个地方，最后注明转换哪个proto

---

[^注释1]  这个--cppout一定是两个`-`，如果只有一个会报错`Unknown flag: -c`

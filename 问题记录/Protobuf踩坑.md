**前情提要**：今天项目上有一个proto2到proto3的升级，并且对原始proto进行了更改。因为他那边是用protobuf3.12.2给生成的.cc和.h文件，所以我这里也开始弄这个版本protobuf的适配。而我本地的protobuf是vcpkg安装的3.21.8版本。

---

## 对protobuf3.12.2进行编译

先在[protocolbuffers/protobuf: Protocol Buffers - Google's data interchange format (github.com)](https://github.com/protocolbuffers/protobuf)上找到3.12.2的release然后下载`protobuf-3.12.2`，
编译方式就是

```bash
cd cmake && mkdir build #

pwd #确认路径无误
C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build #没问题

cmake -G "Visual Studio 17 2022" -A Win32 .. 
cmake --build . --config Release #编译&构建
```

然后报错。
```bash
objectivec_extension.cc
C:\Users\94806\Downloads\protobuf-3.12.2\src\google/protobuf/parse_context.h(749,11): error C2491: “google::protobuf::i
nternal::PackedEnumParser”: 不允许 dllimport 函数 的定义 [C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\libprotoc.vcxpro
j]
C:\Users\94806\Downloads\protobuf-3.12.2\src\google/protobuf/parse_context.h(765,11): error C2491: “google::protobuf::i
nternal::PackedEnumParserArg”: 不允许 dllimport 函数 的定义 [C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\libprotoc.vcx
proj]
  objectivec_field.cc
C:\Users\94806\Downloads\protobuf-3.12.2\src\google/protobuf/parse_context.h(749,11): error C2491: “google::protobuf::i
nternal::PackedEnumParser”: 不允许 dllimport 函数 的定义 [C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\libprotoc.vcxpro
j]
C:\Users\94806\Downloads\protobuf-3.12.2\src\google/protobuf/parse_context.h(765,11): error C2491: “google::protobuf::i
nternal::PackedEnumParserArg”: 不允许 dllimport 函数 的定义 [C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\libprotoc.vcx
proj]
```

基本上都是这种错误，意思就是dll库生成不了，查看Release下的文件，确实.lib库生成了，但是dll库就生成了两个。
```bash
PS C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\Release> ls
    目录: C:\Users\94806\Downloads\protobuf-3.12.2\cmake\build\Release

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2022/11/7     19:13         418816 libprotobuf-lite.dll
-a----         2022/11/7     19:13         525639 libprotobuf-lite.exp
-a----         2022/11/7     16:28         877348 libprotobuf-lite.lib
-a----         2022/11/7     19:14        2198016 libprotobuf.dll
-a----         2022/11/7     19:14        2459398 libprotobuf.exp
-a----         2022/11/7     16:29        4039506 libprotobuf.lib
-a----         2022/11/7     16:24       12200448 libprotoc.lib
-a----         2022/11/7     16:24        2706432 protoc.exe
```

而且这个dll库拿到工程中，会报找不到符号信息的错，就是函数有声明没定义，库不能用。

然后用mingw重新编译，仍然g。。。。

然后疯狂百度，找到一个[(24条消息) 解决protobuf: undefined reference to `google::protobuf::internal::fixed_address_empty_string[abi:cxx11_豆豆517929的博客-CSDN博客_undefined reference to `google::protobuf::internal](https://blog.csdn.net/weixin_44736938/article/details/113886868)上面说是protobuf版本冲突了，于是我吧vcpkg安装的protobuf从电脑里删除并取消了vcpkg的全局应用
```bash
vcpkg remove protobuf
vcpkg integrate remove
```

重复上面两次编译，还是没用。

后来和相关开发同学聊了聊，把原始proto文件拿了过来，然后又在vcpkg上重新安装了protobuf。用相同版本的protoc生成了.cc和.h文件，整合到工程中，可以了。。。。

绕了一个大圈，好在最后问题解决了。
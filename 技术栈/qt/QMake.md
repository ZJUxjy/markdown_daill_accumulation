# QMake

## 1. QMake编译步骤
	* 编译.pro文件生成makefile
	* 编译makefile，生成界面源码、信号槽代码

---

## 2. 具体使用

* 头文件引用
	```
	message($$PWD) //在项目配置文件中打印内容
	INCLUDEPATH += $$PWD/../../include //相对项目路径
	```

* 库引用和库路径指定
	```
	LIBS += -L"库路径" -l库名(/libs += -L".../.../lib" -lopencv_world320)
	DESTDIR += .../.../bin (输出路径指定)
	TARGET = 新的可执行文件名
	```
* 配置项
 ```
	 CONFIG += qt thread debug //连编为可调试的多线程应用程序
```

---

# 条件编译

```
CONFIG+=debug_and_release

CONFIG(debug,debug|release)
{
debug 下的设置内容....
}

CONFIG(release,debug|release)
{
release 下的设置内容....
}
```
进行编译：
```
make debug
make release
make all(debug&release 都进行编译)
```

**屏蔽release版本中所有QDebug()提示信息：**
在pro文件中添加`DEFINES+=QT_NO_DEBUG_OUTPUT`
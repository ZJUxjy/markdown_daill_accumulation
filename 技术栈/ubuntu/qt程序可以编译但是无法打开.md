
具体错误：
```
Qt Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
qt.qpa.plugin: Could not find the Qt platform plugin "xcb" in ""
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.
```
省流直接看解决方法<a href="#result1">第一个报错解决</a>、<a href="#result2">第二个报错解决</a>

# <a id="result1">第一个报错解决</a>

执行：
```bash
sudo gedit /etc/gdm3/custom.conf
```
然后文件是这个样子：
```
# GDM configuration storage
#
# See /usr/share/gdm/gdm.schemas for a list of available options.

[daemon]
AutomaticLoginEnable=true
AutomaticLogin=jingyao

# Uncomment the line below to force the login screen to use Xorg
# WaylandEnable=false

# Enabling automatic login

# Enabling timed login
#  TimedLoginEnable = true
#  TimedLogin = user1
#  TimedLoginDelay = 10

[security]

[xdmcp]

[chooser]

[debug]
# Uncomment the line below to turn on debugging
# More verbose logs
# Additionally lets the X server dump core if it crashes
#Enable=true

```

其中这句：
```
# WaylandEnable=false
```
把`#`去掉，也就是这句话反注释，让他生效。
然后`reboot`（重启）。

再次执行，关于`wayland`的报错就消失了。

---

# 第二个错误

查询找到网上的一个解决方法：
进入这个目录：
`Qt5.12.12/Tools/QtCreator/lib/Qt/plugins/platforms`
这个目录下应该有这些文件
```bash
-rwxr-xr-x  1 jingyao jingyao  15584 Sep 30  2021 libqeglfs.so*
-rwxr-xr-x  1 jingyao jingyao 566664 Sep 30  2021 libqlinuxfb.so*
-rwxr-xr-x  1 jingyao jingyao 237216 Sep 30  2021 libqminimalegl.so*
-rwxr-xr-x  1 jingyao jingyao 189728 Sep 30  2021 libqminimal.so*
-rwxr-xr-x  1 jingyao jingyao 255200 Sep 30  2021 libqoffscreen.so*
-rwxr-xr-x  1 jingyao jingyao 339040 Sep 30  2021 libqvnc.so*
-rwxr-xr-x  1 jingyao jingyao  19744 Sep 30  2021 libqxcb.so*
```
`libqxcb.so`这个最重要，其他的可以先不管。
执行`ldd libqxcb.so`
找一找有没有`not found`，如果有，安装对应的库。

然而这并没有解决我的问题，遂进行如下尝试：

### 尝试

不使用qt creator启动编译生成的程序。
但是因为.pro文件中加了这句：
```cmake
qnx: target.path = /tmp/$${TARGET}/bin
else: unix:!android: target.path = /opt/$${TARGET}/bin
```

也就是生成的程序放在bin目录下，然而我在bin目录下执行`ldd DevTool | grep 'not found'`，结果
```bash
libturbojpeg.so.0 => not found
libosgQOpenGL.so.145 => not found
```

两个库链接不到，这两个库放在我自己定义的系统路径`$(ThirdParty)`下面，而且查看系统路径是有包含这两个库的目录的，既然链接不上就把他拷贝到`/usr/local/lib/`下面把，再次执行`ldd DevTool | grep 'not found'`，没有输出内容，这两个库找到了。

再次执行`./DevTool`，仍然不能运行，继续报xcb相关的错误，说库不完全，不能识别为qt plugins...


好吧，那我直接把qt目录下面`/home/jingyao/Qt5.12.0/Tools/QtCreator/lib/Qt/plugins/platforms`这个拷贝到与可执行文件同级目录下。因为这个目录下包含了xcb库
```bash
jingyao@jingyao-vmware-22:~/Qt5.12.0/Tools/QtCreator/lib/Qt/plugins/platforms$ ll
总用量 1612
drwxrwxr-x  2 jingyao jingyao   4096 Nov 14 16:08 ./
drwxrwxr-x 12 jingyao jingyao   4096 Nov 14 16:08 ../
-rwxrwxr-x  1 jingyao jingyao  15584 Dec  3  2018 libqeglfs.so*
-rwxrwxr-x  1 jingyao jingyao 569008 Dec  3  2018 libqlinuxfb.so*
-rwxrwxr-x  1 jingyao jingyao 237192 Dec  3  2018 libqminimalegl.so*
-rwxrwxr-x  1 jingyao jingyao 189472 Dec  3  2018 libqminimal.so*
-rwxrwxr-x  1 jingyao jingyao 246272 Dec  3  2018 libqoffscreen.so*
-rwxrwxr-x  1 jingyao jingyao 338736 Dec  3  2018 libqvnc.so*
-rwxrwxr-x  1 jingyao jingyao  33320 Dec  3  2018 libqxcb.so*

```

运行，报错
```bash
jingyao@jingyao-vmware-22:~/work/dev-tool/bin$ ./DevTool 
QFactoryLoader::QFactoryLoader() checking directory path "/home/jingyao/work/dev-tool/bin/platforms" ...
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqeglfs.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqeglfs.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqlinuxfb.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqlinuxfb.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqminimal.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqminimal.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqminimalegl.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqminimalegl.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqoffscreen.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqoffscreen.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqvkkhrdisplay.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqvkkhrdisplay.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqvnc.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqvnc.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqwayland-egl.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqwayland-egl.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqwayland-generic.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqwayland-generic.so'" 
         not a plugin
QFactoryLoader::QFactoryLoader() looking at "/home/jingyao/work/dev-tool/bin/platforms/libqxcb.so"
"Failed to extract plugin meta data from '/home/jingyao/work/dev-tool/bin/platforms/libqxcb.so'" 
         not a plugin
qt.qpa.plugin: Could not find the Qt platform plugin "xcb" in ""
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

已放弃 (核心已转储)
```

在运行时加参数` export QT_DEBUG_PLUGINS=1`，失败

然后我重装Qt，尝试Qt5.15，Qt6.4，均不能成功。

## <a id="result2">第二个错最后是如何解决的</a>

这个项目除了最近一次commit之外，其他commit均可以正常编译，于是乎我查看最新commit对.pro文件的改动：删了几行空行，然后删了一个用不到的cpp文件。
那看来和qmake应该没关系了，也确实，这个报错并不是编译错误而是运行错误。

然后就回退到前一个commit，把最新commit的内容分批拷过来，看在那一步出错。

最后是在`dev-tool/bin`这个文件内产生的问题，这个文件是创建的一个给可执行文件打包的地方，内含一个`linuxdeployqt`生成的文件`qt.conf`
```bash
jingyao@jingyao-vmware-22:~/work/dev-tool/bin$ ll
总用量 8060
drwxrwxr-x 7 jingyao jingyao    4096 Nov 14 19:20 ./
drwxrwxr-x 6 jingyao jingyao    4096 Nov 14 16:37 ../
-rwxrwxr-x 1 jingyao jingyao     276 Nov 14 16:36 AppRun.sh*
-rwxrwxr-x 1 jingyao jingyao     202 Nov 14 16:36 copylib.sh*
drwxrwxr-x 3 jingyao jingyao    4096 Nov 14 16:36 data/
-rwxrwxr-x 1 jingyao jingyao 8206624 Nov 14 16:38 DevTool*
drwxrwxr-x 2 jingyao jingyao    4096 Nov 14 16:36 Font/
drwxrwxr-x 2 jingyao jingyao    4096 Nov 14 16:36 Image/
-rw-r--r-- 1 jingyao jingyao     118 Nov 14 00:17 ld.so.conf
drwxrwxr-x 2 jingyao jingyao    4096 Sep  7 22:50 platforms/
-rwxrw-rw- 1 jingyao jingyao     152 Nov 14 15:23 qt.conf*
drwxrwxr-x 2 jingyao jingyao    4096 Nov 14 16:36 translations/
```
这个`qt.conf`的内容：
```
# Generated by linuxdeployqt
# https://github.com/probonopd/linuxdeployqt/
[Paths]
Prefix = ./
Plugins = plugins
Imports = qml
Qml2Imports = qml
```

平平无奇，确实很难想得到程序跑不起来和他会有关系。但事实就是只要它在bin里，程序就无法运行且报xcb....的错，删掉他，程序随便跑。。。

## 原因分析

todo
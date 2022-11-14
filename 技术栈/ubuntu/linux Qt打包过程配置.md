下载地址：[https://github.com/probonopd/linuxdeployqt/releases](https://github.com/probonopd/linuxdeployqt/releases)

将[linuxdeployqt-continuous-x86_64.AppImage](https://github.com/probonopd/linuxdeployqt/releases/download/continuous/linuxdeployqt-continuous-x86_64.AppImage)下载下来后，
赋予权限
```bash
sudo chmod 777 linuxdeployqt-continuous-x86_64.AppImage
```

然后拷贝到系统运行目录下并重命名为`linuxdeployqt`
```bash
sudo cp linuxdeployqt-continuous-x86_64.AppImage /usr/local/bin/linuxdeployqt
```

检查是否安装成功
```bash
linuxdeployqt -version
```

若成功，会显示
```bash
linuxdeployqt  (commit 5fa79fa), build 36 built on 2022-08-21 12:36:03 UTC
```
或者类似的内容。
<a href="#failed">若未成功</a>

既然成功了，那么就来试试给生成的可执行文件进行一个打包。

```
sudo linuxdeployqt DevTool -unsupported-allow-new-glibc
```




待补充：[(28条消息) ubuntu linuxdeployqt 打包Qt程序_超级大洋葱806的博客-CSDN博客_pyqt 打包 ubuntu](https://blog.csdn.net/u014779536/article/details/107854060)
[(28条消息) ubuntu linuxdeployqt 打包Qt程序_超级大洋葱806的博客-CSDN博客_pyqt 打包 ubuntu](https://blog.csdn.net/u014779536/article/details/107854060)
[ubuntu下qt程序打包 - 简书 (jianshu.com)](https://www.jianshu.com/p/779255161e7c/)
[Ubuntu下Qt程序进行打包-pudn.com](https://www.pudn.com/news/62a98ea2a11cf7345fa0ae13.html)




<a id="failed">若安装未成功</a>并出现下面内容：
```bash
dlopen(): error loading libfuse.so.2

AppImages require FUSE to run. 
You might still be able to extract the contents of this AppImage 
if you run it with the --appimage-extract option. 
See https://github.com/AppImage/AppImageKit/wiki/FUSE 
for more information
```

访问[FUSE · AppImage/AppImageKit Wiki (github.com)](https://github.com/AppImage/AppImageKit/wiki/FUSE)按照上面内容安装fuse库


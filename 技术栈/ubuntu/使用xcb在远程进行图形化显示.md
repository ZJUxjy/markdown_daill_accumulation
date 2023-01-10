ssh连接ubuntu后，直接执行带有图形窗口的程序会显示下面的内容
```
qt.qpa.xcb: could not connect to display 
qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

Available platform plugins are:...
```
也就是程序链接不到图形化界面。

这时候如果我们使用的是windows系统，可以安装一个XLaunch应用，启动xlaunch后会让我们选择一个参数，默认是-1也就是自动选择，这里建议我们自己选一个。

xlaunch成功启动之后右下角会有xlaunch的图标，在linux ssh终端中输入
```
export DISPLAY=10.35.1.79:5901
```
这个ip是windows系统的ip地址，:后的数字就是我们刚才选择的数字。
这时候再试一下，就可以在windows里显示远程ubuntu的应用窗口了.

一个xlaunch可以连接多个client，你也可以开启多个xlaunch。



具体错误：
```
Qt Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
qt.qpa.plugin: Could not find the Qt platform plugin "xcb" in ""
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.
```

# 第一个报错解决

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
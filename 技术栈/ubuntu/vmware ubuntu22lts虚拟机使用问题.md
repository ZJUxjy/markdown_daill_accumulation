# 1
问题描述：使用vs code+cmake调试qt程序，报错：
```
qt.qpa.xcb: could not connect to display 127.0.0.53:0.0
```
经查询了解与xserver有关，这个报错之前遇到过，但是当时删除掉linuxdeployqt生成的一个文件后就能正常运行了，这次是gdb调试进不去，命令行./{可执行程序}也报同样错。而且这次xcb相关的库依赖关系全部正常，没有缺失的库。

查询后在[qt.qpa.xcb: could not connect to display :0 | Qt Forum](https://forum.qt.io/topic/120331/qt-qpa-xcb-could-not-connect-to-display-0)中有一个解决办法：
> 命令行输入`export _DISPLAY_=:0`

经上面尝试后，命令行./{可执行程序}可以运行。但是gdb调试仍然无法进行。于是执行
```
sudo vim /etc/profile
```
将上面的内容写入配置文件后重启虚拟机，命令行有效，gdb仍然无效。
亦尝试了[network programming - NS-3 - NetAnim error: qt.qpa.xcb: could not connect to display localhost:0.0 - Stack Overflow](https://stackoverflow.com/questions/67629920/ns-3-netanim-error-qt-qpa-xcb-could-not-connect-to-display-localhost0-0)中提到的将wsl升级后重启宿主Windows主机，也没用。

然后忘记在哪里找到一个方法，前面`export _DISPLAY_=:0`这句改成`export _DISPLAY_=localhost:0`，重复上述操作，再启动虚拟机，虚拟机起不来了。。（中间还有其他操作，但是记不起来了，有可能是这个改动的原因也有可能是其他改动的原因）

虚拟机具体错误情况：


按着`Host SMBus controller not enabled`查找错误解决方式，网上几乎都是一样的解决办法：
恢复模式下重启ubuntu虚拟机，在跳出的menu里选择root，然后执行
````
mount -o remount,rw / # 重新挂载文件系统
````

```
vim /etc/modprobe.d/blacklist.conf 
```
vim输入
```
blacklist i2c-piix4 
# 禁用该模块，这一步还有一种是blacklist intel...的模块，我的电脑是amd cpu，但也尝试了没有用
```
保存退出后
```
update-initramfs -u -k all # 重新生成引导文件
```
重启问题依旧。

最后一个解决方式，，重装虚拟机，但是那就等于没解决。。。



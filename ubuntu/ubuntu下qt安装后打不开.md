
参考链接：[(25条消息) Ubuntu18.04安装完成qt5.15后无法启动qtcreator的解决方法_leo12345678912345的博客-CSDN博客_ubuntu安装qt后打不开](https://blog.csdn.net/leo12345678912345/article/details/121737417)

两步轻松解决：
```shell
sudo apt install build-essential
sudo apt install libxcb-xinerama0
```

一个是编译器问题，一个是没有xcb插件
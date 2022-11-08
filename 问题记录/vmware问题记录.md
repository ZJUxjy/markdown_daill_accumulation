1. vmware另一个程序已锁定文件的一部分,进程无法访问
>把虚拟机文件夹下面.lck文件夹都删除，然后再运行

---

2. 安装vmware后vmware tool装不上
>把软盘、SATA0、1都设置成自动检测，然后关闭客户机，再启动，在图形界面出来之前就点选重新安装vmware tool。之后按照过程安装。

参考链接：[(25条消息) Vmware Tools显示灰色解决办法_warren@伟_的博客-CSDN博客_vmware tools灰色](https://blog.csdn.net/warren103098/article/details/123314208)

---

3. ssh连接虚拟机连不上，报错:`ssh: connect to host 192.168.86.128 port 22: Connection refused`
>检查是否安装openssh-server
>`ps -e|grep ssh`
>没东西显示就说明没安装，执行下面命令进行安装
>`sudo apt-get install openssh-server`
>然后启动服务
>`/etc/init.d/ssh start #或者 service sshd restart`
>再次检查
>`ps -e|grep ssh`

```
6157 ?        00:00:00 sshd
6159 ?        00:00:00 sshd
6236 ?        00:00:00 sshd
 ```
> 安装成功


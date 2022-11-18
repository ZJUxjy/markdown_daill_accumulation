最小安装的ubuntu是默认没有ssh服务的，需要安装
```bash
sudo apt-get install openssh-server
```
开启ssh服务
```bash
sudo service ssh start
```
查看服务是否开启
```bash
 ps -e | grep ssh
```
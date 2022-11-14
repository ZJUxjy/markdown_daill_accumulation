# ssh

ssh一般路径：
```bash
/home/jingyao/.ssh
```
也就是/home/用户名/.ssh
然后用命令行生成key
```bash
ssh-keygen -t rsa
```
就可以在该文件夹下面找到生成的key

---

# hosts

hosts文件在`/etc`目录下，比如我要修改hosts对github进行加速，就可以执行下面命令
```bash
pwd
/etc
sudo vim hosts
#####################################
# https://ping.chinaz.com/www.github.com网址查询github最快的ip地址进行加速
140.82.121.4 github.com
```
然后就可以了。
[ip查询网站](https://ping.chinaz.com/www.github.com)

---

# 环境变量

* 修改/etc/profile新加环境变量
```shell
sudo vim /etc/profile
```

添加语句
```shell
export VAR_NAME=value
```
或者在PATH进行添加
```shell
# 加到PATH末尾
export PATH=$PATH:/path/to/your/dir
 
# 加到PATH开头
export PATH=/path/to/your/dir:$PATH
```
使添加的路径立即生效（仅在当前终端）：
```shell
source /etc/profile
```
这种加法对所有用户有效
重启后永久有效


* 还有一种方法可以在仅当前终端生效：
```shell 
export PATH=/home/jingyao/ThirdParty/osg/lib:$PATH
export PATH=/home/jingyao/ThirdParty/osgQt-master/lib:$PATH
export PATH=/home/jingyao/ThirdParty/libjpeg-turbo/lib:$PATH
libjpeg-turbo
libturbojpeg.so.0
libturbojpeg.so.0
```
上面这句话直接写在终端里，就只会对当前终端生效


* 第三种仅对当前用户生效的方式：
```shell
vim ~/.bashrc
```
添加内容：
```shell
export PATH=/home/yan/share/usr/local/arm/3.4.1/bin:$PATH
```
使添加内容立即生效：
```shell
source ~/.bashrc
```


* 查看系统环境变量的方式：

```shell
env
```

```shell
export
```

上面两句话都可以

打印你想要查看的特定环境变量，执行下面这句就可以：
```bash
echo $PATH
echo $ThirdParty
```


---

# terminal直接对某些文件进行编辑

1. 方法1：
```bash
sudo vim /etc/profile
```

2. 方法2：
```shell
sudo gedit /etc/profile
```
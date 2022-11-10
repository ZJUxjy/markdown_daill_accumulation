# github加速

[ip查询网站](https://ping.chinaz.com/www.github.com)
在这个查询网站中查www.github.com并测速，找到一个能连接且时延小的ip，复制。

## ubuntu
```bash
sudo gedit /etchosts
```
在文件中空白行添加如下格式的内容：
```
140.82.121.4 github.com #前面这个ip是你在网站找到的一个可连上的ip
```
---

## windows

windows下的hosts文件在`C:\WINDOWS\system32\drivers\etc`下面，修改需要拷贝一份然后用编辑器打开后覆盖回去。

添加内容与ubuntu系统下相同
```
140.82.121.4 github.com
```

反正经我本人使用，github连不上了就上去换个ip，都能连上。
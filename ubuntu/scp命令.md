```
scp -P 2233 /home/abc.tar.gz root@123.123.123.123:/root/abc.tar.gz
```
端口的-P一定是大写的，后面不加冒号，加一个空格就行，远程端口后要有`:`。

报错内容
```
Could NOT find OpenSSL, try to set the path to OpenSSL root folder in the system variable OPENSSL_ROOT_DIR (missing: OPENSSL_LIBRARIES OPENSSL_INCLUDE_DIR)
```

解决方式：
安装openssl编译依赖
```
sudo apt-get install libssl-dev
```
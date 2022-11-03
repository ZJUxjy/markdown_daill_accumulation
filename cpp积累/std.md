# std::hex std::dec
hex十六进制，dec十进制

# std::stringstream
1. 用于传输字符串流，知道数据格式则能解析。
2. stringstream::str将流中数据转换成string字符串
3. << 和 >>填入与取出流中数据
```cpp
std::stringstream ss; 
ss << 100 << ' ' << 200; 
int foo,bar; 
ss >> foo >> bar;
```

```cpp
std::stringstream ss;   
ss << "abc";   
string s = ss.str();    
```

```cpp

```
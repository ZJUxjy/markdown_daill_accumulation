是 linux 内核实现IO多路复用（IO multiplexing）的一个实现。（在一个操作里同时监听多个输入输出源）


# select
跨平台
阻塞函数
```
int select (int __nfds, //委托内核检测的最大文件描述符+1
			fd_set *__restrict __readfds, //读

	         fd_set *__restrict __writefds, //写

	         fd_set *__restrict __exceptfds, //异常

	         struct timeval *__restrict __timeout);
```

检测连接数有上限

# poll




# epoll
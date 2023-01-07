## zmq_msg_recv

[zmq官方文档-zmq_msg_recv](http://api.zeromq.org/4-2:zmq-msg-recv)

**原型**
*int zmq_msg_recv (zmq_msg_t *msg_ void *socket, int flags);*

返回值：
-1：接收失败
\>0的整数：接收到数据的字节数

收到的数据写在msg_里
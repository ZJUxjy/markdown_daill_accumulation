
pipe 匿名管道
fifo 具名管道

## pipe
Linux的pipe是单向的，进程间双向通信还得开两个文件描述符，不方便
而且进程要有父子关系才能用pipe，这些都限制了pipe的使用



# condition_variable
条件变量可实现多个线程之间同步操作，

---

### 1.wait()函数

`wait (unique_lock <mutex> &lck)`
>	相关线程被阻塞直到收到notify

`wait(unique_lock <mutex>＆lck，Predicate pred)
	
>	pred=true时阻塞, false时不阻塞
>	wait函数可以拆分为三个操作：释放互斥锁，等待条件变量，再次获取互斥锁


---


### 2.notify_one()

>解除阻塞当前正在等待此条件的线程之一。如果没有线程在等待，则还函数不执行任何操作。如果超过一个，不会指定具体哪一线程。

### 3.notify_all()

>解除阻塞当前正在等待此条件的所有线程。如果没有线程在等待，则还函数不执行任何操作。


事件产生后，会经过：
1. 事件派发
2. 事件过滤
3. 事件分发
4. 事件处理

## 详细过程

要事件派发，就需要有一个唯一对应的QApplication应用程序对象，然后调用对象的`exec()`函数，这样qt的事件检测就开始了。

事件产生后，qt使用应用程序对象调用`notify()`将事件发送到指定窗口。

时间发送过程中通过事件过滤器进行过滤，默认不对任何产生的使劲进行过滤。

事件发送到指定窗口后，窗口的事件分发器会对收到的事件进行分类。

事件分发器会将之后的事件分发给对应的事件处理器函数进行处理，每个事件处理器函数都有默认的处理动作。



回调函数：调用由框架判定时机成熟后调用。

事件的 `ignore()`调用后，事件会传递给他的父窗口。在最外层窗口不处理会被忽略掉。

注意，这些事件都是protected 的，需要在子类重写，例如：
```cpp
protected:

    void closeEvent(QCloseEvent *ev);

    void resizeEvent(QResizeEvent *ev);
```

一个宏：
Q_UNUSED(ev)表示没用到这个事件，编译时不用弹警告信息；
```cpp
void MainWindow::resizeEvent(QResizeEvent *ev){
	Q_UNUSED(ev)
	
    qDebug()<<"old size = "<<ev->oldSize()<<"; currSize: "<<ev->size();

}
```
这样编译时不会报ev未使用的警告

重写了子类的时间函数，父类的就不会再调用了。当然，也可以这样调用父类的函数：

```cpp
void MainWindow::resizeEvent(QResizeEvent *ev){
    qDebug()<<"old size = "<<ev->oldSize()<<"; currSize: "<<ev->size();
    
    QMainWindow::resizeEvent(ev);
}
```
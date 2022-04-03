# C++多线程

程序运行起来，生成一个进程，每个进程会自动产生一个主线程，进程开始运行，该主线程也开始运行。

可以手动写代码在进程中创建其它的线程。

## C++11新标准线程库

从C++11开始，C++本身增加了多线程的支持，意味着可移植性（跨平台）。

主线程从`main()`开始执行，那么我们自己创建的线程也需要从一个函数（初始函数）开始运行。一旦该函数执行完毕，代表线程运行结束。

- 头文件`thread`
- 初始函数，如 `void myprint()`
- 创建线程对象：参数为可调用对象。如`thread mytobj(myprint)`, 此时线程开始执行。
- `join()`: 子线程和主线程汇合 `mytobj.join()`阻塞主线程，等待子线程运行完毕。
- `detach()`: 分离，与主线程关联的`thread`对象就会失去和主线程的关联，此时子线程就会驻留到后台运行。
- `joinable()`: 判断是否成功使用`join()`or`detach()`
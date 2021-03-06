# Java 程序高可用

## 优雅停机
非优雅停机的问题：
```md
请求丢失：内存队列中等待执行请求丢失
数据丢失：处于内存缓存中数据未持久化到磁盘
文件损坏：正在写的文件没有没有更新完成，导致文件损坏
业务中断：处理一半的业务被强行中断，如支付成功了，却没有更新到数据库中
服务未下线：上游服务依然往停止节点发送请求
```
```md
所以在关闭服务之前，我们需要先做好善后工作，比如保存数据，清理资源，下线服务，然后才退出应用。
这种有计划平滑的关闭应用相对直接停止应用，就显得非常『优雅』。
```
### ShutdownHook
```md
当 JVM 接受到系统的关闭通知之后，调用 ShutdownHook 内的方法，用以完成清理操作，从而平滑的退出应用。
```
```java
Runtime.getRuntime().addShutdownHook(
    new Thread(() -> {System.out.println("关闭应用，释放资源");})
);
```
```md
Runtime.getRuntime().addShutdownHook(Thread) 需要传入一个线程对象，后续动作将会在该异步线程内完成。
```
```md
除了主动关闭应用（使用 kill -15 指令）,以下场景也将会触发 ShutdownHook :
代码执行结束，JVM 正常退出
应用代码中调用 System#exit 方法
应用中发生 OOM 错误，导致 JVM 关闭
终端中使用 Ctrl+C(非后台运行)
```
```md
目前很多开源框架都是基于这个机制实现优雅停机，比如 Dubbo，Spring 等。
```
* 相关注意点
```md
尽量在一个 ShutdownHook 完成所有操作，多个 ShutdownHook 之间并无任何顺序，Java 并不会按照加入顺序执行，反而将会并发执行。
不要在 ShutdownHook 执行需要被阻塞代码，如 I/0 读写，这样就会导致应用短时间不能被关闭。
```

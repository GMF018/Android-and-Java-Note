## Handler 原理

### 1.handler 主要涉及的关键类

+ Looper(轮询从MessageQueue中取出消息)
+ Message(存放消息)
+ MessageQueue(消息队列)

### 总结

- Thread 若与 Looper 关联，将会是一一对应的关系，且关联后关系无法改变。
- Looper 与 MessageQueue 是一一对应的关系。
- Handler 与 Looper 是多对一的关系，创建 Handler 实例时要么提供一个 Looper 实例，要么当前线程有关联的 Looper。
- 在 Handler.sendMessage 时，会将 Message.target 设置为该 Handler 对象，这样从消息队列取出 Message 后，就能调用到该 Handler 的 dispatchMessage 方法来进行处理。
- Handler 会对应一个 Looper 和 MessageQueue，而 Looper 与线程又一一对应，所以通过 Handler.sendXXX 和 Hanler.postXXX 添加到 MessageQueue 的 Message，会在这个对应的线程的 Looper.loop() 里取出来，并就地执行 Handler.dispatchMessage，这就可以完成线程切换了。
- Runnable 被封装成 Message 之后添加到 MessageQueue。
- 可以从一个线程创建关联到另一个线程 Looper 的 Handler，只要能拿到对应线程的 Looper 实例。
- 消息可以插队，使用 Handler.xxxAtFrontOfQueue 方法。
- 尚未分发的消息是可以撤回的，处理过的就没法了。
#tornado#
tornado是python提供的异步编程框架。传统的web服务器多用来处理http协议。http是一种无状态协议，连接的生命周期自页面请求开始，页面收到后即断开连接。一次一个连接往往对应一个线程处理。异步服务器要解决的场景往往是长连接的方式，因此不能够使用连接，线程这种对应的方式。tornado是一种事件驱动的服务器，eventloop处理用户的连接请求，当事件发生时，采用异步的方式去处理事件。处理完毕后往往采用回调函数的方式来处理结果，是一种事件，线程的处理模式。

要理解tornado首先要理解几个概念

##generator##
python提供yield用于声明一个generatorfunction,如下代码所示。
```
def foo_gen():
	yield value
```
调用foo_gen()后，生成一个generator对象。调用next方法则能够获取yield的值，yield更像是协程之上的一层抽象，本质上是一个迭代器（因为next方法可以看出），当yield结束时(比如while循环结束，或者遇到return时)，会抛出异常。即调用next却遇不到yield时。

因此tornado利用raise exception的方式（否则会抛出StopIteration异常），在yield之后抛出异常给ioloop(这个后面解释)，达到normal函数的return功能

##协程##
ThreadLocal会产生什么问题

ThreadLocal是怎么内存泄漏的
由于ThreadLocalMap中的key是ThreadLocal的弱引用，一旦发生GC便会回收ThreadLocal，那么此时的ThreadLocalMap存储的key便是null。如果不通过手动remove()那么ThreadLocalMap的Entry便伴随线程的整个生命周期造成内存泄漏，大致就是一个thread ref -> thread -> threadLocals -> entry -> value的强引用关系。因此Java其实是有对于内存泄漏的一些预防机制的，每次调用ThreadLocal的set()、get()、remove()方法时都会回收key为空的Entry的value。

那么为什么ThreadLocalMap的key要设计成弱引用呢？其实很简单，如果key设计成强引用且没有手动remove()，那么key会和value一样伴随线程的整个生命周期，如果key是弱引用，被GC后至少ThreadLocal被回收了，在下一次的set()、get()、remove()还会回收key为null的Entry的value。
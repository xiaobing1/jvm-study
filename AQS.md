# AQS
## 属性
### state: 同步状态 0: 未被占用 1: 已被占用
### head: Node头节点
### tail: Node尾节点

## Node属性
### 静态变量
#### SHARED: Node类, 标示共享模式节点
#### EXCLUSIVE: Node类, 标示排他模式节点, 默认为null
#### CANCELLED: int, 当前线程已取消, 值1
#### SIGNAL: int, 当前线程已经准备好了, 等待资源释放 值-1
#### CONDITION: int, 当前节点在等待队列中, 节点线程等待唤醒 值-2
#### PROPAGATE: int, 当前线程在SHARED情况下, 该字段才会使用 值-3
### 普通变量
#### prev: 前一个节点
#### next: 后一个节点
#### thread: 线程引用
#### waitStatus: 等待状态


### 简略原理
#### 抢占线程 初始化Node对象并指定排他或者共享模式放入Node FIFO双向链表队列中, 设置前一个状态, 调用LockSupport.park方法等待, 解锁后占用资源, 移除标示当前线程的Node节点
#### 释放资源 解锁队列等待前一个线程
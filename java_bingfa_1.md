# java 并发
- 线程的创建与启动
- 线程的生命周期
- 线程的通信
- 线程的同步
- 线程中断与取消
- 线程的锁、原子数据、线程池

### 线程的创建与启动
创建线程的两种方式：

- 继承Thread
- 实现Runable接口

1、继承Thread

	class ExampleThread extends Thread {
		@Override
		public void run(){
			for(int i=0;i<10;i++){
				System.out.println("i="+i);
			}
		}
		
		public static void main(){
			ExampleThread ex = new ExampleThread();
			ex.start();
		}
	}
	
2、实现Runable接口

	class ExampleRunable implements Runable{
		@Override
		public void run(){
			for(int i=0;i<10;i++){
				System.out.println("implements Runable i" + i);
			}
		}
		
		public static void main(){
			Runable runable = new ExampleRunable();
			Thread exRu = new Thread(runable);
			exRu.start();
		}
	}
	
### 线程的生命周期

在java中，线程的状态有5种，分别为：

- 新建状态：New
- 就绪状态：Runnable
- 运行状态：Running
- 阻塞状态：Blocked
- 死亡状态：Dead

线程状态的变化入下图所示：

![thread status](https://github.com/newtry/blog/raw/develop/picture/thread-status.png)


其中等待队列和锁池所在的左侧也属于阻塞状态。阻塞分为以下几种情况：

- 等待阻塞：运行(running)的线程执行o.wait()方法，JVM会把该线程放入等待队列(waitting queue)中。
- 同步阻塞：运行(running)的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池(lock pool)中。
- 其他阻塞：运行(running)的线程执行Thread.sleep(long ms)或t.join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入可运行(runnable)状态。

### 线程间通信

通过wait、notify进行通信

### sleep和wait的区别

wait放弃持有的锁进行等待，sleep也会进入阻塞状态进行等待，但持有的锁是不会放弃的。
## 线程终止的方法

1. 正常终止，线程代码块执行完
2. 使用stop()或suspend()，存在的问题：这两种方法过于粗暴，如果线程占用了一些资源（如打开了一个文件，建立了一个数据库连接什么的），直接stop()或是suspend()会产生问题的，资源无法得到释放。
3. 使用中断 （Thread.interrupt()）
4. 使用标志位

## 任务与线程的取消与关闭

正常情况下，当任务或线程代码正常执行完，他们会自行停止与结束。
线程的取消包括三部分内容：

1. who请求取消 一个线程请求取消另一个线程（通过向线程发送中断消息）
2. when何时取消 线程自己决定何时去取消
3. how如何取消 线程决定怎么样操作使得线程取消

⚠️中断意味着想要取消线程当前的工作

## 多线程的编写

关键在于需要明确任务边界。

## concurrent 框架
框架的主要内容分为三个部分：

1. atomic(基础数据的线程安全类、集合的线程安全实现)
2. locks
3. 线程池（线程调度、线程池、队列）

### automic

concurrent包为每一种java基本数据类型都提供了一种线程安全的包装类。对于集合也进行了线程安全的封装，通过Collections类可将基本集合类型转为线程安全。

### locks

1. ReentrantLock（可重入锁，实现Lock接口）
2. ReentrantReadWriteLock（可重入读写锁，实现ReadWriteLock接口）

同时可指定锁是否是公平的。





	
	
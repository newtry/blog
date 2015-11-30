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

状态流转图

![thread status](https://github.com/newtry/blog/raw/develop/picture/thread-status.png "thread status")

创建、运行、可运行、阻塞、结束

线程的生命周期可由上图详细说明

## 任务与线程的取消与关闭

正常情况下，当任务或线程代码正常执行完，他们会自行停止与结束。
线程的取消包括三部分内容：

1. who请求取消 一个线程请求取消另一个线程（通过向线程发送中断消息）
2. when何时取消 线程自己决定何时去取消
3. how如何取消 线程决定怎么样操作使得线程取消

⚠️中断意味着想要取消线程当前的工作





	
	
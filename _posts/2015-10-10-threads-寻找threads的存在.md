#Threads-寻找Threads的存在

###两种召唤出Threads方法

班门弄斧，迫于无奈，不得不研究Threads，此处有一[良文][id]
良文介绍用不同的方法创建threads

 [id]: http://tutorials.jenkov.com/java-concurrency/creating-and-starting-threads.html#java-threads-video-tutorial
 
####方法之一：class MyThread extends Thread

但是因为此篇文章是寻找Threads的存在，跟它类似

只是我稍微改了一下run method


```
public class MyThread extends Thread{
	public void run(){
		Random r = new Random();
		char c = (char)(r.nextInt(26) + 'a');
		for(int i = 0 ; i < Length; i++){
			System.out.write(c);
		}
		System.out.write('\n');
	}
}

MyThread myThread = new MyThread();
myThread.run();

```

可以注意的点有：

- System.out.write() 不是 thread-safe的，各个thread会来中断别人和打砸抢，也就是这个原因，我故意将Length设置成20，这样打砸抢的概率高一些，比如最终结果的一部分可能是这样的：

```
xgfxgfgfggggfgfgfgfgfgfgfgfgfgfgfgtfgfgf
xxxxxxexexexexexexexxxxexexe
fff
....
```

- 之二就是整个构架/写法吧，因为标准的Java本来就跟我一般熟悉

####方法之二：Runnable Interface Implementation

The second way to specify what code a thread should run is by creating a class that implements java.lang.Runnable. The Runnable object can be executed by a Thread.


创建了java.lang.Runnable的一个子类，然后该Runnable对象可以由一个线程来执行（我直接google翻的...）


```
public class MyRunnable implments Runnable{
	
	public void run(){
		//...
	}
}

Thread thread = new Thread(new MyRunnable());
thread.start();

```

同样结果是这样的

```
pypypypypypypypypypypypypypypypypypypypy
nnnnnnnnnnnnnnnnnnnn
dddddddddddddddddddd
//此处就是一个'\n'
....

```


###避免打砸抢，避免Race condition，让Threads安全起来


要让Threads安全起来有很多方法，首先最关键的就是key blocks/methods其变成Critical Section

可用的方法包括Synchronized Block/ Semaphore / Monitor


针对上述code，最简单的是sychronize block

如下：

```
static Integer lock = 1;
	
public static class MyRunnable implements Runnable{
	public void run(){
		synchronized (lock){
		//...
		}
	}
}
```


>The "Synchronized" keywords prevents concurrent access to a block of code or object by multiple Threads.


此时再度运行，结果就是


```
ssssssssssssssssssss
mmmmmmmmmmmmmmmmmmmm
wwwwwwwwwwwwwwwwwwww
iiiiiiiiiiiiiiiiiiii
...

```










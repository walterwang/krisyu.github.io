#Semaphore


###Greek sēma ‘sign’ + -phore.

首先我去查了一下semaphore的意思，原来是旗语/信号灯的意思

Greek sēma ‘sign’ + -phore.  
-phore
(用于复合字中) 表 "携带者,产生者" 之义,如:semaphore


所以semaphore的意思就是通过一个信号/符号/旗语，然后我们来尝试做到mutually exclusion


				+----+
				|    |
				+----+
				|     
				+     


对了，Semaphore是Dijkstra提出来的，厉害哦，记得graph theory里面他也出现过.


###通过代码来尝试弄懂semaphore


```
struct semaphore{
	int count;
	queueType queue;
};

void semWait(semaphore s){
	s.count--;
	if(s.count < 0){
		/* place this process in s.queue */;
		/* block this process */;
	}
}

void semSignal(semaphore s){
	s.count++;
	if(s.count <= 0){
		/* remove a process P from s.queue */;
		/* place process P on ready list */;
	}
}
```

看起来好像不难的样子

- 初始化
- transmit signal -> 用 semSignal
- receive signal -> semWait



###用起来


感觉比如threads (A,B,C)来用，总是先呼唤semWait，然后呼唤semSignal，呼叫semWait的时候如果不是可用那么就block掉，用好了呼叫semSignal 然后就让waiting threads来执行，好吧，这个也有伪码

值得注意的是下面的semaphore的值是放在1，这样才能实现"mutual exclusion",但是这并不是一个传说中的"binary semaphore"


```
/* program mutualexclusion */
const int n = /* number of process */;
semaphore s = 1 ;
void P(int i)
{
	while(true){
		semWait(s);
		/ * critical section * /;
		semSignal(s);
		/ * remainder * /;
	}
}

void main()
{
	parbegin( P(1), P(2) , ... , P(n));
}

```





然后再看这个比喻：

> Think of semaphores as bouncers at a nightclub. There are a dedicated number of people that are allowed in the club at once. If the club is full no one is allowed to enter, but as soon as one person leaves another person might enter.

觉得还是不那么难理解，不过看课本的图真是把我看晕了.....


###binary semaphore vs general semaphore

```
摘自stack overflow某问题


Actually, both types are used to synchronize access to a shared resource, whether the entity which is trying to access is a process or even a thread.

The difference is as follows:

Binary semaphores are binary, they can have two values only; one to represent that a process/thread is in the critical section(code that access the shared resource) and others should wait, the other indicating the critical section is free.

On the other hand, counting semaphores take more than two values, they can have any value you want. The max value X they take allows X process/threads to access the shared resource simultaneously.


```

信号灯：Semaphore(1)表示只能运行一个程序，Semaphore(n)可以运行n个线程


###Semaphore in Java

java.util.concurrent package里面有semaphore


看个例子吧@ [File][id]

[id]:https://github.com/KrisYu/OSConceptsExamples/blob/master/CriticalSectionSemaphore.java


```
static class StreamPrinter implements Runnable
{
	static Semaphore sema = new Semaphore(1);

	@Override
	public void run()
	{
		try {
			while (true) {
				byte chars[] = message.getBytes();
				sema.acquire();
				for (int idx = 0; idx < chars.length; idx++) {
					byte achar = chars[idx];
					System.out.write((char) achar);
					Thread.yield();
				}
				sema.release();
			}
		}
		catch (InterruptedException ex) {
			System.err.println(ex.getLocalizedMessage());
		}
	}
}

```

主要常用的就三个：

- 初始化  static Semaphore sema = new Semaphore(1);
- sema.acquire();   获得
- sema.release();   释放


当然这里我们也可以"捣蛋",针对这个File，把初始化那一句改成：

```
static Semaphore sema = new Semaphore(100);

```
可以再次看到混乱|||

这是semaphore为1时的结果

```
Now Is The Time For All Good Men
....

```



这是semaphore为100时候的结果：

```
A nModeT iI   MM ldGF odooooAe  odlm dMlNTFT wrG   lenTlm GlToG GIM lson n TGwrTwwl o Io  o
sll s del eNTo
  FsmhTGFoee T oo Tdwrlddw  IGlA eeohol hGo FolGnG

```

###Fun Facts(真的fun么)


- Semaphore(1)表示只能运行一个程序，Semaphore(n)可以运行n个线程
- negative count stands for waiting process in the queue
- strong semaphore enforce FIFO，所以weak semaphore 有可能会starvation




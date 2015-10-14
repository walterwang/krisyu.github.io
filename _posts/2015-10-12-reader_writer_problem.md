#Reader/Writer Problem

###一类问题

Reader/Writer 不同于之前的，我们需要的点是：

- 多个reader可以一起，因为reader是read-only，不需要mutual exclusive
- writer是mutual exclusive的，同时要block掉reader



###Reader优先

```
/* program readersandwriters */ 
int readcount;semaphore x = 1,wsem = 1;void reader(){	while (true){		semWait (x); 		readcount++; 
		if(readcount == 1)	         semWait (wsem);	    semSignal (x);
	    READUNIT(); 
	    semWait (x); 
	    readcount--; 
	    if(readcount == 0)	        semSignal (wsem);	    semSignal (x);	} 
}void writer() 
{	while (true){ 		semWait (wsem); 		WRITEUNIT(); 		semSignal (wsem);	} 
}
void main() 
{
	readcount = 0;	parbegin (reader,writer); 
}
```

尝试分析，x用来控制reader，然后wsem控制writer

- 如果首先是reader开始执行，那么一旦有了一个reader之后，readcount ==1之时，wsem就把writer给block掉，直到READUNIT结束，直到readcount--，writer才被释放出来,同时在block writer的时候又把semaphore x给释放出来了，这个时候再进别的reader一样都没有问题。
- 当没有reader在执行的时候，writer一旦进入，wsem = 0，开始执行WRITEUNIT，这个时候很显然，别的writer都被再尝试执行都会被block掉，这个时候如果看reader的话，同样同样因为wsem这个semaphore可以把reader都给block掉，所以结果就是如果有一个writer，那么别的writer，以及reader都无法进入

这种reader优先有一个问题可能造成writer starve，因为只要有一个reader再读，writer就无法进入，潜在的问题是writer starvation.


###写者优先

//to be understood and analyzed

其实感觉还是很迷茫，要被比如synchronized ,atomic ...砸晕了...


欢迎指出错误和求交流|||
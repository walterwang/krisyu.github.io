#最终番Critical Section

### Single Object need to be shared


>In all the above, a single object must be shared by all of the threads that are cooperating / accessing the critical section. 在所有的尝试implement critical section中，尝试implement mutual exclusion中，很重要的一点就是需要'synchronized'同一个object.
比如在[compare and swap][id1]中，我们传的word是pass by reference，是为了保证各方都能看到word的变化，这样才能保证mutual exclusion啊，就是要有一个各个threads都能看到，感知到的东西。
[id1]:http://krisyu.github.io/2015/Compare-and-Swap之一个分号引起的悲剧/
在[semaphore][id2]中，看这个semaphore的值,当然semaphore也有其特性，在这一篇的这个semaphore的例子中，并且implement也很可爱，用acquire和release来解决问题。

[id2]:http://krisyu.github.io/2015/semaphore/在[Monitor][id3]中，monitor 同样是 multiple threads 共享从而达到效果的，monitor使用的则是wait和notify关键词
[id3]:http://krisyu.github.io/2015/monitor/



###Semaphore vs Monitor>The sem_wait decrements the semaphore value and will ONLY block if the
semaphore value is less than or equal to zero. On the other hand, a
WAIT in the monitor ALWAYS blocks till a SIGNAL is received.
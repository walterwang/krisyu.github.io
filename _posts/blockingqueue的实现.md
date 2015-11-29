#BlockingQueue的实现

blockingQueue是个老生常谈，既然是老生常谈就一定有其常谈的道理，所以还是得弄懂吧,关键点在于

>A blocking queue is a queue that blocks when you try to dequeue from it and the queue is empty, or if you try to enqueue items to it and the queue is already full. A thread trying to dequeue from an empty queue is blocked until some other thread inserts an item into the queue. A thread trying to enqueue an item in a full queue is blocked until some other thread makes space in the queue, either by dequeuing one or more items or clearing the queue completely.



#Stack/Queue
###Stacks

####FILO

#####Array Based 

```
	+---+---+---+---+      +---+---+---+---+---+
S 	| \ | \ | \ | \ |   ...  \ | \ | \ | \ | \ |
	+---+---+---+---+-     +---+---+---+---+---+
	  0   1    2   3                               t
	  
	  
	  
void push(o)
if t.size() - 1 then 
	throw StackFull
else 
	t <- t +1
 	S[t] <- o
 	
int size()
	return t+1	

object pop()
if empty() then 
		throw StackEmpty
else 
	t <- t-1
	return S[t+1]

int size()
	return t+1

- bool empty()
- object top() 
```		




Space | O(n) | 
------------ | ------------- |
push,pop,size,empty,top | O(1)|



####Linked List Based

肯定是往头上扔，头上删

Space | O(n) | 
------------ | ------------- |
push,pop,size,empty,top | O(1)|
 

用处：
	
- web brower history
- undo
- check parentheses matching/html matching
- ...
	 
	 

###Queues 


####FIFO


#####Array Based 

```

	+---+---+---+---+      +---+---+---+---+---+
S 	|   |   | \ | \ |   ...  \ |   |   |   |   |
	+---+---+---+---+-     +---+---+---+---+---+
	  0   1   2   f              r                

Attention can be made here:
Use size N in a circular fashion
f - front
r - rear 
n - number 

int size()
	return n;
	
boolean empty()
	return n=0

void enqueue(o)
	if size = n-1
		throw QueueFull
	else
		Q[r] <- o
		r <- (r+1) mod N
		n <-  n+1
		
虽然可用空间是N，但是因为如果头和尾接触了，就难以分辨头/尾巴，再则，看一看，r其实是指向最末一个item的后一个位置

object dequeue()
	if empty() then 
		throw QueueEmpty
	else
		f <- (f+1) mod N
		n <- n-1

可以看到这个dequeue没有返回值，这也只是定义的区分，有返回值也无妨

object front()		
		
```

STL是有queue的，然后是一个双向的，有front/back access 
不过倒只有一个push 

各种操作看起来也是O(1)的样子



####Linked List Based

得要有一个front/rear pointer
这样所有操作也是O(1)了


```	
struct node{
	int data;
	node* next;
};
node* front, rear;

```
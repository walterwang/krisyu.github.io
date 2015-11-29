#改些代码LinkedList

###LinkedList 

学期末看学期头的代码应当是觉得可以进步的,假装我也是觉得如此，所以我再看之前写的LinkedList在想是否可以把它OOP,因为可能我第一次写的时候就有这种想法。所以来试试吧，然后C++确有经常越学越沮丧之感，因为感觉我自己太经常google语法了，都已经用了一个学期了也是厉害||||

一直都有一些累积/写法上的问题希望遇到一个C++高手求问，其中的一个就是，比如我写LinkedList写出来可能是这样，比如我不想把自己的head暴露在外面，所以我的head是private的，但同时可能我写count需要传入nodePtr head，想到了两个办法，一个是类似于Java，给head 设定一个getter函数，像这样:


```
LinkedList :: nodePtr :: getHead(){
	return head;
}

....

LinkedList l1;
l1.count(l1.getHead());
```

第二个办法是利用函数重载，像这样，写一个private的count和public的count，然后一个有参数(private)，一个没有参数(public)，public调用private来处理问题即可，貌似我看到这样做的人有，第一种写法则没怎么看到,还是我代码看得太少|||

```
private:
    int count(nodePtr head);

public:
	int count();

....

int LinkedList::count(nodePtr head){
    if(head == NULL) return 0;
    return 1 + count(head->next);
}

int LinkedList::count(){
    return count(head); // pay attention to this return here
}
```
注意调用，然后有返回值，所以还是要用return count(head)，无return，则出错|||

### Reverse List

其实是懒啦，代码没有怎么特别的改，只是OOP化了，都没template化（因为太笨），还是看别人用Java写的OOP的东西小爽....已经一小块的心被Java占领了，下学期假装❤️可以一半被Java占领.

代码还是这样，这里：

[LinkedList-v1_C++][id1]
[id1]:http://krisyu.github.io/2015/LinkedList-v1_C++/
<br />

[肢解真神作linkedlist_reverse_list][id2]
[id2]:http://krisyu.github.io/2015/肢解真神作linkedlist_reverse_list/

即使是现在让我来写reverse list感觉也是有困难的, loop 好棒，用三个pointer：prev，curr，next，curr指向head，prev和next都是NULL，然后每次都更新将next变成curr的next，将curr的next变成prev，同时更新prev和curr，最终把head更成prev就解决问题。


而recursive让我依旧迷茫.用纸笔来做两个nodes ok，但是超过stack就试图让我晕掉。


### 可完备之处

Pass by &/*


同时，越写到后面，越要注意，对于任何可能改变head的操作，需要pass by reference，而其他的就不那么有所谓，pass by value即可。

还有可以加的操作包括 insertAfter, insertBack等等等等

然后OOP后的[LinkedList在此][id3]

[id3]:https://github.com/KrisYu/DataStructure/tree/master/LinkedList





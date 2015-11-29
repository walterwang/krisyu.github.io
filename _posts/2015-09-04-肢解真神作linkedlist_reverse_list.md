#肢解真神作LinkedList Reverse List

###先说ReversePrint###


首先这是一个有趣的问题：
如果只是要ReversePrint那么很简单，用Recursive，然后把cout和ReversePrint换一下位置就好了，比如常见的从1打印到n

```
void listN(int n){
  if(n == 0) return;
  cout<<n<<endl;
  listN(n-1);
}

```
这是从 n 到 1 吧，从 1 到 n 就是交换一下listN（n-1）和cout的位置...


但是现在的问题是要reverse list，要像这样变成这样：

```

head → [1 | ] → [2 | ]→ [3 | ]→ [4 | null] 



 [1 | null] ← [2 | ]← [3 | ] ← [4 |  ] ← head

```


###用Loop来做做看###



```
void ReverseList(node *&head){
  node* prev = NULL;
  node* curr = head;
  node* nextNode = NULL;
  
  while(curr != NULL){
    nextNode = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
  }
  head = prev;
}



```

用上面的例子来看

```
第一次loop前：
  prev = NULL；
  curr = head；
  nextNode = NULL；
  
  
loop中后：
  nextNode = node（1）;
  curr->next = NULL;//node（1）指向NULL
  prev = curr;// prev = head;
  curr = next;// curr  node(1)
  
 
 第二次loop：
 //这个时候curr还是node（1）
   nextNode = node(2);
   curr->next = prev;// node(2)指向node（1）
   prev = curr;//prev为node（1）
   curr = next；//curr为node(2)
   
   
 ...
 
 所以应该有信心，然后来看最后一次loop，当curr为node（1）的时候，之前的node关节已经指好，所以：
 
    curr = node(4)的时候，curr->next == NULL;
    
跳出循环，但是之前的node关节已经指好，这个时候需要解决的问题就一个，我们要把head指向最后一个node；这个时候 prev依旧指向node(4)

    head = prev; 

问题解决
```



###真神作Recusrive Reverse List###

看到真神作三个字我先抖了抖腿|||

首先递归，Recursion，我又抖了抖腿：
把不久前写的一篇先贴过来吧：

[递归の信念](http://krisyu.github.io/2015/递归の信念/)

我已经有了递归の信念：

进击吧，代码(再次抖了抖腿)：


```
void reverseListRec(node* &head){
    node* first;
    node* rest;
    
    if (head == NULL) return;
    
    first = head;
    rest = first->next;
    
    if (rest == NULL) return;

    reverseListRec(rest);    
    
    first->next->next = first;
    first->next = NULL;
    head = rest;
    
}

```

前面都很容易理解，两个特殊的base case，linkedlist为空或者就只有一个node，那么就相当于直接return，点来了，看一个简单例子：

```
head → [1 | ] → [2 | null ]

```
看一下步骤，这里的点还包括，head只是一个nodePtr，是指针：


```
first = head;
rest = node(1);

rest ≠ null
reverseListRec(node(1));

这一步会创造一个stack，继续进入
	reverseListRec(node(1))
	first = node(1);
	rest = node(2);
	
	继续进入
	  reverseListRec(node(2)）
	  first = node(2);
	  rest = null;
	
	回到上一个stack：
	  这个stack里面，first = node(1)
	  first->next node(2)的next指回node(1),list被反转
	  同时node(1)指向null
	  然后head = rest，头指针成功被改变

```

当我尝试用更长的linkedlist时候就头晕了，看不那么懂之前的笔记，然后还假装写下了这些:


关键点


- 每一个stack里面的first/ rest变量要弄清楚
- first->next->next 要这样看 (first->next)->next
- 一旦head成功的指向最后一个node之后，head就不再变化，而node则由后向前串起来了，真神奇，真神作.....



<pre>
	
          |\
        /    /\/o\_
       (.-.__.(   __o
    /\_(      .----'
     .' \____/
    /   /  / \
___:____\__\__\__________________

</pre>



###ZZZ###


如有错误，请多指教。

<a href="http://twitter.com/yuxue1989">Twitter</a>

<a href="mailto:xue_yu@me.com?subject=Hello">Email</a>









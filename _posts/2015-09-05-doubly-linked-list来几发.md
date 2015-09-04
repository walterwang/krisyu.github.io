###Doubly linked list来几发###

###struct node###

```
struct node {
  int data;
  node* prev;
  node* next;
}

```

注意得点 第一个node的prev是接地（NULL），最后一个node指向的next是接地(NULL)...

发现wikipedia有这么多伪码还是真码，反正是改了可用的码：

[Doubly linked list](https://en.wikipedia.org/wiki/Doubly_linked_list)



###只写一个findMid的算法###

条件：

- 不是空list
- 有奇数个node存在

求：

- 中间的node

我的第一反应就是loop，两边往中间走，总会碰头：


```
node* findMid(node* head, node* tail){
  while(head != tail && head && tail){
    head = head->next;
    tail = tail->prev;
  }
  return head;
}

```


当然还要看递归

```

node* findMid(node* head, node* tail){
  if (head == tail)  return head;
  return findMid(head->next, tail->prev);
}

```
奏是这么酷炫...


###如果是singly linked list来找中间呢###


同样奇数个node


```
node* findMid(node* p1, node* p1){
  if(p1->next == NULL) return p1;
  return findMid(p1->next, p1->next->next);
}

```

一个node的，成立；

三个node的，成立；

然后再有递归の信念，所以棒棒的（写到这里其实我要睡着了）


偷懒再去copy一个loop版本的：


```

node* findMiddle(node *head)
{
	if (head == NULL || head->next == NULL) return head;

	node *p = head, *q = head->next;
	while (q != NULL)
	{
		q = q->next;
		if (q != NULL) p = p->next, q = q->next;
	}
	return p;
}
```


###zzz###

如有错误，请多指教。



<a href="http://twitter.com/yuxue1989">Twitter</a>

<a href="mailto:xue_yu@me.com?subject=Hello">Email</a>
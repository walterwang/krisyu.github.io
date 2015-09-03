 
##
 
 linkedlist_v1 file @ <https://github.com/KrisYu/DataStructure>
 
 [返回主页](http://krisyu.github.io )

再写LinkedList
----------

为嘛是再写，其实关于Data Structure，我觉得自己真心已经疼爱过他们一次了，奈何学艺不精，所以一直想找机会再仔细看一次，这样既然再次有了疼爱他们的机会，那么也就认真的再爱一次。


C++ 与 C
----------
C到C++，感觉像折翼的天使。好吧，其实问题的关键是在于不要流程化思维和硬想要的OOP思维。

另外，C++的野心太大：
`template模板/通用编程` 以及 `语法糖` 还有 `编译重载`有的时候让C++读起来显得吓人，晦涩难懂，特别是对于初学者。
还是不能一口吃掉一个大饼，还是先写类似C的C++，再来写像C++的C++.


Mac上编译C++11
----------

```
$ clang++ -std=c++11 -stdlib=libc++ t.cpp
```
不谢

LinkedList_v1 (C style C++？)
----------

###struct node###
```
struct node{
  int data;
  node* next;
}
```

###insert node/val  at head###
值得注意的是： 如果要在头上插入node，这里传入的时```node *&head```
所谓的pass by reference，如果写C的话，那么估计应该写 ```node **head```
```
// pass head by reference, since the head will be changed
void insertFront(node *&head, int n){
    node *tmp = new node;
    tmp->data = n;
    tmp->next = NULL;
    
    if (head == NULL) {
        head = tmp;
    } else {
        tmp->next = head;
        head = tmp;
    }
}
```

###traverse 遍历的方法千千万###

这里其实不引入curr变量应该也ok，因为传入的是node* head，把head这个pointer按值传入

```
void traverse(node* head){
    for (node* curr = head; curr != NULL; curr = curr->next)
        cout << curr->data << " ";
    cout << endl;
}
```

跟for循环异曲同工
```
void traverse2(node* head){
    while (head) {
        cout << head->data <<" ";
        head = head->next;
    }
    cout << endl;
}
```

用递归来traverse
```
void traverseRec(node* head){
    if (head == NULL) return;
    cout << head->data << " ";
    traverseRec(head->next);
}
```

###来寻找一个值/node###

```
bool findVal(node *head, int val){
    if (head == NULL) return false;
    if (head->data == val) return true;
    return findVal(head->next,val);
}
```

还可以返回值的地址
我调皮的打印发现NULL的地址是0x0;
```
node* find(node *head, int val){
    if (head == NULL) return NULL;
    if (head->data == val) return head;
    return find(head->next,val);
}
```

###deleteNode或许可以优化###

```

void deleteNode(node *&head, int n){
    //if not found, just return;
    if (!findVal(head,n)) return;
    
    node* prev = NULL;
    node* curr = head;
    // the delete node is at head
    if (head->data == n){
        head = head->next;
        delete curr;
    } else {
        while (curr->data != n) {
            prev = curr;
            curr = curr->next;
        }
        prev->next = curr->next;
        delete curr;
    }
}
```

没有在这个上面花second thought，挑了一个方便走的方向就赶着走了出来，或许这个是可以优化的

###reserveList才是真神作###

```
void reverseList(node *&head){
    node* prev = NULL;
    node* curr = head;
    node* next = NULL;
    
    while (curr != NULL) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head = prev;
}

```


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

无论是recursive还是loop类型的reverse linked list都让我感觉是真神作算法啊~

P.S. 太懒了，暂时就把代码折让扔着，然后等待更简洁，更可爱，更迷人，更可人的linkelist_v2吧（假装就是这样）


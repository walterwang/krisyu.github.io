 
 linkedlist_v1 file @<https://github.com/KrisYu/DataStructure/tree/master/LinkedList> 已OOP重写
 

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
值得注意的是： 如果要在头上插入node，这里传入的是node *&head

所谓的pass by reference，如果写C的话，那么估计应该写 node **head

//pass head by reference, since the head will be changed


```
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

来试试Recursion版本？

感觉貌似没错？

```
void deleteNodeRec(node *&head, int n){
    if (!findVal(head,n)) return;
    
    node* prev = NULL;
    node* curr = head;
    // the delete node is at head
    if (head->data == n){
        head = head->next;
        delete curr;
    } else {
        deleteNodeRec(curr->next,n);
    }
}

```




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

等待进一步肢解....


###LinkedList自带递归特性###

是么？



###ZZZ###

如有错误，请多指教。



<a href="http://twitter.com/yuxue1989">Twitter</a>

<a href="mailto:xue_yu@me.com?subject=Hello">Email</a>


#继续种树BinaryTree


###BFS vs DFS

上一次的Traverse全是递归，然后是一头往里不断深入，还有传说的BFS，是一层一层的遍历的：


因为不断深入的去寻找本身就有一种递归特性，而Stack又是计算机内部执行函数的必备结构，比如考虑main调用add，就是main stack上面再叠加add stack，最后返回值给main

而BFS则需要一个数据结构来记录每层的node，BFS会用到queue

看伪码


```
enqueue root

while Q is not empty
  dequeue r
  enqueue all children of r
end while

```


 不看伪码，看真码😄
 
 用STL里面的queue
 
 但是需要注意的是stl里面的queue的操作
 
 
 
 | size       | int                                |
|------------|------------------------------------|
| empty      | true/false                         |
| push(item) | insert a copy of the item          |
| back       | return back value, but not remove  |
| front      | return front value, but not remove |
| pop        | remove the next element            |



写法：
q.front() 加上 q.pop() 才构成了 dequeue操作

 
 
 
 ```
 ...
 #include <queue>
 ...
 
void binaryTree::BFS(node* root){
    queue<node*> q;
    q.push(root);
    
    while(!q.empty()){
        node* curr = q.front();
        cout << curr->data<<endl;
        q.pop();
        
        if(curr->left)
            q.push(curr->left);
        if(curr->right)
            q.push(curr->right);
    }
}
 
 ```
 
 别问我为什么还加了验证，不然会有segement fault
 
 
  
 
 
###数数




数数的时候，各种递归特性显示无疑


####数节点
 
 

 
 ```

int treeNodesCount(node* root){
    if(root == NULL)
        return 0;
    else 
        return 1 + treeNodesCount(root->left) + treeNodesCount(root->right);
}

 ```



####数叶子

```
int binaryTree::treeLeavesCount(node* root){
    if(root->right == NULL && root->left == NULL)
        return 1;
    else 
        return treeLeavesCount(root->left) + treeLeavesCount(root->right);
}     

```
 
一些binary Tree的各种节点值都可以求出来了，因为公式

e = i + 1 (外部节点 = 内部节点 + 1)
n = 2*e -1




####数高度
 
顺带赠送了一个三目运算函数

 
 ```
 int treeHeight(node* root){
    if(root ==NULL)
        return 0;
    else 
        return max(treeHeight(root->left),treeHeight(root->right)) + 1 ;
}

int max(int x, int y){
    return x>y ?x:y;
}
 
 ```


当然不写max函数也可以写成


```
return 1 + treeHeight(root->left) > treeHeight(root->right) ? treeHeight(root->left) : treeHeight(root->right) ;

``` 
 
 
 棒棒的
 
 








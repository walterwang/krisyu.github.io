#继续种树之Binary Search Tree


(File)<https://github.com/KrisYu/DataStructure/tree/master/BinarySearchTree>

###定义

在Binary Tree上加限制


```

A binary search tree, T, is either empty or the following is true:
i. T has a special node called the root node.ii. T has two sets of nodes, LT and RT, called the left subtree and right subtree of T, respectively.iii. The key in the root node is larger than every key in the left subtree and smaller than every key in the right subtree.iv. LT and RT are binary search trees.


```

然后可以推测的是

最小的node一定在最左边，最大的node一定在最右边


 
###常见操作


大部分操作，应当必有递归之路


####search


```
bool search(int data, node* root){
    if(root == NULL)
        return false;
    else if (root->data == data)
        return true;
    else
        return search(data, root->left) || search(data, root->right);
}
```

如果非不要递归的话，用一个while loop应该也是可行的


不递归伪码

```
if root is NULL  returns false.else{
  curr = root;   while (!curr)    if (curr->data == data) return true;    else if(current->data > data) curr = curr->left;    else curr = curr->right;}

```



####insert



#####非递归版本

```
void binaryTree::insert(int data){
    
    node* newNode = new node;
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    
    node* curr;
    node* currTail;
    
    if(root == NULL){
        root = newNode;
    } else {
        curr = root;
        
        while(curr != NULL){
            currTail = curr;
            if(data > curr->data){
                curr = curr->right;
            } else {
                curr = curr->left;
            }
        }//end while
        
        if(data > currTail->data)
            currTail->right = newNode;
        else
            currTail->left = newNode;
    }
    cout << "Inserted " << data <<endl;
}

```

#####递归版本


#####方法一

在递归版本里，处理root为空是件麻烦事

可以这样写，利用重载，然后一个public，一个private，也正好起保护作用


```
void insertRec(int data){
    
    if(root == NULL){
        node* newNode = new node;
        newNode->data = data;
        newNode->left = NULL;
        newNode->right = NULL;
    
        root = newNode;
        cout << "Inserted " << data <<endl;
    } else 
        insertRec(data,root);
}


void insertRec(int data, node* root){
    
    node* newNode = new node;
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;         
    
    
    
    if(data > root->data){
        if(root->right == NULL)
            root->right = newNode;
        else
            insertRec(data,root->right);
    } else {
        if(root->left == NULL)
            root->left = newNode;
        else
            insertRec(data,root->left);
    }
    cout << "Inserted " << data <<endl;

}


```

#####方法二


再看另一个办法，也是精巧

```
void insertRec2(int data){
    root = insertRec2(data,root);
}

node* insertRec2(int data, node* root){
    
    node* newNode = new node;
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;         
    
    if(root == NULL){
        root = newNode;
    } else {
        if(data > root->data){
            root->right = insertRec2(data,root->right);
        } else {
            root->left =  insertRec2(data, root->left);
        }
    }
    return root;
}

```


###delete


delete貌似比较麻烦，
考察一颗BST（binary search tree）

因为要求删除之后依旧要是BST



```
		60
	   /  \
	  50   70
	 /  \   \
	30  53  80
   /
  23 

```



可能有以下几种状况

- 删除的是一个叶节点，比如80
- 删除的节点右节点为空，比如30
- 删除的节点左节点为空，比如70
- 删除的节点既有左节点，也有右节点，比如50


对应状况分析：

- 叶节点： 父节点指零，然后释放内存 
- 左节点为空，父节点指向右边孩子
- 右节点为空，父节点指向左边孩子
- 如果左右子树都非空的话，那么可能需要找到左子树的最大值或者右子树的最小值，然后将其放到需要删除的值处，然后这样就转化为删除只有一个孩子的结点的状况

注意最后一步的逻辑，`左子树的最大值/右子树的最小值`这样放回应该能够依旧保留Binary Search Tree的大小的顺序

这个delete node的递归算法真乃神人也


```
node* deleteKey(int data, node* root){
    if(search(data,root) == false)
        cout<<"No such node exists\n";
    if(data == root->data)// find the node to delete
    {
        if(root->left && root->right){//left && right nodes exits
            node* tmp = findMin(root->right);// the min of right tree
            root->data = tmp->data;
            root->right = deleteKey(root->data,root->right);//delete the min of the right
        } else {
            node* tmp =root;
            if(root->left == NULL)
                root = root->right;
            else if(root->right == NULL)
                root = root->left;
            free(tmp);
        }
    }
    else if (data < root->data)
        root->left = deleteKey(data, root->left);
    else
        root->right = deleteKey(data,root->right);
    return root;
}


```





###找最大/找最小值



单看一颗Binary Search Tree的最大值/最小值，跳题一下

根据定义： 最大值一定在最右边，最小值一定在最左边



```

node* findMin(node* root){
    if(root == NULL) return NULL;
    if(root->left == NULL) return root;
    else return findMax(root->left);
}

node* findMax(node* root){
    if(root == NULL) return NULL;
    if(root->right == NULL) return root;
    else return findMax(root->right);
}

```







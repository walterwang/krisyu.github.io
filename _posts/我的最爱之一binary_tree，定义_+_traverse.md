#我的最爱之一Binary Tree，定义 + Traverse


###定义


Binary Tree的定义就很美：

  - T has a special node called the root node.  - T has two sets of nodes, LT and RT, called the left subtree and right subtree of T, respectively.  
  - LT and RT are binary trees.

一种递归的美感，当然🌲本身也很美，很有趣，无论是自然界的还是数学中的.


A Christmas Tree


```

              \ /
            -->*<--
              /_\
             /_\_\
            /_/_/_\
           /_\_\_\_\
          /_/_/_/_/_\
         /_\_\_\_\_\_\
        /_/_/_/_/_/_/_\
       /_\_\_\_\_\_\_\_\
      /_/_/_/_/_/_/_/_/_\
     /_\_\_\_\_\_\_\_\_\_\
    /_/_/_/_/_/_/_/_/_/_/_\
             [___]


````


###Node###

简单写法，对于一棵树,
对于一棵树，我们知道的就是 root;


```
struct node{
	int key;
	node *left;
	node *right;
};
```


野心写法
我目前的水平就写上一种就好了


```

template <class elemType> 
struct binaryTreeNode{
	elemType info;
	binaryTreeNode<elemType> *llink;
	binaryTreeNode<elemType> *rlink;};


```


###Traverse###

因为Binary Tree（貌似翻的二叉树吧）本身的定义就很递归，所以无数的递归算法可以涌现在我的眼前，但是就先看Traverse吧：


```
                A
               / \
              B   C
               \
                D
 
```

看这颗树：


PreOrder:
node -> left -> right



```
void InOrder(node *root)
{
  if(root == NULL) return ;
  print(root);
  InOrder(root->left);
  InOrder(root->right);
}

```




Inorder：
left -> node -> right


```
void InOrder(node *root)
{
  if(root == NULL) return ;
  
 
}


```






PostOrder:
left -> right -> node









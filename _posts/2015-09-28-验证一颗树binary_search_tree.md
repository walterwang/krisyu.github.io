#验证一颗树Binary Search Tree

###error prone


当我们有了一个binary tree，需要验证它是否一颗binary search tree之时，乍一想，就检查每个node是否比它的左node大，比右node小，马上一个递归算法出现。


但是其实这样并没有包含所有状况，出错鸟

```

     20
    /  \
  10    30
       /  \
      5    40
      
      
```

这并不是一颗binary search tree（5 怎么能在 20的右子树呢），但是也满足上述条件，所以这个题目还真是error prone啊

所以我们需要做的事：


>
 - 如果是left child，首先要小于node（明显的）
   - 其次left child 的右子树，其值都应该小于node
- 如果是right child，首先要大于node
   - 其次right child 的左子树，其值都应该大于node
   

###涌现的算法



根据上述条件，也很容易涌现算法。

比如可以用一个类似BST的算法，然后把left child 的 right subtree存在一个queue里面，然后之后再做比较大小的事

伪码来一发，就是可以这么任性的不考虑时间\空间复杂度

```
vector<int> v;
queue<int> q;

q.enqueue(root);

while(!q.isEmpty()){
	int node = q.dequeue();
	
	q.push_back(node);
	if(q->left) q.enqueue(q->left);
	if(q->right) q.enqueue(q->right);
}

 
```

这样我们就把一颗树的值都存在了vector v里面，这样来比较大小就很方便



###递归算法


摘自wikipedia

这个算法的好处应该就是没有使用额外的结构，然后就把node的值传下去比较


```
A recursive solution in C++ can explain this further:

struct TreeNode {
    int data;
    TreeNode *left;
    TreeNode *right;
};

bool isBST(TreeNode *node, int minData, int maxData) {
    if(node == NULL) return true;
    if(node->data < minData || node->data > maxData) return false;
    
    return isBST(node->left, minData, node->data) && isBST(node->right, node->data, maxData);
}

```

The initial call to this function can be something like this:

```
if(isBST(root, INT_MIN, INT_MAX)) {
    puts("This is a BST.");
} else {
    puts("This is NOT a BST!");
}

```


还专门为作业写了一篇，真是感动 ヽ(ﾟ´Д`)ﾉﾟ


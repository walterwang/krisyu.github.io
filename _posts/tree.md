#Tree

###Terminology

大部分的概念都是通用的，但是各学派好像在高度方面的认知略不同(是么，还是我的错觉)。i.e.:


- Depth of a node: number of ancestors
- Height of a node : the number of descendants- Height of a tree: maximum depth of any node (3)根据这个定义，只有root的树高度是0

再几个常见概念
binary tree - may like this 可以缺一个孩子
		o
	   / \	  o   o
	   \		    o
		full binary tree - may like this 问题是在于要么两个孩子，要么零个孩子
		o
	   / \	  o   o
	 	 / \			o   o
	complete binary tree - may like this 除去最后一层，都满，然后最后一层缺孩子也是缺右边
		o
	   / \	  o   o
	 / \		o   o
	
perfect(proper) binary tree

		 o
	   /  \	  o    o
	 / \  / \		o   o o  o
	
###Traverse

PreOrder,PostOrder,InOrder都不算难写，而这个pre/post/in是指root被cout的状况.


```
				+
			/     \
		   *       *
		 /   \    / \
		2     -  3   b
		     / \
		    a   1
		    
 ```

倘若想打出好看/正确的表达式的话，稍改一下inorder traverse就行，print "(" before traversing left subtree, print ")" after traversing right subtree.

```
void printExpression(root v){
	if(root != null)
	{
		cout << "( "
		printExpression(root->left);
		print(root);
		printExpression(root->right);
		cout << ")"
	}
}

```
上述伪码待测

当然也有同样略改postorder traverse来求值。

			
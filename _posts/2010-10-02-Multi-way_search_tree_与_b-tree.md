# Multi-way search tree 与 B-Tree

### Multi-way(m-way) search tree

#### defination

m-way search tree，不管它叫什么了，一开始让人小迷茫，首先是它把key 和 pointer分开了， 为什么它想这么做呢？

但是其实看到图还是觉得满符合直觉的，比如如果我想做一个英文字典，那么我可能就会想用m-way tree吧，感觉是这样的，比如每格装字母，有路径的就是一个单词（是么？自己也开始迷茫）：


再看看定义：


```
 
 
	+----+----+----+----+----+----+---+-----+-----+------+------+
	| T0 | k1 | T1 | k2 | T2 | k3 | . |km-2 | Tm-2| km-1 | Tm-1 |
	+----+----+----+----+----+----+---+-----+-----+------+------+



```


A multi-way (or m-way) search tree of order m is a tree in which ：- Each node has at-most m subtrees, where the subtrees may be empty. - Each node consists of at least 1 and at most m-1 distinct keys - The keys in each node are sorted.

The keys and subtrees of a non-leaf node are ordered as:		 T0, k1, T1, k2, T2, . . . , km-1, Tm-1	such that:
		 - All keys in subtree T0 are less than k1.- All keys in subtree Ti , 1 <= i <=  m - 2, are greater than ki but less than ki+1.- All keys in subtree Tm-1 are greater than km-1



再看一下binary search tree，m-way tree其实其特别之处是在于把node和key分开， 这样的好处是在于摆脱了node的结构之后，更加灵活？ 


>
Binary search tree: 1 value and 2 subtrees per node.
>
M-way search tree: M - 1 values and M subtrees per node. M is the degree of the tree.

当然，bi的度就是2嘛.

总的来说，感觉multi-way search tree还是没有那么多限制的：

>
Note: In a multiway tree:
>The leaf nodes need not be at the same level.>A non-leaf node with n keys may contain less than n + 1 non-empty subtrees.
#### insertion & deletion

对于MST(m-way search tree)的insert 和 deletion，感觉基本没有什么限制：

insert就直接从leaf开始grow

对于deletion，需要复习一下 successor 和 predecessor的概念：

 -  successor :  min value of right subtree (右子树的最小值，也就是刚好比要删除的值大一点的值）
 -  predecessor :  max value of left subtree （左子树的最大值，刚好比要删除的值小一点）
 


### B-Tree

####Defination


A B-tree of order m (or branching factor m), where m > 2, is either an empty tree or a multiway search tree with the following properties:
- The root is either a leaf or it has at least two non-empty subtrees and at most m non-empty subtrees.- Each non-leaf node, other than the root, has at least ⎡m/2⎤ non-empty subtrees and at most m non-empty subtrees. (Note: ⎡x⎤ is the lowest integer >  x ).- The number of keys in each non-leaf node is one less than the number of non-empty subtrees for that node.- All leaf nodes are at the same level; that is the tree is perfectly balanced. 
B-Tree 的 b stands for balanced，叶子全在一层这个点是可爱的。然后看起来的确算很对称。


|        |       Root node    | Non-root node
| ------------ | ------------- | ------------ |
| Minimum number of keys  |  	1  | ⎡m/2⎤ -1 |
| Minimum number of non-empty subtrees | 2  | ⎡m/2⎤ |
| Maximum number of keys |   m-1  |   m-1 |
| Maximum number of non-empty subtrees | m | m


当然这里没有考虑root是一个leaf的情况， 不过这个图感觉还是要消化一下。消化然后内化。


#### Insertion

因为要保持B-Tree的balance，所以相比m-way tree的insert和delete相对就会复杂一点：

首先插入是从叶子开始插入，但是同时因为有可能会插入之后key过多（overflow），所以插入所导致的结果可能就是split，然后因为split，就把middle key 上浮，上浮之后如果依旧overflow，可能要新建一个root node...



```
OVERFLOW CONDITION:     A root-node or a non-root node of a B-tree of order m overflows if, after a key insertion, it contains m keys.Insertion algorithm:     If a node overflows, split it into two, propagate the "middle" key to the parent of the node. If the parent overflows the process propagates upward. If the node has no parent, create a new root node. Note: Insertion of a key always starts at a leaf node.
```



####Deletion

首先，基本思路是， deletion也是要从叶子节点开始，如果要delete的并不是leaf，那么交换其与其successor和predecessor（这种一定是leaf），然后再删除。


正如Insertion可能导致Overflow一样，节点数过多。
Deletion可能会导致underflow，就是包含的节点数太少，无法达到要求:


```
UNDERFLOW CONDITION:		A non-root node of a B-tree of order m underflows if, after a key deletion, it contains  m / 2 - 2 keys	The root node does not underflow. If it contains only one key and this key is deleted, the tree becomes empty.

```
 <br />

```
Deletion algorithm:     If a node underflows, rotate the appropriate key from the  adjacent right- or left-sibling if the sibling contains at least m / 2  keys; otherwise perform a merging.A key rotation must always be attempted before a mergingThere are five deletion cases: 1.  The leaf does not underflow.  2. The leaf underflows and the adjacent right sibling has at least m / 2   keys. 			perform a left key-rotation  3. The leaf underflows and the adjacent left sibling has at least m / 2   keys. 			perform a right key-rotation  4. The leaf underflows and each of the adjacent right sibling and the adjacent left sibling has at least m / 2   keys.			perform either a left or a right key-rotation 5. The leaf underflows and each adjacent sibling has m / 2  - 1 keys.			perform a merging
```对我来说，困难的点在于merge，其实merge和split也很对称，split是从底部往上增加nodes，merge是从上方往下走，看一个例子
 <br />
```
delete 10 in this case

	 	       9 
		 /            \
	  3   7           12    /  \   \         /   \    1  4 5   8	   	10    13```



```
a.

	 	       9 
		 /            \
	  3   7           12    /  \   \            \    1  4 5   8	   	      13```


这样underflow， 这样需要perform merge， 注意的点是merge往下走：



```b

	 	       9 
		 /            
	  3   7               /  \   \            \    1  4 5   8	   	    12 13```
我觉得很要紧的点是如果把上一幅图画成这样，我就会更迷茫一些：


```b'

	 	       9 
		 /           \
	  3   7         12 13     /  \   \                1  4 5   8	   	    ```所以最终的结果是：
```c
	  3   7    9       /  \   \    \             1  4 5   8  12 13 
```

所以最终 shrink down one level 如c所示，不过感觉deletion还是很容易出错。




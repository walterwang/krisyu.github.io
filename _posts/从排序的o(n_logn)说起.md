#知其所以然

最近看了刘未鹏的几篇关于算法的文章，深有感触。


###基于比较的排序

看到了证明-基于比较的排序optimal bound是O(nlogn)，觉得有点震惊，有点太棒.

首先使用了一个模型，叫做decision tree,每个vertex代表一个decision，然后每个leaf代表一种可能的outcome，因为排序的数是n个，那么其实最终结果可能有n!种排法，然后又根据树的一个定理

> If a m-ary tree of height h has l leaves, then h ≥ ⌈log<sub>m</sub>l⌉, if the m-
ary tree is full and balanced, then h = ⌈log<sub>m</sub>l⌉.

以上这个定理的证明有意思....

所以这颗比较树的高度至少是 logn! = O(nlogn),所以至少需要O(nlogn)次比较.


### 找假金币问题

很多变种的题目，找轻的金币，轻的小球。

8个金币，其中一个假的轻，一个天平，最少必须称几次可以找出假的金币.
答案是2次.


称法的第一步其实比较counter-intuitive，不是对半来称，而是选6个，3/3称，如果有任一方轻的话，第二次选2个，1/1称..如果平衡就称余下两个.所以最多需要称两次.

答案是 ⌈log<sub>3</sub>8⌉ = 2

这个问题的解法关键是第一步就要想到，不能对半来称，类似decision tree，如果想降低树的高度，因为树的高度决定了time complexity，把树尽量的摊开就能减少树的高度。所以第一次的称法一定不是对半称。

感觉上是这种问题都可以generalized化.



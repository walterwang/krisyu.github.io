---
layout: post
title: "不错的学习 max flow 的资料"
---




#### Ford–Fulkerson方法

几个link:

topcoder出品，基本精品

- [maximum-flow-section-1-topcoder](https://www.topcoder.com/community/data-science/data-science-tutorials/maximum-flow-section-1/)
- [maximum-flow-section-2-topcoder](https://www.topcoder.com/community/data-science/data-science-tutorials/maximum-flow-section-2/)
- [wikipedia Ford–Fulkerson算法](https://zh.wikipedia.org/wiki/Ford–Fulkerson算法)



有几个有意思的点，Ford–Fulkerson是方法不是算法，我们在residual graph里面寻找augmenting path使用不同的算法（DFS / BFS)， 用DFS（或者随意寻找路径）可能会增大工作量以及最终不会converge.

wikipedia 还赠送了一个python实现版本。


这个寻找路径用的是DFS。这里寻找augmenting path 给了三个条件：


- residual > 0
- edge 不在 path 中
- redge 不在 path 中 

配备这三个条件是为了防止一直loop回路？ 比如 A -> B -> A -> B (? unsured here



wikipedia给了一个算法最坏情况，但是实际尝试也不太容易重现这个最坏算法，因为电脑内部存储的原因，每次从一个vertex开始，寻找edge都按一定顺序来寻找。



我在此处建了一个类似的图来测试，但是路径DFS出来也是：



```
A - B - C - D
A - B - D
A - C -B - D
A - D
```


不是worst case，当然也不是best case。所以我有修改版本，用BFS来求路径，这个一定就是最优了（嘿嘿 

path就是

```
A - B - D
A - C - D
```


> Ford–Fulkerson算法的运行时间为O(Ef)（参见大O符号), E图中的边数，f为最大流。 这是因为一条增广路径可以在O(E)的时间复杂度内找到，每轮算法执行后流量的增长至少为1。但是在极端情况下，算法有可能永远不会停止。

实际上老师是不愿意跟我们讨论这个算法的时间复杂度的，因为可能不converage.

#### Edmonds–Karp算法 

这个算法说起也就是在FF方法里面用BFS来找 augmenting path， 但是这个就带来了一个时间复杂度“低一些”的算法 O(VE)。

非常牛的与 capacity 完全无关的时间复杂度证明见clrs.


#Disjoint sets

### Defination

partition 的概念定义了disjoint sets，partion的概念数学中也常见.然后disjoint sets最常见的三个操作:

- make-set(x)
- union(x,y)
- find-set(x)


其实之前写Kruskal Algorithm已经用到disjoint sets了，然后即使是'最笨的'disjoint sets写法、用法也觉得好神奇...
比如[wikipedia][id]上的最简单的伪码写法，是这样，我也觉得这个find好棒...更何况提高版了...
 
[id]:https://en.wikipedia.org/wiki/Disjoint-set_data_structure



```
function MakeSet(x)
    x.parent := x
     
function Find(x)
    if x.parent == x
       return x
    else
       return Find(x.parent)
       
function Union(x, y)
    xRoot := Find(x)
    yRoot := Find(y)
    xRoot.parent := yRoot

```
有一个[super simple disjoint set][id2]，基本implement如wikipedia，这种的好处是union
是O（1），但find可能会退化为O(n)...

[id2]:https://github.com/KrisYu/DataStructure/blob/master/DisjointSet/superSimpleDisjointSet.cpp



###提高版

可以提高的方法有：

- balanced union 
- find with path compression

balanced union

一个是weight rule，nodes少的指向nodes多的root，但并不是更新每个nodes的root.

另一个是height rule，height低的指向height高的root，同样并不更新每个nodes的root.


find with path compression的思想就是就是一步步的找到其指向的root，同时在寻找之后将其parent全部更新为root，这样感觉也很棒..

另外，除了上面写的把一开始把 a.parent = a 之外，还可以搞别的特殊化，比如把其设置成0，或者整棵树的size（负的），这样特殊化很可爱，处理起来也很快

尝试写了一个，用了10个数来测试，没出错。但素但素用来做一个题目segment fault了||||
所以待修改，待更新

 

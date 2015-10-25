#Graph Theory 


依旧是图，最近真是各种课都在graph theory，枪炮与玫瑰齐飞的感觉。


###Relation

首先纯math中的relation直接上手反而会迷茫，不如先看具体的例子，然后再抽象来理解这个relation.
各种比如binary relation, relation on sets, reflexive, symmetric, antisymmetric, transitive, 然后还有combining relations真是把我小弄昏了一会。

这个时候我就需要突然想起了当年学各种再突然想起了读lixiaolai的博客，所以来quote一番。


>其实吧，所有的教科书其实都是一样的，你看这化学书、这物理书、这生物书，其实都是一回事儿……每一章吧，重点其实都是一些概念。

> - 先告诉你这个概念是什么意思，就是『定义』；
- 然后给你讲清楚它的内涵、外延；
 - 然后再讲用这个概念的时候需要注意什么；
- 如果必要的话，还要讲这个概念和其它的概念区别究竟是什么；
- 剩下的就是通过练习，让你熟练地、正确地使用这个概念……
- 最终，你的世界观就是通过对一系列的概念的理解形成的，你的行为其实就是使用这些概念的结果……



###Graph Coloring Problem


Given a graph G and K colors, assign a color to each node so adjacent nodes get different colors.


The minimum value of K for which such a coloring exists is the Chromatic Number of G.


NP-Complete problem

```

   a - b       wed  5 - 7 pm   
   | / |            7 - 9 pm
   c - d            9 - 11 
   		\           11  - 1 
   		 e           1 - 3


```



Greedy Algorithm

- order the vertiex
- order the color
- try the possible color

**A graph with maximum degree at most k is (k+1)-colorable** can be proved via induction 


###Path

Let R be a relation on A, There is a path of length n, n ≥ 1, from a to b iff (a,b) ∈ R<sup>n<sup>.


这个其实不难想到，因为transive等等等，比如有(a,x) (x,b) 那么必定可以有(a,b)

###Poset

Partial Order Set，这个晕了好一会，直到出现Hasse diagram，假装才小明白一会为嘛要叫partial order set，因为antisymmetric保证了这个set没有环的存在，所以也就算partial order吧。



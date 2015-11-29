#Relation，啥？ Relation

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




###基本概念

1. Binary Relation : subset of AxB
2. Relations on set
   - reflexive
   - symmetric
   - antisymmetric
   - transitive
   
只有先掌握基本概念才能进阶，然后基本概念就能引出很多很有趣的问题，还可以值得注意的是symmetric和antisymmetric并非opposite关系，一个relation可以既是symmetric又是antisymm，既不是symmetric也非antisymmetric，一切都跟着定义走，而基本概念的能力和趣味可能也要之后才能发挥。


### Represent Relations Using Digraph

一开始represent relation用的table，用matrix，用的graph，用directed graph简直就是intuitive，因为AxB，（a,b）是ordered pair，而vertices则是Set A (Set B)...

然后再intuitive的有：

reflexive : every node has a loop

symmetric : kind of like undirected graph

当然matrix里面也很intuitive，比如关于对称性和对角线上的元素值。


### Transitive 

把两件事放在一起来看，很有意思，先看第一个定义：

>R on A is transitive iff R<sup>n</sup> ⊆ R for n = 1,2,3....

然后计算transitive closure：
R<sup>*</sup> = R ∪ R<sup>2</sup> ∪ ... ∪ R <sup>n</sup>

那么比如对于那种 R<sup>n</sup> ⊆ R 的relation 其transitive closure就是R，简直了，都不用计算，而这种情况说明的问题则是这个graph其连通性直接看其本身就可以了，比如R中有（a,b），那么a是直接可到b的，而无（a,c），那么a，c之间一定无路径.



最后，需要pin在脑中：
a divides b means b/a equal zero.
#Concept Learning

### Definations

>The problem of inducing general functions from specific training examples is central to learning.

>Concept learning: Inferring a boolean-valued function from training examples of its input and output.

判断是与否，直接可以推断learning algorithm/function应当是产生两个discrete value : 0 与 1.或者说这个function是一个boolean values.


> The inductive learning hypothesis : Any hypothesis found to approximate the target function well over a sufficiently large set of training examples will also approximate the target function well over other unobserved examples

这里依旧有上一次的迷思，因为这个function是在现已有的training set中得出，不一定适用于完全未观察到的，所以这里有这个假设，就像checker game，让机器与机器玩，很大的问题是可能机器走的路数完全与人不一样，training环境与实际工作环境完全不一致。（如同有些公司的training|||）


### Find-S Algorithm


More general than： 

Given hypotheses h<sub>j</sub> and h<sub>k</sub>,h<sub>j</sub> is more-general-thanm-- equaldo h<sub>k</sub> if and only if any instance that satisfies h<sub>k</sub> also satisfies h<sub>j</sub>.

```
1. Initialize h to the most specific hypothesis in H
2. For each positive training instance x
     - For each attribute constraint a, in h			If the constraint a, is satisfied by x			Then do nothing			Else replace a, in h by the next more general constraint that is satisfied by x
3. Out put hypothesis h
```

好像算法还蛮能make sense的，因为感觉整个是用partial order来取代，最终是由specific能找到general的...

然后值得注意的是，这里只用看positive training instance.

除去讲到的几个问题以外，有思考之处包括:是否可以有 Find-G Algorithm，这是从general到specific，可以从specific到general么，如果很多都是instacne都是negative的话，那么在这样的情况下find-s和find-g是mathmatics相等么...




###  CANDIDATE-ELIMINAT algorthim

> The CANDIDATE-ELIMINAT algorthim finds all describable hypotheses that are consistent with the observed training examples


most specific → {<∅,∅,∅,∅,∅,∅>}

most general → {<?,?,?,?,?,?>}


```
Initialize G to the set of maximally general hypotheses in H
Initialize S to the set of maximally specific hypotheses in H
For each training example d, do
	If d is a positive example
		Remove from G any hypothesis inconsistent with d
		For each hypothesis s in S that is not consistent with d
			Remove s from S
			Add to S all minimal generalizations h of s such that 
				h is consistent with d, and some member of G is more general than h
			Remove from S any hypothesis that is more general than another hypothesis in S
	If d is negative example
		  Remove from S any hypothesis inconsistent with d
		  For each hypothesis g in G that is not consistent with d
			Remove g from G
			Add to G all minimal generalizations h of g such that 
				h is consistent with d, and some member of S is more general than h
			Remove from G any hypothesis that is more general than another hypothesis in G

```

这里有一篇写的巨好的[解释][id]，虽然看这个算法描述还是有点略迷茫.

[id]:http://stackoverflow.com/questions/22625765/candidate-elimination-algorithm

然后candidate-eliminat algorithm的好处是，最终给了version space，相当于给了解空间，不像find-s找到的是最specific的那一个，实际上可能有更general的满足。

###  implement尝试

#####findS :

然后google了一下，有人尝试implement的，所以模仿了一下，findS好理解，然后implement也不难.

因为是像我这样处理数据不太要脸的implement的|||

首先只用处理positive的状况，然后总是用next more general来处理.

#####elmination candidate

implement的关键是理解：

 - consistent : consistent是一方为？或者两个相等才能算consistent
 - 从specific 到 general的顺序为 : ∅ → a specific word → ?
 - positive 和 negative 都要处理边界问题，同时要写出正确的more general 和 more specific函数

#####real life：
这两个算法因为其对noise的忍受太弱，无法处理，所以基本没有实际使用，但是连introductory的算法都读起来觉得不容易，也是啧啧啧了（Python学太差）.
 
 


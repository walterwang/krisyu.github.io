#Bipartite graph and Coloring 

###Bipartite graph

“二部图”，这个翻译也是厉害。看到写它的application,写的是job assignment，忍不住想再加hetro sex/marriage，哈哈哈哈。

记得很早之前看过一个纪录片，关于性的，这是一个异性恋之间的调查，然后调查显示每个男人平均每周sex6次，但是女生2次，数字已经记不清，乱编的。

但是这样不对啊，假设调查样本已经足够广了，而且男女人数也类似,那多出来的4次是咋回事呢？

哈哈哈哈，后来在网络上在做了一个类似的统计，才调查出更加符合“真实”状况的结果，因为假设是同一群之间的调查，那么每次♂x♀，必定也发生了♀x♂....哈哈哈哈，比如这个地方一共有4个男人，3个女人，那么他们之间形成的的是bipatite graph，虽然我个人更prefer ♂♂ | ♀♀ | 🌈...但是只是在纯数学

```
			M   ---		W
			M			W
			M	---     W
			M

			这个图画的太纯洁了....
```

他们之间的undirected graph的edge数一定相等的，而男/女之间的sex次数之比应该是 M x Mansex = W x Womansex, thus我们知道sex之比。

而不少美剧（gossip girl）之间的sex关系则是 complete bipartite graph，哈哈哈哈，足够乱...然后我不歧视异性恋....

还有一个有意思的是C<sub>6</sub>， cycle 6是一个bipatite graph，C<sub>5</sub>则不是

```
		   • - •                          •
		  /     \                      /    \
		 •       •                    •      •
		  \     /                     \      /
		   • - •                        • - •
```

重画一下图就能发现，很容易知道/想到如果是奇数的环的话，当然就不可能是bipartite graph。但是偶数的图一定就是bipatite graph么？

seemed so，因为这个bipatite graph又可以变成2-colorable问题，我直觉感受是的，因为如果是偶数的话，始终可以用两个颜色来涂相邻的vertices.



###Graph Coloring Problem

这是大部分人接触graph theory第一次听到的问题吧...

Given a graph G and K colors, assign a color to each node so adjacent nodes get different colors.


The minimum value of K for which such a coloring exists is the Chromatic Number of G.


NP-Complete problem, judge isomorphism also a NP-Complete problem.
Till now , I know p is stand for polynomial

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

感觉反正应该从degree大的vertex开始处理..

**A graph with maximum degree at most k is (k+1)-colorable** can be proved via induction 








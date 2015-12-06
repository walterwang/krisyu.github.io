#Bellman–Ford算法


###前提

前提是:

- the graph is connected 
- no negative cycles

可以有negative edge


###Bellman–Ford算法

看伪码:


```
for v in V:
	v.d = ∞
	v.π = None
s.d = 0
for i frome 1 to |V| -1 :
	for (u,v) in E:
		relax(u,v)
			if v.d > u.d + w(u,v):
				v.d = u.d + w(u,v) 
```

Bellman-Ford的关键点则是针对每个顶点，释放所有的边，然后则用类似的方法处理。
并且时间复杂度一眼可以看出来是O(mn)



然后查了stackoverflow：

<http://stackoverflow.com/questions/6799172/negative-weights-using-dijkstras-algorithm>

得票很高的回答很棒.同时下方的补充也很棒:

> Dijkstra being a greedy algorithm is the reason for its short-sighted choice.

它每步都要选最优的，可能就会错过一些选择，wikipedia做的关于largest path的gif就很能说明问题。因为Dijkstra每次都选最短释放，然后每次都选最短的相邻的释放，



而Bellman-Ford之所以可行的原因是因为每次都释放所有边，然后就有所有的更新了。

Bellman-Ford的关键点在于它每次都在算边，对边排序（不排序也OK）之后再针对每个顶点释放。

//虽然我迄今也没有搞懂Bellman-Ford如何detect negative cycle.

然后特别注意Bellman-Ford是dynamic programming， 其实很能感觉，因为每一步都是在前一步的基础上操作，同样的还有Floyd-Warshall算法（虽然我看到这个是用来看connectivity的，但是貌似同时解决pair shortest path）。
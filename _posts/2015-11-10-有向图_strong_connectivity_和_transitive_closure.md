#Strong Connectivity和Transitive Closure

### Strong Connectivity

这个问题有意思，对于有向图，如何判断其连通性，依旧strong connectivity定义是任两顶点之间可达。第一个想法当然是可以用DFS来判定，因为DFS可以看是否可以从一个点到任何其他点，但是又因为有向图之间的edge是有向的，所以如果用DFS则要针对所有顶点来判断。时间复杂度很高。

动脑一想，其实可以用一个trick的做法，就是每次DFS检查一下逆向的edge是否存在，这样就可以完毕的检查了。或者生成一个对称的逆向的图。


###Transitive Closure

transitive closure正好和最近的离散数学联起来，connectivity relation.然后在数学中已经证明：

R<sup>*</sup> = R ∪ R<sup>2</sup> ∪ ... ∪ R <sup>n</sup>

所以有我们的Floyd-Warshall’s Algorithm，同样，属于不难想到和理解的算法，但是需要注意的是，求并集，每次都要在新的图（that is， 新加的边上操作）.


```
k -> middle node
i -> comming edge from i to k
j -> outting edge from i to j


for k from 1 to n:
	for i from 1 to n (i ≠ k):
		for j from 1 to n(j ≠ i,k):
			if adjacent(Vi,Vk) and adjacent(Vk,Vj)
				if not adjacent(Vi,Vj)
					addEdge(Vi,Vj)
		
```
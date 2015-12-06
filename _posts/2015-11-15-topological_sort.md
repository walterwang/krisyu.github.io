#DAGs and Topological Sort

###DAG(directed acyclic graph )

首先这个graph是要有向无环图,或者是离散数学中的partial order的状况。
partial order其实也就是无环的状况.

Theorem : A poset has no directed cycles other than self-loops.

证明可以用反证法，可以利用antisymmetric 和 transitivity 可以证明.


###数学课 -> CS课
 
看discrete math课上的伪码：
 
```
procedure topological sort
k := 1
while S ≠ ∅
begin 
	ak := a minimal element of S
	S := S -{ak}
	k := k + 1
end {a1, a2,...., an is a compatible total ordering of S}

```

其实是很直觉的做法。

Data Structure课出现的第一个伪码:

```
Algorithm TopologicalSort(G)      H <- G	// Temporary copy of G      n <- G.numVertices()      while H is not empty do
      	Let v be a vertex with no outgoing edges		Label v <-  n		n <-  n − 1		Remove v from H
```
这个remove同时是会将incident edges remove掉的，其实跟上面的算法异曲同工啊....

只是一个看入度，一个看出度，然后

然后来看一看data structure课上可能出现的对应伪码：

```
void TopSort(){
	for( cnt = 0 ; cnt < |V| ; cnt++){
		V = 未输出的入度为0的顶点
		if (这样的V不存在){
			Error("图中有回路");
			break;
		}
		输出V，或者记录V的输出序号;
		for (V 的每个邻接点W)
			Indegree[W]--;
    }
}
```
这个算法其实也算intuitive，因为minimal element总是在最低那块，入度为0那个，总是出度嘛...所以小于别的，这个算法很有意思....

其实这就是BFS topological的变体么

###DFS 

用DFS来做topological sort是一句话就可以说清楚的：

> Topological sort : run DFS, output the reverse of finishing times of vertices 

假装也算比较直观，因为DFS是一步一步往“前”走的，然后逆向输出，就是可以完成的方法。
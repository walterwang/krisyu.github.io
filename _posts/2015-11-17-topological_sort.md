#Topological Sort

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
这个算法其实也算intuitive，因为minimal element总是在最低那块，入度为0那个，总是出度嘛...所以小于别的，这个算法很有意思，特别有意思....

其实这就是BFS topological的变体么，

###DFS 

用DFS来做topological sort是一句话就可以说清楚的：

> Topological sort : run DFS, output the reverse of finishing times of vertices 

假装也算比较直观，因为DFS是一步一步往“前”走的，然后逆向输出，就是可以完成的方法。
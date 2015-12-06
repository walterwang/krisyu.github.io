#Unweighted Graph最短路径以及DAG based Algorithm

###Unweighted Graph

这个很容易理解，因为Unweighted，用BFS稍加改写即可，因为BFS是一层一层往外数，所以只需要增加一个可以记录层数的即可，见伪码：

```
void unweighted(vertex s)
{
    enqueue(s,q);
    while(!isempty(q)){
        v = dequeue(q);
        for(v 的每个邻接点 w){
            if(dist[w] == -1){
                dist[w] = dist[v] + 1;
                path[w] = v;
                enqueue(W,q);
            }
        }
    }
}
```

dist[w] = s到w的最短距离

dist[s] = 0

path[w] = s到w的路上经过的某顶点


###DAG-based

//待读，并未认真看过

```
Algorithm DagDistances(G, s)	for all  v ∈ G.vertices()		if  v = s			v.setDistance(0)		else 			v.setDistance()	{ Perform a topological sort of the vertices }	for u = 1 to n do    {in topological order}	for each  e  u.outEdges()		{ relax edge e }		z  = e.opposite(u)		r  = u.getDistance() + e.weight()		if  r < z.getDistance()		z.setDistance(r)
```
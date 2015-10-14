#Heap君之HeapSort


[Heap君之一][id]

[id]:http://krisyu.github.io/2015/Heap君之一/

[Heap君之二][id2]

[id2]:http://krisyu.github.io/2015/heap君之二/

其实在Heap君之一和之二中已经牵扯到了两种构造Heap的方法，一种是空Heap，逐渐开始插入，一种是已经有了一个array/vector...然后我们将其逐渐变成一个heap

在有array的情况下的伪码已写过：从最末一个非叶节点开始，percDown或者percUp，直到根节点，这样就搭好了heap，这个过程叫做Heapify，时间复杂度则为O(n)

而Heapsort的思路也很好理解，比如要升序排列，那么首先比如构建一个最大堆，然后交换array里第一个与最后一个元素，这个时候，最大的元素已经被放到位，然后重新构建堆，使得前n-1个元素又变为堆，再次交换


伪码如此：

```
Heapsort(A){		BuildHeap(A);		for (i = length(A) downto 2)		{			Swap(A[1], A[i]);			heap_size(A) -= 1;			Heapify(A, 1);		}}
```

Heapsort的时间复杂度是O(nlogn)，同mergesort、quicksort一样，但是感觉实际中很少出现heapsort....quicksort最常出现因为STL里面有qsort....


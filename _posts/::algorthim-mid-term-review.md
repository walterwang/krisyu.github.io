###Algorithm-Analysis

- pseudo code
- O(n!) > O(2^n) > O(n^3) > O(n^2) > O(nlogn) > O(n) > O(logn) > O(1)
  	
  	all can be proved by induction(guess)

###Recursion

- typical examples

	```
	n! = n * (n-1)!;
	x^n = x * x^(n-1); // can be improved from O(n) to O(logn)
	LinearSum(A,n) = A[n-1] + LinearSum(A,n-1);
	ReverseArray(A,i,j);
	Fibonacci numbers ;// O(2^n) exponential
	```
	```
	gcd(x,y) = x,   	      if y = 0   
			 = gcd (y, x%y)   if y >0    //at least half everytime, O(logn)
	```
	
	```
	print(n)  = print(n--); cout << n;		if n > 0
	            return ;					if n = 0
	```
	```
	//同样可优化
	bool isPrime(int p, int i){
		if (i == p) return 1;
		if(p%i == 0) return 0;
		return isPrime(p, i+1);
	} // call from i =2
	```
	
	```
	
	bool palindrome(char str[], int size){
		if(str[0] != str[size-1]) return false;
		else if(strlen(str) <= 1) return true;
		else return palindrome(str+1,size-2);
	} 
	//注意这里的传入方式,str+1就是+1之后的子str，而size-2则是因为比较完一次之后，需要剔除掉头/尾的长度
	
	```

- tail recursion
	
	转成迭代 不是梦 	
	
	
###lists

- Array Implementataion 

	|space 	   |      O(n)    | 		
	|---------- |----------|
	|	size,empty,set(i,o),at(i)	|O(1)      |
	|insert(i,o),erase(i)  |O(n)|
	
A fun fact:

来做这样的假设和分析，如果每次都是插入最末端
We need to expand the array as the array grows, then there's two strategies:

- Incremental strategy: increase the size by a constant c
- Doubling strategy: double the size	
然后考察做n个insert（o）操作，考察total time T(n),那么就可以预估出平均的插入时间：

T(n)/n

通过少量的数学计算，可以知道Incremental strategy的insertion time会是O(n)，而Doubling strategy则是O(1)

- singly linked list
	
	```
	struct node{
		int data;
		node* next;
	};
	
	node* head;
	```
	
	假设只有 head pointer，那么insertAtTail/deleteAtTail必定是O(n)
	
	
	假设有   head/tail pointer，那么insertAtTail是O(1),deleteAtTail依然O(n)，因为singly linked list单向，update tail依旧要从头开始。
	
	|	space			|O(n)|
	|-----------------|--------------|
	| 	  insertAtTail() |     O(1)/O(n)     |
	|	insertAtHead(), deleteAtHead()	|O(1)      |
	| deleteAtTail()  |O(n)|

- doubly linked list

  ```
  struct node{
  	int data;
  	node* next;
  	node* prev;
  };
  node* head;
  node* tail;
  ```
  
	|	space			|O(n)|
	|-----------------|--------------|
	|insert(),delete()| O(1)         |



	
  
	
#More Counting Problem/Principle


###Some Basic Rules 


上次写了一枚[counting porblem][id],试图证明脑子还是要用的。而且数数这件事宁愿数的方式/次数越多越好。

[id]:http://krisyu.github.io/2015/一枚Counting%20Problem/
 

所以先来再梳一些常用的rules

- Product Rule  : n<sub>1</sub> * n<sub>2</sub> * ...*n<sub>k</sub>  √
- Sum Rule  :  n<sub>1</sub> + n<sub>2</sub> + ... + n<sub>k</sub>   √
- Inclusion - Exclusion Rule : n<sub>1</sub> + n<sub>2</sub> - n<sub>3</sub>   √
- Pigeonhole Principle 
- Generalized Pigeonhole Principle  
   
   
```
   not total get，的确很多elegant application，而关键点还是在于找pigeons和找holes
   
   利用Pigeonhole和数学家的大脑还可以继续推Ramsey theory，看party goers的认识状况（超过留个就晕☁️）
   
```

- Permutations : r- permutation P(n,r) = n!/(n-r)!
	
	```
	 r location,choice goes from n to n-r+1 , so P(n,r) = n*(n-1)*....*(n+1-r)
	 P(n,0) = n!/n! = 1    从n中选0排，当然只有一种选法
	 P(n,n) = n!/0! = n!   从n中选n排，根据product rule，也可得到
	```
- Combinations:  r-combination C(n,r) = n!/(n-r)!r!
 	 
 	 ```
 	 combination is choose r but unordered,  so P(n,r) = C(n,r) * P(r,r)
 	 C(n,r) = C(n,n-r) 选r个出来和剩n-r当然一样的
 	 ```


### Binomical Theorem


These come from combination

(x+y)<sup>n</sup> = C(n,0) x<sup>n</sup> + C(n,1) x<sup>n-1</sup>y +... + C(n,n) y<sup>n</sup>


我觉得这个还蛮intuitional的，因为反正是选r个x出来，选n-r个y出来来最终组成x<sup>r</sup> y<sup>n-r</sup>, 所以系数是 C(n,r)

原来我无法使用LaTeX


- Σ<sub>k=0→n</sub>C(n,k) = 2<sup>n</sup>  x=y=1 √
- C(n+1,k) = C(n,k-1)+ c(n,k)
	
	``` 
	既可以通过数学的方式证明
	也可以想从n+1中选k，两种选法，一包含x C(n,k-1)，另一不包含x C(n,k)
	```	
	
- C(m+n,r) = Σ<sub>k=0→r</sub> C(m,r-k) C(n,k)
	
	```
	 同样可以从 m+n 中选 r来证明
	
	 ```
	 
- C(2n,n) = Σ<sub>k=0→n</sub> C(n,k)<sup>2</sup>
	
	```
	 用上面的式子，令 m = n = r
	 
	 ```
- C(n+1,r+1) = Σ<sub>j=r→n</sub> C(n,j)
	
	```
	 乱想之 可以这样证么？
		
		 从 n+1中选r+1 等于 从m中选j * 从n-m中选r-j
		
		 然后再代入 r = j
		
		 //那就此处存疑，参见wikipedia
	```

### Back to counting with repetition


- r-Permutation with repetition  : n<sup>r</sup> √
- r-Combination with repetition : C(n+r-1,r) = C(n+r-1,n-1)
	
	```
	这个要用比如从三种酒里面选五瓶的例子来帮我懂了
	
	
	W | W W |W W
	
	2 bar 来 divide 5 wines
	
	C(2+5,2) = C(2+5,5)
	
	所以一般化就是 C(n+r-1.r) ,亦是 C(n+r-1,n-1)
	
	```
	
	这里还有的启发就是，比如在看无穷集合的时候，我们就用了1-to-1的状况来看另一个集合是否countable，同样，数数也是一样的，有时候一种数法不方便，我们可以换成另一种数法，或者，把一个问题映射成另一个方便数的问题。 比如这种 x<sub>1</sub> + x<sub>2</sub> + x<sub>3</sub> = 11 ,这种求非负值解组合个数也可以看成是三种酒，一共取11瓶出来。
	
	
### Indistinguishable Objects and Distribute problem

- Permutation with indistinguishable objects  n!/(n<sub>1</sub>!n<sub>2</sub>!...n<sub>k</sub>!)

	permutation of n objects,
	n<sub>1</sub> indistingguishable objects of type 1,
	n<sub>2</sub> of type 2....
	
	```
	C(n,n1)C(n−n1,n2)···C(n−n1 −···−nk−1,nk)  i.e. the answer
	```
	
- Distinguishable objects and distinguishable boxes  n!/(n<sub>1</sub>!n<sub>2</sub>!...n<sub>k</sub>!)
	
	
	distribute n distinguishable objects so that n<sub>i</sub> objects are placed into box i ...
	
- Indistinguishable objects and distinguishable boxes  


	```
 	n objects, k boxes 
 	C(k+n-1,n)  
	the same as divide wines
	```	
	
- Distinguishable objects and indistinguishable boxes   	**no simple closed form**
- Indistinguishable objects and indistinguishable boxes 
 	**no simple closed form**

	
	



    
  
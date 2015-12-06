#HashTable

###hash table
 
hash table 绝对是最常见的ADT之一，我还不知道Bubble sort就有听过Hash Table的大名了

- “我要做一个contacts，用啥呢？”
- "hash table"

然后知道了python的dictionary，好像还有啥的hashmap，这就是hash table么？

然后知乎了一下:
[Map、Dictionary、Hash Table 有哪些异同？][id]

[id]:http://www.zhihu.com/question/27581780

再查了一下，C++ STL既有map又有unordered_map，还有hash function用来转string的.


###hash function

- Truncation
- Folding
- Key mod N
- Squaring
- Radix conversion

hash function跟prime number联系紧密,然后能想出来的各类hash function也是目不暇接啊.

### Collision Resolution

Separate Chaining， 我个人是很喜欢separate chaining的，容易理解，好写，问题是一旦load factor变大，效率极速下降.

特别是遇到unsuccessful search,同时容易看出，table size不是重点，table size才是.

Open Addressing:

- Linear Probing- Quadratic probing - Double hashing
然后需要注意的是这里需要使用lazy deletion，否则出现holes难以处理和继续查找.
然后一看quadratic probing的theorem，就知道数学绝对用的多：
> If the table size is prime and load factor is not larger than 0.5, all probes wi
ll be to different locations and an item can always be inserted.一旦load factor升高：
- Dynamically expand the table as soon as the load factor reaches 0.5, which is called rehashing.- Always double to a prime number.- When expanding the hash table, reinsert the new table by using the new hash function.> The most popular is double hashing.
原来double hash是最popular的|||||有种要吐血之感...
看了一张relative efficiency of four collision-resolution methods的图，seprate chaining在load factor低于1的时候表现很不错嘛（无论successful search还是unsuccessful
search），其次 double hashing, 其次quadratic probing,最末linear probing.


###  Application

application应该非常多广

- compiler 用它来记录variables
- spelling checkers google drive sync也用
- game programs transportation table(?)

写到这还没写到为嘛其应用这么广，因为hash table的insert和find O(1)可达.

separate chaining ,load factor should be close to 1.open addressing load factor should not exceed 0.5 unless this is completely unavoidable.

-----------------------
本着不再造轮子以及懒的心情
记一句： STL里有map，虽然key,value 但是是有序的状态，underlying 的data structure是red black tree

C++11里面有unordered_map，也算圆梦hash table
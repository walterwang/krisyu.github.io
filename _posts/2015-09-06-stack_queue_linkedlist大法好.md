#Stack Queue LinkedList大发好


###linkedlist大法好

自从有了linkedlist，腰不酸了，疼不痛了，走路都有劲了...


ADT ADT重在一个A-abstract， 所以一个数据结构多种implement方式，但是我还是要欢呼，鼓掌👏，歌颂linkedlist大法，好啦，其实linkedlist也可以用两个array来做（那些古怪的方式），但是C/C++ person我们就爱指针


所以linkedlist大法好，因为linkedlist不会让你担心空间被用完了的问题，来写一个stack和一个queue吧：



###Stack

写了很短很短的一个Stack类（从C进击到C++），写完有一种酣畅淋漓之感，但是一运行，居然告诉我free了一个本来就没有allocate的memory

发现小bug一枚， fixed


再来做一个Queue：

把interface/implementaion/main拆开写是感觉蛮爽的|||嘿

然后发现netBeans的rename/refactor做的也不错....啊...又困了....


### C++ throw exception

<http://stackoverflow.com/questions/8480640/how-to-throw-a-c-exception>

写stack的时候pop为空return了-1，并且cout了 stack empty，但其实可以用throw exception来处理.

写的比较粗糙的stack 和 queue:

<https://github.com/KrisYu/DataStructure/tree/master/Queue>

<https://github.com/KrisYu/DataStructure/tree/master/Stack>



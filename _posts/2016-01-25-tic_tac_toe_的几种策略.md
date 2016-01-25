#Tic Tac Toe 的几种策略


### 简单AI
这个策略来自于 [Invent Your Own Computer Games with Python][id],简单容易理解，测了几次，居然我还输了两次（咋回事，这智商），感觉这应该不是一个百分之百的winning strategy吧。

AI如下：

	how to make next move:
	 1 make wining move
	 2 block player's winning move
	 3 move on corner
	 4 move on center
	 5 move on side
	 
[id]:https://inventwithpython.com/chapter10.html

程序读起来易懂，让人爱上Python.



### Minimax

大名鼎鼎的minimax，名字很吓人，我想了半天，minimax这个名字应当是用来处理board得分的名字，感觉其实跟简单AI有点类似，不过简单AI比较更粗暴再加了一些随机。

而minimax是把给board score，然后根据score挑最优move，而这个score就是用minimax来算，如果下一步能直接结束，机器（🐔）赢了就是+1，user赢了-1，平局算0。否则怎么来判分呢，首先现在目前的状态是board并未结束，使用dfs来算各种move以及各种move能得的分，然后肯定是取最大的分，但是🐔只走一步显然棋局可能也并未结束，同时我们要预设user有哪些选择，这里要把user当成一个水平相当的对手，user一定是会走对它自己最有利的move，这一个move所造成的情况就是最小化当前board得分，所以这就是为什么叫minimax的原因吧，预估：

- 首先minimax是一个递归的算法
- 需要传递的参数应当包括 board copy, player，需要传出的参数包括 score 和 move
- 在这个递归算法中，当处于computer时，需要尝试取最大，否则需要取最小


虽然我最终figure out出来怎么用Python写，但是还是需要学习，同时minimax 虽然算AI，但是并不能算learning algorithm吧...


### Monte Carlo Method

to be learned and try...


### ML

to be learned and try...

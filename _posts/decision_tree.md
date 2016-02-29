#Decision Tree

### inductive, deductive, abductive

英文差，mark一下:

- inductive ： 归纳，从特殊到一般
- deductive ： 演绎，从一般到特殊
- abductive ： 溯因推理，地上是湿的→下过雨

感觉decision trees算intuitive.


### ID3 vs 信息熵

> ID3, learns decision trees by constructing them top- down, beginning with the question "which attribute should be tested at the root of the tree?'


> To answer this question, each instance attribute is evaluated using a statistical test to determine how well it alone classifies the training examples.

首先，如何选第一层节点，如何再选各个分支，都很有意思。

熵居然出现了，看到信息熵要吓尿了...

两篇文章：

<http://www.ruanyifeng.com/blog/2014/09/information-entropy.html>

<http://www.isnowfy.com/information-theory-and-entropy/>

特别第一篇，好像有点感觉为什么信息熵的公式是这个了...


### ID3


```
ID3 (Examples, Target_Attribute, Attributes)
	Examples are the training examples. Targetattribute is the attribute whose value is to be predicted by the tree. Attributes is a list of other attributes that may be tested by the learned decision tree. Returns a decision tree that c	orrectly classiJies the given Examples.
	
	
    Create a root node for the tree
    If all examples are positive, Return the single-node tree Root, with label = +.
    If all examples are negative, Return the single-node tree Root, with label = -.
    If number of predicting attributes is empty, then Return the single node tree Root,with label = most common value of the target attribute in the examples.
    Otherwise Begin
        A ← The Attribute that best classifies examples.
        Decision Tree attribute for Root = A.
        For each possible value, vi, of A,
            Add a new tree branch below Root, corresponding to the test A = vi.
            Let Examples(vi) be the subset of examples that have the value vi for A
            If Examples(vi) is empty
                Then below this new branch add a leaf node with label = most common target value in the examples
            Else below this new branch add the subtree ID3 (Examples(vi), Target_Attribute, Attributes – {A})
    End
    Return Root
```

* The best attribute is the one with highest information gain, as defined in Equation (3.4).



###奥卡姆剃刀原理

Occam's razor，我要疯了，居然又出现了***奥卡姆剃刀***原理.


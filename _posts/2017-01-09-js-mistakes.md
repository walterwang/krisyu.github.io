---
layout: post
title: "JS - 坑无处不在"
---

# JS - 坑无处不在


> 种一棵树的最好时机是二十年前，其次是现在。

本着这样的心理看了看JS，JS真是大坑啊。

### const, let ,var

我也真是见识到了，let是block level的variable，var其实是block之外的，const最好用来定义常量，当然常量也可以有可变的variable.

### 创建Object


因为JS没有class这个概念，所以我见到的创建类的方法真是多种多样，比如这种:


```
//stopwatch.js
function Stopwatch(elem,workTimer){

}
//main.js
var watch = new Stopwatch(timer,workTimer);
```

比如这样：

```
var Stopwatch = function((elem,workTimer){
...
}

Stopwatch.prototype.start = function(){
...
}
```

更不用说配合上node.js那些传说中的工厂模式啥的了，我要晕|，还是先搞vanilla Javascript.


### 参差不齐

各类JS代码参差不齐，比如我写的，pure naive and ugly，各类JS代码简直也跟php市场有的一拼。

而我此时也是真正认识到，这个写代码也真是搞创作啊。其实有的时候所想还真不是能找来改改就行。要从白纸写起，而我还在读的阶段，甚至都还没到模仿的阶段。

> 熟读唐诗三百首,不会吟诗也会吟

> 熟看代码三万行,不会写也会拼

还想吐槽一下github上搜Github lan:javascript 出来一大堆node.js, angular.js,jquery混用。

我想说的是：[You may not need jquery](http://youmightnotneedjquery.com)


然而推崇的刻意练习，我要怎么找到刻意这个刻度在哪里呢？

还是加油吧，在这个大坑里再玩一会。


### setInterval

还遇到一坑，就是setInterval居然越走越快。谷歌了一下，可能我使用的方式不正确，好像fire了很多的instance，所以导致这样的问题。to be read。所以我才是一个大坑。




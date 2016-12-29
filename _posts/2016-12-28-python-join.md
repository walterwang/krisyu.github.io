---
layout: post
title: "Python join: why string.join(list) instead of list.join(string)?"
---


这里有个问题很有意思：

[Python join: why is it string.join(list) instead of list.join(string)?](http://stackoverflow.com/questions/493819/python-join-why-is-it-string-joinlist-instead-of-list-joinstring)

This has always confused me. It seems like this would be nicer:

```
my_list = ["Hello", "world"]
print my_list.join("-")
# Produce: "Hello-world"
```

Than this:

```
my_list = ["Hello", "world"]
print "-".join(my_list)
# Produce: "Hello-world"
```

因为最近正好在看js的语法，js里面是这样做的：


```
var mack = [];
mack.push('Mack');
→ 1
mack.push('the', 'Knife');
→ 3
console.log(mack);
→ ["Mack", "the", "Knife"]
console.log(mack.join(" "));
→ Mack the Knife
console.log(pop());
→ Knife
console.log(mack);
→ ["Mack", "the"]

```

但是python里面是这样做的：

```
mack = []
mack.append('Mack')
mack.extend(['the','Knife'])
print ' '.join(mack)
```

原因最高票已经解答：

> It's because any iterable can be joined, not just lists, but the result and the "joiner" are always strings.

因为只要是iterable的都可以join，join的结果则是string. join是string的method. 而js里面的join 谷歌一下是 Array.prototype.join(), 所以它是算Array的方法?







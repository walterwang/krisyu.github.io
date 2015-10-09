#一枚counting Problem

### A counting problem

Password Example


Each user on a computer system has a password, which is six to eight characters long, where each character is an uppercase letter or a digit. Each password must contain at least one digit. How many possible passwords are there?


textbook上直接给的解法是排除法，排除掉没有带digit的password.


```
6位的合理passwords = 所有的6位密码 - 不带数字的6位密码
i.e.

P6 =  36^6 - 26 ^6

```

但是如果直接来数的话：


```
_ _ _ _ _ _

就会想这样把密码画出来，然后觉得是 C(6,1) * C(10,1) * 36^5

```

上面两种算法算出来是不一样的，是第二种数多了，如下：


```
9 A B C D 9 这种其实是数了两次，在第一次把数字放在第一位的时候数了一次
			然后把其放在某位又数了一次

```

所以感觉counting problem如果思路多的话多数数无妨，多用多sharp，假装如此吧。


### The Pigeonhole Principle

相信第一次听pigeonhole principle的人都会震惊，这居然是一个principle，lol, so cute

摘自wikipedia

```
In mathematics, the pigeonhole principle states that if n items are put into m containers, with n > m, then at least one container must contain more than one item


This theorem is exemplified in real-life by truisms like "there must be at least two left gloves or two right gloves in a group of three gloves"
```

😄，想起以前看的几副袜子问题啥的.... 也是可爱

更可爱的是居然还有 generalized verison 的 principle


```
If N objects are placed into k boxes, then there is at least one box containing at least ⌈N/k⌉ objects.

```
不过这个generalized version 的 proof我表示稍迷茫，因为在我看来contradiction否定说明的问题并不完全是这个问题，所以 question mark here，此处存疑。






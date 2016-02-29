#Python 爬虫

###基础

转了一圈，又回来写爬虫脚本，但是假装好的是，至少一些东西更清楚了，比如Get协议，POST协议，200...，知乎上很是有一些好的Python技能问答。我最喜欢的一个问答是，Python爬虫如何入门？
答案是****用.****

还有一个人的答案比较赞同，就是先用系统自带的urllib,正则表达式,当然BeautifulSoup比不可少。Scrapy的话可以先尝试自己写模块。

for Python3
基础代码：

```
#encoding:UTF-8
import urllib.request

url = "http://www.baidu.com"
data = urllib.request.urlopen(url).read()
data = data.decode('UTF-8') // UTF-8 may varies, some maybe 'GBK' 
print(data)
```
编码问题...
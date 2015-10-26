#Taylor Swift系列之一

###Objective-C -> Talyor Swift

虽然Swift出生已久，但我基本没有怎么特别看过，原先是OC有很多诡异的其实也是好用的的东西被大家诟病（其实OC我也不熟），比如函数名字有多长，但是无论如何，还是来看看Swift的改变吧。

- let/var, 常量与变量//不惊讶
- 类型转换//不惊讶，两种写法：1.String(width)  2.\(width)
- Array //不惊讶，我觉得更多的写法更贴近常用的语言了，比如Java，C++，好事
- optional//惊讶，这是啥？


###Optional

在写optional之前还有一个惊讶，就是Swift的定义是把类型写在后面的。然后还要时刻提醒自己一点，swift是不太用分号

第二个是Swift自带type inference，就是比如你来定义 var x = 40.0, 这个x不是没有类型，而是人家帮你自动推断了是Double.

第三个Swift其实很严苛，要求一旦declare就要有值 -> 正是因为这种要求，造成了optional的出现。

```
int x;

//人家是这么写的
var x:Int
print(x) // Error: Variable 'x' used before being initialized
```

所以optional应该理解如下:


```
	42     [42]   [ ]
	Int    Int?   Int?

```


就是这只盒子要么是空的，要么就是Int类型的值。




>You’ll rarely need to create implicitly unwrapped optionals in your own code. More often, you’ll see them used to keep track of outlets between an interface and source code (which you’ll learn about in a later lesson) and in the APIs you’ll see throughout the lessons.

###例子🌰


开始还在想John Appleseed到底是谁，恍然大悟，是Appleseed,sigh|||


```
var optionalName: String? = "John Appleseed"// = nil 或者String？后留空
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
} else {
    greeting = "Hello, Yoka"
}

```
如果是nil的话，会跳到else那去，因为盒子是空的，没有值可以给name这个String常量。





//待细看

[Learning Swift: Optional Types][id1] 

[id1]:http://lithium3141.com/blog/2014/06/19/learning-swift-optional-types/


[Difference between optional values in swift?][id2]

[id2]:http://stackoverflow.com/questions/29054096/difference-between-optional-values-in-swift


### for in

for in 大变身了啊，除了有常见的类Java，类C的for in，居然还有这两种for in，问题在于不知道会否常用。


```
for i in 0..<4  //i 0 -> 3

for _ in 0...4 // _ 0 -> 4
```
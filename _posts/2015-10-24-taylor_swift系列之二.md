#Taylor Swift系列之二

###func

居然前面已经有了 var x :Int 的 不走寻常路之举，我们的func也一定要做好准备

**Type在参数名后面**<br /> 
**Type在参数名后面**<br /> 
**Type在参数名后面**<br /> 


重要的事讲了三遍之后看起来习惯多了

```
func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
}

greet("Charlie", day: "a nice day")
```
调用时候同要注意，除了第一个参数名能省，之后的是绝不能省的

Functions that are defined within a specific type are called methods,OOP的就会默认，恩，差不多。


###Class

值得开心的是介绍的部分Swift明写了构造函数（？）init，比如这样：

```
class NamedShape{

    init(name: String) {
       self.name = name
    }
    
    //注意这里无参数，然后直接return String
    func simpleDescription() -> String{
    ...
    }
    ...
}
    

//call with the initializer
let namedShape = NamedShape(name: "my named shape")

```

还有这部分就是Java-like了，构造与override

```
	  子类		父类
		↓        ↓
class Square: NamedShape{

	init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        //利用父类的init方法
        super.init(name: name)
        numberOfSides = 4
    }
    
    override func simpleDescription() -> String {
    ....
    }
}

```

再注意init也可以是optional格式，that is， 如果init失败，可以直接是nil，比如这样：

```
    init?(radius: Double, name: String) {
        self.radius = radius
        super.init(name: name)
        numberOfSides = 1
        if radius <= 0 {
            return nil
        }
    }
     
```

###Keyword

- A *designated*(指定) initializer indicates that it’s one of the primary initializers for a class
- A *convenience*(方便) initializer is a secondary initializer, which adds additional behavior or customization, but must eventually call through to a designated initializer
- A *required* keyword next to an initializer indicates that every subclass of the class that has that initializer must implement its own version of the initializer (if it implements any initializer).
- *downcast* 

....



downcast虽然看起来觉得很迷茫，不知所云，但是一看例子就明了，而且这种语法也非常有英语的特质

```
if let square = shape as? Square 
```


###Enumerations and Structures

这两个都很C/C++ like，之前学C的时候就没有特别认真研究过，可能毕竟还是代码写得太少了。Enumerations can have methods associated with them.不知道C是否可以这样，但是还是略惊讶一下，因为之前没有思考过enum类型带method/带func.

另外是有一个keyword *rawValue*可以用init之用和得到实际值。


>Structures support many of the same behaviors as classes, including methods and initializers. One of the most important differences between structures and classes is that structures are always copied when they are passed around in your code, but classes are passed by reference. Structures are great for defining lightweight data types that don’t need to have capabilities like inheritance and type casting.

实际上C++的Class的实现就是利用C的Structure,但是因为structure算是类似int/char一样的基础类型，所以传递的时候是按值传递，而class是按reference传递.

然后看例子，的确struct用起来简直跟class一样了，包括init，包括调用其中的func.

### Protocol 协议/原型

依旧因为实战经验过少，protocol基本没怎么用过，感觉和类很像，都是blueprint，但是可能是属于可能为

>The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform（遵循） to that protocol.

而且protocol还能建Array







---
layout: post
title: "Swift sequence protocol"
---

Swift's `Sequence` Protocol is closely related with `IteratorProtocol`, the `for in` under the hood is actually iterator. It's fun, I never thought about this before. While reading the document, it says the idiomatic way of is using `for in`, but not iterator.

And it gave a example of writing a struct confirms to this two protocols, the struct needs to implement a `next` method.

For any type confirm this protocol, there're really a lot of useful methods.

- map
- filter
- forEach
- dropFirst
- dropLast
- drop(while: )
- prefix
- prefix(while: )
- suffix
- split
- ...

Take a close look at `map`.

> Returns an array containing the results of mapping the given closure
  over the sequence's elements.
  
The function's prototye is ` func map<T>(
    _ transform: (Element) throws -> T
  ) rethrows -> [T]`, this can illustrate how important Swift deals with the error handling. In fact, every function in the list deals with error handling.


Let's take a close look at forEach:

```
  @_inlineable
  public func forEach(
    _ body: (Element) throws -> Void
  ) rethrows {
    for element in self {
      try body(element)
    }
  }
```

dash _ is used to avoid external name, body is the parameter, it's type is `(Element) -> Void`. For every element in the Sequence, the body function will work on the element.

So now this seems so clear and easy.

```
let numberWords = ["one", "two", "three"]
numberWords.forEach{ print($0) }
```

And we'll find those functions are related with each other, for example, `first(where)` used forEach.

And those functions/usages can make Swift code shorter and more clearable.

- [Sequence Protocol Introduction](https://developer.apple.com/documentation/swift/sequence)
- [Sequence.swift](https://github.com/apple/swift/blob/master/stdlib/public/core/Sequence.swift)


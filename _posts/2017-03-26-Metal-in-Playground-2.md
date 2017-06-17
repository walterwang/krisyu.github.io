---
layout: post
title: "Metal in Playground 2"
---


### Index Buffer

开始用到 index_buffer了，reuse vertices 来了。现在我们的 vertex_data如下：

```
let vertex_data = [
    Vertex(pos: [-1.0, -1.0, 0.0,  1.0], col: [1, 0, 0, 1]),
    Vertex(pos: [ 1.0, -1.0, 0.0,  1.0], col: [0, 1, 0, 1]),
    Vertex(pos: [ 1.0,  1.0, 0.0,  1.0], col: [0, 0, 1, 1]),
    Vertex(pos: [-1.0,  1.0, 0.0,  1.0], col: [1, 1, 1, 1])
]
```

在屏幕上呈现就是

```
		3 - 2
		|   |
		0 _ 1
```

这个时候如果我们像画一个长方形 quad，那么我们再添加 index_data 如下：

```
let index_data: [UInt16] = [
    0, 1, 2, 2, 3, 0
]
```

说这样的画法是 clockwise， 其实两个三角形之间存在的关系吧： clockwise，有了这些数组，我们需要需要做一下更改：

1. 创建index_buffer, 把 index_data 传进去
2. drawPrimitives 被替换成 drawIndexedPrimitives


```
...
var index_buffer: MTLBuffer!

...
indexBuffer = device!.makeBuffer(bytes: indexData, length: MemoryLayout<UInt16>.size * indexData.count , options: [])
...

command_encoder.drawIndexedPrimitives(.Triangle, indexCount: index_buffer.length / sizeof(UInt16), indexType: MTLIndexType.UInt16, indexBuffer: index_buffer, indexBufferOffset: 0)

```

### Model-View—Projection

然后我们就又再次进入了model-view-projection的世界，值得注意的是他把matrix相关的函数抓出来放到 update() 中，而实现随着时间rotation用的是：


```
rotation += 1 / 100 * Float(M_PI) / 4
```


update 的最终归属是放到了draw当中， 这样生成每个frame我们都去update一下rotation这个值得。


draw里的新元素还包括：

```
commandEncoder.setFrontFacing(.counterClockwise)
commandEncoder.setCullMode(.back)
```

这两个貌似被注视到在这个上面也暂时看不出来区别。indexbuffer是不需要传递的，因为我们在drawIndexedPrimitives中用到了它

至此，所有新鲜元素结束




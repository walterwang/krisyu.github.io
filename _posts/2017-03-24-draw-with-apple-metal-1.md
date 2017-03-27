---
layout: post
title: "Apple Metal画东西1"
---

# Apple Metal画东西1

这一系列都是我没啥营养的读书笔记

Metal 和 OpenGL 一样，也是算一个大的状态机吧（？，所以要画一个三角形也是非常麻烦，但是一旦知道怎么画了，模式也是一样的吧（||

### 预热

在render function中：

1. 创建 device
2. 创建 commandQueue
3. 创建 vertexData
4. 把vertexData传入 vertexBuffer （知道vertexData大小，然后用device.makeBuffer传入
5. 创建library
6. 创建 vertex\_func 和 frag\_func （用library.makeFunction
7. 创建 rpld MTLRenderPipelineDescriptor()
8. 把这个rpld的vertexFunc 和 fragmentFunction 设置为刚定义的的vertex\_func 和 frag\_func
9. 设置 rpld 的color pixelFormat，一般是 .bgra8Unorm
10. 根据 rpld 创建 rps MTLRenderPipelineState




### 画

在draw function中：

1. 创建 drawable currentDrawable
2. 创建 rpd currentRenderPassDescriptor
3. 设置rpd 的 clearColor
4. 创建 commandBuffer
5. 创建 commandEncoder
6. 设置 commandEncoder 的renderPipelineState
7. 设置 commandEncoder 的VertexBuffer
8. 画 commandEncoder.drawPrimitives
9. commandEncoder endEncoding
10. commandBuffer present drawable
11. commandBuffer commit 真正的推送到画布上（？

### Shader


初次看来还是比较迷茫的，比如 `[[]]` , 因为它没有像OpenGL 一样什么`layout (location = 0) in vec3 position;`



```
#include <metal_stdlib>

using namespace metal;

struct Vertex {
    float4 position [[position]];
};

vertex Vertex vertex_func(constant Vertex *vertices [[buffer(0)]], uint vid [[vertex_id]]) {
    return vertices[vid];
}

fragment float4 fragment_func(Vertex vert [[stage_in]]) {
    return float4(0.7, 1, 1, 1);
}
```


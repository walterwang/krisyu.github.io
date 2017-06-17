---
layout: post
title: "Apple Metal画东西3"
---




跟OpenGL一样，Metal也可以有uniform变量，定义一块buffer：

```
var uniform_buffer: MTLBuffer!
```

这里的 uniform_buffer 只是变量名而已，还暂时不能说明啥问题，然后依旧把buffer拷贝进去


```
uniform_buffer = device!.newBufferWithLength(sizeof(Float) * 16, options: [])
let bufferPointer = uniform_buffer.contents()
memcpy(bufferPointer, Matrix().modelMatrix(Matrix()).m, sizeof(Float) * 16)
```

然后貌似说明问题的地方来了：

```
command_encoder.setVertexBuffer(uniform_buffer, offset: 0, atIndex: 1)
```

atIndex → 1, 这就是跟OpenGL对应的 layout = 1，因为如果此时去看shader，首先shader里面有一个struct

```
struct Uniforms {
    float4x4 modelMatrix;
};
```

然后看参数，传入的两个参数，除了一开始的Vertex以外，还有Uniform 对应的就是buffer((1))


```
struct Vertex {
    float4 position [[position]];
    float4 color;
};


vertex Vertex vertex_func(constant Vertex *vertices [[buffer(0)]],
                          constant Uniforms &uniforms [[buffer(1)]],
                          uint vid [[vertex_id]])
{
    float4x4 matrix = uniforms.modelMatrix;
    Vertex in = vertices[vid];
    Vertex out;
    out.position = matrix * float4(in.position);
    out.color = in.color;
    return out;
}


fragment float4 fragment_func(Vertex vert [[stage_in]]) {
    return vert.color;
}
```


可以注意看一下shader，首先我们获得变换matrix，然后我们用了Vertex in获得对应的入口，然后有Vertex out，out代表我们变换后的Vertex. 然后fragment take变换之后的Vertex 查了一下，除非单色，否则我们需要传递给fragment 都是这样的struct， 单色我们就可以不要take in 任何argument都行。


看了一下 apple 官方 demo code，也是这种 style

```
struct ColorInOut {
    float4 position [[position]];
    half4 color;
};

....

// fragment shader function
fragment half4 lighting_fragment(ColorInOut in [[stage_in]])
{
    return in.color;
};
```


然后代码除了以上uniform的拷贝和传入， shader部分的变化，代码的其他部分就没有任何新的变化了。



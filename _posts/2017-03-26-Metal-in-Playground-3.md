---
layout: post
title: "Metal in Playground 3"
---

# Metal in Playground 3


### Set up compute kernal

之前我们接触到的是`vertex Vertex vertex_func(){}` 或者 `fragment half4 fragment_func(){}`，现在终于要来见识这个计算的kernal function.

它也是有关键字kernal, return type 是 void, 现在我们不需要传入vertex data，所以整个画的过程可以简化很多：

init 里就只有 registerShaders()了，而registerShaders变化如下：

```
func registerShaders() {
    device = MTLCreateSystemDefaultDevice()!
    queue = device.makeCommandQueue()
    let path = Bundle.main.path(forResource: "Shaders", ofType: "metal")
    do {
        let input = try String(contentsOfFile: path!, encoding: String.Encoding.utf8)
        let library = try device.makeLibrary(source: input, options: nil)
        let kernel = library.makeFunction(name: "compute")!
        cps = try device.makeComputePipelineState(function: kernel)
    } catch let e {
        Swift.print("\(e)")
    }
}
```

特别值得注意的是 makeComputePipelineState，draw当中这样变化: 首先currentRenderPassDescriptor 我们不需要了，commandEncoder也变成了相应的makeComputeCommandEncoder，vertex buffer我们也不需要，但是我们需要传入一个texture，创建thread groups然后dispatch他们（好可怕， MTLSize 是设置的thread group 的dimension

> We use MTLSize to set the dimensions of each thread group and the number of thread groups that will be executed in each compute call.

好可怕的一句话。

```
public func draw(in view: MTKView) {
    if let drawable = view.currentDrawable {
        let commandBuffer = queue.makeCommandBuffer()
        let commandEncoder = commandBuffer.makeComputeCommandEncoder()
        commandEncoder.setComputePipelineState(cps)
        commandEncoder.setTexture(drawable.texture, at: 0)
        let threadGroupCount = MTLSizeMake(8, 8, 1)
        let threadGroups = MTLSizeMake(drawable.texture.width / threadGroupCount.width, drawable.texture.height / threadGroupCount.height, 1)
        commandEncoder.dispatchThreadgroups(threadGroups, threadsPerThreadgroup: threadGroupCount)
        commandEncoder.endEncoding()
        commandBuffer.present(drawable)
        commandBuffer.commit()
    }
}
```

### 开写

最简单的，最简单的长这样： 纯 compute function，playground入口依旧，画出来的就是纯bleen。

```
#include <metal_stdlib>

using namespace metal;

kernel void compute(texture2d<float, access::write> output [[texture(0)]],
                    uint2 gid [[thread_position_in_grid]])
{
    output.write(float4(0, 0.5, 0.5, 1), gid);
}
```

开始渐变,根据画出来的渐变我们知道这个gid.x / width， grid.y / height 这个坐标范围是[0,1]， 记住这件事

```
kernel void compute(texture2d<float, access::write> output [[texture(0)]],
                    uint2 gid [[thread_position_in_grid]])
{
    int width = output.get_width();
    int height = output.get_height();
    float red = float(gid.x) / float(width);
    float green = float(gid.y) / float(height);
    output.write(float4(red, green, 0, 1), gid);
}
```

`float2 uv = float2(gid) / float2(width, height)`，所以它的范围也是[0,1]，这也是我们经常见到`uv = uv * 2.0 - 1.0;`的原因，因为我们想把它clip到[-1,1]中去，这样我们做很多操作就so easy，所以当我们画在中心的圆的时候就这样做就行了 ↓

```
bool inside = length(uv) < 0.5;
output.write(inside ? float4(0) : float4(red, green, 0, 1), gid);
```

这个length是一个常用function，用来决定一个pixel是否在距离我们创造出来的屏幕 0.5 范围之内。查了一下：

> The length function returns the length of a vector defined by the Euclidean norm










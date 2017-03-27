---
layout: post
title: "Metal in Playground 1"
---


# Metal in Playground 1

把代码移到playground去，需要创建 for macOS 的 playground，然后 Shaders.metal 文件是放在 Resources里的，MathUtils 和 MetalView是放在Sources里面， 然后画就是在 Playground 生成的主文件里画。


改变的地方有，读shader,现在读的是文件内容，所以这样操作


```
   func registerShaders() {
        let path = Bundle.main.path(forResource: "Shaders", ofType: "metal")
        let input: String?
        let library: MTLLibrary
        let vert_func: MTLFunction
        let frag_func: MTLFunction
        do {
            input = try String(contentsOfFile: path!, encoding: String.Encoding.utf8)
            library = try device!.makeLibrary(source: input!, options: nil)
            vert_func = library.makeFunction(name: "vertex_func")!
            frag_func = library.makeFunction(name: "fragment_func")!
            let rpld = MTLRenderPipelineDescriptor()
            rpld.vertexFunction = vert_func
            rpld.fragmentFunction = frag_func
            rpld.colorAttachments[0].pixelFormat = .bgra8Unorm
            rps = try device!.makeRenderPipelineState(descriptor: rpld)
        } catch let e {
            Swift.print("\(e)")
        }
    }
```

调用画画是这样操作的，创建frame，创建delegate（其实这个命名delegate不一定合理吧），创建MTKView，然后需要一个current.liveView = view 的操作，动起来


```
import MetalKit
import PlaygroundSupport

let frame = NSRect(x: 0, y: 0, width: 400, height: 400)
let delegate = MetalView()
let view = MTKView(frame: frame, device: delegate.device)
view.delegate = delegate
PlaygroundPage.current.liveView = view
```

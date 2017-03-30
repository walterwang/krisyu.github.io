---
layout: post
title: "Metal in Playground 5"
---


# Metal in playground 5


### load texture 

load texture并没有那么难，首先我们需要告诉有texture这个东西，定义一个变量，其次我们set up 好texture，再把它传入 shader，画出来即可。

改变如下：

```
// define it
var texture: MTLTexture!

// use it 
    
func setUpTexture() {
    let path = Bundle.main.path(forResource: "rocks2", ofType: "jpg")
    let textureLoader = MTKTextureLoader(device: device)
    texture = try! textureLoader.newTexture(withContentsOf: URL(fileURLWithPath: path!), options: nil)
}

// pass it in

commandEncoder.setTexture(texture, at: 1)
```

再看shader变化：

```
kernel void compute(texture2d<float, access::write> output [[texture(0)]],
                    texture2d<float, access::sample> input [[texture(1)]],
                    constant float &timer [[buffer(0)]],
                    uint2 gid [[thread_position_in_grid]])
{
    float4 color = input.read(gid);
    gid.y = input.get_height() - gid.y;
    output.write(color, gid);

}
```


然后可以学到的有两点东西：

1. 这个texture的高宽比好像蛮重要的，最好跟你想创建的‘view盒子一样’
2. 这一句 `    texture = try! textureLoader.newTexture(withContentsOf: URL(fileURLWithPath: path!), options: nil)`这个options值得设置

	- a, MTKTextureLoaderOptionOrigin: true as NSObject 这样就可以解决这个texture被vertical flip的问题
	- b, MTKTextureLoaderOptionSRGB: false as NSObject 这样可以解决texture莫名颜色变暗的问题
	
	
	
	
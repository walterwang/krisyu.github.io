---
layout: post
title: "Metal in Playground 4"
---



### smoothstep 函数

先看最简单的用kernel 画圆：

```
kernel void compute(texture2d<float, access::write> output [[texture(0)]],
                    uint2 gid [[thread_position_in_grid]])
{	
	// preparation settings
    int width = output.get_width();
    int height = output.get_height();
    float red = float(gid.x) / float(width);
    float green = float(gid.y) / float(height);
    float2 uv = float2(gid) / float2(width, height);
    uv = uv * 2.0 - 1.0;
    
    // draw
    bool inside = length(uv) < 0.5;
    output.write(inside? float4(1.0): float4(0.0), gid);
}
```

效果如下：
![]({{site.baseurl}}/images/draw/01.png)

有锯齿感，而锯齿感来源于由0到1的突变感，这也是smoothstep的出现吧。如果我们把draw part换为以下代码：


```
// draw
float d = length(uv);
float r = 0.5;
    
float c = smoothstep(r, r - 0.1, d);
    
output.write(c,gid);
    
```

锯齿感消失，变为一个边缘模糊的圆。

![]({{site.baseurl}}/images/draw/02.png)


实际上我以上的写法好像不太好，应该第二个函数是 r + 0.1，但是这样颜色就刚好反过来。



>The function depends on two parameters, the "left edge" and the "right edge", with the left edge being assumed smaller than the right edge. The function takes a real number x as input and outputs 0 if x is less than or equal to the left edge, 1 if x is greater than or equal to the right edge, and smoothly interpolates between 0 and 1 otherwise.



### clamp

clamp 实际上就是我平时理解的clip嘛, take in 3个数， 然后把比min小的变成min，比max大的变成max

```
x = clamp( (x - e1)/ (e2 - e1), 0.0, 1.0);
```

### mix

mix函数是做linear interpolation

```
mix(color1, color2, f) = color2 * f + color1 * (1-f)
```

### abs, fmod


abs 返回绝对值， fmod 就是mod(%, sin, cos 无需解释，fract是返回分数部分，dot是点乘，pow是幂函数。







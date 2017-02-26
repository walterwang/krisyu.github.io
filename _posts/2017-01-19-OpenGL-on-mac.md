---
layout: post
title: "OpenGL Mac 配置"
---

# OpenGL Mac配置


### 靠谱Mac环境设置教程:


[Installing GLFW & GLEW for OpenGL in Mac OS X El Capitan](https://www.youtube.com/watch?v=D3lIDsSIm6M)

测试mac 10.12.2有效


用glfw 和 glew， 这样配置之后当要使用Xcode建项目的时候：

- 去 build phases 里面加三个 binary libraries
	- libglfw
	- libGLEW
	- OpenGL

- 然后再去 build settings 把 header search path 添加一个`/usr/local/include`

这样正式可以run起来


### 测试GLFW

>  It provides a simple API for creating windows, contexts and surfaces, receiving input and events

因为OpenGL本身提供的东西太少（API嘛？） 所以用库，第一个库glfw. 测试glfw可以从glfw官网找到代码。




### GLM


glm也是必不可少的，相较而言，glm比较简答，直接下载zip的source code，解压缩，然后再去`Header Search Paths`中添加一下解压的文件夹，就可以用起来了


如这篇

<http://stackoverflow.com/questions/22924378/adding-glm-to-xcode-5-1-project>


### AntTweakBar

因为作业需要GUI，然后发现其官网上的方法行不通||||

还好有万能的 brew install ，最后同样需要去 build phase 里面添加 libAntTweakBar.dylib.




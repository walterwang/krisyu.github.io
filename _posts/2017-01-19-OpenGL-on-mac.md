---
layout: post
title: "OpenGL Mac 配置"
---

# OpenGL Mac配置

靠谱Mac环境设置教程:


[Installing GLFW & GLEW for OpenGL in Mac OS X El Capitan](https://www.youtube.com/watch?v=D3lIDsSIm6M)

测试mac 10.12.2有效


用glfw 和 glew， 这样配置之后当要使用的时候：

- 去 build phases 里面加三个 binary libraries
	- libglfw
	- libGLEW
	- OpenGL

- 然后再去 build settings 把 header search path 添加一个`/usr/local/include`

这样正式可以run起来


测试GLFW

>  It provides a simple API for creating windows, contexts and surfaces, receiving input and events

因为OpenGL本身提供的东西太少（API嘛？） 所以用库，第一个库glfw. 测试glfw可以从glfw官网找到代码。











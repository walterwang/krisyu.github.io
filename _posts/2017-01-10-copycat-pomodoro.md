---
layout: post
title: "照着写了一个Pomodoro"
---

# 照着写了一个Pomodoro

原文在此：
<https://www.gorkahernandez.com/blog/fcc-zipline-series-103-build-pomodoro-clock/>



觉得比较棒的点： OOP → 虽然还是没有达到我期待程度的OOP.

但是已经很棒了，基本逻辑是：

take in了这几个参数：

- pomodoroTime 一个番茄钟的时间（可定制
- breakTime 休息时间
- displayElementId 显示时间更新的元素
- messageDisplayId 显示message


而它内部的没有暴露出来的包括：

- timeLeft 好来算百分比
- state 当前状态
- lastState 上一个状态

这个state就是我觉得它设计的好的地方：

- 0: Initial state.
- 1: Paused.
- 2: Running a pomodoro cycle.
- 3: Running a break cycle.

对于番茄钟🍅，人人的理解是不同的，而我的理解还是应当有pause这个选项的，同时还有一些与作者不同的点，那就是一个番茄钟完毕应当暂停。让使用者手动选择继续。

### 开始函数

首先会检查是处于初始状态还是暂停，然后根据lastState就知道现在继续的state应该是怎样。因为同时我们有这个timeLeft来记录，就每隔1s调用tick更新剩余时间。

当剩余时间为0的时候，我们也根据当前状态来吧timeLeft做更新，下一刻是该break还是番茄钟。 （ 这里我做了一些修改，应该是当时间为0的时候我们来播放一个温柔的beep，同时暂停，直到使用者决定开始下一个番茄钟。


### 暂停函数

暂停函数相对比较简单，把当前state状态放到暂停，同时记录上一个状态是什么，当然作者这里写了一个比较长的newState这个函数，因为它每隔对应的状态有不同的属性，比如工作休息的倒计时的颜色是不同的。

### Reset函数

也比较简单，state放到0，timeLeft放到番茄钟，clearInterval，updateDisplay。把东西清理干净。

### updateDisplay

在tick被调用，用来每秒显示剩余时间，就填0，和更新对应的message.




### 想更新的点

所以觉得精巧之处在于给这个pomodoro放几个state，然后查看state来做下一步操作。

我想增加的一些功能：
 
 - longBreak,根据番茄钟使用惯例，每4个番茄钟之后要有一个longbreak，传统15分钟
 - 记录当天做了多少番茄钟


这两个功能也算有点关系：

所以要拆开重组函数，感觉需要take in更多的参数，longBreakTime 和 longBreakCnt。


记录感觉就要用storage。

然后在我毁掉原本的代码之前，原本抄的和小改写的在此处：

<https://github.com/KrisYu/21DaysofFunwithJS/commit/35ce565dd3dd02fde6d584b5434ec5677f56bf6e>


修改后有待美化和更新的代码


- 长break √ 添加了更多的内部状态来支持长break
- 有一个h2，显示已经完成的session 
 
需要做的：

- 存储
- 定制时间
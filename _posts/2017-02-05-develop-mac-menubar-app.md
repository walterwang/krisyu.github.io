---
layout: post
title: "用Swift开发一个macOS Menubar App"
---


# 用Swift开发一个macOS Menubar App


mac, swift, menubar, status bar, tutorial, bash, Terminal 

### 开始

开 Xcode, File/New/Project.. 选择 macOS/Application/Cocoa Application 然后下一步，Product Name 填 HideDesktopFiles，然后填好 Organization Name 和 Organization Identifier，注意语言要选择Swift.

不要勾 Use storyboard，因为我们这里仅仅是想要一个 Menubar App.

继续Next，然后选一个地方来存储你的app.

![]({{site.baseurl}}/images/menubar/01.png)



现在进入AppDelegate.swift，开始敲代码, 在 @IBOutlet weak var window.. 下一行开始输入：

```
let statusItem = NSStatusBar.system().statusItem(withLength: NSSquareStatusItemLength);

```

创建了一个statusItem，因为我们就显示一个图片，所以选这个长度固定.


现在我们来给我们的app添加图片。


到 Assets.xcassets 中，把自己喜欢的图片（最好32*32px png）拖拽到asset中。选中这张图片，更改名字为'StatusBarButtonImage'，切换到attribute，然后记得选中device Mac，Render As选中Template Image.


![]({{site.baseurl}}/images/menubar/02.png)

现在回到AppDelegate.swift中，

```
func applicationDidFinishLaunching(_ aNotification: Notification) {
    // Insert code here to initialize your application
    let button = statusItem.button
    button?.image = NSImage(named:"StatusBarButtonImage")
}
```

这里做的事就是把statusItem的image设置为我们刚刚的图片。

### 隐藏Dock Icon 和 去掉窗口

这个时候我们来运行，并没有看到menubar有任何显示，并且有窗口跳出来。

不要担心，这个时候我们来做的就是 隐藏dock 和 去掉这个窗口。

到 Info.plist文件中去：

添加一个新key `Application is agent`,并将它的值设为YES.

![]({{site.baseurl}}/images/menubar/03.png)

然后 隐藏窗口做的是， 打开MainMenu.xib， 选中window， 把visiable at launch的勾给去掉.

![]({{site.baseurl}}/images/menubar/04.png)

现在运行，我们就可以看到就 Menubar 这里出现图标了，并且没有窗口跳出来了

![]({{site.baseurl}}/images/menubar/05.png)

虽然目前点击这个按钮还暂时没有任何作用。


### 添加菜单


继续到`applicationDidFinishLaunching(_:)` 中去添加菜单：

```
let menu = NSMenu()
menu.addItem(NSMenuItem(title: "Hide Desktop Files", action: #selector(AppDelegate.toggleHideDesktopFiles(sender:)),keyEquivalent:"H"))
menu.addItem(NSMenuItem.separator())
menu.addItem(NSMenuItem(title: "Quit", action: #selector(AppDelegate.quitAction(sender:)),keyEquivalent:"q"))

statusItem.menu = menu
```


这里我们创建了NSMenu，并且添加了多个NSMenuItem

- title
- action → 当按下按钮对应调用的method,这里的写法 #selector(当前文件.method名字（参数）)
- keyEquivalent → Command + shift + 自定义的这个key来激活
- separator 就是一个灰色的分割线

现在我们需要做的就是进一步添加对应的method

### 添加Method


**题外 → 手动分割**

<hr>

如果你的desktop 很杂乱，像我一样有很多files，如果想隐藏这些图标，可以试试打开Terminal。

输入

```
defaults write com.apple.finder CreateDesktop NO (↵Enter)
killall Finder （↵Enter）

```

这个时候你就会发现你的桌面非常整洁，当然这些文件都还在，你可以打开Finder，看desktop文件夹。你也可以读，我们所做的也只是 CreateDesktop 变成了NO。

恢复原样我们同样只用打开Terminal

```
defaults write com.apple.finder CreateDesktop YES (↵Enter)
killall Finder （↵Enter）

```

好吧，它们又回来了。


我们还可以用`defaults read com.apple.finder CreateDesktop`来读当前桌面是否被创建的状态。
<hr>


我们这里做的就是利用 Terminal 的命令来做这件事：


```
func toggleHideDesktopFiles(sender: NSMenuItem) {
    
    let pipe = Pipe()
    let task = Process()
    
    task.launchPath = "/usr/bin/defaults"
    task.arguments = ["read", "com.apple.finder", "CreateDesktop"]
    task.standardOutput = pipe
    
    let file = pipe.fileHandleForReading
    task.launch()
    var result = NSString(data: file.readDataToEndOfFile(), encoding: String.Encoding.utf8.rawValue) as! String
    result = result.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines)
    
    let workTask = Process()
    workTask.launchPath = "/usr/bin/defaults"
    
    if result == "true" {
        workTask.arguments = ["write", "com.apple.finder", "CreateDesktop", "false"]
        sender.state = NSOnState
    } else {
        workTask.arguments = ["write", "com.apple.finder", "CreateDesktop", "true"]
        sender.state = NSOffState
    }
    
    workTask.launch()
    workTask.waitUntilExit()
    let killtask = Process()
    killtask.launchPath = "/usr/bin/killall"
    killtask.arguments = ["Finder"]
    killtask.launch()
}
```

因为我们想要读当前的状态，然后根据当前的状态来做切换是否是影藏还是创建 Desktop， 所以我们先创建 Pipe 和 Process，然后我们就不是用手动来输入这些参数，而是让Process代替我们来做这件事，result是我们来读取Process的结果，但是因为它是NSString，所以需要转成String（OC->Swift遗留问题？），同时我们还需要trim掉它末端的多余space。

然后新建Process，做输入，根据输入的结果，我们选择给我们的NSMenuItem是否添加上√.

这个时候 Run 起来，就可以看到程序的结果了。


![]({{site.baseurl}}/images/menubar/06.png)


### 最终の整理

再调整了一下代码的结构，设置一个变量desktopCreated，一进App的时候我们读取桌面是否被创建放在desktopCreated中，然后再根据这个变量做以后的事情|||


运行，稍作测试，通过


完整项目代码参见：









参考：

<https://www.raywenderlich.com/98178/os-x-tutorial-menus-popovers-menu-bar-apps>

<http://stackoverflow.com/questions/412562/execute-a-terminal-command-from-a-cocoa-app/32240064#32240064>


<https://developer.apple.com/reference/appkit/nssquarestatusitemlength>



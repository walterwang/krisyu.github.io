---
layout: post
title: "一个极简化播放视频的View"
---

# 一个极简化播放视频的View

原po在这里 [How to play video inside a UIView without controls, like a background/wallpaper?](http://stackoverflow.com/questions/35226532/how-to-play-video-inside-a-uiview-without-controls-like-a-background-wallpaper)


快速记录

1. import 必需品 AVKit / AVFoundation
2. 拉一个 @IBOutlet playView 出来，或者手动建view也行
3. 添加video资源
4. 设置按钮

```
    @IBAction func playVideoClip(_ sender: AnyObject) {
        
        guard let path = Bundle.main.path(forResource: "clip0", ofType: "mov") else {
            debugPrint("video.m4v not found")
            return
        }
        
        let player = AVPlayer(url: URL(fileURLWithPath: path))
        player.allowsExternalPlayback = false
        
        let videoLayer = AVPlayerLayer(player: player)
        videoLayer.frame = self.playView.bounds
        self.view.layer.addSublayer(videoLayer)
        player.play()
        
    }
        
```

当然还有很多别的设置可做，比如一直播放， 因为我不用做那件事，所以代码就ending在这里了。

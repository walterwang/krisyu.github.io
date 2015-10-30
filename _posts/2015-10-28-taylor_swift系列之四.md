#Taylor Swift系列之四

###group some UI elements

group UI elements就是把他们放在stack里面，变成stack view，这样针对整个stack view设置的规则依旧好用，一开始我把defaultPhoto这个image View放在下方，然后run app的时候就出错。

然后新建了一个放在stack view，就正常。

第二点是删除之前的image view，用command + x删除。（delete貌似没用|||）

```
View 
	Stack View
		Meal Name Label
		Name Text Field
		Set Default Label Text
		defaultPhoto// that is image View

```

###给Image View配action

发现直接拖拽imageview是没法建立action的，quote如下：

> A view displays content, whereas a control is used to modify it in some way. A control (UIControl) is a subclass of UIView. In fact, you’ve already worked with both views (labels, image views) and controls (text fields, buttons) in your interface.


但是不用担心，我们还有 Gesture recognizers 这个objects.

其实我的思路也是如此的，之前我想做的一件事，就是点击一张图片就做某些事，我第一个想法是用一个按钮覆盖这个图片，第二个想法是按钮填充图片（懒人）。

然而这里是直接把一个tap gesture的object直接放到image View上面。
然后跟code联系起来也是类似的，只是它是在scene dock上，然后通过拖拽这个Tap Gesture Recognizer来建立action，selectImageFromPhotoLibrary 

这个方法虽然只有五句，但是每句都好多故事....


```
@IBAction func selectImageFromPhotoLibrary(sender: UITapGestureRecognizer) {
    // Hide the keyboard.
    nameTextField.resignFirstResponder()
    
    // UIImagePickerController is a view controller that lets a user pick media from their photo library.
    let imagePickerController = UIImagePickerController()
    
    // Only allow photos to be picked, not taken.
    imagePickerController.sourceType = .PhotoLibrary
    
    // Make sure ViewController is notified when the user picks an image.
    imagePickerController.delegate = self
    
    presentViewController(imagePickerController, animated: true, completion: nil)
}
```


###delegate再度出现

跟text Field一样，代理模式再度开启，值得注意的是要用这个tap gesture，需要引入两个代理。

//UIImagePickerControllerDelegate 和 UINavigationControllerDelegate，自动补全时候擦亮双眼....

引入这两个代理之后，就可以使用代理中的方法了，比如这里用了两个方法：

```
func imagePickerControllerDidCancel(picker: UIImagePickerController){
}

func imagePickerController(picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : AnyObject]){
}

```
然后可以看到的是这里有两个特殊的“调用”在“ViewController”身上的“方法”，dismissViewControllerAnimated 和 presentViewController,然后同样

```
func imagePickerController(picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : AnyObject]) {
    // The info dictionary contains multiple representations of the image, and this uses the original.
    let selectedImage = info[UIImagePickerControllerOriginalImage] as! UIImage
    
    // Set photoImageView to display the selected image.
    photoImageView.image = selectedImage
    
    // Dismiss the picker.
    dismissViewControllerAnimated(true, completion: nil)
}

```

这个方法也句句都是故事,which means,需要研究。
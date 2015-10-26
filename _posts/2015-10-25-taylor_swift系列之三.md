#Taylor Swift系列之三

###一定要用AutoLayout

AutoLayout之方便感人，用肯定是要用的。所以AutoLayout的constrain要怎么修正，如何处理，如何重置，如何把几个UI元素再类似于group起来做AutoLayout肯定是需要知道和会debug的。


//calculator的auto layout依旧出错



###Outlet and Action

outlet 常用之一种，类似于propoerty(?)，然后依旧变量名在前，类型在后，这个outlet是Xcode帮我们自动创建的，IBOutlet 是 interface builder，然后类型是UITextField！，是implicitly unwrapped optional类型，一旦初始化之后就一定有值的optional类型。

    @IBOutlet weak var nameTextField: UITextField!




Action就好理解了，就是比如在Java中我们去点鼠标，然后这就是一个mouse event。iOS一定是event-driven programming.

看此Action func跟之前的函数一样，不难理解，然后同样有IB前缀，值得注意的是我们指定了sender的类型，sender parameter 是 UIButton型。


    @IBAction func setDefaultLabelText(sender: UIButton) {
    	mealNameLabel.text = "Default text"
    }
    
    
###模式来了

**target-action pattern**，以上就是传说中的target action模式，target是接受message的object，action则是这个函数。

**delegate**，处理text field的时候就开始用delegate（委托/代表）了，此处text Field是被代表的对象，而ViewController则是它的代理，可以来负责处理它的事


	class ViewController: UIViewController,UITextFieldDelegate



所以这里第一个UIViewController是继承（？），而第二个UITextFieldDelegate则是协议（！是协议）,但是不是添加了这一句就可以完事的，还需要在合适的地方添加：

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Handle the text field's user input through delegate callbacks.
        nameTextField.delegate = self
    }


这个函数当然是合适的地方，直到此时，ViewController彻底成为nameTextField的delegate，然后UITextField协议里面的很多方法就可用啦。


	
###TextField的代理方法

首先如果两个方法都没有，text Field这个时候还是可以开始往里面填东西了。

但是只有有了这两个方法，才能做到docu要我们做的事，利用自动补全，可以看到textField的代理方法大概8个吧。

第一个函数参数是textField，返回值是Bool，它的作用在于textFieldShouldReturn那么就是把textField里面的text拿来return了？然后return之后可以为第二个方法可用？

试了试别的方法，比如把EndEditing改成Begin，感觉就是没有这么“正常”.而且同时发现如果把这个函数

还有的存疑之处是比如，比如这个场景中不只一个UITextField，它做代理也是此番使用么？
试了一下，如果再新建一个text Field，使用代理和同样的函数，那么同样的label也是与之挂钩的，也就是我们的代理全都懂，分辨就找它了。

还有的问题是当出现了两个代理之时，如果我把第一个方法给comment掉了，发现由一个text Field切换到另一个之时，textFieldDidEndEditing依旧可用，然后看了文档表示依旧存疑~~~😂

现就假装记住标准模式就是这么用的吧 😄



    
    func textFieldShouldReturn(textField: UITextField) -> Bool {
        // Hide the keyboard
        textField.resignFirstResponder()
        return true
    }
    

    func textFieldDidEndEditing(textField: UITextField) {
        mealNameLabel.text = textField.text
    }


###注释

特别好用的注释

	// MARK: Action


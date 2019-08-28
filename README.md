# QCKit
本框架以swift语言开发，链式编程为主的框架。其中包含QCChainableUI、QCListView、QCDispatchGroup、QCNotificationCenter、QCString等五大模块，其链式特性，以及高内聚等特性，为iOS开发工程师，对工作中遇到繁琐且重复的的UI创建以及列表视图的创建问题，提供一站式的解决方案。

## 1.QCChainableUI
顾名思义，此模块为链式创建UI控件模块。包含了我们常用的所有UI视图，例如UIView、UIControl、UIButton、UIImageView、UILabel、UITextView、UITextField、UIScrollView、UITableView、UICollectionView、UIWebView、WKWebView、UIProgressView、UISlider、UISwitch、UIToolbar、UIAlertController等十多种UI控件。下面具体介绍它们各自的API：

### 1.1UIView
由于涉及到链式编程，中心思想就是把对象的成员变量改造成传递变量值，返回值为对象本身的函数。例如`let view = UIView()` 要为view设置背景色，传统的形式就是`view.backgroundColor = .red`，改造之后就可以直接调用`UIView().backgroundcolor(.red)`，如果想再调用其他属性例如isHidden，传统方式就是`view.isHidden = true`，链式之后就可以在原来的基础上继续追加代码：`UIView().backgroundcolor(.red).isHidden(true)`
注意：此模块不仅包含了绝大数原生属性（例如frame、alpha、isUserInteractionEnabled等），又扩展了一些编程中常用的属性和方法，例如点击事件、badge相关的属性。
```
let view = UIView()
            .frame(16, 100, 100, 50) //frame
            .borderColor(.red)       //边框色
            .borderWidth(1)          //边框宽度
            .backgroundColor(.green) //背景色
            .cornerRadiusWithClip(5) //圆角
            .superView(self.view)    //父视图，等同于self.view.addSubview(view)
            .badgePadding(8,4)       //以下是badge的属性，此为badge的内边距（左右内边距,上下内边距），默认值为（6，3）
            .badgeBorderWidth(1.5)     //badge的边框宽度 
            .badgeBorderColor(.white)//badge的边框颜色 
            .badgeTop(10)            //badge距离父视图的顶部距离
            .badgeHMargin(10)        //badge距离父视图的水平距离
            .badgeFont(UIFont.systemFont(ofSize: 12))//badge的文字字体
            .badgeBgColor(.red) //badge背景色
            .badgeTextColor(.white)  //badge的文字颜色
            .addAction { (view) in   //扩展了view的点击事件
                print("点击了view")
        }
//            .showAllNumber(true)   //是否显示全部数字（此属性对badgeNumber有效，默认值为false。badgeNumber超过99，若设置为false，则显示+99，否则，显示真实数字）
//            .badgeText("哈哈")        //badge文字  （badge总共有三种形式，分别是badge数字、badge文字、badge原点）
//            .badgeDotWidth(10)     //badge原点宽度

         view.qc_badgeNumber = 100  //设置badgeNumber的值
//        view.badgeIsHidden(false)  //是否隐藏badge
```

### 1.2UILabel
这几个控件模块的完全遵循原生继承关系。如UILabel,继承自UIView,则UIView的方法和属性可以完全继承给UILabel，同样可以调用UIView的链式方法。
除此之外，为UILabel扩展了内边距的属性，一个是单独设置hPadding(水平内边距)，还有一个是textEdgeInsets(上下左右内边距)。
```
let label = UILabel()
            .frame(0, 100, kWidth, 40)
            .font(14)
            .textColor(.white)
            .superView(self.view)
            //            .numberOfLines(0)
            .backgroundColor(.red)
            //            .hPadding(16, 16)  //水平内边距
            .textEdgeInsets(UIEdgeInsets(top: 10, left: 16, bottom: 10, right: 16))//上下左右内边距，此属性的高度自适应。
            .addAction { (label) in
                print("点击了label")
            }
label.text = "测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签测试标签"
```    
### 1.3UIButton   
此模块为UIButton扩展了各种状态的背景色、以及各种状态下的边框颜色，还有图片文字布局类型（图片位置，图片文字间距）
```
let btn =  UIButton()
            .frame(16, 100, kWidth - 32, 40)
            .textFont(15)                          // 按钮字体
            .title("测试按钮")                      // 按钮文字
            .image("测试图片")                      // 按钮图片
            .image_Sel("选中测试图片")               // 按钮选中图片
            .image_Disable("失效测试图片")           // 按钮失效图片
            .image_HighLight("高亮测试图片")         // 按钮高亮图片
            .backgroundColor(.white)               // 按钮正常背景色
            .backgroundColor_Sel(.red)             // 按钮选中背景色
            .backgroundColor_Disable(.gray)        // 按钮失效背景色
            .backgroundColor_HighLight(.green)     // 按钮高亮背景色
            .titleColor(.green)                    // 按钮正常字体颜色
            .titleColor_Sel(.white)                // 按钮选中字体颜色
            .titleColor_Disable(.white)            // 按钮失效字体颜色
            .titleColor_HighLight(.white)          // 按钮高亮字体颜色
            .borderWidth(1)                        // 按钮边框宽度
            .cornerRadiusWithClip(5)               // 按钮圆角大小(其layer.maskToBounds = true)
            .borderColor(.green)                   // 按钮边框颜色
            .borderColor_Sel(.green)               // 按钮选中边框颜色
            .borderColor_Disable(.gray)            // 按钮失效边框颜色
            .borderColor_HighLight(.green)         // 按钮高亮边框颜色
            .layoutButton(.right, 10)              // 按钮图片问题布局设置（共有三个参数：buttonImagePosition（图片相对于文字的位置top/bottom/right/left）, imageTitleSpace(图片文字之间的距离)，fitSize（是否宽度或高度自适应））
            .superView(self.view) 
            .addAction({ (btn) in                  // 按钮点击事件
                  print("手指抬起")
            }) 
            .addActionWithControlEvent({ (btn) in  // 按钮带有事件类型的点击事件
                  print("手指按下")
            }, .touchDown)
            .addActionWithControlEvent({ (btn) in
                  print("手指抬起")
            }, .touchUpInside)
            .addActionWithControlEvent({ (btn) in
                   print("手指多次点击")
            }, .touchDownRepeat)
            .addActionWithControlEvent({ (btn) in
                   print("点击完成")
            }, .primaryActionTriggered)
            .addActionWithControlEvent({ (btn) in
                   print("全部事件")
            }, .allEvents)
//        btn.removeTapWithControlEvent(.touchUpInside)   // 移除按钮带有事件类型的点击事件（用于cell的缓存复用）
```    
### 1.4UITextField
此模块为为UITextField扩展了文本框左右内边距、文本框的左右视图、及右视图的点击事件（比如搜索按钮的点击事件）、占位图文字颜色（可以设置在占位文字之前。原生的占位文字由于是懒加载，如果占位文字没有设置之前，设置占位文字颜色则无效。）、文本输入类型（包含了手机号、纯数字、纯中文、纯字母、字母和数字、金额、整数金额、邮箱、身份证号）、最大值及最大值回调、清除按钮图片设置等
``` 
let textField = UITextField()
            .frame(16,100, kWidth-32, 40)
            .backgroundColor(.white)
            .cornerRadiusWithClip(20)
            .font(14)
            .textColor(.red)
            .borderWidth(1)
            .borderColor(.red)
            .superView(self.view)
            .paddingLeft(16)                   // 设置文本框左内边距             
            .paddingRight(16)                  // 设置文本框右内边距    
            .leftView("左边图标")               // 设置左边图标 
            .rightView("", true, { (_) in      // 设置右边图标，是否显示分割线，右侧图标点击事件
                print("点击右侧图标事件")
            })       
            .tintColor(.red)                   // 设置光标颜色
            .placeholder("请输入金额")       
            .textFieldType(.money)             //设置文本输入类型
            .maxMoney(1000, {                  //设置最大金额数，以及超过最大金额的回调
                 print("输入金额过大，请重新选择")
            })
            .placeholderColor(.red)
            .clearButtonMode(.whileEditing,"inputClearBtn")  // 设置清除按钮模式，以及设置清除按钮图片，可以不设置，默认为原生清除按钮
``` 



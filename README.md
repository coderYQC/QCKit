# QCKit
本框架以swift语言开发，链式编程为主的框架。其中包含QCChainableUI、QCListView、QCDispatchGroup、QCNotificationCenter、QCString等五大模块，其链式特性，以及高内聚等特性，为iOS开发工程师，对工作中遇到繁琐且重复的的UI创建以及列表视图的创建问题，提供一站式的解决方案。

## 1.QCChainableUI
顾名思义，此模块为链式创建UI控件模块。包含了我们常用的所有UI视图，例如UIView、UIControl、UIButton、UIImageView、UILabel、UITextView、UITextField、UIScrollView、UITableView、UICollectionView、UIWebView、WKWebView、UIProgressView、UISlider、UISwitch、UIToolbar、UIAlertController等十多种UI控件。下面具体介绍它们各自的API：

### 1.1UIView
由于涉及到链式编程，中心思想就是把对象的成员变量改造成传递变量值，返回值为对象本身的函数。例如`let view = UIView()` 要为view设置背景色，传统的形式就是`view.backgroundColor = .red`，改造之后就可以直接调用`UIView().backgroundcolor(.red)`，如果想再调用其他属性例如isHidden，传统方式就是`view.isHidden = true`，链式之后就可以在原来的基础上继续追加代码：`UIView().backgroundcolor(.red).isHidden(true)`
注意：此模块不仅包含了绝大数原生属性（例如frame、alpha、isUserInteractionEnabled、layer等），有扩展了一些编程中常用的属性，例如badge相关的属性。
`
let view = UIView()
            .frame(16, 100, 100, 50) //frame
            .borderColor(mainColor)  //边框色
            .borderWidth(1)          //边框宽度
            .cornerRadiusWithClip(5) //圆角
            .superView(self.view)    //父视图，等同于self.view.addSubview(view)
            .badgePadding(8,4)       //以下是badge的属性，此为badge的内边距（左右内边距）
            .badgeBorderWidth(1)     //badge的边框宽度 
            .badgeBorderColor(.white)//badge的边框颜色 
            .badgeTop(10)            //badge距离父视图的顶部距离
            .badgeHMargin(10)        //badge距离父视图的水平距离
            .badgeFont(UIFont.systemFont(ofSize: 12, weight: .light))//badge的文字字体
            .badgeBgColor(mainColor) //badge背景色
            .badgeTextColor(.white)  //badge的文字颜色
//            .showAllNumber(true)   //是否显示全部数字（此属性对badgeNumber有效，badgeNumber超过99，默认为99+，若设置为false则显示+99，否则，显示真实数字）
            .badgeText("哈哈")        //badge文字  （badge总共有三种形式，分别是badge数字、badge文字、badge原点）
//            .badgeDotWidth(10)     //badge原点宽度

//        badge.qc_badgeNumber = 100  //设置badgeNumber的值
//        badge.badgeIsHidden(false)  //是否隐藏badge
`

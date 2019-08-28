# QCKit
本框架以swift语言开发，链式编程为主的框架。其中包含QCChainableUI、QCListView、QCDispatchGroup、QCNotificationCenter、QCString等五大模块，其链式特性，以及高内聚等特性，为iOS开发工程师，对工作中遇到繁琐且重复的的UI创建以及列表视图的创建问题，提供一站式的解决方案。

## 1.QCChainableUI
顾名思义，此模块为链式创建UI控件模块。包含了我们常用的所有UI视图，例如UIView、UIControl、UIButton、UIImageView、UILabel、UITextView、UITextField、UIScrollView、UITableView、UICollectionView、UIWebView、WKWebView、UIProgressView、UISlider、UISwitch、UIToolbar、UIAlertController等十多种UI控件。下面具体介绍它们各自的API：

###1.1UIView
由于涉及到链式编程，中心思想就是把对象的成员变量改造成传递变量值，返回值为对象本身的函数。例如`let view = UIView()` 要为view设置背景色，传统的形式就是`view.backgroundColor = .red`，改造之后就可以直接调用`UIView().backgroundcolor(.red)`，如果想再调用其他属性例如isHidden，传统方式就是`view.isHidden = true`，链式之后就可以在原来的基础上继续追加代码：`UIView().backgroundcolor(.red).isHidden(true)`
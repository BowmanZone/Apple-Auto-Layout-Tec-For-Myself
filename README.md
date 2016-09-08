# Apple-Auto-Layout-Tec-For-Myself
Auto Layout Guide:
https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/index.html#//apple_ref/doc/uid/TP40010853

一些常见的外部改变来源：

1.用户调整窗口的大小（OS X）。

2.用户进入或者离开Splite View，iPad（iOS）。

3.旋转设备。

4.支持不同的size classes（Compact-紧凑、Regular-正常、Any-任意）。

5.支持不同的屏幕尺寸。

大多数这类变化可能发生在运行时状态。尽管屏幕尺寸不会在运行时改变，一样可以创建一个自适应接口来允许程序运行在iphone4s、iPhone+甚至是iPad上。

内部改变来源：
一些用户界面或者是试图控件的大小发生改变

1.应用改变内容显示（文本和图像）。

2.应用支持国际化。国际化的过程使应用程序能够适应不同的语言、地区,和文化，国际化在布局上有三个主要的影响：用户界面转换语言时标签所需要的空间大小，例如德语比英语需要更多的标签空间，而日语有时候需要更少的空间；由于地区的变化，时间和日期格式也会产生微妙的变化，用户界面尺寸仍然需要适应这些变化；语言的改变不仅会影响文本的大小，也会影响组织的布局，例如英语、阿拉伯语和希伯来语的组织布局就是相反的，一个从左往右，一个从右往左。

3.应用支持动态类型（iOS）。用户可以随意更改文本大小，比如字体大小、格式等，用户界面则需要做出适应。

自动布局框架

1.使用代码来制定用户界面。
应用通过编码计算出视图层次结构上的每一个视图的frame来实现布局，而frame则定义了视图在父视图坐标系统中的origin、height和width。为了能够布局用户界面，你不得不计算视图层次结构上的每一个视图的大小和位置，如果一个发生改变，那么你不得不为每一个受影响的视图计算出frame。在许多方面，通过编码定义一个界面的frame提供了很大的灵活性和可行性，当一个变化产生的时候，你可以做任何你想要的改变。然而布局一个简单的用户界面需要相当多的努力设计、调试和维护，因为你必须要管理自己的变化，那么创建一个自适应的用户界面的困难将会是以数量级的增加。

2.使用autoresizing masks自动响应外部变化。
可以使用autoresizing msaks来帮助缓解代码布局带来的压力。autoresizing masks定义一个视图的父视图frame改变的时候，这个视图的frame该如何变化。这简化了为适应外部变化的布局创建工作。然而autoresizing masks支持一些相对较小的子集布局，对于复杂的用户界面，还是需要相应代码辅助布局。此外，autoresizing masks只适用于外部布局变化，不适用于内部布局变化。

3.使用Auto Layout
autoresizing masks仅仅是布局改进的一个迭代，auto layout是一种全新的模式。auto layout思考的不应该是视图的frame，应该是视图之间的关系。Auto Layout通过使用一系列的约束constraints来定义用户界面，约束constraints一般代表了两个视图之间的关系。基于约束的每一个视图，Auto Layout都会计算出它们的大小和位置。这样产生的布局适应内部布局和外部布局。

设计一组约束来创建特定行为的逻辑是非常不同于通过写代码或者面向对象编码的逻辑。幸运的是，掌握Auto Layout与掌握其他的编程任务并没有什么不同。第一：理解基于约束的layouts背后的逻辑;第二：学习API。在学习其他的编程任务的时候，你已经遵循了这些步骤，Auto Layout也不例。

上面所记载的文字旨在帮助我过渡到Auto Layout，下面的文字将帮助我进一步学习Auto Layout。

stack view提供了一种简单的方式来利用Auto Layout的功能，而不引入约束的复杂性。一个satck view管理用户界面元素的行或列。stack view通过属性来管理元素。

axis：（UIStackView Only）定义了satck view的方向，水平或者垂直。轴

orientation：（NSStackView Only）定义了satck view的方向，水平或者垂直。轴

distribution：定义了沿着axis（轴）方向的视图集的布局。

alignment：定义了垂直于stack view axis（轴）方向的视图集的布局。

sapcing：定义了相邻视图的间隔。

stack view同样的对于管理元素视图的 content-hugging 和 compression-resistance 的属性起作用。

可以使用嵌套的stack view来构建复杂的视图。事实上，应该尽可能的多的使用stack view来管理布局，除非单独使用stack view已经不能达到目的，这是就可以使用约束。

注意：尽管嵌套的satck view能够构建复杂的用户界面，也避免不了使用约束来辅助构建界面，因为至少也要为最外层的stack view添加约束来获取位置。

UIStackView Class Reference: https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIStackView_Class_Reference/index.html#//apple_ref/doc/uid/TP40015256

解析约束：https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html#//apple_ref/doc/uid/TP40010853-CH9-SW1


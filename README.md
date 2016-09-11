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

解析约束: https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html#//apple_ref/doc/uid/TP40010853-CH9-SW1

视图的布局被定义成一系列的线性方程，每一个约束都代表一个方程，你的目标就是解析那些有且只有一个可能值的方程。

例子：
    RedView.Leading = 1.0 x BlueView.trailing + 8.0 

item1.Attribute1 Relationship Multiplier x Item2.Attribute2 + Constant

这个约束表示的状态是RedView的前缘必须离BlueView得后缘8.0个点。

    Item 1: RedView，这个Item必须是一个view或者一个layout guide。
    
    Attribute 1: 被约束在Item1上的属性 leading edge.
    
    RelationShip: 左右之间的关系，三个可能的值：=、<=、>=.
    
    Multiplier: attribute2被乘的浮点数值 1.0。
    
    Item2: 与Item1不同，这个值可以被留白。
    
    Attribute2: 被约束在Item2上的属性 trailing。如果Item2被留白，它一定一个属性 Not an Attribute.
    
    Constant: 常数，浮点偏移值，被加在attribute2上的值 8.0。

attribute：属性    Item：元素

大多数约束定义了用户界面上两个元素之间的关系，这些元素可以是视图（集）或者layout guide。约束可以也可以定义单一元素的两个不同属性关系，例如设置一个元素的width和height的宽高比aspect ratio。还可以常数值赋值给一个元素的width和height，这时Item2会被留白，attribute2被设置为Not An Attribute，multiplier也被置0.0。

在Auto Layout中，属性定义了一个可以被约束的功能，通常属性包括了四个边缘edge（leading、trailing、top、bottom）、宽高（width、height） 、水平和垂直的中心点（vertical and horizontal centers），可以查看NSLayoutAttribute来查看所有的属性列表。（OS X和iOS都使用NSLayoutAttribute来定义属性，它们的区别很小，使用时要注意）

多种变化的方程组合可以创建许多不同类型的约束，你可以定义视图间的空隙、定义两个视图的相对大小、甚至是定义一个视图的宽高比。然而，并不是所有的属性都是兼容的。这里有两种基本类型的属性：Size attributes（width、height）和 location attributes（Leading、trailing、top、bottom）。Size attributes指示一个元素究竟有多大，而没有任何location的信息。Location attributes指示一个元素相对于其他的位置，而没有任何元素大小的信息。

记住上面的差异，下面的规则是适用的:

You cannot constrain a size attribute to a location attribute. 

You cannot assign constant values to location attributes. 

You cannot use a nonidentity multiplier (a value other than 1.0) with location attributes. 

For location attributes, you cannot constrain vertical attributes to horizontal attributes. 

For location attributes, you cannot constrain Leading or Trailing attributes to Left or Right attributes.

    // Setting a constant height
    View.height = 0.0 * NotAnAttribute + 40.0
    	 
    // Setting a fixed distance between two buttons
    Button_2.leading = 1.0 * Button_1.trailing + 8.0
     
    // Aligning the leading edge of two buttons
    Button_1.leading = 1.0 * Button_2.leading + 0.0
    
    // Give two buttons the same width
    Button_1.width = 1.0 * Button_2.width + 0.0
    
    // Center a view in its superview
    View.centerX = 1.0 * Superview.centerX + 0.0
    View.centerY = 1.0 * Superview.centerY + 0.0
     
    // Give a view a constant aspect ratio
    View.height = 2.0 * View.width + 0.0

注意：这是方程表达式，不是简单的赋值运算。

当Auto Layout解析这些方程的时候，它并不是简单的将右边的值赋值给左边，相反，它计算出attribute1和attribute2的值来使得等式成立，这就意味着我们可以自由地重组这些方程式：

		// Setting a fixed distance between two buttons
		Button_1.trailing = 1.0 * Button_2.leading - 8.0
		 
		// Aligning the leading edge of two buttons
		Button_2.leading = 1.0 * Button_1.leading + 0.0
		 
		// Give two buttons the same width
		Button_2.width = 1.0 * Button.width + 0.0
		 
		// Center a view in its superview
		Superview.centerX = 1.0 * View.centerX + 0.0
		Superview.centerY = 1.0 * View.centerY + 0.0
		 
		// Give a view a constant aspect ratio
		View.width = 0.5 * View.height + 0.0

这些列子和上面的列子最终实现的效果是一致的。当然在重组这些方程等式的时候，你也要适当的变换约束，比如说 +8.0 变成 -8.0、 2.0* 变成 0.5* 以达到一致的效果。

你可能会发现Auto Layout经常提供多种不同方式来解决相同问题，理想情况下，你应该选择最能明显地描述你意图的解决方案。但是，不同的开发者可能会在到底哪个解决方案是最佳的问题上产生分歧。如果你只选择一种方法并且一直实践下去，从长远来看。你可能会经历更少的问题，而不是花更多的时间去纠结到底哪个是最佳方案。例如，这个教程遵从的经验法则是：

1.整数乘积要好过分数乘积；

2.正数要好多负数；

3.只要有可能，视图在布局中的出现次序应该是：从左往右、从上到下。

到目前为止，所有的列子都是作为等式来表达的约束。约束也能够表达不等式。具体来说，约束关系可以是=、>=、<=.

使用约束来定义一个视图的最大、最小尺寸Size：

		// Setting the minimum width
		View.width >= 0.0 * NotAnAttribute + 40.0
		 
		// Setting the maximum width
		View.width <= 0.0 * NotAnAttribute + 280.0
		
也可以使用两个不等式来代替一个恒等式：

		// A single equal relationship
		Blue.leading = 1.0 * Red.trailing + 8.0
		 
		// Can be replaced with two inequality relationships
		Blue.leading >= 1.0 * Red.trailing + 8.0
		Blue.leading <= 1.0 * Red.trailing + 8.0

两个不等式也不总是相当于一个等式的关系，比如上面例子中的视图width只是定义了最大、最小范围，并没有直接定义width，仍然需要添加一个合理范围内的width来定义视图的width或者中心点。

一般所有的约束都是必要的，Auto Layout必须计算出一个解决方案来满足所有的约束。如果不能满足，那么就会出现一个错误，Auto Layout会在控制台打印出相关信息，并且它会选择一个约束来终断，然后会抛开这个中断的约束再计算出解决方案。

也可以创建可选的约束，所有的约束有一个1~1000的优先级priority。约束必须要有一个1000优先级的，其他所有的约束是可选的。

当在计算解决方案的时候，Auto Layout会尝试以优先级从高到低的顺序来满足所有的约束。如果不能满足一个可选的约束，这个可选约束会被跳过，然后Auto Layout继续满足下一个约束。

尽管一个可选约束不能被满足，但是它还是会影响到布局。如果在跳过skip一个约束后出现了不太明了的布局，系统会选择最接近约束的解决方案。换句话说，不满足条件的可选约束扮演着一个把视图往它们那个结果拉取的角色。
可选的约束和不等式通常会一起起作用。例如：

    Blue.leading >= 1.0 * Red.trailing + 8.0
		Blue.leading <= 1.0 * Red.trailing + 8.0
	
这里为两个不等式提供了不同的约束，>=需要一个高优先级（1000priority）的关系，<=有一个低优先级（250priority）的关系。这就意味着Blueview和Redview之间不能少于8.0点的距离（满足高优先级>=，<=低优先级会被按顺序被满足），然而鉴于布局中的其他约束条件，其他约束可以把Blueview往远处拉。同时，可选约束会把Blueview拉向Redview这边，以尽可能地让它们之间的空隙值接近8.0点。这就是为什么可选的约束和不等式通常会一起起作用。

注意：不要勉强所有的约束优先级都是1000。实际上，属性大体被定义在low（250）、medium（500）、high（750）、required（1000）。你只需要一个或者两个优先级比这些值高一点或者低一点的约束，来防止冲突。如果除此之外，你可能需要重新审视你的布局逻辑。

内在内容大小（intrinsic content size）：

迄今为止，所有的例子都使用约束来定义视图的位置和它们的大小，然而有一些视图会根据它们当前的内容给出一个自然值。（intrinsic content size）比如按钮的intrinsic content size就是它的标题大小加上一点缩进。并不是所有的视图都有intrinsic content size，对于那些有intrinsic content size的视图而言，intrinsic content size能够定义视图的height或者width或者 height和width。

View
Intrinsic content size
UIView and NSView
No intrinsic content size.
Sliders
Defines only the width (iOS).
Defines the width, the height, or both—depending on the slider’s type (OS X).
Labels, buttons, switches, and text fields
Defines both the height and the width.
Text views and image views
Intrinsic content size can vary.

Intrinsic content size是基于视图当前的内容。一个Label或者Button的Intrinsic content size是基于显示文字的数量和所使用的字体大小。对于其他视图，Intrinsic content size甚至更加复杂。例如，一个空的image view没有Intrinsic content size，一旦你添加上了一个image，那么它的Intrinsic content size就会被设置为image的大小。

一个文本视图text view的Intrinsic content size取决于它的内容、是否开启滚动功能、应用在视图上的约束。例如，开启滚动功能，那么视图将不会有Intrinsic content size。With scrolling disabled, by default the view’s intrinsic content size is calculated based on the size of the text without any line wrapping. For example, if there are no returns in the text, it calculates the height and width needed to layout the content as a single line of text. If you add constraints to specify the view’s width, the intrinsic content size defines the height required to display the text given its width.  （这段确实不好翻译）

Auto Layout通过为每一个维度使用一对约束来展示视图的Intrinsic content size。content hugging（内容环抱力）把视图向里拉，以恰到好处地适应内容大小。 compression（压缩阻力）把视图往外推，防止视图将内容剪辑。

这些维度的约束通过不等式来定义：

		// Compression Resistance
		View.height >= 0.0 * NotAnAttribute + IntrinsicHeight
		View.width >= 0.0 * NotAnAttribute + IntrinsicWidth
		 
		// Content Hugging
		View.height <= 0.0 * NotAnAttribute + IntrinsicHeight
		View.width <= 0.0 * NotAnAttribute + IntrinsicWidth

IntrinsicHeight、IntrinsicWidth约束视图的Intrinsic content size

每一个约束都有它们自己的优先级。默认的是，视图的content hugging优先级为250，compression resistance优先级为750.因此，拉伸视图比缩小视图更容易。对于大多数的控件，都有一个期望的行为：例如可以很容易的通过Intrinsic content size来把按钮拉伸得更大，然而，想要缩小它，它的内容就可能会被剪辑掉。

注意：Interface Builder可能偶尔会修改这个属性来防止冲突。

不管怎么样，尽可能使用视图的Intrinsic content size。它可以帮助你动态的布局视图内容，也可以减少约束的创建，避免冲突，但是你需要管理视图的 content-hugging 和 compression-resistance 的优先级。

建议：

		When stretching a series of views to fill a space, if all the views have an identical content-hugging priority, the layout is ambiguous. Auto Layout doesn’t know which view should be stretched.  A common example is a label and text field pair. Typically, you want the text field to stretch to fill the extra space while the label remains at its intrinsic content size. To ensure this, make sure the text field’s horizontal content-hugging priority is lower than the label’s.  In fact, this example is so common that Interface Builder automatically handles it for you, setting the content-hugging priority for all labels to 251. If you are programmatically creating the layout, you need to modify the content-hugging priority yourself. 
		Odd and unexpected layouts often occur when views with invisible backgrounds (like buttons or labels) are accidentally stretched beyond their intrinsic content size. The actual problem may not be obvious, because the text simply appears in the wrong location. To prevent unwanted stretching, increase the content-hugging priority. 
		Baseline constraints work only with views that are at their intrinsic content height. If a view is vertically stretched or compressed, the baseline constraints no longer align properly. 
		Some views, like switches, should always be displayed at their intrinsic content size. Increase their CHCR priorities as needed to prevent stretching or compressing. 
		Avoid giving views required CHCR priorities. It’s usually better for a view to be the wrong size than for it to accidentally create a conflict. If a view should always be its intrinsic content size, consider using a very high priority (999) instead. This approach generally keeps the view from being stretched or compressed but still provides an emergency pressure valve, just in case your view is displayed in an environment that is bigger or smaller than you expected.

The intrinsic content size acts as an input to Auto Layout. When a view has an intrinsic content size, the system generates constraints to represent that size and the constraints are used to calculate the layout.
The fitting size, on the other hand, is an output from the Auto Layout engine. It is the size calculated for a view based on the view’s constraints. If the view lays out its subviews using Auto Layout, then the system may be able to calculate a fitting size for the view based on its content.//satck view根据内容大小和属性来计算自身大小

Select the type of rectangle you want to display.
-
The frame rectangle is the raw frame of the view element.

The alignment rectangle is the total visual space occupied by the view element including any runtime adornments. It can be different than the frame rectangle.

![视图构建器界面](https://developer.apple.com/library/ios/recipes/xcode_help-IB_objects_media/Art/IB_OM_H_frame_selector_2x.png)

![选项](https://developer.apple.com/library/ios/recipes/xcode_help-IB_objects_media/Art/IB_OM_H_frame_align_rect_popup_2x.png)

frame rectangle指的是视图的原始的frame，而alignment rectangle指的是布局视图中的视图可视区域

![frame rectangle 和 alignment rectangle的对比](http://img.blog.csdn.net/20150626144908579?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWFzaV94aQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

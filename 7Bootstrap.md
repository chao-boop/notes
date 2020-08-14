# Bootstrap  框架  主要是做响应式布局和移动端的网站
学的是4.3.1的版本     bs4.ntp.org.cn
Bootstrap 插件全部依赖 jQuery
CDN在线引入
## 响应式原理
响应式所具备的特点:
        网页的宽度自动调整
        尽量少用绝对宽度
        字体要使用rem(相对于跟节点root元素的字体大小) , em 作为单位
        布局使用浮动或弹性

### 媒体查询:根据一个或多个基于设备类型,具体特点和环境来应用样式    部分讲解  详细内容访问:https://drafts.csswg.org/mediaqueries
@media 
比如:  @media all{     //all是条件
            div{
                font-size:3rem;
                    }
                }
        引入方法:
            style标签内
                <style>
                    @media all{}
                </style>
            在css文件内引入外部css文件时后面跟一个括号括号内跟条件 就是@media
            @import url('地址')(all);

            在link内引入  media属性 
            <link rel="stylesheet" href="css地址" media="all"></link>

- 媒体类型:all 所有设备
        print 打印机设备
        screen 彩色的电脑屏幕
        speech 听觉设备()
        注意:tty tv projection handheld braille embossed aural等几种类型在媒体4中已经废弃


- 媒体特性(部分)
    width宽度
        min-width 最小宽度,宽度只能比这个大
        max-width 最大宽度,宽度只能比这个小
    height高度
        min-height 最小高度,高度只能比这个大
        max-height 最大高度,高度只能比这个小
    orientation方向
        Landscape 横屏(宽度大于高度)
        portrait  竖屏(高度大于宽度)
    aspect-ratio 宽度比
    -webkit-device-pixel-ratio 像素比(webkit内核的私有属性)

比如:
    @media (min-width:500px){
        div{
            backgrpund:green;
        }
    }
    
- 逻辑运算符 做条件判断 
    and  合并多个媒体类型(并且的意思)
    ,    匹配某一个媒体查询(或者的意思)
    not  对媒体查询结果取反
    only 仅在媒体查询匹配成功后应用样式(防范老旧浏览器)
    
    比如:
        @media all and (min-width:300px){}  所有设备屏幕宽度比300px大

## 栅格系统  Bootstrap 的栅格系统使用一系列容器，行和列来布局和对齐内容。 它是用 flexbox 构建的，并且完全响应
容器使用:
    <div class="container">    //固定结构 固定class  一个盒子
            <div class="row">//  一行           clas="mt-5" 上margin为5
                <div class="col-sm">     //每一列     最多12列 多了就会换行排列
                    One of three columns
                </div>
                <div class="col-sm">  
                    One of three columns
                </div>
                <div class="col-sm">
                     One of three columns
                </div>
            </div>
    </div>

    <div class="container-fluid"></div>  //另外一个   使用 .container 作为响应像素宽度(当屏幕达到一定值时,盒子宽度也改变)   .container-fluid 表示宽度

- 如果使用的是 <div class="container"> 
    第三层的class 有多个值   

    	<576px	    ≥576px	     ≥768px	    ≥992px	    ≥1200px    当屏幕超过范围时
	None (auto	    540px	    720px	    960px	    1140px      盒子宽度的值
	    .col-	    .col-sm-	.col-md-	.col-lg-	.col-xl-    可用class


1. class="col-xl-1"  表示该标签占一列  最后一个数字是几就占几列  如果超出 该列就会换行   该class为超大屏,屏幕宽度大于等于1200时容器宽度为1140,一行可以设置12列,屏幕尺寸小于1200时一行只能设置一列 
2. class="col-lg-4"  和上面一样 lg为大屏 屏幕宽度大于等于992时 容器宽度固定为960 一行可以设置12列 屏幕小于992时,一行只能设置一列
其他同理


- class="col"设置该class为等宽列  一行类说有列等宽      会自动平分剩余宽度

- col-sm-auto  在中等屏幕下由内容撑开高度  也可以是其他比如-col-md-auto之类的

- w-00  被设置的标签宽度将会被设置为100%  在希望断开的地方加一个  这样可以让后面的列换行

- col-*  设置所有尺寸下都占同样的列数,*代表列数


<!-- 
- 混合排列或者组合模式

比如:
				1、超大屏幕下一行显示6个div,一个div应该占2列
				2、大屏幕下一行显示4个div,一个div应该占3列
				3、中等屏幕下一行显示3个div,一个div应该占4列
				4、小屏幕下一行显示2个div,一个div应该占6列
				5、超小屏幕下一行显示1个div,一个div应该占12列
		 -->
		<div class="row mt-5">
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
			<div class="col-xl-2 col-lg-3 col-md-4 col-sm-6 col-12">超大屏6个，大屏4个，中等屏3个，小屏2个，超小屏1个</div>
		</div>
        
- 对齐:   3.x的版本没有  因为他是浮动布局  4.x是弹性布局
    垂直对齐:
        1.行的对齐方式:
            align-items-start 顶对齐
            align-items-center 中间对齐
            align-items-end 底对齐
        2.列的对齐方式
            align-self-start 底对齐
            align-self-center 中间对齐
            align-self-end 底对齐
    水平对齐:
        justify-content-start 左对齐
        justify-content-center 居中对齐
        justify-content-end 右对齐
        justify-content-around 分散居中对齐(元素两侧间距相等)
        justify-content-between 左右两端对齐(元素之间的间距自动平分)

    列排序:class="order-{breakpoint}-*"  *表示列  数字是几该标签就会被排到第几号   {breakpoint}是相应的-sm-  -md- -lg-之类的
                    order-first代表排在第一列 order-last代表排在最后一列
                
            3.x的版本使用的是 col-{breakpoint}-push-*   ,  col-{breakpoint}-pull-* 来排序

    列偏移:使用offset-{breakpoint}-*   *是偏移的数量  比如offset-md-4往右偏移4列  如果后面又就会跟着一起偏移

    间距:mr-{breakpoint}-auto 使右侧的列远离到最右边
         mr-{breakpoint}-auto 使左侧的列远离到最左边

    嵌套:每一个列里可以在继续放行,那嵌套里面的元素就会以父级的宽度为基准,再分12个列


## 内容部分
### 重置
    更新部分浏览器的预设值，在可变动的文字间距上使用 rem 替代 em。
    避免 margin-top。垂直边缘可能会发生重叠，产生无法预料的错误。更重要的是 margin 应该是单向、简单的思维。
    为了在设备之间之间轻松缩放，block 元素应当在 margin 上采用 rem。
    尽可能使用继承将字体相关属性的声明保持在最低限度。
#### 排版
    class="h1"  h1 到 .h6 的 Class，因为当你想匹配某一标题的字体样式，但不能直接使用 HTML 元素时。
    class="text-muted"  标题文本
    class="display-1"  到4都有  超大标题
    class="lead" 可以使用 .lead 来添加引言内容（字体比标题小一些）。
    用于引用文档中其他来源的内容块。 将任何HTML包含在<blockquote class="blockquote">里作为引用。
    在 <footer class="blockquote-footer"> 里添加需要署名的内容。 并在 <cite> 里添加作者。
    class="text-center"  "text-right"  "text-left"  文本居中 右对齐 左对齐
    class="list-unstyled"  删除列表项上的默认列表样式和左边距（仅限直接子项）。 仅适用于直接子列表项，这意味着你还需要为任何嵌套列表添加类
    删除列表的项目符号并使用两个类的组合应用一些微小的边距，使用 .list-inline和.list-inline-item 来实现。
                        <ul class="list-inline">
                                <li class="list-inline-item">Lorem ipsum</li>       <!-- 3.x的版本是不需要在li身上添加class -->
                                <li class="list-inline-item">Phasellus iaculis</li>
                                <li class="list-inline-item">Nulla volutpat</li>
                        </ul>
    text-truncate可以让超出的内容省略，3.x的版本里使用的是text-overflow 

### 代码
    在 <code> 里编写行内代码，请务必转义HTML的尖括号。
    在 <pre> 里编写多行代码。 再次确保在代码中转义任何尖括号以进行正确渲染。 你可以选择添加 .pre-scrollable 类，它将设置最大高度为340px并提供y轴滚动条。
    使用 <var> 标记变量。
    你可以使用 <kbd> 来标记键盘上的按钮，这看起来很生动
    使用 <samp> 标签来展示可能的输出结果

### 图片
    给图片添加 .img-fluid 类，这样它就变成了一张响应式设计的图片。另外添加 max-width: 100%; 和 height: auto; 可以让图片根据父元素的大小进行等比例缩放。
    .img-thumbnail 类来设置一个1像素宽度的边框
    class="rounded " 圆角
    class="float-left"  "float-right"  左浮动和右浮动

    <picture>标签
				<source media="(min-width:1200px)" srcset="images/1140.jpg">
				<source media="(min-width:992px)" srcset="images/960.jpg">
				<source media="(min-width:768px)" srcset="images/720.jpg">
				<source media="(min-width:576px)" srcset="images/540.jpg">
				<img src="images/img_01.jpg" alt="">	<!-- 当尺寸小于576的时候会显示这个图片 -->
			</picture>
			<!-- .webp	图片的格式 -->
			<!-- 支持情况：>=ios9.3 || >android4.4 -->

### 表格
    class="table" 只需将基类 .table 添加到任何 <table> ，然后就可以使用自定义样式或各种包含的修饰符类进行扩展。使用最基本的.table标记，下面的例子是基于.table-*的表格在 Bootstrap 中的外观。 所有表格样式都在 Bootstrap 4 中继承，这意味着任何嵌套表格的样式都与父表格相同。

     .table-dark 在深色背景上使用浅色文本反转颜色。
     .thead-light 或 .thead-dark 使 <thead> 显示为浅灰色或深灰色。
     .table-striped 来给 <tbody> 的所有行添加条纹效果。
     .table-bordered 类可以给表格内的所有单元添加边框
     .table-borderless 类来移除表格里的所有边框。
     .table-borderless 还可以用在黑色模式。
     .table-hover 类可以使 <tbody> 里的内容在获得鼠标停留时高亮显示。
    .table-sm 类可以让表格所有单元的间距缩小一半。

### 图文区
    如果需要显示带有标题的图像，请考虑使用<figure>（一种全新的玩法）。
    使用包含的 .figure ， .figure-img 和 .figure-caption 类为HTML5 <figure> 和 <figcaption> 元素提供一些基本样式。 <figure> 中的图像没有明确的大小，因此请务必将 .img-fluid 类添加到 <img> 以使其成为响应式设计的图像

    使用文本工具可以轻松对齐 figure 中标题。
    <figure class="figure">
        <img src=".../400x300" class="figure-img img-fluid rounded" alt="A generic square placeholder image with rounded corners in a figure.">
        <figcaption class="figure-caption text-right"> A caption for the above image. </figcaption>
    </figure>

## 工具
### 边框
     class="border"  将 border 类添加到一个元素中，以便移除所有 border 或部分 border。
     或者增加边框：  <span class="border"></span>  四边都添加
                    <span class="border-top"></span>
                    <span class="border-right"></span>
                    <span class="border-bottom"></span>
                    <span class="border-left"></span>
    减少边框：   <span class="border-0"></span>
                <span class="border-top-0"></span>
                <span class="border-right-0"></span>
                <span class="border-bottom-0"></span>
                <span class="border-left-0"></span
    边框颜色：  <span class="border border-primary"></span>                border-
                <span class="border border-secondary"></span>              类似的还有 text-  文本颜色
                <span class="border border-success"></span>                         bg-  背景颜色
                
    边框圆角：class="rounded"
            class="rounded-top"
            class="rounded-right"
            class="rounded-bottom"
            class="rounded-left"
            class="rounded-circle"
            class="rounded-0"

### 颜色
        text-   文字颜色    bg-   背景颜色

### 显示
    	把元素显示成各种类型，3.x的版本只有三种，block,inline,inline-block 
		                    4.x：		class="d-inline>  class="d-block  class="d-inline-block  class="d-flex  class="d-table
        隐藏：在各种尺寸下显示一个元素。只在某一个尺寸下显示，在其它的尺寸下都要隐藏
					    1、隐藏是分为两个部分
						1、比它大的尺寸隐藏
						2、比它小的尺寸隐藏
                                <div class="col bg-primary text-white d-xl-block d-none">只在超大屏幕下显示</div>
                                <div class="col bg-dark text-white d-none d-lg-block d-xl-none">只在大屏幕下显示</div>
                                <div class="col bg-success text-white d-none d-md-block d-lg-none">只在中等屏幕下显示</div>
                                <div class="col bg-warning text-white d-none d-sm-block d-md-none">只在小屏幕下显示</div>
                                <div class="col bg-info text-white d-sm-none">只在超小屏幕下显示</div>
                                <!-- 3.x的版本显示的类名为.visiable-*-block -->
                                <!-- 3.x的版本隐藏的类名为.hidden-* -->
        打印的时候显示： .d-print-none
                        .d-print-inline
                        .d-print-inline-block
                        .d-print-block
                        .d-print-table
                        .d-print-table-row
                        .d-print-table-cell
                        .d-print-flex
                        .d-print-inline-flex

                        <!-- 3.x的版本打印的类名为.visiable-print-block -->
###  嵌入   通过创建可在任何设备上缩放的固有比率，根据父级的宽度嵌入响应式视频或幻灯片.

    将这些规则直接应用到 <iframe>, <embed>, <video>, and <object> 元素；当需要这些样式对应属性时可加入 .embed-responsive-item。

    在 <iframe> 的父元素使用 .embed-responsive 以加入响应式设计。请注意，<iframe> 中的 .embed-responsive-item 并非必须，但我们建议采用它。

    可以使用修饰符类自定义宽高比。

        <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" src="" allowfullscreen></iframe>
        </div>

### flex
    .d-flex 和 .d-inline-flex   （存在响应式  比如.d-sm-flex  .d-sm-inline-flex）

    子元素排列方向（存在响应式）： .flex-row 来设定水平的方向(浏览器预设值)，或者使用 .flex-row-reverse 来作水平方向的反转。
                                    .flex-column 设置垂直方向，或使用 .flex-column-reverse 作垂直方向的反转。
    子元素的对齐方式
				1、主轴上的对齐 - 水平对齐   .justify-content-start 主轴上的对齐-左对齐  .justify-content-end 主轴上的对齐-右对齐 
                                            .justify-content-center 主轴上的对齐-居中对齐 .justify-content-between 主轴上的对齐-两端对齐
                                            .justify-content-around 主轴上的对齐-分散居中对齐  
                                    可响应式：比如：.justify-content-{breakpoint}-between
                                        

				2、交叉轴（纵轴）上的对齐 - 垂直对齐
                                            .align-items-start  交叉轴上的对齐-顶对齐  .align-items-end 交叉轴上的对齐-底对齐
                                            .align-items-center 交叉轴上的对齐-中间对齐 .align-items-baseline 交叉轴上的对齐-基线对齐
                                            .align-items-stretch 交叉轴上的对齐-如果子元素没有设置高或者设置成了auto，子元素将占满整个容器的高度
                                    可响应式：比如：.align-items-{breakpoint}-start
    元素自身对齐方式：
                .align-self-start 元素被拉伸以适应容器。
                .align-self-end 元素位于容器的结尾。
                .align-self-center 元素位于容器的中心。
                .align-self-baseline 元素位于容器的基线上。
                .align-self-stretch 元素被拉伸以适应容器。

                响应式；align-self-xl-start

    填满
            在相邻元素上使用 .flex-fill 来强制它们在相同的宽度上分配所有可用的水平空间。对于等宽导览特别有用

            响应式：.flex-fill  .flex-sm-fill  .flex-md-fill  .flex-lg-fill  .flex-xl-fill

    伸缩值
				1、.flex-grow-*		扩展比例，数字为0表示不扩展，数字为1表示扩展。只有这两个数字
				2、.flex-shrink-*	收缩比例，数字为0表示不收缩，数字为1表示收缩。只有这两个数字

                响应式：.flex-sm-{grow|shrink}-1   .flex-md-{grow|shrink}-0

    自动的边距
                 向右推.mr-auto     向左推 .ml-auto   向左或向右时旁边的也会被推动
                 向上推.mt-auto            向下推 .mb-auto  同理

    wrap
                .flex-nowrap   溢出部分不发生换行
                .flex-wrap   flex子项溢出的部分会被放置到新行，子项内部会发生断行
                .flex-wrap-reverse  反转 wrap 排列

                响应式：.flex-md-wrap  .flex-md-wrap-reverse
    order排序
                例如 .order-*   数字范围1-12   需对每一个子项添上   数字越小排在最左边
                响应式：.order-sm-8
    多行对齐
                多行对齐，对于单行是没有效果的
				align-content-start		顶对齐
				align-content-end		底对齐
				align-content-center	中间对齐
				align-content-between	上下两端对齐
				align-content-around	上下分散对齐
				align-content-stretch	没有给高度或者高度为auto，那高度会取父级的高度

                响应式：.align-content-lg-around
### 浮动
    	<!-- 3.x的版本里的浮动是.pull-left/.pull-right -->
				<div class="float-left">左浮动</div>
				<div class="float-right">右浮动</div>
				<div class="float-left float-none">不浮动</div>

                <!-- 响应式的浮动，float-{breakpoint}-left -->
                <!-- 清除浮动,clearfix -->

### 关闭图标
        使用一般的关闭图标类，关闭 modals 元件和 alerts 元件之类的内容。.
        请务必为屏幕阅读器添加文本,我們可以使用 aria-label 标签属性。

            ×
            <button type="button" class="close" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
            </button>
### 图像替换 
        class="text-hide"  可以使得图标替换内字体 使用 .text-hide 类来保持标题标签的可访问性和SEO优势，但是想要利用 background-image 而不是文字


		<div class="row mt-5">
			<h1 class="text-hide" style="background-image: url('http://getbootstrap.com/docs/4.1/assets/brand/bootstrap-solid.svg'); width: 50px; height: 50px;">Bootstrap</h1>
		</div>
### 内容溢出
        <div style="width: 200px;height: 100px;" class="border overflow-auto">
            这是在具有设置宽度和高度尺寸的元素上使用 .overflow-auto 的示例。 此内容将垂直滚动。这是在具有设置宽度和高度尺寸的元素上使用 .overflow-auto 的示例。 此内容将垂直滚动。这是在具有设置宽度和高度尺寸的元素上使用 .overflow-auto 的示例。
        </div>
			<div style="width: 200px;height: 100px;" class="border overflow-hidden">
            这是在具有设置宽度和高度尺寸的元素上使用 .overflow-hidden 的示例。这是在具有设置宽度和高度尺寸的元素上使用 .overflow-hidden 的示例。这是在具有设置宽度和高度尺寸的元素上使用 .overflow-hidden 的示例。
        </div>
###  定位
		<div class="row mt-5 pos">
			<div class="position-static">默认值，没有定位</div>
			<div class="position-relative">相对定位</div>
			<div class="position-absolute">绝对定位</div>
			<div class="position-fixed">固定定位</div>
			<div class="position-sticky">粘性定位</div>

			<!-- <div class="fixed-top">固定在顶部</div>
			<div class="fixed-bottom">固定在底部</div> -->
			<!-- <div class="sticky-top">粘性置顶，放在这里是没有效果的，需要放在body下的第一层级</div> -->
		</div>


### 阴影
       
		<div class="row mt-5 justify-content-around">
			<div class="bg-light rounded p-3 shadow-none">没有阴影</div>
			<div class="bg-white rounded p-3 shadow-sm">小阴影</div>
			<div class="bg-white rounded p-3 shadow">正常的阴影</div>
			<div class="bg-white rounded p-3 shadow-lg">大的阴影</div>
		</div>

### 尺寸
        宽度  .w-25  宽度25%  自己设置   .w-auto 宽度填满
        高度同理  .h-25%  高度25%        .h-auto  高度填满

        你也可以使用 max-width: 100%; and max-height: 100%; 这些工具。 宽度最大值 高度最大值
### 间距
        很多固定的字符代表：比如
            m是margin   p是padding  t是top b是bottom l是left  r是right x是left和right  y是top和bottom 没写就是全部
            0是值为0 1是25% 2是50% 3是100% 4是1.5倍 5是3倍
            比如
                <div class="bg-danger text-white p-3 m-3"></div>
            	<div class="bg-danger text-white py-3 my-3"></div>

            间距的响应式，{property}{sides}-{breakpoint}-{size} 
            	<!-- 3.x的版本居中是用.center-block -->
### 文本
        class="text-justify" 齐行改变单词间的间隔：
        .text-left .text-right .text-center  左对齐 右对齐  居中对齐

        .text-nowrap 可以让文本不换行。
        对于更长的内容，你可以增加一个 .text-truncate ，可以截掉多余内容 。行内元素需要额外使用 display: inline-block or display: block 来确保正常的显示效果。

        将文字转化为大写
        .text-lowercase 不改变  .text-uppercase 全部大写 .text-capitalize每个单词首字母大写

         字体粗细和斜体
			<p class="font-weight-bold">加粗字体</p>
			<p class="font-weight-normal">正常字体</p>
			<p class="font-weight-light">更细的字体</p>
			<p class="font-italic">倾斜字体</p>

        将文字等宽
			<p class="text-monospace">This is in monospace</p>
		
### 垂直对齐
        请注意，垂直对齐仅影响 inline、inline-block、inline-table、和 table 元素。
	
			<span class="align-baseline">baseline</span>  	默认。元素放置在父元素的基线上。
			<span class="align-top">top</span>   把元素的顶端与行中最高元素的顶端对齐
			<span class="align-middle">middle</span>  把此元素放置在父元素的中部。
			<span class="align-bottom">bottom</span>   把元素的顶端与行中最低的元素的顶端对齐。
			<span class="align-text-top">text-top</span> 	把元素的顶端与行中最高元素的顶端对齐
			<span class="align-text-bottom">text-bottom</span>  把元素的底端与父元素字体的底端对齐。
		
### 可见性
        .visible可以看见 .invisible看不见，占据空间  .d-none看不见，不占据空间
	
## 组件

## 第三方库
### 图标 iconfont
### 按钮样式美化  BUTTONS

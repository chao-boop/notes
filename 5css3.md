# css3介绍
关于预处理器和后处理器   都是插件  比如 后处理器（autoprefixer插件） 预处理器（less，sass插件）  后处理器的插件都是基于postCss来拓展的  
预处理器基于别人的语法写css写好之后在将其编译为css的文件来执行 这样可以简化代码
后处理器，写好css之后将写好的css编译为解决了相关兼容性问题的完整css   

## 选择器  都以例子的方式呈现

- div + p {}    div后面的一个兄弟元素p   是兄弟元素且为p才可以 &&的关系
- div ~ p {}    div后面的所有的兄弟元素p  是兄弟元素且都为p元素
- div[class]    有class属性的div     当然还有很多方式 比如 [class~='a'] [class|='a'] [class^='a'] [class*='a']


- 伪元素选择器 ::selection  被鼠标框选的文字

- :not（[class="a"]） 元素里除了class为a的  也可以加其他的条件 都可以
- :root 根标签
- :target 选择器可用于选取当前活动的目标元素。  URL 带有后面跟有锚名称 #，指向文档内某个具体的元素。这个被链接的元素就是目标元素(target element)。 
- :first-child  :last-child :only-child :nth-child(n)  &&关系
- :first-of-type  :last-of-type :noly-of-type :nth-of-type(n) :nth-of-last-type(n)  
- :empty 内容为空的元素 里面没有节点
- :checked 选择被选中时的元素 表单
- :enabled 选中可用的表单元素
- :disabled 选中被禁用的表单元素
- :read-only 选中只读的表单元素
- :read-write  选中可写的表单元素

## border
 - 边框的多种设置方法：
    四个值：border-radius：左上，右上，右下，左下；
    两个：border-radius：左上右下，右上左下；
    三个：border-radius：左上，右上左下，右上；
    一个值：就是设置了四个角；
    - 如果要单数设置某一个角：
    border-top-left-radius：左上；
    border-top-right-radius：右上；
    border-bottom-left-radius：左下；
    border-bottom-right-radius：右下；
- 阴影 box-shadow   （基于边框的）
        分为外阴影和内阴影
        box-shadow:px,px,px,px,color,inset;    前面两个设置位置左右和上下  第三个设置模糊距离，第四个设置阴影尺寸，最后设置颜色,最后一个将外部阴影改为内部阴影（不写就是外部）

        可以多次赋值，不会覆盖原来的， 但是显示顺序是先定义的在最前面  多次赋值逗号隔开：box-shadow:px,px,px,px,color,inset，px,px,px,px,color,inset，px,px,px,px,color;

    **阴影会遮挡背景颜色 但是不会遮挡内容** 

- border-image
        border-image 属性是一个简写属性，用于设置以下属性：
        border-image-source	用在边框的图片的路径。	
        border-image-slice	图片边框向内偏移。	
        border-image-width	图片边框的宽度。	
        border-image-outset	边框图像区域超出边框的量。	
        border-image-repeat	图像边框是否应平铺(repeated)、铺满(rounded)或拉伸(stretched)。


##  background-image
    可以存放多个图片 ：background-image：url（），url（）； 
                    background-size:100px 100px,100px 100px;
                    background-repeat；no-repeat; 不重复
                    background-position；0 0,100 0;
    设置图片填充位置：   background-origin:padding-box; 有三个值：border-box（图片从边框区开始填充），padding-box（从内边距开始填充 默认值），content-box（从内容区开始填充）
    设置图片截至位置：   background-clip：padding-box; 有三个值：border-box（图片从边框区开始截止），padding-box（从内边距开始截止 默认值），content-box（从内容区开始截止）
                    origin是决定图片从哪个位置开始填充（填充从左上角开始），clip决定从哪里开始截止（将溢出的部分截断）

                    - background-clip还有一个值 text 让图片充满字体 但是只有coogle好使：而且需要配合一个固定属性：  固定写法：
                                    -webkit-background-clip：text；
                                    background-clip：text；
                                    -webkit-text-fill-color：transparent：
                                    text-fill-color：transparent：
    background-repeat的两个新值：1.round：与 repeat 关键字类似。不同在于，当背景图像不能以整数次平铺时，会根据情况缩放图像。2. space：与 repeat 关键字类似。不
                                                                                      同在于，当背景图像不能以整数次平铺时，会用空白间隙填充在图像周围。
                                可以单个赋值也可以一起赋值：background-repeat：round space；   一个横向一个纵向

    background-attachment背景图片的相对位置：  fixed：背景图像相对于视口（viewport）固定。
                                scroll：背景图像相对于元素固定，也就是说当元素内容滚动时背景图像不会跟着滚动，因为背景图像总是要跟着元素本身。但会随元素的祖先元素或窗体一起滚动。
                                local：背景图像相对于元素内容固定，也就是说当元素随元素滚动时背景图像也会跟着滚动，因为背景图像总是要跟着内容。（CSS3）
    background-size 图片大小新值：auto：背景图像的真实大小。
                                cover：将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器。
                                contain：将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包含在容器内

    渐变器（4个）：background-imge:linear-gradient(to right,#ofo 20px,#ffo) 颜色朝着右边开始渐变 20px是渐变的长度（20开始渐变，也可以是百分比） to right（也可以是其他方向）
                                                                                                    是方向也可以是角度比如 45deg   也可以写多个颜色
        background-imge：radial-gradient 从外向内开始渐变

## text
        -webkit-text-stroke：1px red 字体描边 google好用

- @font-face 从外部引入一字体  ：   @font-face{
                                                    font-family:'qe';  给引入的字体取一个名字
                                                    src：url（）；文字的地址
                                                }   
                                    div{
                                        font-family：‘qe’；  使用文字
                                    }

                                示例：使用一个全浏览器兼容的自定义字体  代码如下：

                                        @font-face {
	                                                font-family: 'diyfont';
	                                                src: url('diyfont.eot'); /* IE9+ */
	                                                src: url('diyfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
		                                            url('diyfont.woff') format('woff'), /* chrome、firefox */
		                                            url('diyfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
		                                            url('diyfont.svg#fontname') format('svg'); /* iOS 4.1- */
                                                        }
- 文本设置阴影 text-shadow  还有多种具体设置方法
        text-shadow: h-shadow v-shadow blur color;
        
        h-shadow	必需。水平阴影的位置。允许负值。	测试
        v-shadow	必需。垂直阴影的位置。允许负值。	测试
        blur	可选。模糊的距离。	测试
         color	可选。阴影的颜色。参阅 CSS 颜色值。
- 多列 column
            columns:column-width,column-count		设置或检索对象的列数和每列的宽度。复合属性  column-width设置或检索对象每列的宽度 column-count设置或检索对象的列数
            
            
            column-gap      	设置或检索对象的列与列之间的间隙
            column-rule:column-rule-width,column-rule-style,column-rule-color	设置或检索对象的列与列之间的边框。复合属性
                                                    column-rule-width设置或检索对象的列与列之间的边框厚度。
                                                    column-rule-style设置或检索对象的列与列之间的边框样式。
                                                    column-rule-color设置或检索对象的列与列之间的边框颜色。
            column-span		设置或检索对象元素是否横跨所有列。 none：不跨列 all：横跨所有列
            column-fill		设置或检索对象所有列的高度是否统一。
            column-break-before		设置或检索对象之前是否断行。
            column-break-after		设置或检索对象之后是否断行。
            column-break-inside		设置或检索对象内部是否断行。


## 新的盒模型 box  box-sizing:border-box
原来的正常的盒子：boxWidth=width+padding(2)+border(2)

ie6混杂模式的盒模型 他的width，height大小直接为盒子的width和height （原先width为内容区的大小）
boxWidth=width
可以直接给盒子定宽高 

想要触发该盒模型 在该元素上添加样式： box-sizing:border-box;

- overflow可以只设置一个方向：overflow-x 或 overflow-y  注意当一个方向设置的值不为默认时另一个方向的值将改为auto 默认值为visible

- resize  属性规定是否可由用户调整元素的尺寸。
        注释：如果希望此属性生效，需要设置元素的 overflow 属性，值可以是 auto、hidden 或 scroll。
        none    用户无法调整元素的尺寸。
        both	用户可调整元素的高度和宽度。
        horizontal	用户可调整元素的宽度。
        vertical	用户可调整元素的高度。

## 弹性盒子  使用时需定义盒子类型 display:flex;
   -设置主轴方向 设置到外层盒子，控制内部排列 - flex-flow:<' flex-direction '> || <' flex-wrap '>   复合属性。设置或检索弹性盒模型对象的子元素排列方式。 
                            -单行<' flex-direction '>：定义弹性盒子元素的排列方向。 取值：
                                                        row：主轴与行内轴方向作为默认的书写模式。即横向从左到右排列（左对齐）。
                                                        row-reverse：对齐方式与row相反。
                                                        column：主轴与块轴方向作为默认的书写模式。即纵向从上往下排列（顶对齐）。
                                                        column-reverse：对齐方式与column相反。
                            -多行<' flex-wrap '>：控制flex容器是单行或者多行。取值：
                                                        nowrap：flex容器为单行。该情况下flex子项可能会溢出容器
                                                        wrap：flex容器为多行。该情况下flex子项溢出的部分会被放置到新行，子项内部会发生断行
                                                        wrap-reverse：反转 wrap 排列。
    - 基于主轴横向的方向控制对齐方式 在外层设置 - justify-content：flex-start主轴上左对齐 | flex-end右对齐 | center居中对齐 | space-between 子元素之间均分空余| space-around子元素左右间距均分 ;设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式。

    - 交叉轴 基于主轴纵向竖直的方向控制对齐方式 在外层设置的 align-items：flex-start | flex-end | center | baseline | stretch； 定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式

    - 这个和align-items的效果一样但是要作用在多行元素上才可以 单行作用不上 align-content：flex-start | flex-end | center | space-between | space-around | stretch；当伸缩容器的侧轴还有多余空间时，本属性可以用来调准「伸缩行」在伸缩容器里的对齐方式，这与调准伸缩项目在主轴上对齐方式的 <' justify-content '> 属性类似。请注意本属性在只有一行的伸缩容器上没有效果。
    

    设置在子元素 - align-self：auto默认跟谁父元素 | flex-start 顶部排列| flex-end 底部排列| center 居中| baseline | stretch;定义flex子项单独在侧轴（纵轴）方向上的对齐方式。    如果父元素设置了align-content 则遵循父元素


    -设置在子元素的 order：<integer>;设置或检索弹性盒模型对象的子元素出現的順序。默认值为0 可以为负值

    -一般给子元素统一设置 对剩余空间的分配  flex：none | <' flex-grow '> <' flex-shrink >'? || <' flex-basis '>;复合属性。设置或检索弹性盒模型对象的子元素如何分配空间。
                             flex-grow：<number><number>：用数值来定义扩展比率。不允许负值   默认值为0
                             flex-shrink：<number><number>：用数值来定义收缩比率。不允许负值   默认值为0
                             flex-basis：<length> | <percentage> | auto | content设置或检索弹性盒伸缩基准值。如果所有子元素的基准值之和大于剩余空间，则会根据每项设置的基准值，按比率伸缩剩余空间                      
# 动画
## transform 变换动画
    transform取值：
       

                none：无转换
            2D Transform Functions：
                    matrix()：以一个含六值的(a,b,c,d,e,f)变换矩阵的形式指定一个2D变换，相当于直接应用一个[a,b,c,d,e,f]变换矩阵
                    translate()：指定对象的2D translation（2D平移）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
                        translatex()：指定对象X轴（水平方向）的平移
                        translatey()：指定对象Y轴（垂直方向）的平移
                    rotate()：指定对象的2D rotation（2D旋转），需先有 <' transform-origin '> 属性的定义
                    scale()：指定对象的2D scale（2D缩放）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认取第一个参数的值
                        scalex()：指定对象X轴的（水平方向）缩放
                        scaley()：指定对象Y轴的（垂直方向）缩放
                    skew()：指定对象skew transformation（斜切扭曲）。第一个参数对应X轴，第二个参数对应Y轴。如果第二个参数未提供，则默认值为0
                        skewx()：指定对象X轴的（水平方向）扭曲
                        skewy()：指定对象Y轴的（垂直方向）扭曲
            3D Transform Functions：
                    matrix3d()：以一个4x4矩阵的形式指定一个3D变换
                    translate3d()：指定对象的3D位移。第1个参数对应X轴，第2个参数对应Y轴，第3个参数对应Z轴，参数不允许省略
                    translatez()：指定对象Z轴的平移
                    rotate3d()：指定对象的3D旋转角度，其中前3个参数分别表示旋转的方向x,y,z，第4个参数表示旋转的角度，参数不允许省略
                    rotatex()：指定对象在x轴上的旋转角度
                    rotatey()：指定对象在y轴上的旋转角度
                    rotatez()：指定对象在z轴上的旋转角度
                    scale3d()：指定对象的3D缩放。第1个参数对应X轴，第2个参数对应Y轴，第3个参数对应Z轴，参数不允许省略
                    scalez()：指定对象的z轴缩放
                    perspective()：指定透视距离

    transform-origin：设置或检索对象以某个原点进行转换。该属性提供2个参数值。如果提供两个，第一个用于横坐标，第二个用于纵坐标。如果只提供一个，该值将用于横坐标；纵坐标将默认为50%。

    transform-style：flat | preserve-3d 指定某元素的子元素是（看起来）位于三维空间内，还是在该元素所在的平面内被扁平化。默认flat

    perspective：none | <length> 透视距离

    perspective-origin：指定透视点的位置。 该属性提供2个参数值。如果提供两个，第一个用于横坐标，第二个用于纵坐标。如果只提供一个，该值将用于横坐标；纵坐标将默认为center。
                    <percentage>：用百分比指定透视点坐标值，相对于元素宽度。可以为负值。
                    <length>：用长度值指定透视点坐标值。可以为负值。
                    left：指定透视点的横坐标为left
                    center①：指定透视点的横坐标为center
                    right：指定透视点的横坐标为right
                    top：指定透视点的纵坐标为top
                    center②：指定透视点的纵坐标为center
                    bottom：指定透视点的纵坐标为bottom
    
    backface-visibility：visible | hidden   指定元素背面面向用户时是否可见。



## transition 过渡动画
 有四个属性：transition-property 设置要变化的样式  也可以all所有样式
            transition-duration 设置变化所需时间s
            transition-timing-function 设置变化的运动状态 
            transition-delay 变化间隔时间
            可以一次性按顺序设置  后面两个可选  也可以添多个 逗号隔开
        有些属性是不能设置过渡的



- cubic-bezier 贝塞尔曲线
    transition-timing-function的固定取值都是基于贝塞尔曲线的  我们可以用贝塞尔曲线来自己设置运动的速度变化
        transition-timing-function:cubic-bezier(x1,y1,x2,y2);  控制台有工具类似于颜色选取器
        负值可以弹性运动
## animation 连续动画  变换元素状态  过渡元素transition只能实现一次变换 然而animation可以实现多状态改变的连续动画

    animation：
                <' animation-name '>：检索或设置对象所应用的动画名称  
                                 用@keyframes来定义一个动画的变化过程
                                            @-moz-keyframes animations{                     //百分之0也可以用from表示  百分之百用to表示
                                                        0%{-moz-transform:scale(0);opacity:0;}
                                                        40%{-moz-transform:scale(1);opacity:1;}
                                                        100%{opacity:1;}
                                                        }



                <' animation-duration '>：检索或设置对象动画的持续时间   
                <' animation-timing-function '>：检索或设置对象动画的过渡类型   塞北尔曲线 cubic-bezier(x1,y1,x2,y2)
                                                        step-start：等同于 steps(1, start)
                                                                保留下一帧状态 直到当前动画结束 
                                                        step-end：等同于 steps(1, end)
                                                                保留当前帧状态 直到这段动画结束

                                                                前面参数可以更改 使得动画改变的分为该数值步骤 


                <' animation-delay '>：检索或设置对象动画延迟的时间 

                <' animation-iteration-count '>：检索或设置对象动画的循环次数  infinite：无限循环  <number>：指定对象动画的具体循环次数

                <' animation-direction '>：检索或设置对象动画在循环中是否反向运动   
                                                                        normal：正常方向
                                                                        reverse：反方向运行
                                                                        alternate：动画先正常运行再反方向运行，并持续交替运行
                                                                        alternate-reverse：动画先反运行再正方向运行，并持续交替运行
                <' animation-fill-mode '>：检索或设置对象动画时间之外的状态  running：运动  paused：暂停

                <' animation-play-state '>：检索或设置对象动画的状态。w3c正考虑是否将该属性移除，因为动画的状态可以通过其它的方式实现，比如重设样式
                                                none：默认值。不设置对象动画之外的状态
                                                forwards：设置对象状态为动画结束时的状态
                                                backwards：设置对象状态为动画开始时的状态
                                                both：设置对象状态为动画结束或开始的状态
 


# user-select:value;
控制用户能否选中文本。



 # 根据CSS3规范，视口单位主要包括以下4个：

      1.vw：1vw等于视口宽度的1%。

      2.vh：1vh等于视口高度的1%。

      3.vmin：选取vw和vh中最小的那个。

      4.vmax：选取vw和vh中最大的那个。
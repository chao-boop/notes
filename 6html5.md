# h5新增属性
## input表单元素的新type值
type ="date" 日期   "time" 时间 "week" 周  "unmber" 但是兼容性不好  emil 邮箱  格式不规范会提示错误
color 颜色选择 还有： rang ，search，url   很多浏览器不支持 所以很少用

## contenteditable属性  添加后可以在页面更改内容 默认Flase  可以应用到表格上  没有兼容性问题
会被子元素继承 但是可以被覆盖

##  draggable 属性规定元素是否可拖动
默认flase 
chrome和safari下可以正常使用 firefox下不好使
有些元素的draggable默认为true 比如a标签 imge标签 。所以提示：链接和图像默认是可拖动的。
拖拽组成：被拖拽的物体 目标区域
被拖拽物体：
    拖拽周期：拖拽开始 拖拽进行中 拖拽结束
目标区域：


被拖拽元素的事件
    dragstart拖拽开始事件 当鼠标点击且移动后触发  按下瞬间是不会触发的
    drag拖拽进行中事件 移动中一直触发
    deagend拖拽结束事件 鼠标抬起后触发
目标区域的事件：
    dragenter 当拖拽元素时进入目标区域的范围内时触发 注意是当鼠标进入时触发 而不是当被拖拽元素触碰
    dragover 当鼠标拖拽着元素进入目标区域后移动就会被不停的触发
    dragleave 当鼠标拖拽离开目标区域后触发
    drop 在目标区域松开鼠标时触发  但是要在dragover内取消事件的默认行为e.preventDeault(); 因为所有的标签元素当拖拽周期结束时默认事件是回到原处
# 标签
## 新的语义化标签  语义化标签不过是为了更好的区分结构 本质都是一样的
<header></header>头部
<footer></footer>尾部
<article></article>文章
<section></section>段落
<aside></aside>侧边栏


## canvas画布
获取画布元素对象 然后再对象点getContext（“2d”）方法调用获取画笔 传固定参数
比如：
var can = document.getElementById('can');
var ctx = canvas.getContext('2d');

ctx.linenWidth = 10;//线的粗细
ctx.moveTo(100,100);//画一条线 从哪到哪
ctx.lineTo(200,100);//接着上面画
ctx.stroke();//显示

ctx.beginPath();//重新绘制一个起点
ctx.moveTo(200,100);
ctx.closePath() 方法关闭一条打开的子路径。
- 画一个矩形 
ctx.rect(100,100,200,100);  1前面两个是起始位置 后面是宽高
ctx.stroke();展示
ctx.fill();

- 画圆圈

ctx.arc(x,y,r,sAngle,eAngle,counterclockwise);

x	圆的中心的 x 坐标。
y	圆的中心的 y 坐标。
r	圆的半径。
sAngle	起始角，以弧度计。（弧的圆形的三点钟位置是 0 度）。
eAngle	结束角，以弧度计。
counterclockwise	可选。规定应该逆时针还是顺时针绘图。False = 顺时针，true = 逆时

- arcTo() 方法使用使用切点和一个半径，来为当前子路径添加一条圆弧。
arcTo(x1, y1, x2, y2, radius)
x1, y1	点 P1 的坐标。
x2, y2	点 P2 的坐标。
radius	定义圆弧的圆的半径。

- 创建贝塞尔曲线
quadraticCurveTo()	创建二次贝塞尔曲线。
    	context.quadraticCurveTo(cpx,cpy,x,y);
            cpx	贝塞尔控制点的 x 坐标。
            cpy	贝塞尔控制点的 y 坐标。
            x	结束点的 x 坐标。
            y	结束点的 y 坐标


bezierCurveTo()	创建三次贝塞尔曲线。
        context.bezierCurveTo(cp1x,cp1y,cp2x,cp2y,x,y);
            cp1x	第一个贝塞尔控制点的 x 坐标。
            cp1y	第一个贝塞尔控制点的 y 坐标。
            cp2x	第二个贝塞尔控制点的 x 坐标。
            cp2y	第二个贝塞尔控制点的 y 坐标。
            x	结束点的 x 坐标。
            y	结束点的 y 坐标。

### canvas的属性

            fillStyle	设置或返回用于填充绘画的颜色、渐变或模式。
            strokeStyle	设置或返回用于笔触的颜色、渐变或模式。
            shadowColor	设置或返回用于阴影的颜色。
            shadowBlur	设置或返回用于阴影的模糊级别。
            shadowOffsetX	设置或返回阴影与形状的水平距离。
            shadowOffsetY	设置或返回阴影与形状的垂直距离。
- 为了防止新的图形不被之前设置的所影响
save()	保存当前环境的状态。
restore()	返回之前保存过的路径状态和属性。

- fillStyle 属性设置或返回用于填充绘画的颜色、渐变或模式。	context.fillStyle=color|gradient|pattern;


            值	描述
            color	指示绘图填充色的 CSS 颜色值。默认值是 #000000。
            gradient	用于填充绘图的渐变对象（线性 或 放射性）。
            pattern	用于填充绘图的 pattern 对象。

- createRadialGradient() 方法创建放射状/圆形渐变对象。 	context.createRadialGradient(x0,y0,r0,x1,y1,r1);

            渐变可用于填充矩形、圆形、线条、文本等等。

            提示：请使用该对象作为strokeStyle或 fillStyle 属性的值。

            提示：请使用 addColorStop() 方法规定不同的颜色，以及在 gradient 对象中的何处定位颜色。

        x0	渐变的开始圆的 x 坐标
        y0	渐变的开始圆的 y 坐标
        r0	开始圆的半径
        x1	渐变的结束圆的 x 坐标
        y1	渐变的结束圆的 y 坐标
        r1	结束圆的半径


- createPattern() 方法在指定的方向内重复指定的元素。

                                元素可以是图片、视频，或者其他 <canvas> 元素。

                                被重复的元素可用于绘制/填充矩形、圆形或线条等等。

            context.createPattern(image,"repeat|repeat-x|repeat-y|no-repeat");

            image	规定要使用的模式的图片、画布或视频元素。	 
            repeat	默认。该模式在水平和垂直方向重复。
            repeat-x	该模式只在水平方向重复。
            repeat-y	该模式只在垂直方向重复。
            no-repeat	该模式只显示一次（不重复）。
- 绘制文本
        fillText()	在画布上绘制"被填充的"文本  fillText() 方法在画布上绘制填色的文本。文本的默认颜色是黑色。提示：请使用 font 属性来定义字体和字号，并使用 fillStyle属性以另一种颜色/渐变来渲染文本。。
                    context.fillText(text,x,y,maxWidth);

                                    text	规定在画布上输出的文本。
                                    x	开始绘制文本的 x 坐标位置（相对于画布）。
                                    y	开始绘制文本的 y 坐标位置（相对于画布）。
                                    maxWidth	可选。允许的最大文本宽度，以像素


        strokeText()	在画布上绘制文本（无填充）  strokeText() 方法在画布上绘制文本（无填充色）。文本的默认颜色是黑色。
                        提示：请使用 font 属性来定义字体和字号，并使用 strokeStyle属性以另一种颜色/渐变来渲染文本。。
                            context.strokeText(text,x,y,maxWidth);
                                                text	规定在画布上输出的文本。
                                                x	开始绘制文本的 x 坐标位置（相对于画布）。
                                                y	开始绘制文本的 y 坐标位置（相对于画布）。
                                                maxWidth	可选。允许的最大文本宽度，以像素计。
        measureText()	返回包含指定文本宽度的对象。	context.measureText(text).width;  text	要测量的文本。



- lineCap 属性设置或返回线条末端线帽的样式。  注意："round" 和 "square" 值会使线条略微变长。  	context.lineCap="butt|round|square";
                                                                            butt	默认。向线条的每个末端添加平直的边缘。
                                                                            round	向线条的每个末端添加圆形线帽。
                                                                            square	向线条的每个末端添加正方形线帽。

## svg画图  
svg画矢量图 适合大面积的贴图
canvas适合小面积的绘图 适合动画
    <!-- <style>
        line{
            stroke:black; 设置颜色
            stroke-width:3px; 宽度
        }
    </style>
    <svg>
        <line x1="" y1="" x2="" y2=""></line> 在svg标签内画一条线 给起始位置和结束位置
        <rect height="" width="" x="" y="" rx=“” ry=“”></rect> 画一个矩形 给宽高和起始位置  rx为x方向的圆角 另一个是y方向的圆角
    </svg> -->

- <rect> 标签可用来创建矩形，以及矩形的变种。
                rect 元素的 width 和 height 属性可定义矩形的高度和宽度
                style 属性用来定义 CSS 属性
                CSS 的 fill 属性定义矩形的填充颜色（rgb 值、颜色名或者十六进制值）
                CSS 的 stroke-width 属性定义矩形边框的宽度
                CSS 的 stroke 属性定义矩形边框的颜色
- <circle> 标签可用来创建一个圆。<circle cx="100" cy="50" r="40" stroke="black"stroke-width="2" fill="red"/>
            cx 和 cy 属性定义圆点的 x 和 y 坐标。如果省略 cx 和 cy，圆的中心会被设置为 (0, 0)  r 属性定义圆的半径。
- <ellipse> 标签可用来创建椭圆。椭圆与圆很相似。不同之处在于椭圆有不同的 x 和 y 半径，而圆的 x 和 y 半径是相同的
            <ellipse cx="300" cy="150" rx="200" ry="80"style="fill:rgb(200,100,50);stroke:rgb(0,0,100);stroke-width:2"/>
                    cx 属性定义圆点的 x 坐标
                    cy 属性定义圆点的 y 坐标
                    rx 属性定义水平半径
                    ry 属性定义垂直半径

- <line> 标签用来创建线条。  <line x1="0" y1="0" x2="300" y2="300" style="stroke:rgb(99,99,99);stroke-width:2"/>
                    x1 属性在 x 轴定义线条的开始
                    y1 属性在 y 轴定义线条的开始
                    x2 属性在 x 轴定义线条的结束
                    y2 属性在 y 轴定义线条的结束

- <polygon> 标签用来创建含有不少于三个边的图形  <polygon points="220,100 300,210 170,250"style="fill:#cccccc;stroke:#000000;stroke-width:1"/>
                        points 属性定义多边形每个角的 x 和 y 坐标

- <polyline> 标签用来创建仅包含直线的形状 <polyline points="0,0 0,20 20,20 20,40 40,40 40,60"style="fill:white;stroke:red;stroke-width:2"/>
        和上面一样 区别就是会首位相连
- <text> 添加文本   <text x="" y="">123</text>  给一个位置

- troke-opacitys 设置填充透明度  fill-opacity 设置边框的透明度


- <path> 标签用来定义路径。。大写表示绝对定位，小写表示相对定位。
<path d="M250 150 L150 350 L350 350 Z" /> ，它开始于位置 250 150，到达位置 150 350，然后从那里开始到 350 350，最后在 250 150 关闭路径。

由于绘制路径的复杂性，因此强烈建议您使用 SVG 编辑器来创建复杂的图形。

- <linearGradient> 可用来定义 SVG 的线性渐变。
    <linearGradient> 标签必须嵌套在 <defs> 的内部。<defs> 标签是 definitions 的缩写，它可对诸如渐变之类的特殊元素进行定义。

    <defs>
        <linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" style="stop-color:rgb(255,255,0);
            stop-opacity:1"/>
            <stop offset="100%" style="stop-color:rgb(255,0,0);
            stop-opacity:1"/>
        </linearGradient>
    </defs>

    <linearGradient> 标签的 id 属性可为渐变定义一个唯一的名称
    fill:url(#orange_red) 属性把 ellipse 元素链接到此渐变
    <linearGradient> 标签的 x1、x2、y1、y2 属性可定义渐变的开始和结束位置
    渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个 <stop> 标签来规定。offset 属性用来定义渐变的开始和结束位置。


    线性渐变可被定义为水平、垂直或角形的渐变：
            当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
            当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
            当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变

- <radialGradient> 用来定义放射性渐变。
        <radialGradient> 标签必须嵌套在 <defs> 中。<defs> 标签是 definitions 的缩写，它允许对诸如渐变等特殊元素进行定义。

- 高斯模糊（Gaussian Blur）<filter> 标签必须嵌套在 <defs> 标签内。<defs> 标签是 definitions 的缩写，它允许对诸如滤镜等特殊元素进行定义。

- viewbox 属性  比例尺  <svg viewbox="0,0,250,150"></svg>  

## video 视频标签
自己封装一个控件：
对象. play(): 视频的播放
 对象.pause(): 视频的暂停
对象.paused: 检查video是否在暂停
 var a = 对象.duration; 获取总时间
 var b = 对象.nowTime; 获取当前时间  



属性
play: 视频的播放
pause: 视频的暂停
paused: 检查video是否在暂停
volume: 获取或设置音量
duration: 获取视频总时间
currentTime: 获取当前播放时间
playbackRate属性: 视频播放速度

事件
canPlayType: 检查是否支持HTML5 video元素并且执行所有其他代码, 如果不支持视频, 返回false并显示一条消息
canplay: 通知何时视频加载内容已足够用于开始播放
loadedmetadata: 获取视频的长度, 才有duration属性
timeupdate: 获取视频中的当前位置, 当currentTime属性发生更改时, 引发ontimeupdate事件,在事件处理程序中，从视频对象中检索 currentTime的值并进行显示。currentTime 属性是浮点型变量，该变量可以从 12 位中获取小数位置。但是，出于性能方面的考虑，在 Windows Internet Explorer中一秒内仅引发该事件四次。若要在示例中显示，则需要使用 "toFixed()" 方法将 currentTime 取舍为一位。运行视频时，会更新和显示当前时间。
playing: 点击视频播放
pause: 点击视频暂停
 volumechange: 视频静音设置



 * @ src: 指定所要嵌入视频、文档的URL。
* @ poster: 视频预览图像
* @ autoplay: 视频自动播放
* @ loop: 循环播放
* @ muted: 是否静音
* @ controls: 视频控件
* @ preload: 用于指定是否提前下载，怎样提前下载视频数据，给用户代理相应的提示。autoplay：preload属性将无效
* @ 1. auto：尽可能提前下载视频
* @ 2.metadata：只下载视频的meta信息部分。Meta信息中收集了关于视频的长度、视频的起始祯的图像、视频的长度等信息


# html5进阶篇
## 获取地理位置
通过gps 台式机几乎没有gps，笔记本绝大多数都没有gps，智能手机几乎都有
通过网络 来粗略的估计地理位置
    window.navigator.geolocation.getCurrentPosition(function(position){})
    以上是固定格式 获取位置信息 实现回调函数 传入固定参数

    https协议 file协议可以获取 http写下不能获取
    经度最大值180，纬度最大值90
## 四行写服务器
## deviceorientation 重力感应方向控制
## 手机访问电脑
## devicemotion   感应手机速度变化
## requestAnimationFrame  一秒执行60次 优化动画的 因为屏幕一秒闪动60次 多于的帧会被丢失
## localStorage 浏览器中存储 key/value 对的数据。 cookie存4kb' 这个存大概5兆  可以永久存储也可以临时存储
## history
## worker  可以实现真实的异步线程 

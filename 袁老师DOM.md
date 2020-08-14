## web api概述

标准库：ECMAScript中的对象和函数

 叫web api：浏览器宿主环境中的对象和函数

 1. 知识繁杂
 2. 成体系的知识
 3. 程序思维：知识+程序思维 =应用
 4. 兼容性：了解 不记忆 有框架

## DOM是什么
DOM的核心理念，是将一个HTML或xml文档，用对象模型表示，每个对象称之为DOM对象

dom对象又称之为节点Node

节点的类型

-DocumentType 文档类型节点

-Document 文档节点 表示整个文档   以前获取节点 就直接document。XXX就可以获取到，
    现在新的获取元素节点的方式是通过方法获取：
        document.getElementById：通过id获取对应id的元素 多个id只获取第一个
        document.getElementsByTagname：通过元素名称获取元素
        document.getElementsByClassName:通过元素的类样式获取元素（IE9以下无效）
        document.getElementsByName：通过元素的name属性值获取元素
        document.querySelector:通过元素的css选择器获取元素，得到匹配的第一个，IE8以下无效
        document.querySelecttorAll：通过css选择器获取元素，得到所有匹配的结果 IE8以下无效
        document.documentElement 获取根元素HTML


        注意：用getElementById得到元素的执行效率最高，
                querySelecttorAll不会实时跟新（就是当页面内的元素标签改变了 它还是保存的原来的 不会跟着变 ）
                其他的那些返回对象集合的方法都是实时跟新的（他们返回的集合也是实时集合）
-Comment 注释节点
-Element 元素节点
-Text 文本节点
-Attribute 属性节点
-DocumentFragment 文档片段节点


## 根据节点关系获取节点 （这个就不单针对于元素节点了 也同时包含了其他节点 比如文本节点 注释节点）
-parentNode 获取父节点，父元素
-nextSibling 获取下一个兄弟节点
-childNodes 获取所有的子节点 （也是实时集合）
-firstChild 获取第一个子节点
-lastChild 获取最后一个子节点


获取元素节点（不会管之间的文本节点 注释节点之类）
 -parentElement 获取父元素
 -previousElementSibling 获取上一个兄弟元素
 -nextElementSibling 获取下一个兄弟元素
 -children 获取子元素
 -firstElementChild 获取第一个子元素
 -lastElementChild 获取最后一个子元素

 获取节点信息
 -nodeName 获取节点名称
 -nameValue 获取节点的值
 -nodeType 节点类型 是一个数字

## dom树：文档中不同的节点形成的树形结构


## dom核心 拿到元素对象后进行操作

## 控制内属性值  注意小驼峰命名法
正常的HTML属性：对象.属性名：值
细节：正常的属性即使没有赋值，也有默认值
      布尔属性在dom对象中，得到的是boolean
      某些表单元素可以获取到某些不存在的属性
      某些属性于标识符冲突，需要更换属性名，在前面加html


也可以通过方法来 但是一般不建议使用 规则比较杂乱：查看：getAttribute，赋值:setAttribute（"属性名"，"值"） 也可以加非特性的属性 等等

## 自定义属性
HTML5建议自定义属性使用 data- 作为前缀
如果遵循了HTML5的自定义属性规范，可以使用 dom对象.dataset.属性名 来控制属性

删除自定义属性： removeAttribute("属性名")；  
                delect dom.dataset.属性名

## 获取和设置元素的内容
- innerHTML 获取和设置元素的内部HTML文本  常用
- innerText 获取和设置元素内部的纯文本 （仅得到元素内部的文本 页面所见的 上面是包括了内子元素之类的）
- textContent 获取和设置元素内部的纯文本（得到的是包含了空白之类的文本，看不见的 比如隐藏的元素，样式）


## 元素结构重构（父元素内的子元素）

- 父元素.appendChild(元素) 在某个元素末尾加入一个子元素    append 可以加入在末尾多个子元素 但是不推荐使用 还没成为正式标准
-父元素.insertBefore(待插入的元素，哪个元素之前) 和上面一样 但是可以选择插入哪个子元素之前
-父元素.replaceChild（替换的元素，被替换的元素） 替换元素

注意：更改元素结构效率降低 可以打包一次性更改

## 创建和删除元素
1. 创建元素 
-document.createElement("元素名") 创建一个元素对象
-document.createTextNode（"内容"）创建文本节点

克隆元素
-对象.cloneNode(是否深度克隆) 参数true为深度克隆会把内部的子元素之类的全部克隆  若为false则只克隆对象元素的属性


2. 删除元素
-removeChild 父元素调用，传一个子元素对象 把传入的子元素删除 但是只是让他在页面消失，其对象仍然存在 如果需要也已将其调出

-remove 把自己删除   删除调用元素对象



## dom元素的样式
## 控制dom元素的类样式
 -clssName 获取元素的类名
 -classList dom4的新属性，是用于控制元素类名的对象 IE10以下不可用
    -add 用于添加一个class类名
    -remove 用于移除一个class类名
    -contain 用于判断一个一个类名是否存在
    -toggle 用于添加/移除一个类名（会先判断 有就移除 没有就添加 第二个参数可以使其只添加不移除 false只移除不添加）IE不可用

## 获取样式 
-dom.style 得到 行内样式 对象  也就是内联样式
-window.getComputedStyle（dom元素） 得到某个元素最终计算的样式 （值也一定是计算过后的的） 可以有第二个参数 用于得到某个元素的某个伪元素样式
## 设置样式
dom.style.样式名 = 值
设置的是行内样式

也就是说我们修改样式只能该内联样式，css文件的改不了

>样式与属性区别
   css 样式是css渲染引擎解析的  如 style="color:red;" 
   html标签属性是html解析的  <input name="email" autoComplete="off"/>


# DOM事件
1. 术语
-事件类型 ：点击，鼠标按下，鼠标抬起，鼠标移入，移出，键盘按下，抬起，，，
-事件处理程序：一个函数，当某件事情发生时运行
-事件注册：将一个事件处理程序，挂载到某个事件上
事件流
当某个事件发生的时候，那些元素会监听到该事件发生，这些元素发生该事件的顺序
**当一个元素发生了某个事件，那该元素的所有祖先元素都发生了该事件**
目前 规定，事件默认情况下以事件冒泡的情况下触发（最里面先开始） 
事件源：目标事件


## 事件注册
事件绑定
### dom0的方法
将事件名称前面加上on，作为dom属性名，给该属性赋值为一个函数，即为事件注册 比如：点击事件 对象.onclick = function(){};

移除：给事件属性赋值，通常赋值为null和undefined  因为后面的会覆盖前面的所以基于这个原理，再次赋值就可以

### dom2  

对象.addEventListener（“事件名称不用加on”，处理函数）； 第三参数控制是否在捕获阶段触发 默认是冒泡false 但是如果目标是事件源 第三个参数无效
与dom0的区别：dom2可以为某个元素的同一事件，添加多个处理程序 按书写顺序先后进行
              dom2允许开发者控制事件处理的阶段（冒泡和捕获阶段）
              
移除：dom对象.removeEventListener("事件名称"，处理函数)；  但是这里要注意在添加的时候就不能使用匿名函数了 因为这样就获取不了处理函数的引用了

注意
dom2在IE8及以下不可用 使用另外两个方式：attachEvent，detachEvent添加和移除事件

第三个参数可以写一些配置：对象.addEventListener（“事件名”，函数名，{once：true}）；once表示事件只执行一次  capture为true表示事件发生在捕获阶段，当然也可以直接写个true  配置可以多个 逗号隔开



## 事件对象
    比如：鼠标，键盘

### 获取
    通过事件处理函数的参数获取
    旧版本的IE浏览器通过window.event获取

对象.onclick = function(e){ //传对象参数进去 event 简写e
    e = e || window.event; //判断一下有没有 旧版本IE浏览器没有
    console.log(e);
                            }


### 事件对象  通用成员  事件属性

####   target & srcElement  事件目标（事件源） （后面的srcElement是兼容性写法，旧版本不存在target）

event.target.nodeName 　　//获取事件触发元素标签名（li，p，div，img，button…）

event.target.id　　　　　　//获取事件触发元素id

event.target.className　　//获取事件触发元素class

event.target.innerHTML　 //获取事件触发元素的内容（li）


例： 对象.onclick = function(e){
    e = e || window.event;
    var source = e.target || e.srcElement; //判断有没有，没有重新付
    console.log(e.target);
}

- 可以实现事件委托：通过给祖先元素注册事件，在程序处理程序中判断事件进行不同的处理，  就是只绑定一个父元素事件，然后点击内子元素也可以做出反应 这个e.targer就是代表内相应子元素 这样我们就可以判断不同元素然后做出不同反应  
    比如：
            var div = document.quersySelector（”div“）//获取div对象
            div.onclick = function(e){                 //绑定事件
                if(e.target.tagName == 'BUTTON'){       //判断是否点击的子元素是否为button

                }
            }
事件委托通常适用于动态生成元素的区域



#### currentTarget 当前目标：获取绑定事件的元素，等效于this （e.currentTarget === this）

currentTarget指向的是绑定事件的元素（哪个元素对象绑定的就指向谁），等效于this

#### type 得到事件的类型 返回字符串

#### preventDefault & returnValue

preventDefault方法 阻止浏览器默认行为
直接调用一下方法 e.preventDefault();就可以

也可以用dom0的方式：在事件处理程序中返回false  就是直接在处理函数最后return false；   


这两个区别就是  return false 是在事件执行完后再阻止，而preventDefault是不管在什么时候都取消默认行为

#### stopPropagation 阻止事件冒泡
e.stopPropagation();

#### eventPhase 得到事件所处的阶段
分别为：事件捕获，事件目标，事件冒泡

-e.bubbles 返回布尔类型 判断是否存在冒泡


## 鼠标事件

### 事件类型
-click 单机鼠标主键（一般是左键）或者是聚焦时按下回车键触发
-dblclick 用户双击主鼠标按键触发（频率取决于系统配置）
-mousedown 用户按下鼠标任意按键时触发
-mouseup 用户抬起鼠标任意按键时触发
-mousemove 鼠标在元素上移动触发
-mouseover 鼠标进入元素时触发
-mouseout  鼠标离开元素时触发
-mouseenter 鼠标进入元素时触发，该事件不会冒泡
-mouseleave 鼠标离开元素时触发，该事件不会冒泡

### 鼠标事件对象
所有的鼠标事件，事件处理程序中的事件对象，都为MouseEvent

-altkey 触发事件时，是否按下了键盘的alt键
-ctrlKey 触发事件时，是否按下ctrl键
-shiftKey 触发事件时，是否按下shift键
-button 触发事件时，按下的鼠标事件类型 返回的是代表事件的数字（0是左键 1是中键 2是右键）

位置：
-page ： pageX pageY 当前鼠标距离页面的横纵坐标（相对整个页面）
-client： clientX clientY  鼠标相对于视口的坐标  也可以直接 X Y 等同于clientX clientY
-offset：  offsetX offsetY 鼠标相对于事件源的内边距的坐标  
-screen： screenX screenY 鼠标相对于屏幕
-movement：movementX movementY 只在鼠标移动事件中有效，相对于上一次鼠标位置偏移的距离


## 键盘事件
### 事件类型
-keydown  按下键盘上任意键触发，如果按住不放，会重复触发此事件
-keypress 按下键盘上一个**字符键**时触发
-keyup 抬起键盘上任意键触发


keydown keypress如果阻止了事件事件默认行为，文本不会显示

### 事件对象

KeyboarEvent内
-code 得到按键字符串，适配键盘布局（就是可以区分左右的按键 比如两个alt键）但是不区分字母大小写

-key 得到按键字符串，不适配按键布局，但是能得到打印字符（区别大小写）
-keyCode，which 得到键盘按键编码（自己的数字编码） 不推荐使用

## 其他事件
### 表单事件

-focus  元素聚焦的时候触发（能与用户发生交互的元素都可以聚焦） 该事件不会冒泡
-blur    元素失去焦点时触发  不会冒泡
-submit 提交表单事件 仅在from元素有效
-change 文本改变事件
-input 文本改变事件 即时触发

## 其他事件

window全局对象

-load，DOMContentLoaded，readystatechange
    window的load：页面中所有资源全部加载完毕的事件（就是等资源全部加载完才发生） 不常用 一般给图片注册该事件，
            我们先了解浏览器渲染页面的过程：
                    1.得到页面源代码
                    2.创建document节点
                    3.从上到下，将元素依次添加到dom树中，每添加一个元素，进行预渲染
                    4.按照结构，依次渲染子节点

    document的DOMContentLoaded  dom树构建完后发生的事件

    readystatechange ： loading （对象正在加载数据），interactive（触发DOMContentLoaded事件） ，complete（触发window的load事件）


-unload ，beforeunload
    beforeunload window是事件，关闭窗口时运行，可以阻止关闭窗口 
            比如 window.onbeforeunload = function(){return "确定关闭？";} //会弹出窗口选项 显示返回的文本 
    unload window的事件 关闭窗口时运行

-scroll  窗口发生滚动时运行的事件  元素也可以（当内容超出盒子产生滚动条）
    通过scrollTop和scrollLeft 可以获取和设置滚动问题

-resize 窗口尺寸发生改变时运行的事件，监听的是视口尺寸
-contextmenu  右键菜单事件 
-paste 粘贴事件
-copy 复制事件
-cut 剪切事件


css3过渡 https://www.runoob.com/css3/css3-transitions.html


transitionend 事件在 CSS 完成过渡后触发。
注意： 如果过渡在完成前移除，例如 CSS transition-property 属性被移除，过渡事件将不被触发。


# 补充
## 元素位置
-offsetParent 获取某个元素第一个定位的祖先元素，如果没有，则得到body （body的offsetParent为null）
-offsetLeft   -offsetTop  相对于该元素的offsetParent的坐标  如果offsetParent是body则将其当作整个网页
-getBoundingClientRect方法  该方法得到

## 事件模拟
-click
-sumbit
-
## 其他补充
-window.scrollX window.pageXOffset 相对于根元素的scrollLeft
-window.scrollY window.pageYOffset  相对于根元素的scrollTop
-scrollTo设置滚动条位置，scrollBy
-resizTo，resizeBy控制浏览器的尺寸 结合BOM









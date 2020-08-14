# 什么是BOM
BOM简称浏览器对象模型

主要处理浏览器窗口（window）和框架（iframe）

##  BOM核心 -window
window对象是BOM的底层（核心）对象 玩转BOM，就是window的属性和方法

window对象他具有双重角色 既可以通过js访问浏览器窗口的一个接口，又是一个全局对象，

##  BOM的组成
1. window： javaScript 层级中的顶层对象表示浏览器的窗口
 内主要属性：
    innerheight返回窗口的文档显示区的高度
    innerwidth返回窗口的文档显示区的高度
    pageXOffset设置返回当前页面相对于窗口显示区左上角的x位置
    pageYOffset设置返回当前页面相对于窗口显示区左上角的Y的位置
    screenLeft，screenTop 和 screenX ，screenY 只读整数，声明了窗口的左上角在屏幕上的x坐标和y坐标 两种效果一样，可以||来兼容性写法
 内主要方法：
    alert() 显示带有一段消息和一个确认按钮的警告框。 
    clearInterval() 取消由 setInterval() 设置的 timeout。 
    clearTimeout() 取消由 setTimeout() 方法设置的 timeout。 
    close() 关闭浏览器窗口。 
    confirm() 显示带有一段消息以及确认按钮和取消按钮的对话框。 
    open() 打开一个新的浏览器窗口或查找一个已命名的窗口。 
    print() 打印当前窗口的内容。第一个参数是地址，第二个参数是名字，第三个参数是窗口大小  返回的是该窗口的window
    prompt() 显示可提示用户输入的对话框。 
    scrollBy() 按照指定的像素值来滚动内容。 
    scrollTo() 把内容滚动到指定的坐标。 
    setInterval() 按照指定的周期（以毫秒计）来调用函数或计算表达式。 
    setTimeout() 在指定的毫秒数后调用函数或计算表达式。 

2. NAvigation：包含客户端浏览器的信息
 内主要属性：
    cookieEnabled 返回指名浏览器是否启用cookie的布尔值 （cookie可以缓存数据，实现用户在规定时间内不重复登录）
    onLine 返回指明系统是否处于脱机模式的布尔值 （是否断网）
   userAgent 返回由客户机发送服务器的user-agent头部的值 



3. History：包含浏览器窗口访问过的URL
 内主要属性：
    length 返回浏览器历史列表中的URL数量
 内主要对象方法
    back（） 加载history列表中的前一个URL
    forward（）加载history列表中的下一个URL
    go（） 加载history列表中的某个具体页面

4. Location：包含当前URL的信息
 内主要属性：（其实就是拆分URL）
    hash 设置或返回从井号 (#) 开始的 URL（锚）。 
    host 设置或返回主机名和当前 URL 的端口号。 
    hostname 设置或返回当前 URL 的主机名。 
    href 设置或返回完整的 URL。 
    pathname 设置或返回当前 URL 的路径部分。 
    port 设置或返回当前 URL 的端口号。 
    protocol 设置或返回当前 URL 的协议。 
    search 设置或返回从问号 (?) 开始的 URL（查询部分）。
 内方法：
    assign() 加载新的文档。 
    reload() 重新加载当前文档。 
    replace() 用新的文档替换当前文档。 


5. Screen：包含客户端显示屏的信息


# js必会常用知识点

## 浏览器基本组成：
            用户界面
            浏览器引擎
            渲染引擎
            网络
            ui后端
            js引擎
            数据引擎
## 属性和特性

属性包含特性  特性先天自带的，然后属性包括了先天的和后天的添加的 
比如value name之类的这种就是特性 那些自定义的就不是特性，不同通过dom.属性名 来访问修改 因为不存在映射关系，
## 图片预加载和懒加载

预加载就是等全部在后加载完了再显示出来
懒加载就是轮到了才执行

## Math.random() 取随机数应用 这个和java的一样

## getelementsByClassNmae()的封装

## 断点测试

# 运动
一个重要函数 循环定时器： setInterval（function（）{}， 30）；两个参数一个函数和一个时间触发间隔
例  
    clearInterval(a); //该方法可以关闭一个定时器这样可以避免多次触发定时器而产生的问题
    a = setInterval (function(){},30);
## 变速运动
通过定时器的方式不断增加元素的某个样式值 可以匀速 加速 减速 实现变速运动 

## 弹性运动  
其实弹性运动就是利用了这个原理 让一个值不断的递减使增加，到0的时候开始往回运动
## 重力运动

## 轮播图

锁机制（if和boolean 进入改变boolean 出来改）


# 数组 
## 方法列举
- forEach（function（ele，index，self）{}，thisValue） 遍历数组 传递一个函数作为参数 ： 表示该函数会被执行数组长度次  内函数可以给三个参数 第一个是相应索引内容 第二个是索引值 第三个是数组本身    thisValue是可选。传递给函数的值一般用 "this" 值。如果这个参数为空， "undefined" 会传递给 "this" 值（指定索引的数组对象）

- filter（function（ele，index，self）{}，thisValue） 对数组过滤的作用 基于遍历  传递参数和foreach一样 
        不同的是filter执行完之后会返回一个新的数组 通过return来进行数组的筛选  他是按照要求看看有没有达到你的要求 达到了就返回索引内的东西
- map（function（ele，index，self）{}，thisValue）  传参和foreach一样 也可以返回一个新数组 但是他的返回值是具有映射关系  他会按照要求返回相应的东西

-every 可以用来判断数组中的元素是否都符合条件 内函数都符合（遇到false会break） 才会返回 传递参数和foreach一样 
-some 他和every的区别就是有一个符合就返回

 - reduce（function（prevValue，icurValue，index，self ）{}） 不同的是前面多了一个参数   。。。


 ## 利用上述方法实现列表的筛选 










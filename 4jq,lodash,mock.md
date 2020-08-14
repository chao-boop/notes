# 以下都为工具库

#   jquery.js 简介  使得对html和css的操作更加简洁
一个强大的工具库  
注意jq2.0以上不支持IE8

## jquery选择器
-  基础选择器 
		$('#list1').css('background','green');              id选择器
		$('.red').css('background','grey');                 类选择器
		$('li').css('border','2px solid pink');             元素选择器
		$('*').css('border','2px solid orange');            通配符选择器
		$('li,p').css('font-size','20px');                  组合选择器 选中li和p标签
		
- 层级选择器
		$('div a').css('color','green');                    后代选择器 （div后面的所有a标签  无论什么层级）
		$('div>a').css('color','red');                      子选择器（div的下一级所有a标签）
		$('div a.link + a').css('color','purple');          相邻选择器（div后面的class名为link的a元素的相邻a标签）
		$('div a.link ~ a').css('color','blue');            div后面的class名为link的a元素的后面的所有的a标签

- 属性选择器
		$('#ulColor li[class]').css('background','pink');                                         选中到id为ulcolor的后面的li中有class属性的所有标签
		$('#ulColor li[title=blue]').css('background','grey');                                     选中到id为ulcolor的后面的li中所有属性title为blue的标签                 
		$('#ulColor li[title!=blue]').css('background','yellowgreen');                                          和上面相反
		$('#ulColor li[title|=css]').css('background','darkgreen');	//前缀是用-隔开的                           选中以这个为前缀的 且以-隔开的
		$('#ulColor li[id^=color]').css('background','hotpink');	//以属性值为开始（不需要-隔开）              这个前缀不要求必须用-隔开的
		$('#ulColor li[id$=color]').css('background','purple');                                                 选中以这个为后缀的 也不要求-
		$('#ulColor li[lang*=cn]').css('background','olive');	//属性中包含cn字符串                                
		$('#ulColor li[lang~=cn]').css('background','skyblue');	//属性中包含cn单词，用空格隔开的
		$('#ulColor li[class=cl][name=kaivon]').css('background','teal');	   同时具备两个条件class=cl和name=kaivon

- 基础过滤选择器
		$('#olColor li:eq(1)').css('border','5px solid pink');                              选中到id为ulcolor的后面的li中第二个 注意索引从0开始                     
		$('#olColor li:gt(1)').css('border','5px solid grey');			//大于
		$('#olColor li:lt(3)').css('border','5px solid yellowgreen');	//小于
		$('#olColor li:not(#olColor li:eq(2))').css('border','5px solid darkgreen');	//排除 
		$('#olColor li:even').css('border','5px solid hotpink');		//偶数
		$('#olColor li:odd').css('border','5px solid purple');			//奇数
		$('#olColor li:first').css('border','5px solid olive');			//第一个
		$('#olColor li:last').css('border','5px solid skyblue');		//最后一个
		$('#olColor li:lang(en)').css('border','5px solid teal');		//lang属性
		$('#olColor li:target(tar)').css('border','5px solid yellow');	//tatget属性
		$(':root').css('border','2px solid blue');	//根节点
		$(':header').css('border','5px solid darkgreen');				//所有的h标签

- 子元素过滤器
		$('#paragraph p:first-child').css('color','pink');				//第一个子元素必需是p标签 既是第一个有为p标签才可以
		$('#paragraph span:first-of-type').css('color','yellowgreen');	//选择到第1个span标签  span内的第一个就可以
		$('#paragraph span:last-child').css('color','darkgreen');   	//最后一个 即是p又是最后一个
		$('#paragraph p:last-of-type').css('color','hotpink');      	//p的最后一个就可以
		$('#paragraph p:nth-child(2)').css('color','blue');				//选择到第2个子元素，并且这个子元素必需是p标签
		$('#paragraph span:nth-of-type(2)').css('color','olive');
		$('#only p:only-child').css('color','skyblue');					//选择到只有一个子元素的标签
		$('#only-two span:only-of-type').css('font-size','30px');		//选择到只有一个span子元素的标签

- 内容过滤选择器
		$('#content:contains(kaivon)').css('color','blue');     		//内容为kaivon就选中
		$('div:empty').css({                        					//内没有内容就选中
			width:'100px',
			height:'100px',
			background:'green'
		});
		$('#has:has(p)').css('border','1px solid #000');       元素里面有p标签就选中 无论层级 孙子元素也包括
		$('#title:parent').css('border','1px solid #f00');      找到他的父级标签

-  表单过滤选择器
		$(':button').css('border','2px solid #f0f');	//选择到所有的按钮  不分是input还是button 是按钮就选中
		$('#sex input:checkbox').wrap('<span></span>').parent().css('border','2px solid purpLe');    属性为checkbox的
		$(':checked').wrap('<span></span>').parent().css('border','2px solid blue');            选择被选中的表单


## 过滤
 - 获取后代元素
		$('.child').children().css('border-color','green');	//.children()	获取所有子元素(第一层)
		$('.child').children(':eq(1)').css('border-width','3px');	//可以接收一个选择器的参数，这个选择器用来过滤子元素
		$('.child').find('span:eq(0)').css({	//.find()	获取匹配到的后代元素。它与children不同的地方为：children找到的是子元素，find找到的是后代元素
			'font-size':'30px',
			color:'red'
		});


- 获取祖先元素
		$('.parent li ul li:first').parent('ul').css('border','4px solid blue');	//.parent()		获取父元素。也可以加一个参数.ul。就表示要找到父级必需有个class
		  
		parents()	获取祖先元素。所有祖先元素都会被找到，一直找到HTML
		parentsUntil('li')	获取祖先元素（但是有个范围，找到li就不再往上找了）
		offsetParent()	获取最近的有定位的祖先元素
		
		//获取祖先元素.closest() 获取祖先元素，与parents有点像。但区别是closest会找自己，parents不会找自己
		 closest() 方法获得匹配选择器的第一个祖先元素，从当前元素开始沿 DOM 树向上。
		$('.closest li ul li').closest('li').css('border','5px solid purple');	//会从自己查起，如果自己的标签满足的话，自己的标签就算


- 获取后面的兄弟元素
		$('.next li:first').next('li').css('background','cyan');	//.next()	获取后面紧临的兄弟元素。参数也是个选择器，可选
		$('.next li:first').nextAll('li').css('border','5px solid #000');	//.nextAll()	获取后面所有的同辈兄弟元素
		$('.next li:first').nextUntil('div').css('border','5px solid red');	//获取后面所有的同辈兄弟元素（但是有个范围，找到div就不找了）

- 获取前面的兄弟元素(与next一样)
		$('.prev li:last').prev('li').css('background','cyan');
		$('.prev li:eq(3)').prevAll('li').css('border','5px solid #000');
		$('.prev li:eq(3)').prevUntil('div').css('border','5px solid red');


- 获取所有的兄弟节点
		$('.siblings li:eq(2)').siblings().css('border','5px solid skyblue');
		$('.siblings li:eq(2)').siblings('.select').css('background','yellow');	//添加了参数，进行过滤


##  DOM操作

- 操作class
		$('.setClass li:first').addClass('red');											//添加class  添加 不会替换已有的
		$('.setClass li:eq(1)').removeClass('green');										//移除class(不给参数，移除所有class)
		console.log(																		//是否包含某个class  返回布尔型
			$('.setClass li:last').hasClass('green'),	//true
			$('.setClass li:last').hasClass('orange'),	//false
		);
																							//toggleClass 切换class。在添加、删除间切换
		$('.setClass p').click(function(){
			$(this).toggleClass();
		});


- 插入元素（内部插入）
		$('.insideAdd').append('<h2>append方法插入</h2>');				//append()，在元素里面的末尾插入DOM。这个与appendChild的方法是一样的。
		$('.insideAdd').append($('.insideAdd p'));
		$('<h2>appendTo方法插入</h2>').appendTo('.insideAdd');			//appendTo将匹配的元素插入到目标元素的最后面。这个与append一样，只不过内容和目标的位置相反。append方法里直接写一个标签的字符串，就相当于创建一个DOM对象
		$('.insideAdd').prepend('<h2>prepend方法插入</h2>');			//prepend()，与append的语法一样，只不过是插入到父级元素的前面
		$('<h2>prependTo方法插入</h2>').prependTo('.insideAdd');		//prependTo()，与appendTo是一样的，不同的也是插入的位置是在前面


-  插入元素（外部插入，插入为兄弟节点）
		$('.outsideAdd h2').after('<p>after方法添加到h2后面</p>');							//after()（语法类似于append）
		$('<p>insertAfter方法添加到h2后面</p>').insertAfter('.outsideAdd h2');				//insertAfter()（语法类似于appendTo）
		$('.outsideAdd h2').before('<p>before方法添加到h2前面</p>');						//before()（语法类似于prepend）
		$('<p>insertBefore方法添加到h2前面</p>').insertBefore('.outsideAdd h2');			//insertBefore()（语法类似于prependTo）


- 插入元素，html与text方法。相当于原生的innerHTML、innerText属性
		console.log($('.htmlText').html());                                                 //不给参数 获取内所有节点内容包括标签节点
		$('.htmlText').html('<h2>这是html方法添加的标题</h2><p>这是html方法添加的内容</p>');	//设置 替换内容 
		console.log($('.htmlText').text());										// 不给参数 获取纯文本不会获取内标签 不同标签内的文本会按顺序拼接返回
		$('.htmlText').text('<h2>这是text方法添加的标题</h2><p>这是<em>text</em>方法添加的内容</p>'); //给参数 替换内所有节点 但只是以纯文本 若参数有标签则会转化为特殊字符
		1.4版本以上可以以函数形式传递参数 详情可参照jQuery官方文档

- 包裹元素
		$('.wrap span').wrap('<li>');									//wrap()，在每个匹配的元素外层包上一个html元素
		$('.wrap li').wrapAll('<ul>');									//wrapAll()，在所有匹配元素外面包一层HTML元素  单个包含
		$('.wrap span').wrapInner('<strong>');							//wrapInner()，在匹配元素里的内容外包一层结构  整体包含
		$('.wrap li').unwrap();											//.unwrap()将匹配到的元素的父级删除


- 删除元素
		//$('.del .title').remove();									//remove()，移除自己
		$('div').remove('.title');										//也可以添加参数。从div中移除一个.title的div
		$('.del ul').empty();											//empty()，清空子元素
		$('.del .end').click(function(){
			alert(1);
		});
		//detach()，与remove()一样，这两个方法都有一个返回值，返回被删除的DOM。它们的区别就在这个返回值身上  remove会删除一切 detach不保留事件
		var end=$('.del .end').detach();	//再次添加后是有事件的
		//var end=$('.del .end').remove();	//再次添加后没有事件
		setTimeout(function(){
			$('.del').append(end);	//1s后，被删除的那个元素会被重新添加上
		},1000);


- 克隆与替换元素
		$('.clone p').click(function(){
			alert(2);
		});
		//$('.clone p').clone().appendTo('.clone');
		$('.clone p').clone(true).appendTo('.clone');										//clone的参数为true时表示，会把事件也克隆了
		$('<h3>使用replaceAll方法主动替换</h3>').replaceAll('.clone .replaceAll');			//创建一个元素然后用它替换掉其它元素
		$('.clone .name2').replaceAll('.clone .name1');										//使用已有的元素替换掉其它元素（剪切操作）
		$('.clone .replaceWidth').replaceWith('<h3>使用replaceWidth方法被动替换</h3>');

		
- 属性操作-通用属性操作
		console.log($('.attr img').attr('src'));								//images/img_01.jpg（如果有多个img的话，它返回的是第一个img的src值）
		$('.attr img').attr('title','这是一张美食图片');						//如果有多个img的话，设置的是所有的img
		$('.attr img').attr({													//同时设置多个属性
			class:'delicious',
			alt:'美食'
		});
		console.log($('.attr img').prop('src'));								DOM元素的属性分为两种(1)标签属性：直接写在标签上的属性
																			(2)对象属性　　由于所有的DOM元素都是Object类型,所以我们可以通过对象的方								式为DOM元素设置属性

 
		console.log(															
			$('.attr img').attr('kaivon'),	//liu													
			$('.attr img').prop('kaivon'),	//undefined								
		);
		$('.attr img').prop({
			id:'food',
			kaivon:'liuliu',													//自定义的属性prop并没有添加到DOM标签身上，但是它会添加到DOM对象身上	
		});
		$('.attr img').attr('kaivon','liuliuliu');
		$('.attr img').removeAttr('kaivon');
		$('.attr img').removeProp('id');										//删除的是DOM对象身上的属性，并不是DOM标签身上的属性
		$('.attr img').prop('index',5);
		console.log($('.attr img').prop('index'));								//5 这条属性是添加在DOM对象身上
		$('.attr img').removeProp('index');
		console.log($('.attr img').prop('index'));								//undefined removeProp是删除DOM对象身上的属性
		console.log($('.attr input').val());	//这是一个正经的输入框
		$('.attr input').val('这不是一个输入框');


- 属性操作-css类属性操作
		console.log(
			$('.css').css('border'),	//2px solid rgb(0, 0, 0)
			$('.css').css('height'),	//19.9125px
		);
		$('.css h2').css('width','200px').css('height','100px').css('background','#ccc').text('插入一个标题'); //链式操作
		$('.css h2').css({
			color:'green',
			fontSize:'30px',
			'line-height':'100px',
		});
		$('.css p').css({																		//对象形式传递
			width:'200px',
			height:'200px',
			padding:'20px',
			margin:'20px auto',
			border:'2px solid #f00',
		});
		console.log(
			$('.css p').width(),		//200   计算宽度
			$('.css p').height(),		//200	计算高度
			$('.css p').innerWidth(),	//240	为匹配的元素集合中获取第一个元素的当前计算宽度值,包括padding，但是不包括border。
			$('.css p').innerHeight(),	//240	为匹配的元素集合中获取第一个元素的当前计算高度值,包括padding，但是不包括border。
			$('.css p').outerWidth(),	//244	获取元素集合中第一个元素的当前计算宽度值,包括padding，border和选择性的margin。（注：返回一个整数（不包含														“px”）表示的值，或如果在一个空集合上调用该方法，则会返回 null。）
			$('.css p').outerHeight(),	//244	获取元素集合中第一个元素的当前计算高度值,包括padding，border和选择性的margin。返回一个整数（不包含“px”）												表示的值  ，或如果在一个空集合上调用该方法，则会返回 null。
		);
		$('.css p').width(300).height(100).innerWidth(400).outerWidth(500);	//给width与给innerWidth设置的都是width属性的值。但是innerWidth与outerWidth都会动态的算出一个宽度值，赋给width属性

		$('.css').css('position','relative');	//先把父级设置成相对定位
		$('.css div').css({
			width:'100px',
			height:'100px',
			background:'green',
			position:'absolute',
			left:'100px',
			top:'200px'
		});
		//相对于document
		console.log(									//.offset()在匹配的元素集合中，获取的第一个元素的当前坐标，坐标相对于文档。 设置匹配的元素集合中每一个元素的坐标， 坐标相对于文档。
			$('.css div').offset().left,	//110
			$('.css div').offset().top,		//1648.3499755859375
			//此方法没有.right与.bottom
		);
		$('.css div').offset({
			left:200,
			top:1800,
		});

		//position()获取匹配元素中第一个元素的当前坐标，相对于offset parent的坐标。( 译者注：offset parent指离该元素最近的而且被定位过的祖先元素 )
		console.log(
			$('.css div').position().left,
			$('.css div').position().top,
		);

		console.log(
			$(document).scrollTop(),.			//scrollTop()获取匹配的元素集合中第一个元素的当前垂直滚动条的位置或设置每个匹配元素的垂直滚动条位置。设置											每个匹配元素的垂直滚动条位置
			$(document).scrollLeft(),			//scrollLeft()获取匹配的元素集合中第一个元素的当前水平滚动条的位置。设置每个匹配元素的水平滚动条位置。
		);
		
## 事件
- 绑定事件1：通过事件名称函数
		$('#btn1').mouseover(function () {
			$(this).css('background', 'orange');
		}).mouseout(function () {
			$(this).css('background', 'grey');
		});

- 绑定事件2：通过on添加
		$('#btn2').on('click', function () {
			$(this).css('background', 'blue');
		});
		$('#btn2').on('click', { name: 'kaivon' }, function (event) {
			console.log(event.data.name);
		});
		$('#btn3').on('click', 'h2', { color: 'red' }, function (event) {
			//$(this)指向h2
			$(this).css('border', '1px solid ' + event.data.color);
		});
	on可以添加多个事件
		$('#btn2').on(
			{
			mouseover: function () {
				$(this).css('background', 'pink');
			},
			mouseout: function () {
				$(this).css('background', 'cyan');
			}
		});

- 绑定事件3：one()	只会执行一次
		$('#btn4').one('click', 'button', { color: 'purple' }, function (event) {
			$(this).css('background', event.data.color);
			console.log('只会打印一次');
		});

- 解除事件：off()
		$('#btn5').click(function () {
			//$('#btn1').off();			//没有参数，会把所有的事件全部解除
			$('#btn1').off('mouseover'); 给了参数就会相应的解除
		});
- 手动触发绑定事件：trigger()  和  triggerHandler()
		$('#btn6').on({
			click: function () {
				console.log('btn6的点击事件');
			},
			mouseover: function (event, name, age) {
				console.log('btn6的鼠标移入事件：' + name + ' : ' + age);
				$(this).css('background', 'brown');
			},
			end: function () {
				console.log('这是一个自定义的事件');
			}
		});

		setTimeout(function () {
			$('#btn6').trigger('click');
		}, 500);
		setTimeout(function () {
			$('#btn6').trigger('mouseover',['kaivon',18]);
		}, 1000);
		setTimeout(function(){
			$('#btn6').trigger('end');
		},1500);

			手动触发绑定事件：triggerHandler()

	区别1：trigger()会触发事件的默认行为；triggerHandler()不会触发事件的默认行为
		$('input').focus(function(){
			console.log('获取到焦点了');
		});
		$('#trigger').click(function(){
			$('input').trigger('focus');
		});
		$('#triggerHandler').click(function(){
			$('input').triggerHandler('focus');
		});

	区别2：trigger()会执行所有选中元素的事件；triggerHandler()只会执行第一个元素的事件
		$('#color li').click(function(){
			console.log($(this).html()+' '+$(this).index());
		});
		setTimeout(function(){
			//$('#color li').trigger('click');
			$('#color li').triggerHandler('click');
		},2000);
		
	区别3：trigger()会冒泡；triggerHandler()不会冒泡
		$('#bubble h2').click(function(){
			console.log('h2被点击了');
		});
		$('#bubble span').click(function(){
			console.log('span被点击了');
		});
		setTimeout(function(){
			//$('#bubble span').trigger('click');
			$('#bubble span').triggerHandler('click');
		},2500);

	区别4：trigger()可以使用链式操作；triggerHandler()不可以使用链式操作（但是return $(this);//最后将对象返回也可以实现链式操作）
		$('#btn7').on({
			mouseover:function(){
				$(this).css('width','200px');
				return $(this);//最后将对象返回也可以实现链式操作
			},
			mouseout:function(){
				$(this).css('height','200px');
			}
		});
		setTimeout(function(){
			// $('#btn7').trigger('mouseover').trigger('mouseout');
			$('#btn7').triggerHandler('mouseover').triggerHandler('mouseout');
		},3000);


-  事件对象  使用和原生js一样传入参数event，
		$('#btn8').click(function(event){
			console.log(event);
		});
		下面是原生js传入事件对象的方法
		$('#btn9')[0].onclick=function(ev){
			console.log(ev);
		};

## 内置特效



- 基本特效
		hide（）隐藏  show（）显示  toggle（）显示或隐藏

		$('#hide').click(function () {   			//设置一个隐藏所需的时间
			//$('#box').hide('fast');
			//$('#box').hide('nomal');
			//$('#box').hide('slow');
			$('#box').hide(4000, function () {
				console.log('隐藏动画完成了');
			});
		});
		$('#show').click(function () {				//给一个会调函数 后面这个参数可选
			$('#box').show('nomal', function () {
				console.log('显示动画完成了');
			});
		});

		var n = 0;
		$('#toggle').click(function () {
			$('#box').toggle('nomal', function () {
				var re = n++ % 2;
				//console.log(n++ % 2);

				if (re == 0) {
					console.log('隐藏动画结束了');
				} else {
					console.log('显示动画结束了');
				}
			});
		});


- 滑动特效
		slideup()滑动隐藏  slidedown滑动显示  .slideToggle()用滑动动画显示或隐藏一个匹配元素。    参数和上面一样

		$('#slideUp').click(function () {
			$('#box').slideUp(4000, function () {		
				console.log('滑动隐藏动画结束了');
			});
		});
		$('#slideDown').click(function () {
			$('#box').slideDown('nomal', function () {
				console.log('滑动显示动画结束了');
			});
		});

		var n = 0;
		$('#slideToggle').click(function () {
			$('#box').slideToggle('nomal', function () {
				var re = n++ % 2;
				//console.log(n++ % 2);

				if (re == 0) {
					console.log('滑动隐藏动画结束了');
				} else {
					console.log('滑动显示动画结束了');
				}
			});
		});


- 渐变特效
		.fadeIn()通过淡入的方式显示匹配元素。 .fadeOut()通过淡出的方式隐藏匹配元素。 .fadeTo()调整匹配元素的透明度。.fadeToggle()通过匹配的元素的不透明度动画，来显示或隐藏它们。

		$('#fadeOut').click(function () {
			$('#box').fadeOut('slow', function () {
				console.log('淡出隐藏动画结束了');
			});
		});
		$('#fadeIn').click(function () {
			$('#box').fadeIn('slow', function () {
				console.log('淡入显示动画结束了');
			});
		});

		var n = 0;
		$('#fadeToggle').click(function () {
			$('#box').fadeToggle('nomal', function () {
				var re = n++ % 2;
				//console.log(n++ % 2);

				if (re == 0) {
					console.log('淡出隐藏动画结束了');
				} else {
					console.log('淡入显示动画结束了');
				}
			});
		});

		$('#fadeTo').click(function () {
			$('#box').fadeTo('nomal', 0.5, function () {
				console.log('透明度变化完成了');
			});
		})


- 自定义
		animate根据一组自定义css来执行动画 ，然后给定一个时间 还可以给一个回调
		/* $('#animate').click(function () {
			$('#box').animate({
				width: 200,
				left: '+=50',
				height: 'toggle',
				'border-radius': 50
			}, 500, function () {
				console.log('运动结束了');
			});
		}); */

	可以链式操作
		$('#animate').click(function () {
			$('#box').animate({ width: 200 }, 'fast')
				.delay(2000)	//让后面的动画延迟执行		.delay()设置一个延时来推迟执行队列中后续的项。
				.animate({ height: 200 }, 'slow')
				.delay(1000)
				.animate({ opacity: 0.5 }, 1000);
		});


	控制动画
		$('#stop').click(function () {					.stop()停止匹配元素当前正在运行的动画。
			$('#box').stop();
		});
		$('#finish').click(function () {					finish（）停止当前正在运行的动画，删除所有排队的动画，并完成匹配元素所有的动画。
			$('#box').finish();							
		});
	
## ajax
- get请求		jQuery.get()使用一个HTTP GET请求从服务器加载数据。
		$('#get').click(function () {
			$.get('http://api.duyiedu.com/api/student/findAll', { appkey: 'kaivon_1574822824764' }, function (data) {
				console.log(data);
			}, 'json');
		});
		$('#ajaxGet').click(function () {
			$.ajax({
				url: 'http://api.duyiedu.com/api/student/findAll',
				type: 'get',	
				/* data:{
					appkey:'kaivon_1574822824764',
				}, */
				data: 'appkey=kaivon_1574822824764',
				dataType: 'json',									dataType类型: String从服务器返回的预期的数据类型。默认：智能猜测（xml, json, 																												script, 或 html）	
				success: function (data) {
					console.log(data);
				}
			});
		});

- post请求		jQuery.post()使用一个HTTP POST 请求从服务器加载数据。
		$('#loginBtn1').click(function () {
			var username = $('#login input[name=account]').val();
			var password = $('#login input[name=password]').val();

			$.post('http://api.duyiedu.com/api/student/stuLogin', { appkey: 'kaivon_1574822824764', account: username, password: password }, function (data) {
				console.log(data);
			}, 'json');    //四个参数 url 数据 回调 数据类型

			//console.log(username,password);
		});

		$('#loginBtn2').click(function () {
			$.ajax({
				url: 'http://api.duyiedu.com/api/student/stuLogin',
				type: 'post',
				data: {
					appkey: 'kaivon_1574822824764',
					account: $('#login input[name=account]').val(),
					password: $('#login input[name=password]').val()
				},
				dataType: 'json',									dataType类型: String从服务器返回的预期的数据类型。默认：智能猜测（xml, json, 																													script, 或 html）。
				success: function (data) {
					console.log(data);
				},
				error: function (status) {
					console.log('错误原因：' + status);
				}
			});
		});

- JSON请求			jQuery.getJSON()使用一个HTTP GET请求从服务器加载JSON编码的数据。	如果URL包含字符串“callback=?”（或类似的参数，取决于服务器端 API 																							是如何定义的），这个请求被视为JSONP形式请求
		$('#json').click(function () {
			$.getJSON('http://api.duyiedu.com/api/student/findAll', { appkey: 'kaivon_1574822824764' },function(data){
				console.log(data);
			});
		});


## 插件  
		https://plugins.jquery.com/		jq库的相关插件
		http://www.jq22.com/			国内的插件网站

		https://alvarotrigo.com/fullPage/zh/		
		https://github.com/alvarotrigo/fullPage.js/tree/master/lang/chinese#fullpag

- 插件的使用
- 插件的制作


# lodash.js   Lodash 通过降低 array、number、objects、string 等等的使用难度从而让 JavaScript 变得更简单。
Lodash 的模块化方法 非常适用于：

遍历 array、object 和 string
对值进行操作和检测
创建符合功能的函数

## array相关
		//chunk()   把数组拆分成一个二维数组，拆分后的第1个数组的长度为第二个参数的值
		console.log(_.chunk(['a', 'b', 'c', 'd'], 2));	//[["a", "b"],["c", "d"]]

		//compact() 过滤掉原数组里的非真（转布尔值后为false）数据
		console.log(_.compact([0, 1, false, 2, '', 3, null, NaN, undefined]));	//[1, 2, 3]

		//concat()  合并数组，与Array对象的方法一样

		//difference()  在第一个数组中把第二个数组里的数据都排除掉
		console.log(_.difference([1, 3, 5, 7, 9], [3, 7]));	// [1, 5, 9]

		//differenceBy	与上面的方法一样，只不过它可以再接收一个迭代器的函数做为参数
		console.log(_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor));	//[3.1, 1.3]

		//differenceWith()	与上面的方法一样，只不过它可以接收一个比较器的函数做为参数，对每个数据都要比较一下
		var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
		console.log(_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual));	//[{ 'x': 2, 'y': 1 }]

		//drop()    切掉数组的前n（第二个参数，默认为1）位
		console.log(_.drop(['a', 'b', 'c', 'd', 'e'], 2));	//['c', 'd', 'e']
		//dropRight()   切割数组，切掉数组的后n位

		//dropWhile()	去掉数组中，从起点到第二个方法返回假的数据。与Array对象身上的filter()方法一样
		//dropRightWhile()	与上面一样，不过它是从右边开始查，查到返回假的那个数据都去除

		//take()	提取数组的前n（第二个参数，默认为1）位。与drop方法相反
		console.log(_.take(['a', 'b', 'c', 'd', 'e'], 2));
		//takeRight()/takeWhile()/takeRightWhile()	与上面的一样

		//fill()    填充数组，与Array对象身上的fill()方法一样
		//findIndex()   查找到第一个满足条件的数据的索引值（从左往右查），没找到返回-1。与Array对象身上的findIndex()方法一样
		//findLastIndex()	这与上面的findIndex是一样的，区别是它是从右往左的查

		//flatten()	减少一级数组嵌套深度，与Array的flat()这个方法相似
		console.log(_.flatten(['a', ['b', ['c', ['d']]]]));

		//flattenDeep()	把数组递归为一维数组。相当于[].flat(Infinity)
		console.log(_.flattenDeep(['a', ['b', ['c', ['d']]]]));	//["a", "b", "c", "d"]

		//flattenDepth()	减少n（第二个参数）层数组的嵌套。相当于[].flat(2)
		console.log(_.flattenDepth(['a', ['b', ['c', ['d']]]], 2));	//["a", "b", "c", "d"]

		//fromPairs()	把数组转换为一个对象，与Object.fromEntries()方法一样
		//head()/first()	获取数组里第一个元素，就是取下标为0的那个数据
		//last()	取数组里的最后一位数据，取下标为length-1的那个数据

		//indexOf()	查找数据，并返回数据对应的索引值，与Array对象身上的indexOf()方法一样
		//lastIndexOf()	查找数据，并返回数据对应的索引值，与Array对象身上的lastIndexOf()方法一样
		//initial()	获取数组里除了最后一位的所有数据。相当于删除数组里的最后一个数据，与Array对象身上的pop()方法一样。区别在于pop方法会改变原数组，而这个方法不会改变原数组
		//tail()	获取除了array数组第一个元素以外的全部元素，想当于Array对象身上的shift()，与initial()相反

		//intersection()	取数组的交集
		console.log(_.intersection(['a', 'b'], ['b', 'c'], ['e', 'b']));	//['b']

		//union()	取数组的并集（合并起来，去掉重复的）
		console.log(_.union([2], [1, 2]));	//[2, 1]

		//xor()	删除数组的交集，留下非交集的部分
		console.log(_.xor(['a', 'b'], ['b', 'c'], ['e', 'b']));	//["a", "c", "e"]

		//join()	把数组转成字符串，这个方法原生的Array对象也有

		//nth()	取数组里的某个数据，就是通过下标取到某个数据。只不过它的数字可以为负。表示倒着找
		var array = ['a', 'b', 'c', 'd'];
		console.log(
			_.nth(array, 1),	//b
			_.nth(array, -3),	//c
		);

	以下这几个方法，用后面remove的方法代替
		//pull()	根据给的参数（参数为数据）删除原数组里的对应数据
		//pullAll()	与上面的方法一样，就是参数为数组（好比call,apply这两个方法）
		//pullAllBy()\pullAllWith()	与前面方面的语法一样
		//pullAt()	根据给的参数（参数为索引）删除原数组里的对应数据

		//remove()	根据函数删除原数组里的数据
		var arr = ['a', 'b', 'c', 'd', 'e'];
		_.remove(arr, function (value, index, array) {
			return index > 2;
		});
		console.log(arr);	//["a", "b", "c"]

		//without()	根据给的参数（参数为数据）删除原数组里的对应数据
		var arr = ['a', 'b', 'c', 'd', 'e'];
		console.log(
			_.without(arr, 'b', 'c'),
			arr
		);

		//reverse()	颠倒数组，这个方法原生的Array对象也有
		//slice()	截取数组，这个方法原生的Array对象也有

		//uniq()
		console.log(_.uniq([1, 2, 2, 1]));	//[1, 2]
		//uniqBy()/uniqWith() 与前面的一样

		//zip()	把各数组中索引值相同的数据放到一起，组成新数组
		console.log(_.zip(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));	//[["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]

		//zipObject()	与上面方法一样，区别是它输出的是对象
		console.log(_.zipObject(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));	//{小明: "男", 小红: "女", 小刚: "男"}

		//zipWith()

		//unzip()	这个方法与zip相反，把每个数组里索引值一样的数据放在一起
		console.log(_.unzip([["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]));	//[['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]]
		//unzipWith()	与zipWidth()一样，接收了一个迭代器的函数

## collection
		//countBy()	按照一定规则统计数量，key循环次数，value为匹配到的数量
		console.log(_.countBy(['one', 'two', 'three'], 'length'));	//{3: 2, 5: 1}	按每个字符串的length进行统计，length为3的有两个数据。length为5的有1个数据

		//groupBy()	按照一定规则进行分组，key为循环次数，value为匹配到的数组
		console.log(_.groupBy(['one', 'two', 'three'], 'length'));	//{3: ["one", "two"], 5: ["three"]}

		//each()/forEach()	循环，与原生Array.forEach一样
		//eachRight()/forEachRight()	倒着循环
		//every()	与原生Array.every方法一样
		//filter()	过滤数组，与Array对象上的filter()方法一样
		//find()	查找数据，与Array对象上的find()方法一样
		//findLast()	与上面一样，区别在于它是从右往左查
		//flatMap()		生成一个扁平化的数组，与原生的flatMap()方法一样		
		//flatMapDeep()	与上面一样，不过它可以递归
		//flatMapDepth()	与上面一样，它可以递归，并且可以指定递归的深度
		//includes()	与Array对象上的includes()方法一样

		//invokeMap()	使用第二个参数（方法）去处理数组，返回处理后的结果（数组）
		console.log(
			_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort'),	//[ [1, 5, 7],[1, 2, 3]]
			_.invokeMap([123, 456], String.prototype.split, ''),	//[["1", "2", "3"],["4", "5", "6"]]
		);

		//keyBy()	创建一个对象，里面的key由第二个参数决定。value为原数组里对应的那条数据
		var array = [
			{ 'dir': 'left', 'code': 97 },
			{ 'dir': 'right', 'code': 100 }
		];
		var result = _.keyBy(array, function (o) {
			return String.fromCharCode(o.code);	//key为使用fromCharCode解析后的字符。value为它所在数组里的那条数据
		});
		console.log(result);

		//key为dir，value为key所在原数组里的那条数据
		console.log(_.keyBy(array, 'dir'));

		//orderBy()	排序，既能升序又能降序
		var users = [
			{ 'user': 'fred', 'age': 48 },
			{ 'user': 'barney', 'age': 34 },
			{ 'user': 'fred', 'age': 40 },
			{ 'user': 'barney', 'age': 36 }
		];
		console.log(
			_.orderBy(users, 'age', 'asc'),	//以age属性的值进行升序排序
			_.orderBy(users, 'user', 'desc'),	//以user属性的值进行降序排序
		);

		//sortBy()		排序，只能升序
		console.log(
			_.sortBy(users, function (o) {
				return o.user;
			}),
		);

		//partition()	根据第2个参数把一个数组分拆成一个二维数组
		var users = [
			{ 'user': 'barney', 'age': 36, 'active': false },
			{ 'user': 'fred', 'age': 40, 'active': true },
			{ 'user': 'pebbles', 'age': 1, 'active': false }
		];
		console.log(
			_.partition(users, function (o) {	//active为true的放在一起，active为false的放在一起
				return o.active;
			}),
			_.partition(users, { 'age': 1, 'active': false }),//把第二个参数对应的数据放一起，其余的放一起
		);
		
		//reduce()	与Array对象上的reduce()方法一样
		//reduceRight()	与Array对象上的reduceRight()方法一样
		
		//reject()
		var users = [
			{ 'user': 'barney', 'age': 36, 'active': false },
			{ 'user': 'fred', 'age': 40, 'active': true }
		];
		console.log(
			_.reject(users, function (o) {
				return o.active;	//barney
			}),
			_.reject(users, { 'age': 36, 'active': false }),	//fred
			_.reject(users, ['user', 'fred']),	//barney
			_.reject(users, 'age'),	//[]
		);

		//sample()	从数组中随机取一个数据
		console.log(_.sample(['a', 'b', 'c', 'd', 'e']));

		//sampleSize()	获得 n 个随机数据
		console.log(_.sampleSize(['a', 'b', 'c', 'd', 'e'], 3));

		//shuffle()	随机排序
		console.log(_.shuffle(['a', 'b', 'c', 'd', 'e']));

		//size()	返回集合长度
		console.log(
			_.size(['a', 'b', 'c', 'd', 'e']),	//5
			_.size({ a: 1, b: 2 }),	//2
			_.size('kaivon'),	//6
		);

		//some()	与Array对象上的some()方法一样
## function
		//defer()	推迟调用函数，在第二次事件循环的时候调用 
		_.defer(function (text) {
			console.log(text);
		}, '第二次事件循环');
		console.log('第一次事件循环');

		//delay()
		_.delay(function (text) {
			console.log(text);
		}, 1000, '延迟一秒执行');

		//flip()	调用函数时翻转参数
		function fn1() {
			console.log(arguments);
		}
		fn1 = _.flip(fn1);
		fn1(1, 2, 3);

		//negate()	结果取反函数
		function fn2(n) {
			return n % 2 == 0;
		};
		console.log(_.filter([1, 2, 3, 4, 5, 6], _.negate(fn2)));	//[1, 3, 5]

		//once()	函数只能调用一次
		function fn3(){
			console.log('fn3');
		}
		var newFn3=_.once(fn3);
		newFn3();
		newFn3();

		//_.throttle(func, [wait=0], [options={}]) 节流
		//_.debounce(func, [wait=0], [options={}]) 防抖

## lang
	//castArray()	强制转为数组，其实就是在外面加一层方括号
		console.log(
			_.castArray('a'),	//["a"]
			_.castArray({ a: 1, b: 2 }),	//[{a: 1, b: 2}]
		);

		//clone()	浅拷贝
		var obj1 = {
			a: 1,
			b: {
				c: 2
			}
		};
		var obj2 = _.clone(obj1);
		console.log(obj1, obj2);
		obj2.b.c = 3, console.log(obj1, obj2);

		//cloneDeep()	深拷贝
		var obj3 = _.cloneDeep(obj1);
		obj3.b.c = 4, console.log(obj1, obj3);

		//conformsTo()	通过第二个参数来检测对象的属性值是否满足条件
		var object = { 'a': 1, 'b': 2 };
		console.log(
			_.conformsTo(object, { 'b': function (n) { return n > 1 } }),	//true
			_.conformsTo(object, { 'b': function (n) { return n > 2 } }),	//false
		);

		//ea()	比较两个值是否相等。与Object.is()这个方法一样
		console.log(
			_.eq(12, 12),	//true
			_.eq({ a: 1 }, { a: 1 }),	//false
			_.eq(NaN, NaN),	//true
		);

		//gt()	第一个值是否大于第二个值
		console.log(
			_.gt(3, 1),	//true
			_.gt(3, 3),	//false
		);
		//gte()	第一个值是否大于等于第二个值
		//lt()	小于
		//lte()	小于等于

		//isArray()
		console.log(
			_.isArray([1, 2, 3]),	//true
			_.isArray(document.body.children),	//false
			_.isObject({}),		//true
			_.isObject(null),	//false
		);

		//toArray()
		console.log(
			_.toArray({ a: 1, b: 2 }),	//[1, 2]
			_.toArray('abc'),	//["a", "b", "c"]
			_.toArray(null),	//[]
## object
//assign()	合并对象，与Object.assign()方法一样
		//assignIn()/extend()	与上面一样，不过它能继承原型身上的属性
		//assignInWith()/extendWith()	与上面一样，接收一个比较器的函数做为参数
		//assignWith()	也是接收一个比较器的函数做为参数

		//at()	根据传入的属性创建一个数组
		var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
		console.log(_.at(object, ['a[0].b.c', 'a[1]']));	//[3, 4]

		//create()	与Object.create()一样

		//defaults()	合并对象，与assign()一样，不过assign方法合并时遇到相同的属性，后面的会覆盖前面的。defaults刚好相反，前面的覆盖后面的
		console.log(
			_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 }),	//{a: 1, b: 2}
			_.assign({ 'a': 1 }, { 'b': 2 }, { 'a': 3 }),	//{a: 3, b: 2}
		);

		//defaultsDeep()	与defaults一致，不过它会深递归

		//toPairs()/entries()	把对象里可枚举的属性(不包括继承的)创建成一个数组，与Object.entities()的方法一样
		//toPairsIn()/entriesIn()	与上面的一样，但它包括继承的属性

		//findKey()	与前面讲的find方法一样，只不过它返回的是key
		var users = {
			'barney': { 'age': 36, 'active': true },
			'fred': { 'age': 40, 'active': false },
			'pebbles': { 'age': 1, 'active': true }
		};
		console.log(_.findKey(users, { 'age': 1, 'active': true }));	//pebbles

		//findLastKey()	与上面一样，只不过它从反方向开始遍历

		//forIn()	与原生 的for...in循环一样，只不过它是一个函数，语法与forEach一样。它遍历的是自己的属性与继承的属性
		//forInRight()	与上面一样，只不过是反方向遍历
		//forOwn()	与forIn()一样，只不过forOwn只能遍历到自己的属性
		//forOwnRight()	与上面一样，只不过是反方向遍历

		//functions()/functionsIn()	这两个没有说？？？？？？

		//get()	获取属性的值，与Object.defineProperty()	属性描述对象上的get方法一致
		//set()	设置属性的值，与Object.defineProperty()	属性描述对象上的set方法一致
		//setWith()	与上面的一样，只不过可以给一个参数决定返回的是对象还是数组
		console.log(_.setWith({}, '[0][1]', 'a', Array));

		//has()	检查属性是否为对象的直接属性，与Object.hasOwnProperty()方法返回true一样
		//hasIn()	检查属性是对象的直接属性还是继承属性，也与Object.hasOwnProperty()一样，true表示直接属性，false表示继承属性

		//invert()	把对象的key与value颠倒，后面的属性会覆盖前面的属性
		var object = { 'a': 1, 'b': 2, 'c': 1 };
		console.log(_.invert(object));	//{1: "c", 2: "b"}

		//invertBy()	与上面一样，它遇到相同的值后不会覆盖，而是会把所有放在一个数组里。另外它多了一个遍历器方法

		//invoke()	调用方法去处理取到的属性值
		var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };
		console.log(_.invoke(object, 'a[0].b.c.slice', 1, 3)); //[2, 3]	用slice方法去截取a[0].b.c的1-3位

		//keys()	把对象的key放到一个数组里，与Object.keys()的方法一样
		//keysIn()	与上面一样，只不过它包含继承到的属性
		//values()	把对象的value放到一个数组里，与Object.value()的方法一样
		//valuesIn()	与上面一样，只不过它包含继承到的属性

		//mapKeys()	修改对象的key，value不会变
		var result = _.mapKeys({ 'a': 1, 'b': 2 }, function (value, key) {
			return key + value;
		});
		console.log(result);	//{a1: 1, b2: 2}

		//mapValues()	与上个方法一样，只不过它修改的是value，key不会变

		//merge()	它与assign一样，不过它遇到相同的属性名后并不会覆盖，它会合并
		var object = {
			'a': [{ 'b': 2 }, { 'd': 4 }]
		};
		var other = {
			'a': [{ 'c': 3 }, { 'e': 5 }]
		};
		console.log(_.merge(object, other));

		//mergeWith()	与上面的方法一致，不过多了接收一个比较器的函数做为参数

		//omit()	删除对象里的属性
		console.log(_.omit({ 'a': 1, 'b': '2', 'c': 3 }, ['a', 'c']));	//{b: "2"}

		//_.omitBy	与上面一样，不过是接收一个迭代器的函数做为参数

		//pick()	筛选对象里的属性
		console.log(_.pick({ 'a': 1, 'b': '2', 'c': 3 }, ['a', 'c']));	//{a: 1, c: 3}

		//pickBy()	与上面一样，不过是可接收一个迭代器的函数做为参数

		//result()	获取对象属性，它与get一样。只不过它遇到函数的属性时会调用函数，并且把this指向对象本身
		var obj = {
			a: 12,
			b: function () {
				console.log(this.a);
			}
		};
		console.log(_.result(obj, 'a'));	//12
		_.result(obj, 'b');	//12
		console.log(_.get(obj, 'b'));	//它只能取到这个函数，并不能执行

		//toPairs()	把对象的key与value一起放到数组里
		function Foo() {
			this.a = 1;
			this.b = 2;
		}
		Foo.prototype.c = 3;
		console.log(_.toPairs(new Foo()));
		console.log(_.toPairsIn(new Foo()));

		//unset()	删除属性
		var object = { 'a': [{ 'b': { 'c': 7 } }] };
		_.unset(object, 'a[0].b.c'), console.log(object);

		//update()	这个与set一样，不过它可以接收一个函数的参数
		var object = { a: 10 };
		_.update(object, 'a', function (n) { return n * n });
		console.log(object);	///{a: 100}

		//updateWith()	与上面的一样，不过可以接收一个路径的参数，决定生成的属性放在哪里
		var object = {};
		_.updateWith(object, '[a][b]', function () {
			return 12;
		}, Object);
		console.log(object);

## string
//camelCase()	转换字符串为驼峰格式
		console.log(
			_.camelCase('kaivon_chen'),
			_.camelCase('kaivon chen'),
		);

		//capitalize()	首字母为大写
		console.log(_.capitalize('kaivon'));	//Kaivon

		//endsWith()	查检结尾的字符
		console.log(_.endsWith('abc', 'c'));	//true

		//escape()	把特殊字符转义成真正的HTML实体字符
		console.log(_.escape('ka<iv>on'));	//ka&lt;iv&gt;on

		//unescape()	与上面相反
		console.log(_.unescape('ka&lt;iv&gt;on'));	//ka<iv>on

		//kebabCase()	转换字符为加-的形式
		console.log(_.kebabCase('k a i'));	//k-a-i

		//lowerCase()/toLower()	转小写
		//upperCase()/toUpper()	转大写

		//lowerFirst()	首字符转小写
		//upperFirst()	首字符转大写

		//pad()	填充字符串到指定的长度(左右填充)
		console.log(_.pad('abc', 8, '-')); 	//--abc---

		//padEnd()
		console.log(_.padEnd('abc', 8, '-'));

		//padStart()
		console.log(_.padStart('abc', 8, '-'));

		//parseInt()	把字符串类型的数字转成数字，

		//repeat()	重复字符串
		console.log(_.repeat('kaivon', 2));	//kaivonkaivon

		//replace()	替换字符串
		console.log(_.replace('kaivon', 'von', '***'));	//kai***

		//snakeCase()	转换字符串为_的形式
		console.log(_.snakeCase('k a i'));	//k_a_i

		//split()	分隔字符串为数组，与原生String.split()一样

		//startCase()	转换字符串为+空格的形式，并且首字符大写
		console.log(
			_.startCase('kaivon-chen'),	//Kaivon Chen
			_.startCase('kaivonChen'),	//Kaivon Chen
			_.startCase('kaivon_chen'),	//Kaivon Chen
		);

		//startsWith()	检查字符串的开始字符
		console.log(_.startsWith('kaivon', 'k'));	//true

		//template()	编译模板
		var compiled = _.template('hello <%= user %>!');	//user为一个占位符
		console.log(compiled({ 'user': 'kaivon' }));	//拿到数据后，给user赋值，它就能正确解析出内容了

		//trim()	去除首尾空格，或者指定字符
		console.log(_.trim('kaivon-', '-'));	//kaivon
		//trimEnd()	去除后面的空格，或者指定字符
		//trimStart()	与上面的一样，只不过去除的是左边的

		//truncate()
		console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!'));	//Hi kaivon! How are you feel...
		console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!', {
			//'length': 10,	//限制固定的字符个数
			'separator': /!/	//加个正则，遇到第一个空格后就加三个点
		}));

		//words()	把字符串的单词拆分成数组
		console.log(_.words('kaivon chen'));	//["kaivon", "chen"

# mock.js  用来随机生成大量数据供前端测试 （数据的获取需要后端支持 mock可以拦截ajax请求并反馈数据）

## mock语法
		//1. 属性值是字符串 String
		console.log(
			Mock.mock({
				'data1|1-4': '陈学辉',		//随机重复1-4次
				'data2|3': '好帅',	//固定重置3次
			})
		);

		//2. 属性值是数字 Number
		console.log(
			Mock.mock({
				'number1|+1': 100,	//整数，自动加1并且初始值为100
				'number2|1-100': 12,	//整数，1-100之间的随机数，包括1和100（1=<数字<=100）	12用来确定是数据为数字类型
				'number3|1-100.5': 12,	//小数，整数部分为为1-100间随机数，包括1和100；小数部分为固定5位随机数
				'number4|1-100.1-10': 12,	//小数，整数部分为为1-100间随机数，包括1和100；小数部分为1-10个随机数（位数随机，数字也随机）
				'number5|123.1-10': 12,	//数字123后面随机添加1-10位小数
				'number6|123.10': 12,	//数字123后面固定添加10位小数，但小数的值是随机的
			})
		);

		//3. 属性值是布尔型 Boolean
		console.log(
			Mock.mock({
				'b1|1': false,	//随机生成一个布尔值，true与false的概率各为一半
				'b2|1-5': true,	//随机生成一个布尔值，值为value的概率是min / (min + max)，值为!value的概率是max / (min + max)
			})
		);

		//4. 属性值是对象 Object
		console.log(
			Mock.mock({
				'num1|1-3': { a: 10, b: 20, c: 30, d: 40 },	//随机选取对象里1-3个属性
				'num2|2': { a: 10, b: 20, c: 30, d: 40 },	//随机选取对象里2个属性
			})
		);

		//属性值是数组 Array
		console.log(
			Mock.mock({
				'arr1|1': ['a', 'b', 'c', 'd', 'e'],	//随机选取数组里1个数据
				'arr2|1-3': ['a', 'b', 'c', 'd', 'e'],	//通过重复属性值生成一个新数组，min<=重复次数<=max
			})
		);

		//6. 属性值是函数 Function
		console.log(
			Mock.mock({
				'result': function () { return 1 + 2 }	//把函数的返回值当作属性的结果
			})
		)

		//7. 属性值是正则表达式 RegExp
		console.log(
			Mock.mock({
				'reg1': /[a-z][A-Z][0-9]/,
				'reg2': /\w\W\s\S\d\D/,
				'reg3': /\d{5,10}/
			})
		)

##  Random对象
		Mock.Random
		var Random = Mock.Random;
		// console.log(Random);

- 1.Basics	基础类里的方法，共7个

		//Random.boolean()		随机一个布尔值
		console.log(
			Random.boolean(),
			Random.boolean(1, 9, true),
			Random.boolean(1, 2, false),
		);

		//Random.natural()		随机一个自然数（大于等于 0 的整数）
		console.log(
			Random.natural(),
			Random.natural(100),
			Random.natural(0, 50),
		);

		//Random.integer()	随机一个整数（包含负数）
		console.log(
			Random.integer(),
			Random.integer(-100),
			Random.integer(-50, 50),
		);

		//Random.float()	随机一个小数
		console.log(
			Random.float(),
			Random.float(0),
			Random.float(-10, 10),
			Random.float(-10, 10, 3),
			Random.float(-10, 10, 2, 5),
		);

		//Random.character()	//随机一个字符
		console.log(
			Random.character(),
			Random.character('abc123'),
			Random.character('lower'),
			Random.character('symbol'),
		);

		//Random.string()	随机一个字符串
		console.log(
			Random.string(),
			Random.string(5),
			Random.string(7, 10),
			Random.string('symbol', 5),
			Random.string('abc123', 1, 3),
		);

		//Random.range()	随机一个整数数据的数组
		console.log(
			Random.range(7),
			Random.range(3, 7),
			Random.range(1, 10, 2),
		);
	


以下都是直接调声明的Random对象   var Random = Mock.Random;

- 2、Date	日期类里的方法，共4个
		//Random.date()		随机一个日期
		console.log(
			Random.date(),
			Random.date('yyyy-MM--dd : HH-m-ss'),
		);

		//Random.time()		随机一个时间
		console.log(
			Random.time(),
			Random.time('A HH:mm:ss:SS'),
		);

		//Random.datetime()	随机一个日期+时间
		console.log(
			Random.datetime(),
		);

		//Random.now()	返回当前的日期和时间字符串
		//week 定到这个周的第一天
		console.log(
			Random.now(),
			Random.now('minute'),
		);


- 3、Image	图片类里的方法，花2个
		//Random.image()	生成一个随机的图片地址
		console.log(
			Random.image(),
			Random.image('200x100'),
			Random.image('200x100', '#ffcc33', '#FFF', 'png', 'kaivon'),
		);

		//Random.dataImage()	//生成一段随机的 Base64 图片编码
		console.log(
			//Random.dataImage(),
			Random.dataImage('200x100'),
		)

		//Color	颜色类里的方法，共5个
		//Random.color()	随机一个16进制的颜色
		console.log(
			Random.color(),
		);

		//Random.hex()
		console.log(
			Random.hex(),
		);

		//Random.rgb()
		console.log(
			Random.rgb(),	//随机生成一个rgb格式的颜色
		);

		//Random.rgba()
		console.log(
			Random.rgba(),	//随机生成一个rgba格式的颜色
		);

		//Random.hsl()
		console.log(
			Random.hsl(),	//随机生成一个hsl格式(色相、饱和度、亮度)的颜色
		);


- 5、Text	文本类里的方法，共8个
		//Random.paragraph()	随机生成一段文本
		console.log(Random.paragraph());
		console.log(Random.paragraph(2));
		console.log(Random.paragraph(1, 3));

		//Random.cparagraph()	随机生成一段中文文本。
		console.log(Random.cparagraph());
		console.log(Random.cparagraph(2));
		console.log(Random.cparagraph(1, 3));

		//Random.sentence()	随机生成一个句子，句子首字母大写
		console.log(Random.sentence());
		console.log(Random.sentence(5));
		console.log(Random.sentence(1, 5));

		//Random.csentence()	随机生成一段中文文本
		console.log(Random.csentence());
		console.log(Random.csentence(5));
		console.log(Random.csentence(1, 5));

		//Random.word()		随机生成一个单词
		console.log(Random.word());
		console.log(Random.word(5));
		console.log(Random.word(1, 5));

		//Random.cword()	随机生成一个汉字
		console.log(Random.cword());
		console.log(Random.cword(5));
		console.log(Random.cword(1, 5));
		console.log(Random.cword('零一二三四五六七八九十', 3));
		console.log(Random.cword('零一二三四五六七八九十', 5, 7));

		//Random.title()	随机生成一个标题
		console.log(Random.title());
		console.log(Random.title(3));
		console.log(Random.title(1, 5));

		//Random.ctitle()	随机生成一句中文标题
		console.log(Random.ctitle());
		console.log(Random.ctitle(3));
		console.log(Random.ctitle(1, 5));


- 6、Name	名字类里的方法，共6个
		//Random.first()	随机生成一个常见的英文名
		console.log(Random.first())

		//Random.last()		随机生成一个常见的英文姓
		console.log(Random.last());

		//Random.name()		随机生成一个常见的英文姓名
		console.log(Random.name(true));	//是否添加一个中间值

		//Random.cfirst()	//随机生成一个常见的中文名
		console.log(Random.cfirst());

		//Random.clast()	//随机生成一个常见的中文姓
		console.log(Random.clast());

		//Random.cname()	随机生成一个常见的中文姓名
		console.log(Random.cname());


- 7、Web	Web类里的方法，共6个
		//Random.url()	//随机生成一个 URL
		console.log(Random.url());
		console.log(Random.url('http'));	//指定协议
		console.log(Random.url('http', 'kaivon.cn'));	//指定域名

		//Random.protocol()		随机生成一个 URL 协议
		console.log(Random.protocol());

		//Random.domain()	随机生成一个域名
		console.log(Random.domain());

		//Random.tld()	随机生成一个顶级域名
		console.log(Random.tld());

		//Random.email()	随机生成一个邮件地址
		console.log(Random.email());
		console.log(Random.email('kaivon.cn'));	//指定@后的域名

		//Random.ip()	随机生成一个 IP 地址
		console.log(Random.ip());


- 8、Address	地址类里的方法，共5个
		//Random.region()	随机生成一个（中国）大区
		console.log(Random.region());

		//Random.province()	随机生成一个（中国）省（或直辖市、自治区、特别行政区）
		console.log(Random.province());

		//Random.city()		随机生成一个（中国）市
		console.log(Random.city());
		console.log(Random.city(true));	//是否生成所属的省

		//Random.county()		随机生成一个（中国）县
		console.log(Random.county());
		console.log(Random.county(true));	//指示是否生成所属的省、市

		//Random.zip()		随机生成一个邮政编码
		console.log(Random.zip());


- 9、Helper	帮助类里的方法，共5个
		//Random.capitalize()	//把字符串的第一个字母转换为大写
		console.log(Random.capitalize('kaivon'));

		//Random.upper()	//把字符串转换为大写
		console.log(Random.upper('kaivon'));

		//Random.lower()	//把字符串转换为小写
		console.log(Random.lower('KAI'));

		//Random.pick()		//从数组中随机选取一个元素
		console.log(Random.pick(['a', 'b', 'c', 'd', 'e']));

		//Random.shuffle()	//打乱数组中元素的顺序
		console.log(Random.shuffle(['a', 'b', 'c', 'd', 'e']));


- 10、Miscellaneous	其它类里的方法，共3个
		//Random.guid()		随机生成一个 GUID
		console.log(Random.guid());

		//Random.id()		随机生成一个 18 位身份证
		console.log(Random.id());

## 占位符@的用法 简化操作	  直接@加上相应的方法 就可以直接调用
			console.log(
			Mock.mock('@EMAIL'),  
			Mock.mock('@CITY(true)'),
			Mock.mock('@cword("陈学辉好帅", 1, 3)'),
		);

	扩展方法   当然也可以自己写一个随机的 
		Random.extend({
			constellation: function (date) {
				var constellations = ['白羊座', '金牛座', '双子座', '巨蟹座', '狮子座', '处女座', '天秤座', '天蝎座', '射手座', '摩羯座', '水瓶座', '双鱼座'];
				return this.pick(constellations)
			}
		});
		console.log(Random.constellation());
		console.log(Mock.mock('@constellation')) //z这两个效果一样的  上面的是因为之前声明了一个Random所以可以直接调用方法


## mock方法  主要用来拦截请求并发送拟定的随机数据

-Mack.mock('url',{});  给一个要拦截的地址 和一个返回的数据：
	实例： 基于jquery工具库
	$('#btn').click(function () {  				//注册一个点击事件
			$.ajax({							//调用ajax
				url: 'js/data.json',
				type: 'get',
				dataType: 'json',
				success: function (data) {
					console.log(data);
					createDom(data.data);		//会调执行这个函数
				}
			});
		});

		function createDom(data) {				这个函数用来处理拆分返回的数据
			var str = '';
			data.forEach(function (item, index) {
				str += `
					<tr>
						<td>${item.sNo}</td>
						<td>${item.name}</td>
						<td>${item.sex}</td>
						<td>${item.email}</td>
						<td>${item.birth}</td>
						<td>${item.phone}</td>
						<td>${item.address}</td>
						<td>
							<button>编辑</button>
							<button>删除</button>
						</td>
					</tr>
				`;
			});
			$('#table-body').html(str);
		};


		Mock.mock('js/data.json', {					//调用mack方法 
			"status": "success",
			"msg": "查询成功",
			"data|10": [{						//用到了mack语法
				"id|+1": 1,
				"name": "@cname",					//@加random对象内的方法 简化了操作	
				"birth": "@date",
				"sex|1": ['男', '女'],
				"sNo|+1": 11000,
				"email": "@email",
				"phone": "@natural(13000000000,19900000000)",
				"address": "@county(true) @ctitle(5,10)",
				"appkey": "@string(4,7)_@date(T)",
				"ctime": "@date(T)",
           		"utime": "@date(T)"
			}],
		});
- Mock.setup 延迟返回数据
		Mock.setup({
			timeout:5000,
		});


- //https://github.com/YMFE/yapi  一个可以提供前后端数据交互的网址 毕竟maock只能返回虚拟数据 并不能实现数据交互

# moment.js   主要是一些日期方面的工具库
## 解析方法
		//解析
		//moment() 
		console.log(moment());	

		//moment(String)
		console.log(moment('2013-02-08'));	//返回2013年2月8号的日期对象
		console.log(
			moment('2013-039'),	//返回2013年的第39天，2013年2月8号
			moment('2013050'),	//返回2013年的第50天，2013年2月19号
			moment('2013W065'),	//返回2013年的第6个星期的第5天，2013年2月8号（W表示星期）
			moment('2013-02-08T09'),//返回2013年2月8号9点（T表示时间）
		);
		console.log(moment('kaivon'));//警告，同时照样能返回那个对象，不过对象里的参数的值是不正确的

		//moment(String) 带格式 
		console.log(moment("12-25-1995", "MM-DD-YYYY"));
		console.log(moment("12/25/1995", "LL"));

		//moment(String) 多个格式 
		console.log(moment("29-06-1995", ["MM-DD-YYYY", "DD-MM", "DD-MM-YYYY"]));

		//moment(String) 特殊格式 
		console.log(moment("2010-01-01T05:06:07", moment.ISO_8601));

		//moment(Object) 
		console.log(moment({ year: 2010, month: 3, day: 5, hour: 15, minute: 10, second: 3, millisecond: 123 }));//注意：这里的月份也是从0开始，此时对应的是4月

		//moment(Number) 
		console.log(moment(1318781876406));//这个参数为毫秒数

		//unix()
		console.log(moment.unix(1318781876406 / 1000));//这个参数为秒数

		//moment(Date)
		console.log(moment(new Date(2011, 9, 16)));

		//moment(Number[])	参数为一个数组	[year, month, day, hour, minute, second, millisecond]
		console.log(moment([2010, 1, 14, 15, 25, 50, 125]));//注意月份是从0开始的，这里对应的是2月

		//moment(JSONDate) 
		console.log(moment("/Date(1198908717056-0700)/"));	//前面一串数字为时间戳，-后面的是时区

		//moment(Moment) 参数为一个moment对象，用于克隆
		var a=moment([2012]);
		var b=moment(a);
		console.log(a.valueOf()===b.valueOf());

		//clone()	也可以使用clone去克隆
		var a=moment([2008]);
		var b=a.clone();
		console.log(a,b);

		/*
			GMT	世界时，格林尼治标准时间 
			UTC	协调世界时，世界统一时间、世界标准时间
		 */
		//utc()
		console.log(moment().format());	//GMT //默认为本地当前时间，东八区的时间（+08:00）
		console.log(moment.utc().format());	//UTC		//UTC的时间（世界标准时间，位于0时区，时区用Z表示，它与北京时间相差8个小时）

		//isValid()
		console.log(
			moment([2015, 25, 35]).isValid(),	//false
			moment([2015, 10, 35]).invalidAt(),	//2
		);

## 取值和赋值方法
		console.log(moment().seconds() === new Date().getSeconds());	//true
		console.log(moment.utc().seconds() === new Date().getUTCSeconds());	//true

		//millisecond()/milliseconds()	获取或设置毫秒
		console.log(moment().millisecond());
		console.log(moment().milliseconds());
		console.log(moment().millisecond(100).valueOf());
		console.log(moment().milliseconds(100).valueOf());

		//second()/seconds()	获取/设置秒
		//minute()/minutes()	获取/设置分
		//hour()/hours()		获取/设置小时
		//date()/dates()		获取/设置日期
		//day()/days()			获取/设置星期
		console.log(
			moment().day(),	//1
			moment().day('Sunday'),//设置星期的时候可以传入一个星期的英文单词
		);

		//weekday()	根据语言环境获获取/设置星期，根据语言环境获取或设置星期几
		moment.locale('zh-cn');	//把当前的语言环境设置为中文
		console.log(
			moment().weekday(),	//0	
			moment().weekday(0),	//0	//英文下是周日，中文下是周一
		);

		//dayOfYear() 	获取或设置年份的日期（今天是今年的第几天）
		console.log(moment().dayOfYear());	//111
		console.log(moment().dayOfYear(1));

		//week()/weeks()	获取或设置年份的星期（当前星期是今年的第几个星期）
		console.log(moment().week());	//17
		console.log(moment([2021, 4, 20]).week());	//20

		//month()/months()	获取或设置月份，设置时范围为0-11，还支持月份名称
		console.log(moment().month());	//3
		console.log(moment().month('July'));	//3

		//quarter()/quarters()	获取或设置季度
		console.log(moment().quarter());	//2 
		console.log(moment().quarter(4));	//2 

		//year()/years()	获取或设置年份
		console.log(moment().year());
		console.log(moment().year(2088));

		//weekYear()
		console.log(moment([2020, 0, 1]).weekYear());
		console.log(moment([2020, 11, 31]).weekYear());

		//weeksInYear() 根据语言环境获取当前 moment 年份的周数
		console.log(moment().weeksInYear());	//52

		//get() 获取日期
		console.log(moment().get('year'));
		console.log(moment().get('M'));
		console.log(moment().get('date'));

		//set()	设置日期
		console.log(
			moment().set('year', 2030),
			moment().set('month', 8),
			moment().set({
				'year': 2008,
				'month': 7,
				'date': 8
			}),
		);

		//max()	对比多个日期，返回最大的那个日期
		//min()	对比多个日期，返回最小的那个日期
		var a = moment('2019-10-15');
		var b = moment({ year: 2010, month: 3, date: 5 });
		var c = moment([2020, 10, 20]);
		console.log(moment.max(a, b, c));	//c
		console.log(moment.min(a, b, c));	//b

## 操作和显示方法
		//操作
		//add()		增加日期
		console.log(moment().add(7, 'days'));//以今天的日期往后加7天
		console.log(moment().add(5, 'M'));//以今天的日期往后加5个月。这里第二个参数使用的是快捷键
		console.log(moment().add(365, 'days').add(1, 'months'));
		console.log(moment().add({ days: 365, months: 1 }));

		//注意：如果原始日期中的日期大于最终月份的天数，则跳到最后一天
		console.log(moment([2010, 0, 31]).add(1, 'months'));

		//subtract() 减少日期
		console.log(moment().subtract(7, 'days'));
		console.log(moment().subtract(1.5, 'months').valueOf() === moment().subtract(2, 'months').valueOf());	//true 如果传小数的话，会被四舍五入

		//startOf() 把日期设置成参数的开始值
		console.log(moment().startOf('year'));//设置成今年第一天
		console.log(moment().startOf('month'));//设置成当月第一天
		console.log(moment().startOf('hour'));//设置成当前小时的最开始那一秒
		console.log(moment().minutes(0).seconds(0).milliseconds(0));

		//endOf() 
		console.log(moment().endOf('year'));//置成今年的最后一天的最后一刻
		console.log(moment().endOf('month'));//设置为当月的最后一天的最后一刻

		//local()	在日期上设置个标记，以使用本地时间
		var a = moment.utc([2011, 0, 1, 8]);
		console.log(a.hours());	//8
		a.local();
		console.log(a.hours());	//16

		//utcOffset() 获取本地时间与UTC时间的偏移量（差值）以分钟数为单位
		console.log(moment().utcOffset());	//480
		console.log(moment().utcOffset(10));	//把本地时间与UTC时间的偏移量设置成10，也就是本地时间比UTC时间多10个小时


		//显示
		//format()	格式化时间，它的参数非常丰富
		console.log(moment().format());	//2020-04-21T11:38:30+08:00
		console.log(moment().format('DDDo, W, MMMM Do YYYY, h:mm:ss a - ZZ'));

		//本地化的格式，它定义了一些常用格式，这些格式会根据语言环境来决定显示的内容
		moment.locale('zh-cn');
		console.log(moment().format('LLLL'));


		//fromNow()	相对于现在的时间
		console.log(
			moment([2008]).fromNow(),	//12 年前	2008年相对于今天是12年前的时间
			moment([2008]).fromNow(true),	//12 年
		);


		//from() 一个时间相对于另一个时间的时间
		var a = moment([2007, 0, 15]);
		var b = moment([2007, 0, 29]);
		console.log(
			a.from(b),	//a相对于b是14天前的时间
			a.from(b, true),
		);

		//toNow() 到现在的时间
		console.log(
			moment([2008]).toNow(),	//12 年内
			moment([2008]).toNow(true),	//12 年
		);

		//to() 	一个时间到另一个时间的间隔
		var a = moment([2007, 0, 15]);
		var b = moment([2007, 0, 29]);
		console.log(
			a.to(b),	//14 天内	a到b的时间在14天内
			a.to(b, true),	//14 天
		);

		//calendar()	返回一个相对于参数（默认为当前时间）的日历时间。最终的结果它会根据两个时间的接近程度来决定。一共定义了6个档（读一下文档）最大的范围限制在一个星期，超过一个星期就会显示为“其它”
		console.log(moment().calendar());
		console.log(moment().calendar(moment([2020, 3, 15])));	//下星期二11:54 当前的日期为参数的日期的下星期2
		console.log(moment().calendar(moment([2020, 3, 20])));	//明天11:56
		console.log(moment().calendar(moment([2020, 4, 20])));	//2020/04/21

		//diff()	返回两个时间的差值
		var a=moment([2007, 0, 29]);
		var b=moment([2007, 0, 28]);
		console.log(a.diff(b));	//86400000 默认取两个时间差的毫秒数
		console.log(a.diff(b, 'days'));	//1

		//valueOf()   获取毫秒时间戳
		console.log(
			moment().valueOf(),
			new Date().valueOf(),
		);

		//unix()
		console.log(moment().unix());

		//daysInMonth()		获取某月的天数
		console.log(moment().daysInMonth());	//30
		console.log(moment('2020-02').daysInMonth());	//29

		console.log(moment().toDate());
		console.log(moment().toArray());
		console.log(moment().toObject());//toObject()	把日期的各个组成部分拆分成了属性，返回整个对象
## 查询方法
		//isBefore()	检查一个时间是否在另一个时间之前，默认是都转成毫秒数进行计算
		console.log(moment('2010-10-20').isBefore());	//true	没给参数默认为现在的时间
		console.log(moment('2010-10-20').isBefore('2010-10-19'));	//false	第一个日期是否在第二个日期之前
		console.log(moment('2009-10-20').isBefore('2010-10-19', 'year'));	//false	二个参数为对比的单位，可以给的有year month week isoWeek day hour minute second
		console.log(moment('2010-10-20').isBefore('2008-12-31', 'month'));	//false

		//isSame()	检查两个时间是否相同
		console.log(moment('2010-10-20').isSame('2010-10-20'));
		console.log(moment('2010-10-20').isSame('2010-12-20', 'year'));

		//isAfter() 检查一个时间是否在另一个时间之后
		console.log(moment('2010-10-20').isAfter('2010-09-19'));	//true

		//isSameOrBefore()	检查一个时间是否在另一个时间之前或者与之相同（<=）
		console.log(
			moment('2010-10-20').isSameOrBefore('2010-10-21'),	//true
			moment('2010-10-20').isSameOrBefore('2010-10-20'),	//true
			moment('2010-11-20').isSameOrBefore('2010-10-20'),	//false
		);

		//isSameOrAfter() 检查一个时间是否在另一个时间之后或者与之相同（>=）
		console.log(
			moment('2010-11-20').isSameOrAfter('2010-10-21'),	//true
			moment('2010-10-20').isSameOrAfter('2010-10-20'),	//true
			moment('2010-10-19').isSameOrAfter('2010-10-20'),	//false
		);

		//isBetween()	检查一个时间是否在其他两个时间之间
		console.log(
			moment('2010-10-20').isBetween('2010-10-19', '2010-10-25'),	//true
			moment('2010-10-20').isBetween('2010-10-19', undefined),	//true undefined等于moment(),就是当前的时间
			moment('2010-10-20').isBetween('2009-10-19', '2012-01-01', 'year'),	//true

			//第四个参数为包容性，第三个参数为null，表示对比单位为默认毫秒数
			moment('2016-10-30').isBetween('2016-10-30', '2016-12-30', null, '()'),	//false
		);

		//isLeapYear()	检测是否为闰年
		console.log(
			moment().isLeapYear(),	//true
			moment([2019]).isLeapYear(),	//false
		);

		//isMoment() 检测变量是否为moment对象
		console.log(
			moment.isMoment(),	//false
			moment.isMoment(new Date()),	//false
			moment.isMoment(moment()),	//true
		);

		//isDate()	检测变量是否为原生的Date对象
		console.log(
			moment.isDate(),	//false
			moment.isDate(new Date()),	//true
			moment.isDate(moment()),	//false
		);
## 国际化自定义
	//设置语言环境 (全局) 
		//moment.locale('zh-cn');
		console.log(moment.locale());	//en //返回当前的语言环境

		console.log(
			moment().weekday(0),	//根据语言环境获取或设置（传参）星期几。英文环境为星期天，中文环境为星期一
			moment().format('LLLL'),	//格式化时间，参数为本地化格式。英文环境与中文环境都不同
			
			moment().month(),
		);

		//设置语言环境 (局部) 
		var myMoment = moment();
		myMoment.locale('ar-dz');

		console.log(moment().format('LLLL'));
		console.log(myMoment.format('LLLL'));

		//months()/weekdays() 
		/* moment.locale('ru');
		moment.locale('zh-hk'); */
		console.log(
			moment.months(),
			moment.monthsShort(),
			moment.weekdays(),
			moment.weekdaysShort(),
			moment.weekdaysMin(),   //获取语言环境下的星期最小缩写数组
		);

		//localeData()
		console.log(
			moment.localeData(),
			moment.localeData().monthsShort(),
		);


		//自定义
		moment.updateLocale('zh-cn', {
			//设置月份名称
			months: '一月_二月_三月_四月_五月_六月_七月_八月_九月_十月_十一月_十二月'.split('_'),

			//设置月分名称的缩写
			monthsShort: '1月_2月_3月_4月_5月_6月_7月_8月_9月_10月_11月_12月'.split('_'),

			//设置星期名称
			weekdays: '星期日_星期一_星期二_星期三_星期四_星期五_星期六'.split('_'),

			//设置星期名称的缩写
			weekdaysShort: '周日_周一_周二_周三_周四_周五_周六'.split('_'),

			//设置星期名称的最小缩写
			weekdaysMin: '日_一_二_三_四_五_六'.split('_'),


			//设置长日期格式，是个对象
			longDateFormat: {
				LT: 'Ah点mm分',
				LTS: 'Ah点m分s秒',
				L: 'YYYY-MM-DD',
				LL: 'YYYY年MMMD日',
				LLL: 'YYYY年MMMD日Ah点mm分',
				LLLL: 'YYYY年MMMD日ddddAh点mm分',
				l: 'YYYY-MM-DD',
				ll: 'YYYY年MMMD日',
				lll: 'YYYY年MMMD日Ah点mm分',
				llll: 'YYYY年MMMD日ddddAh点mm分'
			},

			//设置相对时间，from()与to()的方法返回的值就是从这里取的
			relativeTime: {
				future: '%s内',
				past: '%s前~~~',
				s: '几秒',
				m: '1 分钟',
				mm: '%d 分钟',
				h: '1 小时',
				hh: '%d 小时',
				d: '1 天',
				dd: '%d 天',
				M: '1 个月',
				MM: '%d 个月',
				y: '1 年',
				yy: '%d 年'
			},

			//设置时间段，参数：小时,分钟,大小写
			meridiem: function (hour, minute, isLower) {
				const hm = hour * 100 + minute;
				if (hm < 600) {
					return '凌晨';
				} else if (hm < 900) {
					return '早上';
				} else if (hm < 1130) {
					return '上午';
				} else if (hm < 1230) {
					return '中午';
				} else if (hm < 1800) {
					return '下午@@@@';
				} else {
					return '晚上';
				}
			},

			//设置日历
			calendar: {
				sameDay: function () {
					return this.minutes() === 0 ? '[今天]Ah[点整]' : '[今天]LT';
				},
				nextDay: function () {
					return this.minutes() === 0 ? '[明天]Ah[点整]' : '[明天]LT';
				},
				lastDay: function () {
					return this.minutes() === 0 ? '[昨天]Ah[点整]' : '[昨天]LT';
				},
				nextWeek: function () {
					let startOfWeek, prefix;
					startOfWeek = moment().startOf('week');
					prefix = this.diff(startOfWeek, 'days') >= 7 ? '[下]' : '[本####]';
					return this.minutes() === 0 ? prefix + 'dddAh点整' : prefix + 'dddAh点mm';
				},
				lastWeek: function () {
					let startOfWeek, prefix;
					startOfWeek = moment().startOf('week');
					prefix = this.unix() < startOfWeek.unix() ? '[上]' : '[本]';
					return this.minutes() === 0 ? prefix + 'dddAh点整' : prefix + 'dddAh点mm';
				},
				sameElse: 'LL'
			},
			week: {
				dow: 1,	//星期的第一天是周1
				doy: 4
			}
		});

		console.log('今天是：' + moment().format('MMMM') + ' ' + moment().format('dddd'));
		console.log('今天是：' + moment().format('MMM') + ' ' + moment().format('ddd'));

		console.log(moment().format('LLLL'));

		console.log(moment([2008]).from());

		console.log(moment().calendar(moment([2020, 3, 15])));

## 时长方法
//时长
		console.log(moment.duration());

		console.log(
			moment.duration(100),//给一个参数表示为毫秒
			moment.duration(2, 'seconds'),//时长为2s
			moment.duration(3, 'minutes'),//时长为3min
			moment.duration(1, 'M'),
			
			//参数也可以是一个对象
			moment.duration({
				seconds: 1,
				minutes: 2,
				hours: 3,
				days: 4,
				weeks: 5,
				months: 6,
				years: 7
			}),

			//ASP.NET 风格的时间跨度
			moment.duration('23:59:59'),	//时:分:秒
		);

		//clone() 克隆一个时长对象
		var d1 = moment.duration();
		var d2 = d1.clone();
		d1.add(1, 'second');
		console.log(d1, d2);

		moment.locale('zh-cn');
		//humanize() 	显示一段时长
		console.log(
			moment.duration(1, 'minutes').humanize(),
			moment.duration(24, 'hours').humanize(),
			moment.duration(1, 'minutes').humanize(true),	//1 分钟内
			moment.duration(-1, 'minutes').humanize(true),	//1 分钟前
		);

		//milliseconds()	此方法会计算溢出
		//asMilliseconds()
		console.log(
			moment.duration(500).milliseconds(),	//500
			moment.duration(1500).milliseconds(),	//500
			moment.duration(15000).milliseconds(),	//0
			//moment.duration(1500)

			moment.duration(500).asMilliseconds(),	//500
			moment.duration(1500).asMilliseconds(),	//1500
			moment.duration(15000).asMilliseconds(),//15000
		);

		//seconds()
		//asSeconds()
		console.log(
			moment.duration(500).seconds(),		//0
			moment.duration(1500).seconds(),	//1
			moment.duration(15000).seconds(),	//15

			moment.duration(500).asSeconds(),	//0.5
			moment.duration(1500).asSeconds(),	//1.5
			moment.duration(15000).asSeconds(),//15
		);


		//add()	增加时长，这个方法可以添加多种类型的参数
		var a = moment.duration(1, 'd');	//时长为1天
		var b = moment.duration(2, 'd');	//时长为2天
		console.log(
			a.add(b).days(),
			moment.duration().add(1, 'd').days()	// 1
		);

		//subtract()	减少时长
		var a = moment.duration(3, 'd');
		var b = moment.duration(2, 'd');
		console.log(
			a.subtract(b).days(),	//1
			moment.duration(5, 'd').subtract(1, 'd').days()	//4
		);

		//duration(x.diff(y))	获取两个时长的差值
		var a = moment([2018, 10, 21, 10, 05]);
		var b = moment([2018, 10, 21, 10, 06]);
		console.log(
			moment.duration(b.diff(a)),
		);

		//as()
		console.log(
			moment.duration(1000).as('milliseconds'),//1000
			moment.duration(1000).as('seconds'),//1
		)

		//get()
		var d = moment.duration({
			seconds: 1,
			minutes: 2,
			hours: 3,
			days: 4,
			months: 5,
			years: 6
		});
		console.log(d);
		console.log(
			d.get('seconds'),
			d.get('minutes'),
			d.get('hours'),
			d.get('days'),
			d.get('months'),
			d.get('years'),
		)




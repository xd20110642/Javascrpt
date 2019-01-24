#文档对象(DOM) 浏览器对象(BOM)
1. 用HTML写的就是文档对象
2. window对象就是浏览器对象 cookie navigator 

#数据类型(基本数据类型与复杂数据类型)
1. 基本数据类型: Number String Boolean undefined null 
2. 对象 Obejct(Array,function)

		var a   => console.log(a)   undefined 定义了没有赋值就为undefined  未定义
		 "object"——如果这个值是对象或 null;
		null 被认为是一个空的对象引用  typeof null => object
3. 对null的详解(空的对象引用)
		
		var car=null;
		typeof car ==> object 		
4. 对布尔值的判断

	| 数据类型 | 转化为true | 转化为false |
	| ------ | ------ | ------ |
	| string | 任何非空字符串 | ""(空字符串) |
	| Number| 任何非零数字值(包括无穷大) | 0和NaN(参见本章后面有关NaN的内容) |
	|obejct|任何对象 |null
5. object对象类型
	1. 每一个对象都存在	**constructor** 构造函数  保存着用于创建当前对象的函数
	2. **hasOwnProperty(propertyName)**:用于检查给定的属性在当前对象实例中(而不是在实例 的原型中)是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式指定(例 如:o.hasOwnProperty("name"))。

			var obj={
	   		 key:123
			};
			obj.hasOwnProperty('key');                             //true
			obj.hasOwnProperty('hasOwnProperty');                  //false
#函数参数
##（在函数体内可以通过 arguments 对象来 访问这个参数数组，从而获取传递给函数的每一个参数。）
1. arguments对象只是与数组类似(它并不是Array的实例)，因为可以使用方括号语法访 问它的每一个元素(即第一个元素是 arguments[0]，第二个元素是 argumetns[1]，以此类推)，使用length属性来确定传递进来多少个参数。在前面的例子中，sayHi()函数的第一个参数的名字叫 name，而该参数的值也可以通过访问 arguments[0]来获取


			function howManyArgs() {
		    alert(arguments.length);
		}
		howManyArgs("string", 45);  //2
		howManyArgs();              //0
		howManyArgs(12);            //1
		
---
#变量
1. 基本类型:操作保存在变量中的实际的值
2. 引用类型:保存在内存中的对象   JavaScript 不允许直接访问内存中的位置， 也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。 为此，引用类型的值是按引用访问的。 **所以就存在浅拷贝和深拷贝的事情**
	
		var num1=5;   
		var num2=num1;
     	num2=4  不影响num1
![基本类型引用值](http://111.231.202.143/macdownimg/基本数据类型.png)
		
		var obj=new Object()
		var obj1=obj
		修改obj1的属性 就会影响到 obj
![对象引用](http://111.231.202.143/macdownimg/object.png)

		例如:
		 function addTen(num) {
        num += 10;
		return num; }
		
		var count = 20;
		var result = addTen(count); alert(count); //20，没有变化 alert(result); //30
基本类型 是不会改变的

			function setName(obj) {
		    obj.name = "Nicholas";
		}
		var person = new Object();
		setName(person);
		alert(person.name);    //"Nicholas"
引用类型 就会被改变

---
#object类型
1. **声明对象的方法**
	1. var xx=new Object()        2. var xx={name:1}
2. **Array类型**	
	1. 判断是不是数组 Array.isArray()
	2. push() 添加在末尾 返回新的长度
	3. pop()方法则从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项
	4. shit() 除数组中的第一个项并返回该项，同时将数组长度减 1
	5. unshit()组前端添加任意个项并返回新数组的长度
	6. sort()数组排序   [参考链接](http://www.w3school.com.cn/js/jsref_sort.asp)
	7. concat() 合并数组

			 var colors = ["red", "green", "blue"];
	    	var colors2 = colors.concat("yellow", ["black", "brown"]);
	    	alert(colors);     //red,green,blue
	    	alert(colors2);    //red,green,blue,yellow,black,brown
	8. 迭代方法
		1. every(**数组项的值，该项在数组中的位置,数组对象本身**):对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true;传入的函数必须对每一项都返回 true，这个方法才返回 true;
		
				 var numbers = [1,2,3,4,5,4,3,2,1];
			     var everyResult = numbers.every(function(item, index, array){
			         return (item > 2);
				});
				alert(everyResult); //false
		2. some（**数组项的值，该项在数组中的位置,数组对象本身**）对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。	只要传入的函数对数组中的某一项返回 true，就会返回 true
		
				 var someResult = numbers.some(function(item, index, array){
	         		return (item > 2);
					});
					alert(someResult); //true
		3. filter(**数组项的值，该项在数组中的位置,数组对象本身**)对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。   它利用指定的函数确定是否在返回的数组中包含某一项    **用于过滤数据**
		
				var numbers = [1,2,3,4,5,4,3,2,1];
				var filterResult = numbers.filter(function(item, index, array){
				    return (item > 2);
					 });
					alert(filterResult);//[3,4,5,4,3]
				
		4. map(**数组项的值，该项在数组中的位置,数组对象本身**) 对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组 <br>而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。
		
		
				var numbers = [1,2,3,4,5,4,3,2,1];
			    var mapResult = numbers.map(function(item, index, array){
			        return item * 2;
			    });
    			alert(mapResult);  //[2,4,6,8,10,8,6,4,2]
    			
---
#函数(function)   
<h6>函数的名字仅仅是一个包含指针的变量而已。因此，即使是 在不同的环境中执行，全局的 sayColor()函数与 o.sayColor()指向的仍然是同一 个函数。</h6>
1. 函数带括号和不带括号的区别
	
			funtion sum(){}
			
			var a=sum
			
		使用不带圆括号的函数名是访问函数指针，而非调用函数。此时，anotherSum 和 sum 就都指向了同一个函数，因此 anotherSum()也 可以被调用并返回结果
2. 把函数当值来传递
	
		 function add10(num){
        return num + 10;
		}
	    var result1 = callSomeFunction(add10, 10);
	    alert(result1);   //20
 		要访问函数的指针而不执行函数的话，必须去掉函数名后 面的那对圆括号。因此上面例子中传递给 callSomeFunction()的是 add10 而不 是执行它们之后的结果。
 		
3. 函数内部属性(arguments,this)与方法
	1. apply()和 call() bind();
	
		调用一个对象的一个方法，用另一个对象替换当前对象
		
		B.apply(A, arguments);即A对象应用B对象的方法。
		
		apply()方法接收两个参数:一个 是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是 Array 的实例，也可以是 arguments 对象
				
				function sum(num1, num2){
		   				 return num1 + num2;
				}
			function callSum1(num1, num2){
			<!--这个是 this调用sum 并且传入参数-->
			    return sum.apply(this, arguments);
			}
	![call与apply](http://111.231.202.143/macdownimg/call%E4%B8%8Eapply.png)	
		
			window.color = "red";
			var o = { color: "blue" };
			function sayColor(){
			    alert(this.color);
			}
			<!--sayColor的this通过bind绑定到了 o上面-->
			<!--this指向了sayColor上面-->![]()
			var objectSayColor = sayColor.bind(o);
			objectSayColor();    //blue
			
----
#Global类型（Global）
1. url编码方式
	1. encodeURI()主要用于整个 URI(例如，http://www.wrox.com/illegal value.htm)，而 encode-URIComponent()主要用于对 URI 中的某一段(例如前面 URI 中的 illegal value.htm)进行编码。 
	<br>它们的主要区别在于，encodeURI()不会对本身属于 URI 的特殊字符进行编码，例如冒号、正斜杠、 问号和井字号;而encodeURIComponent()则会对它发现的任何非标准字符进行编码
			
	![call与apply](http://111.231.202.143/macdownimg/编码.png)
	
---
#面向对象
1. 构造函数 创建对象
		
		funtion Person(){
			this.name=xxx
		}
		var a=new Person()
		使用new发生的事情
		(1) 创建一个新对象;
		(2) 将构造函数的作用域赋给新对象(因此 this 就指向了这个新对象);  constructor构造函数
		(3) 执行构造函数中的代码(为这个新对象添加属性);
		(4) 返回新对象。
2. 理解原型对象
	
	**所有原型对象都会自动获得一个 constructor (构造函数)属性，这个属性包含一个指向 prototype 属性所在函数的指针。**
3. 判断属性是在实例上还是在原型上
	
	使用 hasOwnProperty()方法可以检测一个属性是存在于实例中，还是存在于原型中。这个方法(不 要忘了它是从 Object 继承来的)只在给定属性存在于对象实例中时，才会返回 true。
		
		  function Person(){
   		 }
    	Person.prototype.name = "Nicholas";		var person1 = new Person();
		var person2 = new Person();
		alert(person1.hasOwnProperty("name"));  //false
		person1.name = "Greg";
		alert(person1.name); //"Greg"——来自实例 
		alert(person1.hasOwnProperty("name")); //true
4. 获取	可枚举的实例属性

	![枚举](http://111.231.202.143/macdownimg/枚举.png) 
		
5. 更简单的原型语法

		function Person(){
		}
		Person.prototype = {
			constructor:Person,
		    name : "Nicholas",
		    age : 29,
		    job: "Software Engineer",
		    sayName : function () {
		        alert(this.name);
		    }
		};		

---
#继承(在es6中 使用class语法糖可以完美的解决下面的继承的所有问题)			
1.  **所有引用类型默认继承object**
2. 确定原型和实例的关系
	
		instanceof 
		只要用这个操作符来测试实例与原型链中出现过的构造函数，结果就会返回 true
3. 经典继承(避免污染父类)
	
		funtion Person(){
		this.colors=['red','black']
		}		
		funtion Son(){
		// this.调用Person 而在这里this是window对象  那么就是 window.Perosn 是全局对象调用
			Person.call(this)
		}
		var son1=new Son()
		son1.colors.push('pink');//colors:['red','black','pink'];
		var son2=new Son();//colors:[‘red’,'black]
		
		---传递参数---
		
		funtion Person(name){
		this.name=name;
		this.colors=['red','black']
		}		
		funtion Son(){
		// 传递参数
			Person.call(this,'你好')
		}
		var son1=new Son()
		son1.colors.push('pink');//colors:['red','black','pink'];
		var son2=new Son();//colors:[‘red’,'black]
4. 创建对象
	
		 Object.create()。这个方法接收两个参数:一 个用作新对象原型的对象和(可选的)一个为新对象定义额外属性的对象。在传入一个参数的情况下， Object.create()与 object()方法的行为相同
		 var person={
		 	name:1,
		 	age:18
		 }
		 
		 var son=Obejct.create(person,{
		 time:10
		 })
		 son.tiem ===> 10	

---
#函数表达式
<h5>函数名带括号() 是返回执行的结果  不带括号是 指向定义函数的指针
	<br>
		funtion a(){
		}
	var b=a  ==> b指向的a函数的地址的指针<br>
	var c=a() ==》 c是等于a函数的执行结果
</h5>
1. 递归  一个函数通过名字调用自身的情况下构成的
2. 闭包 **是指有权访问另一个 函数作用域中的变量的函数**
	1. 创建闭包的方式有:在一个函数内部创建另一个函数  创建一个匿名函数
3. 匿名函数具有 全局性  **所以this通常指向 window全局对象**
	
		var name="xd";
		var object={
			name:'lwj',
			say:function(){
				return function(){//匿名函数 全局性 this指向window
					this.name;
				}
			}
		}
		//object.say() ==> 返回的是一个匿名函数 funtion(){ return this.name}
		//然后执行匿名函数 匿名函数 this指向 window
		object.say()() ==> xd  
4. ES5创建块级作用域方法使用的是 **立即执行函数** 在ES6中 可直接使用let 使用块级作用域变量
		
		//避免变量污染
		(function(){
			
		})();		
		将函数声明包含在一对圆括号中，表示它实际上是一个函数表达式。而紧随其后的另一对圆括号会立即调用这个函数	
		
		//常用于封装对象 类似jQuery 
		// // 封装私有化 变量  避免变量污染  xd是获取到立即执行函数的返回结果 也就是 xd={
    	//  name:name
    	//}   而且 调用函数 不带括号 就是 指向的该函数的指针 也就是地址 
		var xd=(function(){
			funtion name(){
				console.log(1)
			}		
			return{
				name:name
			}
		})();
		
---
#BOM(浏览器对象模型)
1. BOM核心是----window对象,在ES5中window对象和var声明的变量 全局对象 === 顶层对象
2. 窗口位置
	1. screenLeft 和 screenTop 属性，分别用于表示窗口相对于屏幕左边和上边的位置

3. location对象
	1. 	location.replace(‘http:xxx’)   不会生成历史记录

---
#DOM
1. 获取特性三个方法		**getAttribute()  setAttribute() removeAttribute()**

	1. 获取特性 getAttribute() 传递给 getAttribute()的特性名与实际的特性名相同,**也可以获取到自定义属性** 
			
			<div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr" my_special_attribute="hello!"	></div>
			
			因此要想得到 class 特性值，应 该传入"class"而不是"className"，
			var div = document.getElementById("myDiv");
			alert(div.getAttribute("id"));
			alert(div.getAttribute("class"));
			alert(div.getAttribute("title"));
			alert(div.getAttribute("lang"));
			alert(div.getAttribute("dir"));
			div.getAttribute("my_special_attribute")
	2. 设置特性 setAttribute() 参数:要设置的特性名和值  <br> 如果特性已经存在，setAttribute()会以指定的值替换现有的值;如果特性不存在，setAttribute() 则创建该属性并设置相应的值	
			
				div.setAttribute("id", "someOtherId");
   				 div.setAttribute("class", "ft");
	3. 删除样式 removeAttribute
	
			div.removeAttribute('class')	
2. 动态加载js css
			
			 function loadScript(url){
		        var script = document.createElement("script");
		        script.type = "text/javascript";
		        script.src = url;
		        document.body.appendChild(script);
		}
		然后，就可以通过调用这个函数来加载外部的 JavaScript 文件了:
		    loadScript("client.js");		
		    
		    
3. classLsit 操作		    
	![classList](http://111.231.202.143/macdownimg/classList.png)
4. 自定义属性
	
			<div id="myDiv" data-appId="12345" data-myname="Nicholas"></div>
			//本例中使用的方法仅用于演示
		var div = document.getElementById("myDiv");
		//取得自定义属性的值
		var appId = div.dataset.appId; var myName = div.dataset.myname;
		//设置值
		div.dataset.appId = 23456; div.dataset.myname = "Michael";
5. 设置样式
	
		
		对于使用短划线(分隔不同的词汇，例如 background-image)的 CSS 属性 名，必须将其转换成驼峰大小写形式，才能通过 JavaScript 来访问。
		z-index ===> style.zIndex	
6. 偏移量 offset  **用于做轮播的偏移计算的 常用 left和top   自读的**
	1. offsetHeight<br>
	  元素在垂直方向上占用的空间大小，以像素计。包括元素的高度、(可见的) 水平滚动条的高度、上边框高度和下边框高度
	2. offsetWidth:<br>元素在水平方向上占用的空间大小，以像素计。包括元素的宽度、(可见的)垂 直滚动条的宽度、左边框宽度和右边框宽度
	3. offsetLeft:<br>元素的左外边框至包含元素的左内边框之间的像素距离。
	4.  offsetTop:<br>元素的上外边框至包含元素的上内边框之间的像素距离。
7. 客户区 client **用于判断可视区域  自读   动条占用的空间不计算在内**
	1. clientWidth 属性是元素内容区宽度加 上左右内边距宽度
	2. clientHeight 元素内容区高度加上上下内边距高度
8. 滚动大小  scroll  **用于设置最小和最大高度  适用于超出一个屏幕显示的高度 目前我的理解范围内只能用于body对象才能实现**
	1. scrollHeight:在没有滚动条的情况下，元素内容的总高度。
	2. scrollWidth:在没有滚动条的情况下，元素内容的总宽度。
	3. scrollLeft:被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。 
	4. scrollTop:被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。
	
	**scrollWidth 和 scrollHeight 主要用于确定元素内容的实际大小**<br>
	**带有垂直滚动条的页面总高度就是 document.documentElement.scrollHeight**

	不包含滚动条的页面而言，scrollWidth 和 scrollHeight 与 clientWidth 和 clientHeight 之间的关系并不十分清晰  可以认为 近似相等
	
	document.body.scrollTop + document.documentElement.scrollTop;
		
9. 获取元素的大小和位置  getBoundingClientRect()
	
		left、top、right 和 bottom	
	![图片](https://pic1.zhimg.com/80/v2-641fabfd753a1fa5f4749cc8d72d61b0_hd.jpg)
	
---
#事件
1. 	事件冒泡   即事件开始时由最具体的元素(文档中嵌套层次最深的那个节点)接收，然后逐级向上传播到较为不具体的节点(文档)。
	
		 <!DOCTYPE html>
		    <html>
		    <head>
		        <title>Event Bubbling Example</title>
		    </head>
		    <body>
		        <div id="myDiv">Click Me</div>
		    </body>
		    </html>
		    
		    如果你单击了页面中的<div>元素，那么这个 click 事件会按照如下顺序传播: 
		    (1) <div>
			(2) <body>
			(3) <html>
			(4) document
	![冒泡](http://111.231.202.143/macdownimg/冒泡.png)
2. 事件捕获  是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。
		
	![捕获](http://111.231.202.143/macdownimg/捕获.png)
3. DOM事件流  	捕获 ==> 目标阶段  ==> 冒泡
	
		实际的目标(<div>元素)在捕获阶段不会接收到事件。这意味着在捕获阶段，
		事件从 document 到<html>再到<body>后就停止了。下一个阶段是“处于目标”阶段，
		于是事件在<div> 上发生，并在事件处理(后面将会讨论这个概念)中被看成冒泡阶段的一部分。然后，冒泡阶段发生， 事件又传播回文档。  
	![DOM事件流](http://111.231.202.143/macdownimg/DOM事件流.png)
4. 事件监听
	1. 事件就是用户或浏览器自身执行的某种动作。诸如 click、load 和 mouseover，都是事件的名字
	2. 响应某个事件的函数就叫做事件处理程序(或事件侦听器)。事件处理程序的名字以"on"开头
5. 事件监听和取消事件监听
	1. 用于处理指定和删除事件处理程序的操作:addEventListener() 和 removeEventListener(),接受三个参数
	2. **要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是true，表示在捕获 阶段调用事件处理程序;如果是false，表示在冒泡阶段调用事件处理程序。**
	3. 通过 addEventListener()添加的事件处理程序只能使用 removeEventListener()来移除,移除时传入的参数与添加处理程序时使用的参数相同。这也意味着通过addEventListener()添加的匿名函数将无法移除
			
				var handler = function(){
		        alert(this.id);
		    };
		    btn.addEventListener("click", handler, false);
			//这里省略了其他代码
			btn.removeEventListener("click", handler, false); //有效!
			
			handler 指向的是函数的指针地址
	
6. 事件对象 在触发 DOM 上的某个事件时，会产生一个事件对象 event，这个对象中包含着所有与事件有关的信息		
	
	![event](http://111.231.202.143/macdownimg/event.png)
	![event2](http://111.231.202.143/macdownimg/event2.png)
7. window对象事件
	1. onload事件 页面加载完毕事件
	2. unload事件	窗口卸载事件
	3. resize事件 当窗口或框架的大小变化时在 window 或框架上面触发
	4. scroll事件 当用户滚动带滚动条的元素中的内容时，在该元素上面触发
		
			在混 杂模式下，可以通过<body>元素的 scrollLeft 和 scrollTop 来监控到这一变化;
			而在标准模式下， 除 Safari 之外的所有浏览器都会通过<html>元素来反映这一变化
8. 焦点事件
	1. blur 失去焦点触发事件
	2. focus 获得焦点触发事件

---
#表单事件
1. 表单属性
	
		 acceptCharset:服务器能够处理的字符集;等价于 HTML 中的 accept-charset 特性。
		 action:接受请求的 URL;等价于 HTML 中的 action 特性。
		 elements:表单中所有控件的集合(HTMLCollection)。
		 enctype:请求的编码类型;等价于 HTML 中的 enctype 特性。
		 length:表单中控件的数量。
		 method:要发送的 HTTP 请求类型，通常是"get"或"post";等价于 HTML 的 method 特性。 		 name:表单的名称;等价于 HTML 的 name 特性。
		 reset():将所有表单域重置为默认值。
		 submit():提交表单。
		 target:用于发送请求和接收响应的窗口名称;等价于 HTML 的 target 特性。
2. 提交事件
	1. 通过submit()来完成
3. 选择框
	1. 选择框的value值
	
			 如果没有选中的项，则选择框的 value 属性保存空字符串。
			 如果有一个选中项，而且该项的 value 特性已经在 HTML 中指定，则选择框的 value 属性等于选中项的 value 特性。即使 value 特性的值是空字符串，也同样遵循此条规则。
			 如果有一个选中项，但该项的 value 特性在 HTML 中未指定，则选择框的 value 属性等于该项的文本。
			 如果有多个选中项，则选择框的 value 属性将依据前两条规则取得第一个选中项的值。
	!['选择框'](http://111.231.202.143/macdownimg/value.png)
	
---
#JSON对象
1. JSON.stringify()和 JSON.parse()。在最简单的情况下，这两个方法分别用于把 JavaScript 对象序列化为 JSON 字符串和把 JSON 字符串解析为原生 JavaScript 值
		
						
	
		
						
	
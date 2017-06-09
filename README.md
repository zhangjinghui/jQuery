# jQuery 笔记  

---

1. jQuery 的 **HelloWorld**！  
```js
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	
	//$(function(){}) 相当于 window.onload, 代码写在 {} 之间
	$(function(){
		//1. 选取 button: $("button")
		//2. 为 button 添加 onclick 响应函数: $("button").click(function(){})
		//代码编写在 function 的 {} 中. 
		$("button").click(function(){
			//3. 弹出 helloworld
			alert("helloworld");
		});
	})
	
</script>
```
2. **jQuery 对象** 与 **DOM 对象**  
 + jQuery 对象：对 DOM 对象的一个包装(DOM 对象数组)  
 + jQuery 对象不能使用 DOM 对象的方法；DOM 对象也不能使用 jQuery 对象的方法。  
 + 一个不成文的规定：如果获取的是 jQuery 对象，要在变量前加 $  
 + **jQuery 对象转换为 DOM 对象**：jQuery对象是一个数组，可以使用下标的方式获取 DOM 对象  
 + **DOM 对象转换为 jQuery 对象**：使用 $()包裹 DOM 对象即可。  

## 选择器 $()  
![选择器.jpg](https://ooo.0o0.ooo/2017/06/07/5937ba2eba385.jpg)  
**选择器包括**：基本选择器、层次选择器、过滤选择器（基本过滤、内容过滤、可见性过滤、属性过滤、子元素过滤、表单对象属性过滤）
1. **基本选择器**  
![图片1.png](https://ooo.0o0.ooo/2017/06/06/59361952581be.png)  
```html
<!-- 导入 jQuery 库 -->
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	
	$(function(){
		//1. 使用 id 选择器选择 id=btn1 的元素: $("#btn1")
		//2. 为选择的 jQuery 对象添加 onclick 响应函数: 
		// $("#btn1").click(function(){}), 响应函数的代码
		//写在 function(){} 的中括号中.
		$("#btn1").click(function(){
			$("#one").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$(".mini").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			$("div").css("background", "#ffbbaa");
		});
		$("#btn4").click(function(){
			$("*").css("background", "#ffbbaa");
		});
		$("#btn5").click(function(){
			$("span,#two").css("background", "#ffbbaa");
		});
	})

</script>

</head>
<body>		
<input type="button" value="选择 id 为 one 的元素" id="btn1" />
<input type="button" value="选择 class 为 mini 的所有元素" id="btn2" />
<input type="button" value="选择 元素名是 div 的所有元素" id="btn3" />
<input type="button" value="选择 所有的元素" id="btn4" />
<input type="button" value="选择 所有的 span 元素和id为two的元素" id="btn5" />
</script>
```
2. **层次选择器**  
![图片2.png](https://ooo.0o0.ooo/2017/06/06/593625162b1d0.png)
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">

	$(function(){
		
		$("#btn1").click(function(){
			$("body div").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$("body > div").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			$("#one + div").css("background", "#ffbbaa");
		});
		
		$("#btn4").click(function(){
			$("#two ~ div").css("background", "#ffbbaa");
		});
		$("#btn5").click(function(){
			$("#two").siblings("div").css("background", "#ffbbaa");
		});
		$("#btn6").click(function(){
			//以下选择器选择的是近邻 #one 的 span 元素, 若该span
			//和 #one 不相邻, 选择器无效. 
			//$("#one + span").css("background", "#ffbbaa");
			$("#one").nextAll("span:first").css("background", "#ffbbaa");
		});
		$("#btn7").click(function(){
			$("#two").prevAll("div").css("background", "#ffbbaa");
		});
		
	})

</script>
</head>
<body>		
<input type="button" value="选择 body 内的所有 div 元素" id="btn1" />
<input type="button" value="在 body 内, 选择子元素是 div 的." id="btn2" />
<input type="button" value="选择 id 为 one 的下一个 div 元素" id="btn3" />
<input type="button" value="选择 id 为 two 的元素后面的所有 div 兄弟元素" id="btn4" />
<input type="button" value="选择 id 为 two 的元素所有 div 兄弟元素" id="btn5" />
<input type="button" value="选择 id 为 one 的下一个 span 元素" id="btn6" />
<input type="button" value="选择 id 为 two 的元素前边的所有的 div 兄弟元素" id="btn7" />
```
### **过滤选择器**  
 + 过滤选择器主要是通过特定的过滤规则来筛选出所需的 DOM 元素, **该选择器都以 “:” 开头**  
 + 按照不同的过滤规则, 过滤选择器可以分为 **基本过滤**、 **内容过滤**、 **可见性过滤**、 **属性过滤**、 **子元素过滤** 和 **表单对象属性过滤** 选择器  

1. **基本过滤选择器**  
![图片1.png](https://ooo.0o0.ooo/2017/06/06/593669c66d5c5.png)  
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		function anmateIt(){
			$("#mover").slideToggle("slow", anmateIt);
		}
		anmateIt();
		
		$("#btn1").click(function(){
			$("div:first").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$("div:last").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			$("div:not(.one)").css("background", "#ffbbaa");
		});
		
		$("#btn4").click(function(){
			$("div:even").css("background", "#ffbbaa");
		});
		$("#btn5").click(function(){
			$("div:odd").css("background", "#ffbbaa");
		});
		$("#btn6").click(function(){
			$("div:gt(3)").css("background", "#ffbbaa");
		});
		
		$("#btn7").click(function(){
			$("div:eq(3)").css("background", "#ffbbaa");
		});
		$("#btn8").click(function(){
			$("div:lt(3)").css("background", "#ffbbaa");
		});
		$("#btn9").click(function(){
			$(":header").css("background", "#ffbbaa");
		});
		
		$("#btn10").click(function(){
			$(":animated").css("background", "#ffbbaa");
		});
		$("#btn11").click(function(){
			$("#two").nextAll("span:first").css("background", "#ffbbaa");
		});
		
	});
	
	
</script>
</head>
<body>		
<input type="button" value="选择第一个 div 元素" id="btn1" />
<input type="button" value="选择最后一个 div 元素" id="btn2" />
<input type="button" value="选择class不为 one 的所有 div 元素" id="btn3" />

<input type="button" value="选择索引值为偶数的 div 元素" id="btn4" />
<input type="button" value="选择索引值为奇数的 div 元素" id="btn5" />
<input type="button" value="选择索引值为大于 3 的 div 元素" id="btn6" />

<input type="button" value="选择索引值为等于 3 的 div 元素" id="btn7" />
<input type="button" value="选择索引值为小于 3 的 div 元素" id="btn8" />
<input type="button" value="选择所有的标题元素" id="btn9" />

<input type="button" value="选择当前正在执行动画的所有元素" id="btn10" />
<input type="button" value="选择 id 为 two 的下一个 span 元素" id="btn11" />
```
2. **内容过滤选择器**  
![图片1.png](https://ooo.0o0.ooo/2017/06/07/593797afb4d30.png)  
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		
		$("#btn1").click(function(){
			$("div:contains('di')").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$("div:empty").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			// 选取的是父 div
			$("div:has(.mini)").css("background", "#ffbbaa");
		});
		
		$("#btn4").click(function(){
			$("div:parent").css("background", "#ffbbaa");
			//$("div:not(:empty)").css("background", "#ffbbaa");
		});
		
	});
	
</script>
</head>
<body>		
<input type="button" value="选择 含有文本 'di' 的 div 元素" id="btn1" />
<input type="button" value="选择不包含子元素(或者文本元素) 的 div 空元素" id="btn2" />
<input type="button" value="选择含有 class 为 mini 元素的 div 元素" id="btn3" />
<input type="button" value="选择含有子元素(或者文本元素)的div元素" id="btn4" />
```
3. **可见性过滤选择器**  
![图片2.png](https://ooo.0o0.ooo/2017/06/07/59379b8b2295e.png)  
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		
		$("#btn1").click(function(){
			$("div:visible").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			//alert($("div:hidden").length);
			//show(time): 可以使不可见的元素变为可见, time 表示时间, 以
			//毫秒为单位
			//jQuery 的很多方法支持方法的连缀, 即一个方法的返回值来时调用该
			//方法的 jQuery 对象: 可以继续调用该对象的其他方法. 
			$("div:hidden").show(2000).css("background", 
					"#ffbbaa");
		});
		$("#btn3").click(function(){
			//val() 方法可以返回某一个表单元素的 value 属性值. 
			alert($("input:hidden").val());
		});
		
	});
	
</script>
</head>
<body>		
<input type="button" value="选取所有可见的  div 元素" id="btn1">
<input type="button" value="选择所有不可见的 div 元素" id="btn2" />
<input type="button" value="选择所有不可见的 input 元素" id="btn3" />
```
4. **属性过滤选择器**  
![图片3.png](https://ooo.0o0.ooo/2017/06/07/59379df6c60ac.png)  
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(function(){
		
		$("#btn1").click(function(){
			$("div[title]").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$("div[title='test']").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			//选取的元素中包含没有 title 的 div 元素. 
			$("div[title!='test']").css("background", "#ffbbaa");
		});
		
		$("#btn4").click(function(){
			$("div[title^='te']").css("background", "#ffbbaa");
		});
		
		$("#btn5").click(function(){
			$("div[title$='est']").css("background", "#ffbbaa");
		});
		$("#btn6").click(function(){
			$("div[title*='es']").css("background", "#ffbbaa");
		});
		$("#btn7").click(function(){
			$("div[id][title*='es']").css("background", "#ffbbaa");
		});
		
		$("#btn8").click(function(){
			$("div[title][title!='test']").css("background", "#ffbbaa");
		});
		
	})
</script>
</head>
<body>		
<input type="button" value="选取含有 属性title 的div元素." id="btn1"/>
<input type="button" value="选取 属性title值等于'test'的div元素." id="btn2"/>
<input type="button" value="选取 属性title值不等于'test'的div元素(没有属性title的也将被选中)." id="btn3"/>
<input type="button" value="选取 属性title值 以'te'开始 的div元素." id="btn4"/>

<input type="button" value="选取 属性title值 以'est'结束 的div元素." id="btn5"/>
<input type="button" value="选取 属性title值 含有'es'的div元素." id="btn6"/>
<input type="button" value="组合属性选择器,首先选取有属性id的div元素，然后在结果中 选取属性title值 含有'es'的 div 元素." id="btn7"/>
<input type="button" value="选取 含有 title 属性值, 且title 属性值不等于 test 的 div 元素." id="btn8"/>
```
5. **子元素过滤选择器**  
![图片4.png](https://ooo.0o0.ooo/2017/06/07/5937a12c39162.png)  
**注意**：获取子元素需要在 ： 前添加空格
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(document).ready(function(){
		
		$("#btn1").click(function(){
			//选取子元素, 需要在选择器前添加一个空格. 
			$("div.one :nth-child(2)").css("background", "#ffbbaa");
		});
		$("#btn2").click(function(){
			$("div.one :first-child").css("background", "#ffbbaa");
		});
		$("#btn3").click(function(){
			$("div.one :last-child").css("background", "#ffbbaa");
		});
		
		$("#btn4").click(function(){
			$("div.one :only-child").css("background", "#ffbbaa");
		});
		
	});
</script>
</head>
<body>		
<input type="button" value="选取每个class为one的div父元素下的第2个子元素." id="btn1"/>
<input type="button" value="选取每个class为one的div父元素下的第一个子元素." id="btn2"/>
<input type="button" value="选取每个class为one的div父元素下的最后一个子元素." id="btn3"/>
<input type="button" value="如果class为one的div父元素下的仅仅只有一个子元素，那么选中这个子元素." id="btn4"/>
```
6. **表单元素过滤选择器**  
![图片5.png](https://ooo.0o0.ooo/2017/06/07/5937a4e174217.png)  
```html
<script type="text/javascript" src="jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(function(){
		$("#btn1").click(function(){
			//使所有的可用的单行文本框的 value 值变为 尚硅谷
			alert($(":text:enabled").val());
			$(":text:enabled").val("尚硅谷");
		});
		$("#btn2").click(function(){
			$(":text:disabled").val("www.atguigu.com");
		});
		$("#btn3").click(function(){
			var num = 
				$(":checkbox[name='newsletter']:checked").length;
			alert(num);
		});
		
		$("#btn5").click(function(){
			//实际被选择的不是 select, 而是 select 的 option 子节点
			//所以要加一个 空格. 
			//var len = $("select :selected").length
			//alert(len);
			
			//因为 $("select :selected") 选择的是一个数组
			//当该数组中有多个元素时, 通过 .val() 方法就只能获取第一个被选择的值了. 
			//alert($("select :selected").val());
			
			//jQuery 对象遍历的方式使 each, 在 each 内部的 this 是正在
			//得到的 DOM 对象, 而不是一个 jQuery 对象
			$("select :selected").each(function(){
				alert(this.value);
			});
		});
		
		$("#btn4").click(function(){
			$(":checkbox[name='newsletter']:checked").each(function(){
				alert(this.value);
			});
		});
	})
</script>

</head>
<body>
<h3>表单对象属性过滤选择器</h3>
 <button id="btn1">对表单内 可用input 赋值操作.</button>
	 <button id="btn2">对表单内 不可用input 赋值操作.</button><br /><br />
 <button id="btn3">获取多选框选中的个数.</button>
 <button id="btn4">获取多选框选中的内容.</button><br /><br />
 <button id="btn5">获取下拉框选中的内容.</button><br /><br />
```
![图片6.png](https://ooo.0o0.ooo/2017/06/07/5937a74525a75.png)  
## jQuery 对象的几个方法  
 + **val()**:获取或设置表单元素的 value 属性值。  
 + **attr()**:和 val()方法类似。一个参数代表获取属性，两个参数代表为属性赋值。  
 + **each()**:对 jQuery 对象进行遍历，参数为 function ，函数内部的 this 是正在遍历的 DOM 对象，可对其进行包装。例如：$(this)  
 + **text()**:和 val() 方法类似。获取或设置元素结点的文本子节点的值  
 + **prevAll()**:之前的所有节点  
 + **nextAll()**:之后的所有节点  
 + **siblings()**:所有兄弟节点  
 + **$.trim()**:去除指定字符串的前后空格  
 + **parent()**:获取父节点 jQuery对象  
 + **find()**:获取子节点中符合表达式的 jQuery对象  
 + **is()**:判断给定对象是否符合参数选择器，返回逻辑值

## 补充  
1. jQuery 对象可进行隐式迭代，为 jQuery 对象添加事件，相当于为整个 DOM 数组隐式迭代添加事件(在 JS 中需要使用循环)  
2. each(function(){})是显示迭代，可为其响应函数添加 index 属性，获取正在遍历对象的索引  
3. defaultValue:DOM 对象的属性，可以获取表单默认值  
4. jQuery 对象的方法连缀:调用一个方法的返回值还是该对象  
```js
$("#addEmpButton").click(function(){
		 $("<tr></tr>").append("<td>" + $("#name").val() + "</td>")
		               .append("<td>" + $("#email").val() + "</td>")
		               .append("<td>" + $("#salary").val() + "</td>")
		               .append("<td><a href='deleteEmp?id=xxx'>Delete</a></td>")
		               .appendTo("#employeetable tbody")
		               .find("a")
			           .click(function(){
			            	   return removeTr(this)
		});
});
```

## 结点操作  
1. 查找结点：通过选择器查找 **元素结点** ，进而使用 **attr()**、**text()** 读写 **属性结点**、**文本结点**。  
```js
<script type="text/javascript" src="jquery-1.12.3.js"></script>
<script type="text/javascript">
	//测试使用 jQuery 操作文本节点, 属性节点. 
	//及查找元素节点

	$(function() {
		//1. 操作文本节点: 通过 jQuery 对象的 text() 方法
		alert($("#bj").text());
		$("#bj").text("尚硅谷");

		//2. 操作属性节点: 通过 jQuery 对象的 attr() 方法. 
		//注: 直接操作 value 属性值可以使用更便捷的 val() 方法. 
		alert($(":text[name='username']").attr("value"));
		$(":text[name='username']").attr("value", "尚硅谷");

	})
</script>
```
2. 创建结点：使用$(html)  
```js
// 返回对应结点的 jQuery对象
var $li = $("<li id='atguigu'>尚硅谷</li>");
```
3. 插入节点：(不仅可以插入，还具有移动结点的效果)  
![图片1.png](https://ooo.0o0.ooo/2017/06/08/5938d74765d57.png)
![图片2.png](https://ooo.0o0.ooo/2017/06/08/5938d74780a8d.png)  
```js
<script type="text/javascript" src="jquery-1.12.3.js"></script>
<script type="text/javascript">	
	$(function(){
		// 1. appendTo 和 append: 主语和宾语的位置不同:  
		$("<li id='atguigu'>尚硅谷</li>").appendTo($("#city");	
		$("#city").append("<li id='atguigu'>[尚硅谷]</li>");
	
		// 2. prependTo 和 prepend: 主语和宾语的位置不同: 
		$("<li id='atguigu'>尚硅谷</li>").prependTo($("#city"));
		$("#city").prepend("<li id='atguigu'>[尚硅谷]</li>");

		// 3. insertAfter 和 after: 主语和宾语的位置不同: 
		$("<li id='atguigu'>尚硅谷</li>").insertAfter($("#city"));
		$("#city").after("<li id='atguigu'>[尚硅谷]</li>");

		// 4. insertBefore 和 before: 主语和宾语的位置不同: 
		$("<li id='atguigu'>尚硅谷</li>").insertBefore($("#city"));
		$("#city").before("<li id='atguigu'>[尚硅谷]</li>");

	})
</script>
```
4. 删除节点  
 + **remove()**:删除当前节点及其所有子节点  
 + **empty()**：清空当前节点的后代节点  

```js
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">
	
	//测试使用 jQuery 删除节点
	$(function(){
		//1. 为 #city 的每一个 li 添加 click 响应函数: 点击时, li 被删除
		//$("#city li").click(function(){
		//	$(this).remove();
		//});
	
		//jQuery 对象的 remove() 方法: 将把 jQuery 对象对应的
		//DOM 节点直接删除. 
		$("#bj").remove();
		
		//2. 清空 #game 节点
		//jQuery 对象的 empty() 方法: 清空 jQuery 对象对应的 
		//DOM 对象的所有的子节点. 
		alert("要清空了!");
		$("#game").empty();
	})
</script>
```
5. 复制节点  
 + **clone()**：返回调用该方法的 jQuery对象的一个副本，该方法可选参数 true，表示克隆节点的同时，一并克隆事件。  
 + 克隆对象若有 id 属性，在克隆后需要修改。  

6. 替换节点  
 + **replaceAll()**:调用该方法的对象 替换 参数对象  
 + **replaceWith()**:参数对象 替换 调用该方法的对象  
 + 以上两个方法都返回被替换的对象  
 + 以上两个方法都有移动结点的功能  

```js
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(function(){
		//节点互换需要先克隆节点. 
		alert(1);
		var $bj2 = $("#bj").clone(true);
		var $rl = $("#rl").replaceWith($bj2);
		$("#bj").replaceWith($rl);
	})
</script>
```
7. *包裹结点*  
 + wrap():将每一个匹配元素单独包裹  
 + wrapAll():将所有匹配元素使用一个元素包裹  
 + wrapInner():将每一个匹配元素的子内容（包括文本结点）进行单独包裹  

```js
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">
	//测试使用 jQuery wrap, wrapAll, wrapInner
	$(function(){
		//包装 li 本身
		$("#game li").wrap("<font color='red'></font>");
		
		//包装所有的 li
		$("#city li").wrapAll("<font color='red'></font>");

		//包装 li 里边的文字. 
		$("#language li").wrapInner("<font color='red'></font>");
	})
</script>
```
## 属性操作  
1. 属性的获取、设置、删除
 + attr():获取或设置属性，一个参数是获取，两个参数是设置  
 + removeAttr():删除指定元素的指定属性  
 + jQuery中有很多方法都是一个方法实现获取和设置，例如:val()、text()、height()、width()、css()、html()  

2. **html()**:该方法用于获取指定元素内的html代码，相当于 js 中的 **innerHTML**  
3. **val()**:该方法可获取表单标签（文本框、下拉列表框、单选框）的value值，多选下拉列表框返回的是数组，但对于多选框只能返回第一个值。  
```js
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">

	$(function(){
		//1. 为 #address 添加 focus(获取焦点), blur(失去焦点) 响应函数
		$(":text").focus(function(){
			//2. 当获取焦点时, 若 #address 中是默认值
			//(defaultValue 属性, 该属性是 DOM 对象的属性), 就使其值置为 ""
			var val = $(this).val();
			
			if(val == this.defaultValue){
				$(this).val("");
			}
		}).blur(function(){
			//3. 失去焦点是, 若 #address 的值在去除前后空格后等于 ""
			//则为其恢复默认值. 
			var val = this.value;	
			if($.trim(val) == ""){
				this.value = this.defaultValue;
			}
		});
		
		$(":button:eq(3)").click(function(){
			$(":checkbox[name='c']").val(["check2", "check4"]);
		});
		
		$(":button:eq(4)").click(function(){
			//即便是为一组 radio 赋值, val 参数中也应该使用数组. 
			//使用一个值不起作用。 
			$(":radio[name='r']").val(["radio2"]);
		});
		
		$(":button:eq(5)").click(function(){
			//val() 可以直接获取 select 的被选择的值. 
			alert($("#single").val());
			alert($("#multiple").val());
			
			//val 不能直接获取 checkbox 被选择的值
			//若直接获取, 只能得到第一个被选择的值. 
			//因为 $(":checkbox[name='c']:checked") 得到的是一个
			//数组. 而使用 val() 方法只能获取数组元素的第一个值
			//若希望打印被选择的所有值, 需要使用 each 遍历. 
			//alert($(":checkbox[name='c']:checked").val());
			$(":checkbox[name='c']:checked").each(function(){
				alert(this.value);
			});
			
			//而 raido 被选择的只有一个, 所以可以直接使用 val() 方法. 
			alert($(":radio[name='r']:checked").val());
		});
		
	})

</script>
```
## CSS DOM 操作  
1. 样式操作  
 + 获取和设置 class：使用 attr() 方法  
 + 追加样式：addClass()  
 + 移除样式：removeClass()  
 + 切换样式：toggleClass()，如果类名存在则删除，如果不存在则添加  
 + 判断样式是否存在：hasClass()  

2. CSS-DOM 操作  
 + 设置元素样式属性：css()  
 + 设置元素透明度：opacity 属性  
 + 设置元素高度、宽度：height()、width()  
 + 获取元素在当前视窗中的相对位移：offset()  

```js
<script type="text/javascript" src="scripts/jquery-1.3.1.js"></script>
<script type="text/javascript">
	$(function(){
		
		//测试 jQuery 样式相关的方法. 
		
		//1. hasClass(): 某元素是否有指定的样式
		alert($("div:first").hasClass("SubCategoryBox")); //true
		
		//2. 移除样式
		$("div:first").removeClass("SubCategoryBox");
		
		alert($("div:first").hasClass("SubCategoryBox"));
		
		//3. 添加样式
		$("div:first").addClass("SubCategoryBox");
		
		//4. 切换样式: 存在, 则去除; 没有, 则添加. 
		$(".showmore").click(function(){
			$("div:first").toggleClass("SubCategoryBox");
			return false;
		});
		
		//5. 获取和设置元素透明度: opacity 属性
		alert($("div:first").css("opacity"));
		
		$("div:first").css("opacity", 0.5);
		
		//6. width 和 height
		alert($("div:first").width());
		alert($("div:first").height());
		
		$("div:first").width(400);
		$("div:first").height(80);
		
		//7. 获取元素在当前视窗中的相对位移: offset(). 
		//其返回对象包含了两个属性: top, left. 该方法只对可见元素有效
		alert($("div:first").offset().top);
		alert($("div:first").offset().left);
		
	});
</script>
```
## jQuery 中的事件  
1. js 中 **window.onload=function(){}** 与 jQuery 中 **$(document).ready(function(){})** 的区别  
![图片1.png](https://ooo.0o0.ooo/2017/06/09/593a36e164154.png)  
2. 事件绑定 bind("chick",function(){}) 可动态绑定事件  
3. 合成事件  
 + hover()：模拟光标悬停事件。光标移入元素，执行第一个函数，移出时执行第二个函数  
 + toggle():模拟鼠标连续单击事件。单击一次，执行第一个函数，单击两次执行第二个...，循环往复（toggle() 还可以用于切换元素的可见状态）  

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Untitled Document</title>
		<link href="css/style.css" type="text/css" rel="stylesheet" />
		<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
	
		<script type="text/javascript">
			//为 .head 添加 Onclick 响应函数: 若 .content 隐藏则显示, 若 .content 显示, 则隐藏
			$(function(){
				/*
				$(".head").click(function(){
					//使用 is() 方法, 来判断某个给定的 jQuery 对象是否符合指定
					//的选择器. 
					var flag = $(".content").is(":hidden");
					
					if(flag){
						//show() 方法: 使隐藏的变为显示
						$(".content").show();
					}else{
						$(".content").hide();
					}
				});
				*/
				
				//bind: 为某 jQuery 对象绑定事件. 
				/*
				$(".head").bind("click", function(){
					//使用 is() 方法, 来判断某个给定的 jQuery 对象是否符合指定
					//的选择器. 
					var flag = $(".content").is(":hidden");
					
					if(flag){
						//show() 方法: 使隐藏的变为显示
						$(".content").show();
					}else{
						$(".content").hide();
					}
				});
				*/
				
				//mouseover: 鼠标移上去
				//mouseout: 鼠标移出. 
				/*
				$(".head").mouseover(function(){
					$(".content").show();
				}).mouseout(function(){
					$(".content").hide();
				});
				*/
				
				//合成事件: hover: 鼠标移上去执行第一个函数, 移出执行第二个函数. 
				/*
				$(".head").hover(function(){
					$(".content").show();
				}, function(){
					$(".content").hide();
				});
				*/
				
				//合成事件: toggle: 第一次点击执行第一个函数, 第二次点击执行第二个
				//函数 ... 循环执行. 
				$(".head").toggle(function(){
					$(".content").show();
				}, function(){
					$(".content").hide();
				});
			})
		</script>
	
	</head>
	<body>
		<div id="panel">
			<h5 class="head">什么是jQuery?</h5>
			<div class="content">
				jQuery是继Prototype之后又一个优秀的JavaScript库，它是一个由 John Resig 创建于2006年1月的开源项目。jQuery凭借简洁的语法和跨平台的兼容性，极大地简化了JavaScript开发人员遍历HTML文档、操作DOM、处理事件、执行动画和开发Ajax。它独特而又优雅的代码风格改变了JavaScript程序员的设计思路和编写程序的方式。
			</div>
		</div>
	</body>

</html>
```
4. **事件冒泡**:若父节点与子节点都绑定了同一事件，当操作子节点时，事件会按照 DOM 层次结构，像水泡一样不断向上级传递。  
阻止事件冒泡的方法：在事件处理函数中返回 false（return false 还可以停止元素的默认行为，例如：超链接、提交按钮)  
```js
<script type="text/javascript" src="../scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">

	$(function(){
		//事件的冒泡: 什么是事件的冒泡
		$("body").click(function(){
			alert("body click");
		});
		
		$("#content").click(function(){
			alert("div click");
		});
		
		$("span").click(function(){
			alert("span click");
			//如何解决事件的冒泡: 通过在响应函数的结尾返回 false, 可以阻止冒泡. 
			return false;
		});
	})
</script>
```
5. **事件对象** 的属性  
为事件函数添加一个参数，即可在函数中访问事件对象。常用属性 event.pageX、event.pageY，分别表示发生事件时，光标相对于页面的坐标值  
```js
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">

	/*
	1. 事件: 当鼠标移动时, 就会触发 mousemove 事件. 
	2. 如何得到事件对象: 在响应函数中添加一个参数就可以. 
	3. 事件对象的两个属性: pageX,pageY
	*/
	$(function(){
		//事件的 pageX, pageY 属性
		$("body").mousemove(function(obj){
			$("#msg").text("x: " + obj.pageX 
					+ ", y: " + obj.pageY);
		});
	})

</script>
```
6. **移除事件**  
 + $("btn").unbind("click"):移除指定事件  
 + $("btn").unbind()：移除所有事件  
 + one("click",function(){}) 与 bind() 的区别是，one() 绑定的事件触发一次后就会失效  

```html
<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
<script type="text/javascript">
	//测试移除事件: 使用 unbind 移除事件. 
	//one(): 只为某一个元素添加一次事件, 事件函数响应后, 将不再被触发响应. 
	$(function(){
		
		$("#rl").one("click", function(){
			alert("红色警戒. ");
		});
		
		$("li:not(#rl)").click(function(){
			alert(this.firstChild.nodeValue);
			
			//对于 #bj 节点, 点击一次后, 就没有 click 响应函数了
			if(this.id == "bj")
				$("#bj").unbind("click");
		});
	})
</script>
```
## jQuery 中的动画  
 + hide():隐藏元素，相当于.css("display", "none")  
 + show():显示元素  
 + 以上两个方法可设置变化时间毫秒数（默认立即变化），会同时增大（或减少）元素的高度、宽度、不透明度  
 + fadeIn():提高不透明度，可指定变化时间参数  
 + fadeOut():降低不透明度，可指定变化时间参数  
 + slideDown():由上至下，延伸显示  
 + slideUp():由下至上，缩短隐藏  
 + toggle():切换元素可见状态  
 + slideToggle():通过高度变化，切换可见状态  
 + fadeToggle():通过不透明度变化，切换可见状态  
 + fadeTo():参数取值范围（0~1），适用于以渐进的方式调整不透明度  

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Untitled Document</title>
		<link href="css/style.css" type="text/css" rel="stylesheet" />
		<script type="text/javascript" src="scripts/jquery-1.7.2.js"></script>
	
		<script type="text/javascript">
			//演示动画效果: show() 和 hide() 方法中传入毫秒数以达到动画的效果
			/*
			$(function(){ 
				$(".head").toggle(function(){
					$(".content").show(1000);
				}, function(){
					$(".content").hide(1000);
				});
			})
			*/
			
			//只改变高度
			/*
			$(function(){ 
				$(".head").toggle(function(){
					$(".content").slideDown(500);
				}, function(){
					$(".content").slideUp(500);
				});
			})
			*/
			
			//只改变透明度
			/*
			$(function(){ 
				$(".head").toggle(function(){
					$(".content").fadeIn(1000);
				}, function(){
					$(".content").fadeOut(1000);
				});
			})
			*/
			
			//toggle() 可以切换元素的可见状态. 
			//slideToggle(): 通过高度变化来切换匹配元素的可见性
			//fadeToggle(): 通过透明度来切换元素的可见性.
			//fadeTo(): 把不透明度以渐近的方式调整到指定的值 (0 – 1 之间). 
			$(function(){ 
				$(".content").show();
				var i = 1; 
				
				$(".head").click(function(){
					//$(".content").toggle();
					//$(".content").slideToggle();
					//$(".content").fadeToggle();
					
					$(".content").fadeTo("slow", i);
					i = i - 0.1;
				});
			})
		</script>
	</head>
	<body>
		<div id="panel">
			<h5 class="head">什么是jQuery?</h5>
			<div class="content">
				jQuery是继Prototype之后又一个优秀的JavaScript库，它是一个由 John Resig 创建于2006年1月的开源项目。jQuery凭借简洁的语法和跨平台的兼容性，极大地简化了JavaScript开发人员遍历HTML文档、操作DOM、处理事件、执行动画和开发Ajax。它独特而又优雅的代码风格改变了JavaScript程序员的设计思路和编写程序的方式。
			</div>
		</div>
	</body>
</html>
```

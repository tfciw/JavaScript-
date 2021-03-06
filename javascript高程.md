<style type="text/css">
	strong {
		color: red
	}
</style>
<h1>ECMAScript基础</h1>
<p>原始值：是存储在栈的数据段，简单（变量访问的位置就是值）。</p>
<p>引用值：存储在堆里面的数据，变量访问的位置是在堆里的指针。</p>
<p>原始类型：undefined null number string Boolean。</p>
<p>typeof 运算符（var也是运算符，用于申明变量的运算符）返回的只有五种值:undefined number string Boolean object。</p>
<p>null为什么会返回对象，这是javascript最开始的一个错误，es沿用了下来，定义为是对象的占位符。</p>
<p><strong>只有typeof运算符可以对未申明的变量做运算，会返回undefined<em style="color:blue">(其实&&也可以，只是有特定条件)</em></strong></p>
<p><strong>函数如果没有返回值，用typeof运算符也是返回undefined。</strong></p>
<p>string是唯一没有固定大小的原始类型</p>
<p>强制类型转换String(null)->'null' null.toSrting() -> runtime error </p>
<p>
<pre>
var a = new Boolean(false)
var a = false
console.log(a && true)
//如果是用的实例化一个boolean对象，去判断的话会返回真，因为对象在boolean运算是作为真
//如果是赋值一个原始类型的boolean值，则会返回false
</pre>
</p><hr>
<p>
<pre>
var a = new Number(0)//->true
var a = 0	//-> 0
console.log(a && true)
//同理实例化的是一个对象boolean运算符吧对象当做真
</pre>
</p><hr>
<p>
	toFixed() 方法，返回number类型的几位小数点,15.toFixed(2) -> 15.00
</p>
<p>substring() slice() 两种从字符串中截取字串的方法<strong>一定要注意substring都是小写</strong>，如果只传入一个参数，默认第二个参数是字符串的长度，如果第二个参数是负数，那么slice将长度加上第二个参数当成第二个参数，substring会当成0处理</p>
<p><strong>substring(2,0)实际上是substring(0,3)，因为substring总是把小的数字作为起始位</strong></p>
<p><h2>instanceof 运算符</h2></p>
<p>实例化的对象呗typeof返回都是object，只有instance能返回具体的类型</p>
<pre>
var a = new Array
console.log(a instanceof Array) // true	
var a = new Array
if(a instanceof Array) {
    console.log('array')
}
</pre><hr>
<h2>++a a++ 前增量运算符 和后增量运算符 </h2>
<p>
<pre>
var a = 1
console.log(++a) -> 2
console.log(a++) -> 1
虽然a的值都被改变了，但是在进行增的那条语句，前增量是运算发生在表达式之前，后增量是发生在表达式之后
</pre>
</p><hr>
<h2>位运算符 ~ </h2>
<pre>
var a = 5 //要想获得-6，该怎样计算
var b = - a - 1 //一元运算符

var a = 5 //要想获得-6，该怎样计算
var b = ~a
//这两种方法都一样
</pre>
<h2>布尔运算符</h2>
<p>
	&&：左边为真返回右边，左边为假，返回左边
	||：相反
</p>
<h2>== 运算符</h2>
<p>
	undefined == null  -> true <br>
	undefined 和 null进行运算是不会转换为任何值 <br>
	boolean值会转为数字 true -> 1 false -> 1 <br>
</p>
<h2>函数执行过return语句后会停止执行代码，也就是说return语句后的代码都不会被执行</h2>
<h2>函数无重载</h2>
<h2>函数的arguments对象，可以模拟函数重载</h2>
<pre>
function a() {
	if(arguments.length === 1) {
		console.log(arguments[0])
	}
	if(arguments.length === 2) {
		console.log(arguments[0] + arguments[1])
	}
}
</pre><hr>
<h2>函数也是一种类，对象，也就是说他们是引用类型，变量存储的只是值得指针，那么也就可以解释为什么函数无重载，因为修改了指针的指向，同时用new来申明函数会比普通的方式慢一些。</h2>
<h2><strong>函数下面有length属性，返回的是参数的个数</strong></h2>
<pre>
var a = function() { }
console.log(a.hasOwnProperty('length')) // -> true 0
console.log(a.hasOwnProperty('arguments')) // -> true null
</pre>
<h2>什么叫闭包？</h2>
<p>
	不整那些没用的，一句话，在函数内部使用了外部的变量就是闭包
<pre>
var z = 1
function a() {
	console.log(a)  //这就是一个简单地闭包
}

//在函数内部定义一个闭包函数会更复杂
function b(x, y) {
	function c() {
		return x + y
	}
	return c()	
}
//在函数c里调用了外部的变量，这会让js的垃圾回收机制（标记清除）以为变量
</pre>
</p>
<hr>
<h1>对象基础</h1>
<h2>申明一个array对象</h2>
<pre>
// var a = new Array(20) // -> 20 
var a = new  Array('20') // -> 1 
console.log(a.length)
</pre><hr>
<h2>字符串 数组的一些容易混淆的方法</h2>
<p>
	slice 是字符串的 用于截取字符串的字串 substring
	split 将字符串分割成数组<strong>split不传参数 和传一个空参数是不一样的split() != split('') </strong>
<pre>
var a = '1,2'
var b = a.split(',')
console.log(b) // -> ['1','2']
</pre><hr>
	join 用符号链接数组的每一项
<pre>
var a = [1,2]
var b = a.join('-')
b -> 1-2
</pre><hr>
	splice 用于删除数组项 或添加数组项 <strong>返回的是删除的项！！！</strong>
<pre>
</pre>
</p>
<h2>栈 队列</h2>
<p>
	push，pop 栈操作
	push：添加，pop：取出，弹出
	想象一叠盘子，取（加）盘子肯定只能从最上面取
	shift，unshift 队列操作
	shift：删除，取出，unshift：添加
	想象排队，肯定是先排队的先办完事
</p>
<h2>reverse 将数组翻转顺序 sort 排序</h2>
<strong>只有数组有该方法，字符串没有</strong>
<h2>Date()</h2>
<pre>
var a = new Date() //实例化一个时间对象
a.getTime() //获取时间戳 毫秒
setTime() //设置时间戳 毫秒
toLocaleString() //转为当地时间
toLocaleDateString() //转为当地时间日期
toLocaleTimeString() //转为当地时间时分秒
getFulleYrar() 
getMonth()
getDate() //第几天
getDay() //星期几
getHours() //复数的形式获取
getMinutes() //复数的形式获取
getSeconds() //复数的形式获取
</pre>
<h2>关键字this</h2>
<p>
	在js中关键字this总是指向调用该方法的对象
	例如
<pre>
var obj = {}
obj.color = 'red'
obj.function = function() {
	console.log(this.color)
}
obj.function() // -> red
//假如没有指向this。单纯的console.log(color) 会报错，color未定义
<strong>
一般都是在方法（function）里出现this，那么this指向的就是调用该方法的对象，这里的方法不是this，是function，即调用该方法的对象。
</strong>
</pre><hr>
</p>
<h2>创建对象 - 工厂方式</h2>
<p>
<pre>
var fMan = function(age, hight, weight) {
	var tempMan = {}
	tempMan.age = age
	tempMan.hight = hight
	tempMan.weight = weight
	tempMan.showInfo = function() {
		console.log(this)
	}
	return tempMan
}
var Adon = fMan(25, 1.78, 68)
Adon.showInfo()
</pre><hr>
</p>
<h2>URI编码</h2>
<hr>
<h2>BOM下的document对象</h2>
<p>
	alinkColor：激活的链接的颜色，lastModified：最后的修改时间，
</p>
<h2>Math 内置函数</h2>
<p>
	Math.random() //返回0-1（不包含）的数字
<pre>
var a = Math.random()
console.log(a.toFixed()) //返回0或者1 这是取小数点的 如果为空就是取整数位，会默认执行一次Math.random操作
console.log(a.toFixed(2)) // 返回0.XX
Math.floor(a) // 返回0 向下取整
Math.ceil(a) // 返回1 向上取整
</pre><hr>
</p>
<h2>new 运算符</h2>
<p>
当代码 new Foo(...) 执行时：<br>
1，一个新对象被创建。它继承自Foo.prototype。<br>
2，使用指定的参数调用构造函数Foo，并将 this绑定到新创建的对象。new Foo 等同于 new Foo()，只能用在Foo 不传递任何参数的情况。<br>
3，如果构造函数返回了一个“对象”，那么这个对象会取代整个new出来的结果。如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象。（一般情况下构造函数不返回任何值，不过用户如果想覆盖这个返回值，可以自己选择返回一个普通对象来覆盖。当然，返回数组也会覆盖，因为数组也是对象。）
</p>
<h1>性能优化 - 字符串的拼接</h1>
<p>
	一般而言我们用 + 做字符串拼接，如
<pre>
var a = '1'
var b = '个'
console.log(a + b) // '1个'
实际上简单地字符串拼接却做了很多动作
1，创建一个a字符串，哪怕没有申明变量，也会创建一个字符串来存储 '1' 
2，创建一个b字符串，同理
3，创建一个空字符串，用于存储结果
4，把a的值存储到结果
5，把b存储到结果
(如果还需要将结果赋值给另一个变量或者a，b则还会执行一步更新操作)
</pre><hr>
</p>
<h2>通过原型给String定义一个方法</h2>
<pre>
var a = []
// console.log(a.hasOwnProperty('indexOf')) // -> false 数组没有该方法
a = ['1', 2, '3', 'a']
Array.prototype.indexOf = function(vItem) {
	for(var i=0; i< this.length; i++) {
		if(this[i] === vItem ) {
			return i
		}
	}
	return -1
} 
console.log(a.indexOf('a'))
</pre><hr>
<h2>修改对象下的原型的方法</h2>
<p>
	同理，问题：如果在另一个地方需要用到原始方法，则会失败。<br>
	我们知道函数是对象的一种，对他的引用是对其指针的存储，一旦修改引用该指针的变量，则该函数没有引用的话则会被垃圾回收机制回收。所以保险起见先定义个originToString方法指向原始方法，再修改这个方法
</p>
<h1>事件</h1>
<h2>事件流 - 冒泡型事件 以及 捕获型事件</h2>
<h2>事件监听函数</h2>
<p>
	分配方式：html javascript;<br>
	分配在javascript中必须全部小写
<pre>
obj.onclick = function() {
	fn.body....
}
</pre><hr>
	分配在html中可小写onclick, 大写 ONCLICK, 驼峰 onClick, 类匈牙利 OnClick.
</p>
<h2>IE 中事件绑定的方法</h2>
<p>
	attachEvent 添加事件
<pre>
obj.attachEvent('onclick', fn)
obj.onclick = function() {}
//这两者等价的
obj.detachEvent('obclick', fn) // 解除事件
</pre><hr>
</p>
<h2>DOM 分配事件和移出事件的方法</h2>
<p>
	addEventListener() // 绑定 <br>
	removeEventListener() // 移除 <br>
<pre>
obj.addEventListener('onclick', fn, isTrue)
//第一个参数监听的事件名，第二个参数是处理的方法或者其指针，第三个是一个boolean值，true用作捕获阶段，false则是冒泡，默认是false（冒泡）
<strong>如果事件是以false的方式绑定，那么同样需要一false的方式解除，如果参数不一样不会报错，只是不会真正的移除该事件</strong>
</pre><hr>
</p>
<h2>事件对象</h2>
<p>
	包含的信息：<br>
	1，引起事件的对象 <br>
	2，事件发生时鼠标的信息 <br>
	3，事件发生时键盘的信息 <br>
	<strong>事件对象只有发生时才被创建，事件执行完毕会销毁事件对象</strong>
</p>
<h2>IE的事件对象</h2>
<p>
	window.event 尽管是window的属性，可是还是只能在事件发生时访问，事件执行完毕会销毁。<br>
	为什么在高级浏览器（dom）访问对象只需传递一个参数即可
<pre>
document.body.onclick = function(e) {
	console.log(e)
}
//不管是传的e还是oEvent都能获取到，因为 e = arguments[0]
document.body.onclick = function(oEvent) {
	console.log(oEvent) //或者传递a，都行的
}
</pre><hr>
</p>
<h2>关于事件对象的属性以及方法（IE，DOM）</h2>
<p>
<pre>
|----------------------IE--------------------------
cancelBubble	boolean 是否阻止事件向上冒泡
clietX			int 	鼠标在客户端区域的x坐标
clietY			int 	鼠标在客户端区域的y坐标
ctrlKey 		boolean 是否按下ctrl键
shiftYey 		boolean 是否按下shift键
keyCode			int 	keydown/keyup 按钮按下的unicode编码
offsetX			int 	鼠标相对于引起引起事件对象的x坐标
offsetY			int 	鼠标相对于引起引起事件对象的y坐标
screenX 		int 	鼠标相对于屏幕的x坐标
screenY 		int 	鼠标相对于屏幕的y坐标
srcElement		element 引起事件的对象
type			string	事件名称
|----------------------DOM--------------------------
cancelBubble	boolean 事件冒泡是否被取消
clietX			int 	鼠标在客户端区域的x坐标
clietY			int 	鼠标在客户端区域的y坐标
screenX 		int 	鼠标相对于屏幕的x坐标
screenY 		int 	鼠标相对于屏幕的y坐标
detail 			int 	鼠标点击的次数
ctrlKey 		boolean 是否按下ctrl键
shiftYey 		boolean 是否按下shift键
stopPropagation function调用该方法可阻止冒泡事件
tarket 			element 引起事件的对象
type			string	事件名称
</pre><hr>
</p>
<h2>关键键盘码keyCode （相同之处）</h2>
<pre>
window.addEventListener('keydown', function(e) {
	console.log(String.fromCharCode(e.keyCode).toLowerCase())
})
//如何知道我按的是哪个键，将keyCode在用字符串的String.fromCharCode方法返回（大写）
</pre><hr>
<h2>组织事件的默认行为（不同之处）</h2>
<p>
	ie: oEvent.returnValue = fasle  <br>
	dom: oEvent.preventDefault()
</p>
<h2>停止事件冒泡</h2>
<p>
	ie：oEvent.cancelBubble = true <br>
	dom：oEvent.stopPropagation()
</p>
<h1>高级DOM编程技术</h1>
<h2>obj.style</h2>
<p>
	obj.style.backgroundColor = 'red'，能够通过对象下面的style对象来获取或是设置属性，不过他获取的是内联样式，不能获取到css规则 <br>
	那么document.styleSheets[0].cssRules || document.styleSheets[0].rules可以获取到css规则
</p>
<h2>获取表单</h2>
<pre>
docuemnt.getElementById('form') //需要在html给form绑定id
docuemnt.getElementByTagName('form')[0] //以标签名的方式获取（数组）
docuemnt.forms[0] //直接获取到表单（数组），类似上面的方法
</pre>
<h2>获取表单项</h2>
<pre>
console.log(document.forms[0].input1 == document.forms[0][0]) // => true
通过name属性或者length去筛选
</pre>
<h1>拖拽</h1>
<h1>Error</h1>
<h2>取出错误信息</h2>
<pre>
window.onerror = function(sMessage, sUrl, sLine) {
	console.log(sMessage + sUrl + sLine)
	return true
}
//一定要返回true才不会执行浏览器默认的报错
</pre>
<h2>try-catch-finally</h2>
<pre>
try {
	notExistFn() //执行发现错误立即退出try
	console.log('error') //并不会执行
} catch (error) {
	console.log('错误原因：' + error) // 错误原因：ReferenceError: notExistFn is not defined
} finally {
	console.log('finally') //finally
}
</pre>
<h2>throw与try-catch的结合组装error</h2>
<pre>
function fnError() {
	if(arguments.length < 2) {
		throw '参数要大于2个'
		return
	}
	console.log('fnError')
}
try {
	fnError()
} catch (e) {
	console.log(e)
}
</pre>
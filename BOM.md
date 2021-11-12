# BOM

浏览器对象模型

​    \*  - BOM可以使我们通过JS来操作浏览器，在BOM中为我们提供了一组对象，用来完成对浏览器的操作

## BOM对象

Window

​    \*    - 代表的是==整个浏览器的窗口==，同时window也是==网页中的全局对象==

 Navigator

​    \*    - 代表的==当前浏览器的信息==，通过该对象可以来识别不同的浏览器

Location

​    \*    - 代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面

History

​    \*    - 代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录

​    \*     由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器==向前或向后翻页==，而且该操作==只在当次访问时有效==    【浏览器关闭之后，无法访问上次的信息】

Screen     【很少用，移动端可能会用，pc端很少用】

​    \*    - 代表用户的屏幕的信息，通过该对象可以获取到用户的==显示器的相关的==信息

这些BOM对象在浏览器中都是作为window对象的属性保存的，可以通过window对象来使用，也可以直接使用

## Navigator

​    \*  - 代表的当前浏览器的信息，通过该对象可以来==识别不同的浏览器==

​    \*  - 由于历史原因，Navigator对象中的大部分属性都已经不能帮助我们识别浏览器了，一般我们只会使用==userAgent==来判断浏览器的信息， userAgent是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，不同的浏览器会有不同的userAgent

![image-20211018203631953](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211018203631953.png)

火狐的userAgent

​    \*  Mozilla/5.0 (Windows NT 6.1; WOW64; rv:50.0) Gecko/20100101 ==Firefox==/50.0

Chrome的userAgent

​    \*  Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) ==Chrome==/52.0.2743.82 Safari/537.36

IE8

​    \*  Mozilla/4.0 (compatible; ==MSIE== 8.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)

IE9

​    \*  Mozilla/5.0 (compatible; ==MSIE== 9.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)

IE10

​    \*  Mozilla/5.0 (compatible; ==MSIE== 10.0; Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)

IE11

​    \*  Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; rv:11.0) like Gecko

​    \*  - 在IE11中已经将微软和IE相关的标识都已经去除了，所以我们基本已经不能通过UserAgent来识别一个浏览器是否是IE了

 \* 如果通过UserAgent不能判断，还可以通过一些浏览器中特有的对象，来判断浏览器的信息

​    \* 比如：ActiveXObject

~~~js
			if(/firefox/i.test(ua)){
				alert("你是火狐！！！");
			}else if(/chrome/i.test(ua)){
				alert("你是Chrome");
			}else if(/msie/i.test(ua)){
				alert("你是IE浏览器~~~");
			}else if("ActiveXObject" in window){
				alert("你是IE11，枪毙了你~~~");
			}

			if("ActiveXObject" in window){
				alert("你是IE，我已经抓住你了~~~");
			}else{
				alert("你不是IE~~~");
			}
			alert("ActiveXObject" in window);
~~~

## History  【用的不多！！】

length

​      \*  - 属性，可以获取到==当次访问==的链接数量

**方法**

back()

​      \*  - 可以用来回退到上一个页面，作用和浏览器的回退按钮一样

 forward()

​      \*  - 可以跳转下一个页面，作用和浏览器的前进按钮一样

go()

​      \*  - 可以用来跳转到指定的页面

​      \*  - 它需要一个整数作为参数

​      \*   1:表示向前跳转一个页面 相当于forward()

​      \*   2:表示向前跳转两个页面

​      \*   -1:表示向后跳转一个页面    back()

​      \*   -2:表示向后跳转两个页面

## Location

​    \*  - 该对象中封装了浏览器的地址栏的信息

如果直接打印location，则可以获取到地址栏的信息（当前页面的完整路径）

如果直接将location属性修改为一个完整的路径，或相对路径， 则我们页面会自动跳转到该路径，并且会==生成相应的历史记录==

![image-20211019182621970](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211019182621970.png)

![image-20211019182637199](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211019182637199.png)

assign()

​      \*  - 用来跳转到其他的页面，作用和直接修改location一样

- ==会生成历史记录==

reload()

​      \*  - 用于重新加载当前页面，作用和刷新按钮一样

​      \*  - 如果在方法中传递一个true，作为参数，则会==强制清空缓存刷新页面==   

Ctrl 	F5

 replace()

​      \*  - 可以使用一个新的页面替换当前页面，调用完毕也会跳转页面

​      \*   ==不会生成历史记录==，不能使用回退按钮回退

~~~js
location = "http://www.baidu.com";
location = "01.BOM.html";
location.assign("http://www.baidu.com");

location.reload(true);
location.replace("01.BOM.html");
~~~

# 定时器

![image-20211019183411409](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211019183411409.png)

## 定时调用

JS的程序的执行速度是非常非常快的，如果希望一段程序，可以每间隔一段时间执行一次，可以使用定时调用

【遇到alert程序暂时停止，点击确认之后，程序再接着执行！！】

 **setInterval()**   【用的更多！！！】

定时调用

 可以将一个函数，每隔一段时间执行一次

参数：

​     \*   1.回调函数，==该函数会每隔一段时间被调用一次！！！！==

​     \*   2.每次调用间隔的时间，单位是毫秒

返回值：

​     \*   返回一个Number类型的数据，这个数字用来作为定时器的唯一标识

**clearInterval()**

可以用来关闭一个定时器，方法中需要一个==定时器的标识作为参数==，这样将关闭标识对应的定时器

clearInterval(timer);

clearInterval()可以接收任意参数，如果参数是一个有效的定时器的标识，则停止对应的定时器，如果参数不是一个有效的标识，则什么也不做  【刚开始没bug】

​      \* 目前，我们每点击一次按钮，就会开启一个定时器，==点击多次就会开启多个定时器==，这就导致图片的切换速度过快，==并且我们只能关闭最后一次开启的定时器==

所以在开启定时器之前，需要将==当前元素上==的其他定时器关闭

**setTimeout**()

延时调用

​    \*  延时调用一个函数不马上执行，而是隔一段时间以后在执行，而且只会执行一次

 延时调用和定时调用的区别，定时调用会执行多次，而延时调用只会执行一次

延时调用和定时调用实际上是可以互相代替的，在开发中可以根据自己需要去选择

**clearTimeout**()

使用clearTimeout()来关闭一个延时调用

## 定时器的应用

目前我们的定时器的标识由==全局变量timer保存==，所有的执行正在执行的定时器都在这个变量中保存

定义一个变量，用来保存定时器的标识



~~~js
/* 清除默认样式 */
			*{
				margin: 0;
				padding: 0;
			}
//一条竖线
<div style="width: 0; height: 1000px; border-left:1px black solid; position: absolute; left: 800px;top:0;"></div>

~~~

## 轮播图

【这块知识跟着视频学习，但是自己没有完成，掌握的少！！】

一般给子元素开启绝对定位的时候，要给父元素开启相对定位

 \#outer的宽和高是固定的，\#imgList是图片ul，每次改变ul的left值，这样图片就可以显示出来



![image-20211020160614225](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211020160614225.png)

下面的点是超链接，

设置超链接浮动，这样内联元素也会变成块元素

~~~js
 float: left;
/*设置透明*/
opacity: 0.5; 
/*兼容IE8透明*/
filter: alpha(opacity=50); 
~~~





# 类的操作

通过style属性来修改元素的样式，==每修改一个样式，浏览器就需要重新渲染一次页面==，这样的执行的性能是比较差的，而且这种形式当我们要修改多个样式时，也不太方便

【不建议使用js改变多个样式！！，这样css和js掺和在一起】

【以后编程尽量要使css和js分离】

我们可以通过修改元素的class属性来间接的修改样式，这样一来，我们只需要修改一次，即可同时修改多个样式，==浏览器只需要重新渲染页面一次，性能比较好==，并且这种方式，可以使表现和行为进一步的分离

  \* 判断一个元素中是否含有指定的class属性值，如果有该class，则返回true，没有则返回false

## 二级菜单









## JSON

\- JS中的对象只有JS自己认识，其他的语言都不认识，如java不认识js中的对象

【如果是字符串，js认识字符串，java也认识字符串！！】

 **如果需要兼容IE7及以下的JSON操作，则可以通过引入一个外部的js文件来处理**

JSON就是一个特殊格式的==字符串==，这个字符串可以被任意的语言所识别，并且可以转换为任意语言中的==对象==，JSON在开发中主要用来数据的交互

JSON

​    \*   - JavaScript Object Notation     JS对象表示法

​    \*   - JSON和JS对象的格式一样，只不过JSON字符串中的属性名必须加双引号

​    \*    其他的和JS语法一致

JSON分类：

​    \*    1.对象 {}

​    \*    2.数组 []

JSON中允许的值：

​    \*    1.字符串

​    \*    2.数值

​    \*    3.布尔值

​    \*    4.null

​    \*    5.对象     【只能是常见的对象，不能是函数对象！！】

​    \*    6.数组

【没有undefined！！】

~~~js
var arr = '[1,2,3,"hello",true]';		
var obj2 = '{"arr":[1,2,3]}';	
var arr2 ='[{"name":"孙悟空","age":18,"gender":"男"},{"name":"孙悟空","age":18,"gender":"男"}]';
			
~~~

将JSON字符串转换为JS中的对象

在JS中，为我们提供了一个工具类，就叫JSON，这个对象可以帮助我们将一个JSON转换为JS对象，也可以将一个JS对象转换为JSON

json --> js对象

​    \*  JSON.parse()

​    \*   - 可以将以JSON字符串转换为js对象

​    \*   - 它需要一个JSON字符串作为参数，会将该字符串转换为JS对象并返回

JS对象 ---> JSON

​    \*  JSON.stringify()

​    \*   - 可以将一个JS对象转换为JSON字符串

​    \*   - 需要一个js对象作为参数，会返回一个JSON字符串

​    \* JSON这个对象在IE7及以下的浏览器中不支持，所以在这些浏览器中调用时会报错

eval()

​    \*  - 这个函数可以用来执行一段字符串形式的JS代码，并将执行结果返回

​    \*  - 如果使用eval()执行的字符串中含有{},它会将{}当成是代码块，如果不希望将其当成代码块解析，则需要在字符串前后各加一个()

​    \*  - eval()这个函数的功能很强大，可以直接执行一个字符串中的js代码，但是在开发中尽量不要使用，首先它的执行性能比较差，然后它还具有安全隐患
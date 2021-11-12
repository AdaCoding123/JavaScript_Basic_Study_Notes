# DOM

宿主对象

【浏览器创建的对象！】

![image-20211010185109376](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010185109376.png)

对象

- 将网页中==每一个部分==转换成一个对象，这样就可以采用面向对象的方法来操作对象，非常简单

模型【最难理解！！】

- 体现出节点之间的关系

![image-20211010185816478](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010185816478.png)

节点

![image-20211010190144419](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010190144419.png)

![image-20211010190217645](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010190217645.png)

元素就是标签！

节点的属性

![image-20211010190519800](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010190519800.png)

浏览器已经为我们提供 ==文档节点== 对象这个对象是window属性

?          \*  可以在页面中直接使用，**文档节点代表的是整个网页**	

【和平常的属性和方法是一样的，相同的操作即可！！】

【重点：找对象，改对象！！】

~~~js
//获取到button对象，这个现在就是按钮
			var btn = document.getElementById("btn");
			
			//修改按钮的文字
			btn.innerHTML = "I'm Button";
~~~

## 事件

【交互】

![image-20211010193039258](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010193039258.png)

事件，就是==用户和浏览器之间的交互行为==，比如：点击按钮，鼠标移动、关闭窗口。。。

【处理事件的方法是重点！！】

我们可以在事件对应的==属性==中设置一些js代码，这样当事件被触发时，这些代码将会执行。

DOM Event中

可以为按钮的对应事件==绑定处理函数==的形式来响应事件【回调函数】，这样当事件==被触发==时，其对应的函数将会被调用

这种写法我们称为结构和行为耦合，不方便维护，不推荐使用 

推荐使用分离！

~~~js
			//绑定一个单击事件
			//像这种为单击事件绑定的函数，我们称为单击响应函数
			btn.onclick = function(){
				alert("你还点~~~");
			};
~~~

## 文档的加载

浏览器在加载一个页面时，是按照**==自上向下==**的顺序加载的，

?          \*  读取到一行就运行一行,如果将script标签写到==页面的上边==，在代码执行时，页面还没有加载，DOM对象也没有加载，会导致无法获取到DOM对象

 onload事件会在==整个页面加载完成之后！！！！==【DOM加载完成之后】才触发，为window绑定一个onload事件，该事件对应的响应函数将会在页面加载完成之后执行，  这样可以确保我们的代码执行时所有的DOM对象已经加载完毕了

**建议：将js代码编写到页面的下部就是为了，可以在页面加载完毕以后再执行js代码**

~~~js
window.onload = function(){
				//获取id为btn的按钮
				var btn = document.getElementById("btn");
				//为按钮绑定一个单击响应函数
				btn.onclick = function(){
					alert("hello");
				};
			};
~~~

## DOM查询

获取元素节点

![image-20211010194332626](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211010194332626.png)

【以上这些方法最好背下来，一定要自己会写，虽然有提示！！】

**innerText**

?        \*  - 该属性可以获取到元素内部的文本内容

?        \*  - 它和innerHTML类似，不同的是它会自动将html去除

**innerHTML**

用于获取元素内部的HTML代码的，对于==自结束标签==【input，】，这个属性没有意义

~~~js
//为id为btn01的按钮绑定一个单击响应函数
				var btn01 = document.getElementById("btn01");
				btn01.onclick = function(){
					//查找#bj节点
					var bj = document.getElementById("bj");
					//打印bj
					//innerHTML 通过这个属性可以获取到元素内部的html代码
					alert(bj.innerHTML);
				};
				
				
				//为id为btn02的按钮绑定一个单击响应函数
				var btn02 = document.getElementById("btn02");
				btn02.onclick = function(){
					//查找所有li节点
var lis = document.getElementsByTagName("li");
					
					//打印lis
					//alert(lis.length);
					
					//变量lis
					for(var i=0 ; i<lis.length ; i++){
						alert(lis[i].innerHTML);
					}
				};
				
				//为id为btn03的按钮绑定一个单击响应函数
				var btn03 = document.getElementById("btn03");
				btn03.onclick = function(){
					//查找name=gender的所有节点
					var inputs = document.getElementsByName("gender");
					//alert(inputs.length);
					for(var i=0 ; i<inputs.length ; i++){
						alert(inputs[i].className);
					}
				};
			};
~~~

### 获取元素节点

**getElementById**

【返回一个】最好用！！！精确

**getElementsByTagName**()

【一个数组】

可以根据标签名来获取一组==元素节点==对象，这个方法会给我们返回一个==类数组对象==，所有查询到的元素都会封装到对象中

即使查询到的元素只有一个，也会封装到数组中返回

**getElementsByName**

【一个数组】

多用于获取表单类元素

如果需要读取==元素节点==属性，直接使用 元素.属性名

例子：元素.id    元素.name    元素.value

注意：class属性【名】不能采用这种方式，

读取class属性时需要使用 元素.className  【class是保留字，不能使用！！】

**图片切换的练习**

切换图片就是修改img的src属性

重点：实现循环

~~~js
//要修改一个元素的属性 元素.属性 = 属性值
img.src = imgArr[index];
					
//当点击按钮以后，重新设置信息
info.innerHTML = "一共 "+imgArr.length+" 张图片，当前第 "+(index+1)+" 张";
					
~~~

### 获取元素节点的**子节点**

调用的对象不同！

【**节点 **    包括该节点下面的所有元素和文本节点】

![image-20211012150256973](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211012150256973.png)

**childNodes**属性会获取包括文本节点在内的所有节点

?        \* 根据DOM标签标签间空白也会当成文本节点

?        \* 注意：在IE8及以下的浏览器中，不会将空白文本当成子节点，

?        \*  所以该属性在IE8中会返回4个子元素而其他浏览器是9个

**children**

属性可以获取当前元素的所有子元素

**firstChild**

可以获取到当前元素的第一个子节点（包括空白文本节点）

**firstElementChild**

获取当前元素的第一个子元素【有空格也没关系】

firstElementChild不支持IE8及以下的浏览器，==如果需要兼容他们尽量不要使用==

函数是对象，对象也可以做参数！！

### 获取父节点和兄弟节点

![image-20211012150109403](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211012150109403.png)



**previousElementSibling**

获取前一个兄弟==元素==，IE8及以下不支持

~~~js
myClick('btn11',function(){
        var bj=document.getElementById('bj');
        
        var fc=bj.firstChild;
        var con=fc.nodeValue;
        alert(con)
      })
// 和innerHTML相同的作用！！！

checkedAllBox.onclick = function(){
//alert(this === checkedAllBox);
//设置多选框的选中状态
for(var i=0; i <items.length ; i++){
	items[i].checked = this.checked;
			}
    
// 6如果四个多选框都选中，则checkedAllBox也应该选中；如果四个多选框都没选中，则checkedAllBox也应该不选中
    for (var i = 0; i < items.length; i++) {
        items[i].onclick=function(){
          // checkedAllBox.checked=true;
          for(var j=0;j<items.length;j++){
            if(!items[j].checked)
              {checkedAllBox.checked=false
              break;}
          }
        };
~~~

在事件的响应函数中，响应函数是给谁绑定的this就是谁

## DOM查询的剩余方法

**document.body**

在document中有一个属性body，它保存的是body的引用

**document.documentElement**

保存的是html根标签

**document.all**

代表页面中所有的元素

**getElementsByClassName**()

可以根据class属性值获取==一组====元素节点==对象，但是该方法不支持IE8及以下的浏览器

**document.querySelector**()

【选择器！！】

?       \*  - 需要一个选择器的字符串作为参数，可以根据一个CSS选择器来查询一个元素节点对象，虽然IE8中没有getElementsByClassName()但是可以使用querySelector()代替

?       \*  - 使用该方法总会==返回唯一的一个==元素，如果满足条件的元素有多个，那么它只==会返回第一个==

**document.querySelectorAll**()

?       \*  - 该方法和querySelector()用法类似，不同的是它会将符合条件的元素封装到==一个数组中返回==

?       \*  - 即使符合条件的元素只有一个，它也会==返回数组==

~~~js
var body = document.body;
var html = document.documentElement;
var all = document.all;
all = document.getElementsByTagName("*");
~~~

## DOM增删改

| 方法                     | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| getElementById()         | 返回带有指定 ID 的元素。                                     |
| getElementsByTagName()   | 返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。 |
| getElementsByClassName() | 返回包含带有指定类名的所有元素的节点列表。                   |
| appendChild()            | 把新的子节点添加到指定节点。                                 |
| removeChild()            | 删除子节点。                                                 |
| replaceChild()           | 替换子节点。                                                 |
| insertBefore()           | 在指定的子节点前面插入新的子节点。                           |
| createAttribute()        | 创建属性节点。                                               |
| createElement()          | 创建元素节点。                                               |
| createTextNode()         | 创建文本节点。                                               |
| getAttribute()           | 返回指定的属性值。                                           |
| setAttribute()           | 把指定属性设置或修改为指定的值。                             |

**document.createElement**()

【创建标签】

?        \*  可以用于创建一个元素节点对象，

?        \*  它需要一个==标签名==作为参数，将会根据该标签名创建元素==节点对象==，并将创建好的==对象作为返回值==返回

**document.createTextNode**()

【创建标签内容】

?        \*  可以用来创建一个文本节点对象

?        \*  需要一个==文本内容==作为参数，将会根据该内容创建文本节点，并将新的==节点返回==

**appendChild**()

?        \*  - 向一个父节点中添加一个新的子节点

用法：父节点.appendChild(子节点);

只有添加的节点是新的，全部没有被替换！！！

**insertBefore**()

?        \*  - 可以在指定的子节点前插入新的子节点

语法：父节点.insertBefore(新节点,旧节点);

 **replaceChild**()

?        \*  - 可以使用指定的子节点替换已有的子节点

语法：父节点.replaceChild(新节点,旧节点);

**removeChild**()

?        \*  - 可以删除一个子节点

语法：

- **父节点.removeChild(子节点);**

- **子节点.parentNode.removeChild(子节点);**

使用innerHTML也可以完成DOM的增删改的相关操作，一般我们会两种方式结合使用

~~~js
//1 添加新元素
myClick("btn03",function(){
          // 创建广州这个节点
          var li=document.createElement('li');
    		//将文本当成节点处理
          var gzText=document.createTextNode('广州');
          li.appendChild(gzText);

          var bj=document.getElementById('bj');
          city. replaceChild(li,bj)
        });

// 2添加元素，整个city都是新的，被替换了
var city = document.getElementById("city");
city.innerHTML += "<li>广州</li>";

//3二者结合的方法，添加时值影响最新的，而不是替换全部			
//创建一个li
var li = document.createElement("li");
//向li中设置文本
li.innerHTML = "广州";
//将li添加到city中
city.appendChild(li);
~~~

### 删除

点击超链接以后，超链接会跳转页面，这个是超链接的默认行为，但是此时我们不希望出现默认行为，两种方法：

- 可以通过在响应函数的最后return false来取消默认行为

- ```
  <a href="javascript:;">Delete</a>
  ```

Window 对象方法

![image-20211013093541509](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211013093541509.png)

confirm()用于弹出一个带有确认和取消按钮的提示框，需要一个字符串作为参数，该字符串将会作为提示文字显示出来

   \* 如果用户点击确认则会返回true，如果点击取消则返回false

### 添加

 ~~~js
 // 获取input的值
var empName=document.getElementById('empName').value;
 ~~~

### a的索引问题

for循环会在页面加载完成之后立即执行，而响应函数会在超链接被点击时才执行，当响应函数执行时，for循环早已执行完毕

# 样式

## 操作内联样式（css）

通过JS修改元素的样式：

语法：==元素.style.样式名 = 样式值==

注意：如果CSS的样式名中含有-，这种名称在JS中是不合法的比如background-color，需要将这种样式名修改为==驼峰命名法==，去掉-，然后将-后的字母大写

我们通过style属性设置的样式都是内联样式【写在元素的标签中】，==而内联样式有较高的优先级==，所以通过JS修改的样式往往会立即显示， 但是如果在样式中写了!important，则此时样式会有最高的优先级，即使通过JS也不能覆盖该样式，此时将会**导致JS修改样式失效**，所以**尽量不要为样式添加!important**

![image-20211016122759883](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211016122759883.png)

如何不知道如何写名称去手册查看！！！

语法：元素.style.样式名

通过style属性==设置和读取==的都是**内联样式，无法读取==样式表==中的样式**

~~~js
 box1.style.width='300px';
          box1.style.height='300px';
          box1.style.backgroundColor='blue';
~~~



## 获取元素的样式

获取元素的==当前显示==的样式

**语法：元素.currentStyle.样式名**

【只有IE支持，chrome不支持！！】

​     \* 它可以用来读取当前元素正在显示的样式如果当前元素没有设置该样式，则获取它的默认值，==currentStyle只有IE浏览器==支持，其他的浏览器都不支持

​      \* 在==其他浏览器中可以使用getComputedStyle()==这个方法来获取元素当前的样式，这个方法是window的方法，可以直接使用，需要两个参数

* 第一个：要获取样式的元素

- 第二个：可以传递一个伪元素【after、before】，一般都传**null**

该方法会返回一个对象，对象中封装了当前元素对应的样式

可以通过对象.样式名来读取样式，如果获取的样式没有设置，==则会获取到真实的值，而不是默认值==**【比currentStyle更好，方便计算】**

​     \*  比如：没有设置width，它不会获取到auto，而是一个长度，但是该方法不支持IE8及以下的浏览器

​     \* 通过currentStyle和getComputedStyle()读取到的样式都是==只读的==，不能修改，如果要修改必须通过style属性

定义一个函数，用来获取指定元素的当前的样式

参数：

- obj 要获取样式的元素

- name 要获取的样式名

~~~js
box1.currentStyle.backgroundColor;
var obj=getComputedStyle(box1,null);
var obj=getComputedStyle(box1,null).width;

function getStyle(obj,name){
          // 正常浏览器
          // 不加window就是变量，变量找不到就会报错，如果属性找不到就是undefined
          if(window.getComputedStyle) 
          // 这样更灵活
             return getComputedStyle(obj,null)[name];
         else
        //  IE8浏览器
          return obj.currentStyle[name];
        }
// 不建议使用下面的，更推荐使用getComputedStyle
        // if(obj.currentStyle)
        //   return obj.currentStyle[name];
        // else
        //   return getComputedStyle(obj,null)[name];
        // }
~~~

处理兼容性问题，以后思路都是一样的！！

## 其他样式相关的属性

**clientWidth**

**clientHeight**

​     \*  - 这两个属性可以获取元素的**可见宽度和高度**，这些属性都是不带px的，返回都是一个数字，可以直接进行计算， 这些属性都是==只读的，不能修改==【包括两部分内容，当修改时无法赋值！！】

- 会获取元素宽度和高度，包括内容区和==内边距==【padding】【不包括边框】
- 计算展示在页面上的宽度和高度，如果有滚动条，则要减去滚动条的宽度！！

**offsetWidth**

**offsetHeight**

?      \*  - 获取元素的整个的宽度和高度，包括==内容区、内边距和边框==

**offsetParent**

?      \*  - 可以用来获取当前元素的定位父元素，会获取到离当前元素最近的开启了相对定位的祖先元素【只要postion不是static，默认值】

【static，fix，absolute，relative】

?      \*   如果所有的祖先元素都没有开启定位，则返回body

~~~js
<div id="box3">
		<div id="box2" style="position: relative;">
				<div id="box1"></div>
		</div>
</div>

~~~

 **offsetLeft**

?      \*  - 当前元素相对于其==定位父元素==【offsetParent】的水平偏移量

**offsetTop**

?      \*  - 当前元素相对于其定位父元素【offsetParent】的垂直偏移量

【没有提供四个！！】

**scrollWidth**

**scrollHeight**

?      \*  - 可以获取元素整个滚动区域的宽度和高度

- 父元素的高度是300px，子元素的高度是600px，所以滚动高度是600px

**scrollLeft**

?      \*  - 可以获取==水平滚动条滚动的距离==

![image-20211016134815346](C:\Users\Carrie_Lee\AppData\Roaming\Typora\typora-user-images\image-20211016134815346.png)

**scrollTop**

?      \*  - 可以获取垂直滚动条滚动的距离

~~~js
#box4{
        width: 200px;
        height: 300px;
        background-color: #bfa;
        /* 此时溢出的子元素，被截断了 */
        /* overflow: hidden; */
        /* 增加滚动条，此时父元素滚动起来，子元素被包含起来 */
        overflow: auto;
      }
      
#box5{
        width: 150px;
        height: 600px;
        background-color: yellow;
      }
      
//当满足scrollHeight - scrollTop == clientHeight
//说明垂直滚动条滚动到底了
					
//当满足scrollWidth - scrollLeft == clientWidth
//说明水平滚动条滚动到底
//alert(box4.scrollHeight - box4.scrollTop); // 600 
~~~

【比如软件协议，可以检测用户是否已经阅读协议！！！】

如果为表单项添加disabled="disabled" 则表单项将变成不可用的状态

当垂直滚动条滚动到底时使表单项可用

**onscroll**

?     \*  - 该事件会在元素的滚动条滚动时触发

disabled属性可以设置一个元素是否禁用，

?       \*  如果设置为true，则元素禁用

?       \*  如果设置为false，则元素可用

~~~js
<input type="checkbox" disabled="disabled" />我已仔细阅读协议，一定遵守
<input type="submit" value="注册" disabled="disabled" />
~~~

##
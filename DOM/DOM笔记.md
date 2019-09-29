nhuo# 第六章 DOM
### 6.1 DOM的概述
6.1.1 DOM的概念
DOM文档对象模型，DOM对象不仅仅是一个普通的内置对象，它还是一个巨大的API的核心对象，他将文档的内容呈现在js面前，并赋予了js操作文档的能力。

6.1.2 DOM和JavaScript的关系
一个web页面是一个文档，这文档可以在浏览器窗口或者作为html源代码显示出来，但上述两种情况都是同一个文档，DOM提供了对同一份文档的另一种表现，存储和操作方式。DOM能够使用JavaScript脚本语言进行修改

6.1.3 DOM节点
加载html页面是web浏览器生成一个树形结构，用来表示页面的内部结构。DOM将这种结构理解为节点组成，根据w3c的html DOM标准，html文档找那个的所有内容都是节点
> 整个文档是一个文档节点
> 每个html元素是元素节点
> html元素内的文本是文本节点
> 每个html属性都是属性节点
> 注释也是节点，叫注释节点

6.1.4 DOM树
DOM树体现着html页面的层级结构，而DOM树有DOM文档树和DOM元素树两种，DOM元素树包含的只有元素节点，而DOM文档树则包括DOM文档中所有内容

### 6.2 获取元素
6.2.1 用id获取元素
getElementById()的方法，接受一个参数：获取元素的id，如果找到相应元素，则返回该元素的，否则返回null

6.2.2 用标签名获取元素
getElementsByTagName()可以获取该元素名称下所有的元素，返回一个伪数组，或者说是一个HTMLCollection

在某一个元素中，并不是在全局文档中利用标签获取元素，这样更加精准

6.2.3用class获取

6.2.4 用选择器获取元素
querySelector()和querySelectorAll()可以依靠选择器找到元素,但是前者只能找到元素列表的第一个元素,而后者可以全部找到.注意,该方法性能没有直接利用标签寻找高.

        var ul = document.getElementById('ul')
        var x = document.querySelector('#div>div a');
        var lis = ul.querySelectorAll('li');
        console.log(lis);

### 6.3 获取和设置元素中的其他信息
6.2.2 获取元素名
当我们使用id获取元素的时候，元素的名称会和整个元素一起显示出来如果想要拿到该元素的元素名，也就是标签名则需要用tagName属性
该属性只能获取，不能设置

	var div = document.getElementById('mydiv')
    console.log(div, div.tagName)

6.2.3 获取元素节点里的内容
当获取元素之后如果我们需要拿到元素中的内容（所有东西），则需要用另一种方法得到。元素里的内容可能包括：文本或元素。需要用innerHTML属性

innerHTML属性除了可以获取标签内的内容外，还可以设置标签内的内容

6.2.4 获取元素节点中的文本
利用innerText属性获取的只能是文本节点，不能是其他，当然innerText属性除了获取，也可以设置元素的文本


6.3.4 获取元素的类名
利用className属性获取元素的类名，以字符串的形式返回。
同时可以设置新的className类名，返回值是一个字符串，如果更换其中一个类，则需要考虑该字符串中其他类是否应该改一起设置

6.3.5 获取元素样式
style可以获取元素内联样式的所有属性，当然如果继续在style中找属性名如：backgroundColor，就可以得到该属性的值，以字符串的形式返回。同时也可以设置该属性，从而达到增加或更改样式。注意需要注意的是，以js形式增加的样式的优先级大于css优先级

	elem.style
	elem.style.backgroundColor

---

##### 6.3.6 获取元素的属性
getAttribute()可以获取元素的某个属性，要将属性名称放在括号中，记得要用引号引起来，返回值就是字符串形式的属性值

##### 6.3.7 设置元素的属性
setAttribute('属性'， '值')可以设置元素的某个属性，第一个参数是属性名，第二个参数是属性值，都需要用引号引起来，以逗号分隔

### 6.3.8 删除元素属性
removeAttribute(),可以删除某个元素的某个属性，括号中放需要删除的属性名，用引号包裹

### 6.4 增加元素
#### 6.4.1 创建元素节点
利用js创建一个元素的方法是，先在文档中创建一个标签document.createElement()括号中写标签名，当然要用字符串形式。创建之后不时就存在了，而是需要将这个已经创建的元素放到你想放到的元素(父级元素)中去

	// 创建元素
	var div = document.createElement('div')
	// 给body增加子元素
	document.body.appendChild(div)

#### 6.4.2 创建文本节点   
利用JS创建元素的文本节点,先在文档中创建文本document.createTextNode('一段文字')在括号中将要创建的字符串放入,最后插入到需要的元素中.


            var p = document.getElementById('p');
            var text = document.createTextNode('一段文字');
            p.appendChild(text);

#### 6.4.3 css样式赋予   
style.cssText是一个CSS样式的集合,它可以把CSS层叠样式表中的CSS样式直接放在该属性后,就不需要一条一条去赋予样式了,可以一次性赋予样式.

        var div = document.getElementById('mydiv');
        div.style.cssText='width:100px;height:100px;background-color:blue;';

#### 6.4.4 在某元素前插入创建的新元素   
insertBefore()这个函数和appendChild()用法基本一致,都是向父级中插入一个子元素,但区别是insertBefore()是可以选择插入的位置,它需要插入到某一个元素之前的位置,因此需要那个子元素,insertBefore()有两个参数,第一个参数是需要插入的元素,第二个参数是在谁之前插入,两个参数用逗号分隔.

## 6.5 删除和替换元素
#### 6.5.1 元素的替换
元素的替换是在父元素中一个子元素需要被另一个新的子元素所替代，使用replaceChild()方法，该方法两个参数，第一个参数是将要替换的新元素，第二个是被替换的旧元素，中间用逗号分隔

	var mydiv = document.getElementById('mydiv')
    var myp = document.createElement('p')
    // 在父元素中替换子元素，第一个是新元素，第二个是旧的
    document.body.replaceChild(myp, mydiv)

#### 6.5.2 元素的删除
元素的删除是在父元素的其中一个子元素需要删除，使用removeChild()方法，将需要删除的元素放入括号中

	document.body.removeChild(mydiv)

### 6.6 查找节点(node)
节点是在DOM树上每一个节点，其中包括元素、文本、属性、注释等等，常用的有三个，元素、文本、属性。

#### 6.6.1 节点属性

	console.log(document.body.nodeName)
    console.log(mydiv.nodeName)
    console.log(mydiv.nodeValue)
    console.log(mydiv.nodeType)

#### 6.6.2 层级节点
节点可以分为父节点与子节点和兄弟节点，当我们知道其中之一的时候，可以用一些方法找到另一个

#### 6.6.3 获取所有子节点
使用childNodes属性拿到是该元素下的所有节点，包含所有节点类型，不单单只是元素

#### 6.6.4 获取第一个和最后一个子节点
用firstChild和lastChild可以拿到该元素下的第一个和最后一个子节点，注意不一定是元素节点

#### 6.6.5 获取父节点
使用parentNode属性可以拿到该元素的父节点，注意父节点只有一个

#### 6.6.6 获取兄弟节点
使用previousSibling nextSibling可以获得该元素的前一个和后一个兄弟节点，只能获取一个

	console.log(mydiv.previousSibling)
    console.log(mydiv.nextSibling)

#### 6.7 元素的宽高属性
#### 6.7.1 offsetWidth offsetHeight
需要获取一个元素的宽度和高度，使用style是无法获取的，所以选择使用offsetWidth和offsetHeight属性。该属性可以获取元素的占位宽高，包含‘内边距和边框’

    console.log(mydiv.style)//这种方法只能拿到内联样式
    console.log(mydiv.offsetWidth, mydiv.offsetHeight)

#### 6.7.2 clientWidth clientHeight
clientWidth clientHeight属性也可以获取元素的宽高，但与offsetWidth不同的是不包含边框。包含内边距

	console.log(mydiv.clientWidth, mydiv.clientHeight)

### 6.8 子元素与父元素的距离
offsetLeft offsetTop是距离body左边界和上边界的距离，但如果该子元素使用了position属性，则offsetLeft好offsetTop参照的不再是body而是距离他最近的父元素
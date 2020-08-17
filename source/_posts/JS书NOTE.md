---
title: JS书NOTE
date: 2020-05-22 13:47:58
tags: JavaScript
---
## 第二章：在HTML中使用JavaScript
* 在script标签内（嵌入式js）， 遇到</ script>标签需要转义：在前面加上 \ 
* 如果外部文件引用全部放置在< head >标签中， 效果是加载完所有的JS之后再展示页面，当JS多时容易有明显延迟， 如果是较多JS的网页需要把引用放在< /body>标签上方

#### defer属性
* 如果在标签加入 defer = "defer" 效果是立即加载，延迟执行
* 延迟脚本之间不一定按照排列的顺序执行
* 延迟脚本不一定会在DOMContentLoaded事件触发前执行
* 延迟脚本最好只有一个

#### async属性
* 语法为在src前加 async
* async脚本不保证执行先后顺序，因此需要互不依赖
* 一定会在load事件前执行，但不一定会在DOMContentLoaded事件触发之前或之后执行

### 基本语法/概念

* 语法
</br>
**在JS中，ECMAScript中的一切都区分大小写 例如函数typeOf（正确写法）而不能用typeof(typeof是一个关键字)**
</br>
</br>**标识符： 变量，函数，属性的名字**
以字母/下划线（_）/美元符号$开头 其他可以是字母/下划线（_）/美元符号$/数字
</br></br>标识符采用驼峰式命名：changeButtonColor
</br></br>**注释**://单行注释
</br>/*
</br>* 这里是
</br>* 多行注释
</br>*/
* 变量
1.var定义变量，没有块的概念，可以跨块访问，不能跨函数访问，不初始化出现undefined，不会报错。 现在可以不用var了
</br></br>
2.let定义变量，只能在块作用域里访问，也不能跨函数访问，对函数外部无影响。 
</br></br>
3.const定义常量，只能在块作用域里访问，也不能跨函数访问，使用时**必须初始化**(即必须赋值)，而且**基础变量不能修改** 用于定义object和function。

* 数据类型</br>
5种基础的数据类型：Undefined， Null, Boolean, Number, String
</br>一种复杂的数据类型	： Object	
* 检验数据类型的方法：typeof</br>
typeof(message) 或者 typeof message**推荐第一种但是第二种也可以因为typeof是操作符而不是函数**可能得到： “undefined”, "boolean", "string", "number", "object", "function"
</br></br>
1. Undefined
</br>此类型只有一个值就是undefined，**在使用var或let声明变量**，但是又**未对其加以初始化**的时候，这个变量的值就是undefined 对为声明的变量使用typeof，结果也是undefined
2. Null
</br>只有一个值为null，typeof null 得到的结果是object， 因为在JS中，null可以表示一个空对象指针（其表达数据类型的二进制码是一个指向object的指针）如果定义的对象在将来准备用于保存对象，可以用null将其初始化，之后检查null值就可以知道其是否保存了一个对象的引用
</br></br>实际上，undefined值是派生自null值的，因此**null==undefined返回true**
1. Boolean
</br>只有两个字面值，true和false，区分大小写
</br>任何类型都有对应true和false的值
</br>String：true：任何非空字符串 false：“”（空字符串）
</br>Number：true： 非0数字 false：0或者NaN
</br>Object: true: 任何对象 false：null
</br>Undefined： true：没有 false：undefined
</br>转化函数：Boolean（a）把变量a转换成了Boolean值
</br>if函数中，变量会自动转换成Boolean值
1. Number类型
</br>55十进制 070八进制（0开头，后面没有大于8的数字）（严格模式无效）0xA（0x开头，A和a都可以，不分大小写）
</br>浮点数：保存所需空间是整数的两倍
</br>科学计数法：3.125e16 = 3.125* 10的16次方 7e-10 7 *10的-7次方
</br>数值范围： Number.MAX_VALUE表示能表示的最大值，大于它就是Infinity 小于它的负数形式就是-Infinity  Number.MIN_VALUE表示最精确的值 确定一个值能否取到可以用isFinite（）函数
</br>NaN：这个数值用来表示一个本来要返回数值的操作数未返回数值的情况
</br>NaN不等于NaN（false）
</br>NaN进行任何操作都返回NaN
</br>用isNaN函数检验是否为NaN，直接console.log返回的值是undefined isNaN会自动将其他类型转换成数字，比如“10”就会被转换成数字10，true就会被转换成数字1，但是“blue”就不会被转换成数字
</br> **数值转换**
</br> Number()函数：可以用于任何数据类型转换成Number，true为1，false为0，null为0，undefined为NaN，字符串可识别10进制与16进制，8进制的前导0会被忽视，转换成10进制，空字符串为0，其他形式NaN**只要有非数字部分，就是NaN 前后空格可以忽略，但是数字中间的空格不能忽略**
</br>parserInt（）函数：Number功能➕不识别小数➕能自动省略后面的字母➕空字符串为NaN➕可检查16进制与8进制
</br>parseInt有两个参数，第一个是一个字符串，第二个是解析的进制，比如（ab，16）就是171
</br>比如“21321sjiaobcisdoabc”等于21321 “cdascsd21321”等于NaN
</br>parseFloat（）函数：与parseInt类似，只能解析一个小数点，也能解析整数，只解析10进制
1. String类型
</br> 双引号或单引号没区别，但是需要统一用一种
</br>string中的转义序列：</br>“\n, 换行”</br> “\t,制表符"</br> "\b，退格 " </br> "\r， 回车" </br>"\f，进纸 "</br>
"\\， 斜杠" </br>"\'，在双引号包裹的string中表示单引号 "</br> "\"， 在单引号包裹的string中表示双引号" </br>"\xnn ，以16进制代码nn表示的一个字符（n范围是0-F）"</br> "\unnnn，以十六进制代码nnnn表示的一个unicode字符（n的范围是0-F）"</br>
在ECMAScript中，字符串是不可改变的，对字符串的修改经历了，创建新的字符串空间，重新赋值，销毁原字符串等操作</br>toString()函数: toString后面可以加上参数：基数，用于表示几进制表达，例如toString（2）表示数字的二进制表达 e.x. num=10; num.toString(2)->'1010'
</br>**toString()方法不能用于null或者undefined 当其可能是null或者undefined时可以使用String（）函数 ->把null转化成“null”， undefined转化成“undefined”**
1. Object类型
</br>基本语法: var o = new Object();
</br>Object的实例都具有下列属性和方法：
</br>constructor：保存着用于创建当前对象的函数 对之前的例子来说构造函数就是Object（）
</br>hasOwnProperty（propertyName）：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在 propertName必须以字符串的形式指定
</br>isPrototypeOf（object）:用于检查传入的对象是否是当前对象的原型
</br>propertyIsEnumerable（propertyName）：用于检查给定的语句能否使用for-in语句来枚举，propertName必须以字符串的形式指定
</br>toLocalString（）：返回该对象的字符串表示，与本地相关
</br>toString（）：返回对象的字符串表示
</br>valueOf（）：返回对象的字符串，数字或者是布尔值表示 通常与toString（）返回值相同
1. 操作符
</br>操作符的逻辑：先调用对象的toString或者（和）valueOf方法


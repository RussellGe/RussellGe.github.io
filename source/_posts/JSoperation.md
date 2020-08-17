---
title: JSoperation
date: 2020-08-12 21:16:42
tags: JavaScript
---

### 逻辑与&&  短路操作

#### &&运算符的三种理解

##### 1.当两两个操作数都是布尔值：对两数执行AND操作

##### 2.对真值与假值做AND操作（假值：undefined，null, false,0,-0,NaN,''）

##### 3.短路操作，当第一个值为真值时返回第二个值，当第一个值为假值时返回第一个值

例如：20&&100 -->100.    0&&100 --> 0

##### **当第一个值返回值是假时，不会去计算第二个值，这个方法很重要，因为有些假值的引用会引起报错**

**例如：var p = null     p.x 会报错**

**所以在这里我们可以写成：  p&&p.x，就是在p这个值存在的时候才会去取p.x这个属性,是一种更简单的写法**





### 逻辑或 || 

##### 可以理解为：取出第一个为真值的操作数

**这种用法常常写在函数体内，用于给变量一个默认初始值： 比如:  var x = para.length || 500 如果有para.length这个属性就会用它，没有则给默认值500**

















### JS原型链

**对象构造方法：Object.create(第一个参数：原型；第二个参数，这个对象)， 如果原型为null可以创造没有原型的对象**

**构造函数的原型等于实例的原型**

**例如：let arr = [] //可以看成是等于new Array.    那么arr.__ proto __(下划线表示函数私用原型)== Array.prototype（prototype表示构造函数原型） **



```
__proto__     函数的私用原型：一些属性，apply，length等在这里
prototype     函数的构造原型：一些改变其结构的方法在这里
最顶部的原型：Object.prototype   Object.prototype == Object.__proto__.__proto__
Array.prototype.__proto__  == Array.__proto__.__proto__  == Object.prototype

在用构建函数生成新的object时，对象的原型会指向构建函数的构建原型
例如： let russ = new Array()
    russ.__proto__ == Array.prototype
```



#### **设置prototype的方法：**

##### Object.setPrototypeOf(a,b) -->这样b就是a的prototype(__ proto __)



#### 检查构造原型的方法：

#####  a  instanceof b       本质：检查b是否在a的原型链的prototype里（构造函数 ）.   判断b.prototype是否在a的原型链上 

##### b.isPrototypeOf(a)  与上面的例子同理,区别是isPrototypeOf用于判断某个对象是否是另一个对象原型链中的一份子





#### 对象属性检测:

```
in    'a' in b  检测a属性是否在b以及b的原型链上
b.hasOwnProperty(a) 检测a属性是否在b上（不包括原型链）
```


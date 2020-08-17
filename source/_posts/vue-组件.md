---
title: vue-组件
date: 2020-06-04 09:44:13
tags: Vue
---
* **组件的data必须是一个函数**
</br>在组件中，data写法为：
</br>data:(){</br>
  return{</br>
  	count:0</br>
  	}
</br>}
**这么做是为了保证vue中的组件保持独立，否则他们会共享数据， 可以理解为在JS中，data是vue对象的一个属性，如果直接写data的话，所有对vue对象的引用会直接的指向这个基本数据类型，所以我们需要把data改变成引用数据类型**

* 通过prop向子组件传递数据
</br>用法：**在子组件中添加一个prop</br>
prop：[‘title’] 添加之后，在父组件引用这个子组件的title attribute时，值就传入了子组件**
</br></br>在props中由于attribute大小写不敏感，需要把驼峰法转化为短横线法
</br></br>props还可以以对象的形式定义 例如title:String
定义了类型为string的prop title
</br></br>props接受所有数据类型并且带有检查功能


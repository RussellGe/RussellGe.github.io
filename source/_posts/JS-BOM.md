---
title: JS_BOM
date: 2020-06-01 19:58:22
tags:
---
## BOM

#### Navigator
**现在只用navigator.userAgent属性**
**可以得到代理信息**
</br>**用法：</br>if(/firefox/.text(navigator.userAgent)){
判断后操作</br>
火狐：firefox 谷歌：chrome IE：MSIE IE11: 没法识别}**

#### History
**back()返回上级 forward（）访问上级 length属性 可以得到访问的连接数量 go()跳转到指定页面，需要一整数作为参数**

#### Location
**location属性直接修改，则页面会自动跳转界面，并生成相应的历史记录 assign() 用来跳转到其他界面，作用和直接修改一样 reload（）更新，等于是刷新 里面的属性如果是true，则是强制清空缓存刷新页面 replace（）可以用一个新的页面替换当前页面，不生成相应的历史记录**
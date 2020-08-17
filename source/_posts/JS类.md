---
title: JS类
date: 2020-07-06 16:13:50
tags: JavaScript
---

## JS中的类

#### class语法

```javascript
class MyClass {
  // class 方法
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

new Myclass()-->会得到一个新的对象

`new` 会自动调用 `constructor()` 方法，因此我们可以在 `constructor()` 中初始化对象。

```javascript
class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

// 用法：
let user = new User("John");
user.sayHi();
```

当 `new User("John")` 被调用：

1. 一个新对象被创建。
2. `constructor` 使用给定的参数运行，并为其分配 `this.name`。
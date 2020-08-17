---
title: JS对象属性
date: 2020-07-06 13:56:26
tags:Javascript
---

## 属性标志和属性描述符

#### 属性标志：

**writable**   表示这个值可以修改

**enumerable**   表示这个值可以在循环中被列举出来

**configuiable**   表示这个值可以被删除

以上三个值的默认值都是true

[Object.getOwnPropertyDescriptor(第一个值，obj名称， 第二个值，需要查询的属性名称。string形式)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor) 方法允许查询有关属性的 **完整** 信息。

![截屏2020-07-06 下午2.04.13](/Users/apple/Desktop/截屏2020-07-06 下午2.04.13.png)

#### 定义属性标志：

如果该属性存在，`defineProperty` 会更新其标志。否则，它会使用给定的值和标志创建属性；在这种情况下，如果没有提供标志，则会假定它是 `false`

```javascript
Object.defineProperty(user, "name", {
  value: "John"
});

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/*
{
  "value": "John",
  "writable": false,
  "enumerable": false,
  "configurable": false
}
```

使属性变成不可配置是一条单行道。我们无法使用 `defineProperty` 把它改回去。

确切地说，不可配置性对 `defineProperty` 施加了一些限制：

1. 不能修改 `configurable` 标志。
2. 不能修改 `enumerable` 标志。
3. 不能将 `writable: false` 修改为 `true`（反之亦然）。
4. 不能修改访问者属性的 `get/set`（但是如果没有可以分配它们）。





有一个方法 [Object.defineProperties(obj, descriptors)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)，允许一次定义多个属性。

语法是：

```javascript
Object.defineProperties(obj, {
  prop1: descriptor1,
  prop2: descriptor2
  // ...
});
```

例如：

```javascript
Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});
```

**注意，在这个定义中，默认值是false**



- [Object.preventExtensions(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)

  禁止向对象添加新属性。

- [Object.seal(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)

  禁止添加/删除/修改属性。为所有现有的属性设置 `configurable: false`。

- [Object.freeze(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

  禁止添加/删除/更改属性。为所有现有的属性设置 `configurable: false, writable: false`。

还有针对它们的测试：

- [Object.isExtensible(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible)

  如果添加属性被禁止，则返回 `false`，否则返回 `true`。

- [Object.isSealed(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed)

  如果添加/删除属性被禁止，并且所有现有的属性都具有 `configurable: false`则返回 `true`。

- [Object.isFrozen(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen)

  如果添加/删除/更改属性被禁止，并且所有当前属性都是 `configurable: false, writable: false`，则返回 `true`。





#### 属性的 getter 和 setter



##### [Getter 和 setter](https://zh.javascript.info/property-accessors#getter-he-setter)

访问器属性由 “getter” 和 “setter” 方法表示。在对象字面量中，它们用 `get` 和 `set` 表示：

```javascript
                let obj = {
  get propName() {
    // 当读取 obj.propName 时，getter 起作用
  },

  set propName(value) {
    // 当执行 obj.propName = value 操作时，setter 起作用
  }
};
```





## [访问器描述符](https://zh.javascript.info/property-accessors#fang-wen-qi-miao-shu-fu)

访问器属性的描述符与数据属性的不同。

对于访问器属性，没有 `value` 和 `writable`，但是有 `get` 和 `set` 函数。

所以访问器描述符可能有：

- **`get`** —— 一个没有参数的函数，在读取属性时工作，
- **`set`** —— 带有一个参数的函数，当属性被设置时调用，
- **`enumerable`** —— 与数据属性的相同，
- **`configurable`** —— 与数据属性的相同。

例如，要使用 `defineProperty` 创建一个 `fullName` 访问器，我们可以使用 `get` 和 `set` 来传递描述符：

```javascript
let user = {
  name: "John",
  surname: "Smith"
};

Object.defineProperty(user, 'fullName', {
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  }
});

alert(user.fullName); // John Smith

for(let key in user) alert(key); // name, surname
```

Getter/setter 可以用作“真实”属性值的包装器，以便对它们进行更多的控制。

例如，如果我们想禁止太短的 `user` 的 name，我们可以创建一个 setter `name`，并将值存储在一个单独的属性 `_name` 中：

```javascript
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short, need at least 4 characters");
      return;
    }
    this._name = value;
  }
};

user.name = "Pete";
alert(user.name); // Pete

user.name = ""; // Name 太短了……
```
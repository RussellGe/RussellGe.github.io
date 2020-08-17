---
title: JS中的几个类
date: 2020-07-11 11:37:44
tags:JavaScript
---

- #### ArrayBuffer

  **used to represent a generic, fixed-length raw binary data buffer.**

  

  **You cannot directly manipulate the contents of an `ArrayBuffer`; instead, you create one of the [typed array objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) or a [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView) object which represents the buffer in a specific format, and use that to read and write the contents of the buffer.**

  - #### [`ArrayBuffer.isView(arg)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/isView)

    Returns `true` if `arg` is one of the ArrayBuffer views, such as [typed array objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) or a [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView). Returns `false` otherwise.

    

  - #### [`ArrayBuffer.prototype.byteLength`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/byteLength)

    The read-only size, in bytes, of the `ArrayBuffer`. This is established when the array is constructed and cannot be changed.

    

  - #### [`ArrayBuffer.prototype.slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/slice)

    Returns a new `ArrayBuffer` whose contents are a copy of this `ArrayBuffer`'s bytes from `begin` (inclusive) up to `end` (exclusive). If either `begin` or `end` is negative, it refers to an index from the end of the array, as opposed to from the beginning.

    
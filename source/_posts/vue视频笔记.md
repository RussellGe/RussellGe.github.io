---
title: vue视频笔记
date: 2020-07-20 17:11:51
Tags:vue
---

### Vue virtual Dom

##### render function:



Import {h} from 'vue'  **in vue3**                                                等同于<div id='foo' onclick='onClick'>hello </div>

render( ////h){.  **in vue2**

​	return h('div',{

​		attires:{.    **in vue2**

​	///	id: 'foo'

​		},

​		on:{.   **anything with on will automatically be bound as an event listener**

​			click: this.onClick

​	///	}



​    id: 'foo'.   **in vue3**

​	click: this.onClick

}, 'hello' )



}
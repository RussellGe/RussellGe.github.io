---
title: Vue 1
date: 2020-05-20 13:06:51
tags: vue
---
# Vue笔记
## vue中的核心语法
### 基础
* html:{{message}} -></br>
vue: </br>
var app = new 
		
		vue({   </br>
        el: "the ID of the html part"</br>
		data:{  
			message: "Hello World"</br> 
		}</br>
		computed:{</br>
			reversedMessage: function(){</br>
				//这里的this指向的是app实例</br>
				return this.message.split('').reverse().join('')
				</br>}</br>}</br>
				**计算属性的setter：设置后可以通过给计算属性赋值改变其所用的data的值**
		methods: {</br>
  			reversedMessage: function () {</br>
    				return this.message.split('').reverse().join('')</br>
 		 	}</br>
		} })
	**计算属性（computed）基于message的变化响应，方法：每次重新的渲染总会再次执行方法 如果需要进行大量的计算，则计算属性需要占用缓存**
	

**如果想要修改message的值，可以使用app.message = new value  Vue把message当成app的一个属性**</br>
### 指令</br>
**Vue中的指令以v-开头**</br>

* v-blind: 绑定指令 </br>语法：v-blind: title = “message”（3部分： 可以理解为主谓宾结构————将message property绑定到该元素的title attribute上）</br>**可以缩写为 ：**

* v-on: 添加事件监听器</br>语法： v-on：click=‘xxx’ （监听click事件，当click事件发生时调用xxx函数）</br>**可以缩写为 @**

* v-model：用于实现表单输入和当前应用之间的双向绑定</br>
语法：< p> {{message}}< /p>
</br>< input v-model = 'message'></br>绑定之后，用户输入将会实时的显示在网页上

* v-once: 一次性插入，将不会改变插入后的值 

**动态参数：[参数名] attribute可以动态改变**

**修饰符： 加. 后缀， 例如.prevent可以告诉指令对于触发的事件调用event.preventDefault()函数**

### 条件/循环
* v-if: 判断一个property是否为**true 注意一定是小写** 如果是的话则显示标签内容，不是则隐藏</br>
*拓展*：< transform >是Vue设定的动画标签，可以自动加动画效果， 例如name="fade" 就有渐入渐出效果

* v-for： 用于渲染一组数据</br>
Example： < li v-for = 'todo in todos'>  (第一个todo是代名，无影响， 第二个todos是真正的property名)</br>
{{todo.text}}
</br>< /li></br></br>
data: {</br>
 todos:[{text: "fdsfcdsa"}, {text:'hhhhhh'}]
 </br>}
 
 (传入的数据是用json格式写的， 如果添加了新的属性，也会实时渲染上去)


## 组件化
**组件的本质：一个拥有预定义选项的Vue实例** **所有的组件都是Vue实例，并且接受相同的*选项对象***</br>

* ##### 初始化语法： 
Vue.component('todo-item' **设定的新标签名字** ,{</br>
prop: ['todo'], **prop 是一个自定义的attribute， 这个新标签可接收这个prop**</br>
 template:"< li>{{todo.text}}< li>" **设定的新标签自带的内容**</br>
})
* ##### html中使用：
< todo-item </br>
v-for = "item in List" **把LIST中的数据渲染到网页上**</br> 
v-bind:todo = 'item' **把得到的item property 绑定到我们预先设置好的attribute（prop）todo上**</br>
v-bind:key = "item.id"**给每一个todo-item 一个PK**>

**组件刷新的机制： 当一个Vue实例被创建时， 会将data对象（注意，data其实是一个对象）中的所有property加入Vue的响应式系统，当property的值发生改变的时候， 视图就会响应**
</br>**这样的机制导致我们在定义data的property时候，需要先将所有需要的property设置初始值，因为新加入的property还未在被定义时加入响应式系统**</br>

* 阻碍响应的方法：</br>
 Object.freeze(obj) 用了此方法之后，obj中的property将被阻止修改
 
* Vue实例自带一些property：</br>
  Vue实例自带一些property，例如el，data 需要引用他们时可以在前面加上$，以便和用户定义的property区别开来
###   实例的生命周期钩子：
**用户可以在不同的生命周期添加自己的代码**
![生命周期](https://cn.vuejs.org/images/lifecycle.png)
例如：created钩子： 可以在一个实例被创建的时候执行代码
**钩子里的函数一般都会使用 this， 所以不使用箭头函数或者是回掉函数**
### 侦听器
**当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。**</br>
 因为 AJAX 库和通用工具的生态已经相当丰富，Vue 核心代码没有重复 </br>
 提供这些功能以保持精简。这也可以让你自由选择自己更熟悉的工具。</br>
< script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script></br>
< script src="https://cdn.jsdelivr.net/npm/lodash@4.13.1/lodash.min.js"></script></br></br>
* < script></br>
var watchExampleVM = new Vue({</br>
  el: '#watch-example',</br>
  data: {</br>
    question: '',</br>
    answer: 'I cannot give you an answer until you ask a question!'</br>
  },</br>
  watch: {</br>
    // 如果 `question` 发生改变，这个函数就会运行</br>
    question: function (newQuestion, oldQuestion) {</br>
      this.answer = 'Waiting for you to stop typing...'</br>
      this.debouncedGetAnswer()</br>
    }</br>
  },</br>
  created: function () {</br>
    // `_.debounce` 是一个通过 Lodash 限制操作频率的函数。</br>
    // 在这个例子中，我们希望限制访问 yesno.wtf/api 的频率</br>
    // AJAX 请求直到用户输入完毕才会发出。想要了解更多关于</br>
    // `_.debounce` 函数 (及其近亲 `_.throttle`) 的知识，</br>
    // 请参考：https://lodash.com/docs#debounce</br>
    this.debouncedGetAnswer = _.debounce(this.getAnswer, 500)</br>
  },</br>
  methods: {</br>
    getAnswer: function () {</br>
      if (this.question.indexOf('?') === -1) {</br>
        this.answer = 'Questions usually </br>contain a question mark. ;-)'</br>
        return</br>
      }</br>
      this.answer = 'Thinking...'</br>
      var vm = this</br>
      axios.get('https://yesno.wtf/api')</br>
        .then(function (response) {</br>
          vm.answer = _.capitalize(response.data.answer)</br>
        })</br>
        .catch(function (error) {</br>
          vm.answer = 'Error! Could not reach the API. ' + error</br>
        })</br>
    }</br>
  }</br>
})</br>
< /script>

### 绑定HTML对象
**用于方便的处理attributes：class和style的绑定**
#### class
* 对象语法：</br>
< div v-bind:class="{ active: isActive }">< /div>
用 isActive（一个data中的property）来决定class active是否存在
</br>同样我们可以传入一组对象，进行多个判断</br>
</br>**更加实用的方式是外联式➕计算属性**
</br>< div v-bind:class="classObject">< /div></br>
data: {</br>
  isActive: true,</br>
  error: null</br>
},</br>
computed: {</br>
  classObject: function () {</br>
    return {</br>
      active: this.isActive && !this.error,</br>
      'text-danger': this.error && this.error.type === 'fatal'</br>
    }</br>
  }</br>
}</br>

* 数组语法</br>
 < div v-bind:class="[activeClass, errorClass]">< /div>
</br>data: {</br>
  activeClass: 'active',</br>
  errorClass: 'text-danger'</br>
}</br>**我们在数组语法中同样可以写条件判断**
</br>< div v-bind:class="[isActive ? activeClass : '', errorClass]">< /div>**我们也可以在数组语法中使用对象语法**</br>< div v-bind:class="[{ active: isActive }, errorClass]">< /div>**在组件上使用class绑定时候，不会覆盖之前的class，而是向后添加新的class**
</br>
#### style </br>
* 对象语法</br>
< div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">< /div>**CSS的property名可采用驼峰式或者短横线分隔式**</br>
</br>**vue会自动侦测并帮助添加需要浏览器引擎渲染的前缀，例如transform**
</br></br>**你可以为 style 绑定中的 property 提供一个包含多个值的数组，常用于提供多个带前缀的值**
</br>
### 条件渲染
* 存在v-else模块
</br>< h1 v-if="awesome">Vue is awesome!< /h1>
< h1 v-else>Oh no 😢< /h1>
</br>
v-else 元素必须紧跟在带 v-if 或者 v-else-if 的元素的后面，否则它将不会被识别。
* v-else-if标签
< div v-if="type === 'A'"></br>
  A</br>
< /div></br>
< div v-else-if="type === 'B'"></br>
  B</br>
< /div></br>
< div v-else-if="type === 'C'"></br>
  C</br>
< /div></br>
< div v-else></br>
  Not A/B/C</br>
< /div></br>
* 多个元素打包获得v-if：</br>
可以创造一个template标签，在其中添加v-if， 标签包含的所有字标签都将会获得v-if标签</br>
</br>
#### key值</br>
**Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染 可以理解为，改变标签的attributes或者innerHTML**</br>
key值用来定义组件名字，可以让他不复用</br>

#### v-show
**可以理解为一个预先加载html的v-if**
</br>**v-if是惰性的，在第一次条件为真之前这个元素其实是不存在的，而v-show是预先加载，并通过简单的css来切换**
</br>
</br>**不推荐v-if与v-for一起使用**</br>
### 列表循环
* 我们可以用 v-for 指令基于一个数组来渲染一个列表。v-for 指令需要使用 item **in（或者of）** items 形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名。
</br></br>在 v-for 块中，我们可以访问所有父作用域的 property。v-for 还支持一个可选的第二个参数，即当前项的索引。**可以理解为PK**
* 维护机制
如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染
</br></br>
为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key attribute
</br></br></br></br></br></br></br></br></br></br>

* 数组更新</br>
  **变更方法 它们也将会触发视图更新**
  </br>push()
pop()
shift()
unshift()
splice()
sort()
reverse()  </br>
**替换方法 它们不会变更原始数组，而总是返回一个新数组**  </br>
filter()、concat() 和 slice() 
## 事件处理
### 监听事件
* 用v-on来监听DOM事件，并在触发时执行一些JS代码
* 有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 $event 把它传入方法：< button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
< /button>
* 事件修饰符</br>
.stop
.prevent
.capture
.self
.once
.passive
</br></br>
< !-- 阻止单击事件继续传播 --></br>
< a v-on:click.stop="doThis">< /a>
</br></br>
< !-- 提交事件不再重载页面 --></br>
< form v-on:submit.prevent="onSubmit">< /form>
</br></br>
< !-- 修饰符可以串联 --></br>
< a v-on:click.stop.prevent="doThat">< /a>
</br></br>
< !-- 只有修饰符 --></br>
< form v-on:submit.prevent>< /form>
</br></br>
< !-- 添加事件监听器时使用事件捕获模式 --></br>
< !-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 --></br>
< div v-on:click.capture="doThis">...< /div>
</br></br>
< !-- 只当在 event.target 是当前元素自身时触发处理函数 -->
< !-- 即事件不是从内部元素触发的 --></br>
< div v-on:click.self="doThat">...< /div>

### 表单绑定输入
* 	你可以用 v-model 指令在表单 < input>、< textarea> 及 < select> 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 v-model 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。
*  v-model 在内部为不同的输入元素使用不同的 property 并抛出不同的事件：</br>
text 和 textarea 元素使用 value property 和 input 事件；
checkbox 和 radio 使用 checked property 和 change 事件；
select 字段将 value 作为 prop 并将 change 作为事件。



### 组件基础
* 组件的data必须是一个函数，不然对一个组件进行操作，所有组件都会受到影响
* 我们通过Prop向子组件传递数据，Prop可以是基础数据类型，也可以是OBJECT
* 在注册了prop之后，我们可以这样传递数据：< blog-post title="My journey with Vue">< /blog-post>这样我们就给组件的prop： title赋上值了

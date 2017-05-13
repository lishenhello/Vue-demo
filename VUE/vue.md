*vue笔记：*
=======
[官方文档](https://cn.vuejs.org)
### 引包：
> 1) cdn资源："https://unpkg.com/vue"。
> 2) 直接下载引用。

### 注意事项：
	1)创建一个Vue的构造器实例对象。插入到html中将要渲染的地方。
		var app = new Vue({
			el:'#app',          (插入元素,勿直接插入body否则会报错)
			data:{
				message:'hello lishen !'
			}
		})
		vue实例对象的属性有 el(插入元素),data(初始化数据),computed(计算属性),methods(方法),watch(监控)等。。 
	2)使用自定义组件的时候(自定义标签),要是用Vue.component来声明。其中prop是父组件用来传递数据的一种自定义属性。因为组件有自己独立的作用域,注意。。自定义组件是不能在html中直接渲染的,必须通过template来实现。。虚拟标签
		Vue.component('demo-aa-bb',{
				props:['demo'],
				template:'<li>{{demo.text}}</li>'
			})
	3）注意,不要在实例属性或者回调函数中使用箭头函数,因为箭头函数绑定父上下文。会使得函数中的this不会指向实例对象。而是指向window对象。。
	4)在使用Vue.extend()创建子类构造器时注意data必须是一个函数。。
	5)任何复杂逻辑都应当使用计算属性。。
	6)计算属性基于它的依赖缓存,只有当其相关依赖发生改变时才会重新取值。优化性能。
	7)使用相同的条件模板可提高复用性(输入文本可保持不变)。可使用参数'key'来决定是否复用元素。。
	8)对于dom事件细节,可通过由'.'表示的指令来调用修饰符(事件修饰符)。
		.stop   	阻止事件的冒泡。。
		.prevent  	取消默认行为。。
		.capture 	事件捕获。。
		.self    	该元素本身(非子类元素)触发时触发回调。。
		.once 		只触发一次。。
		.enter 		按键修饰符enter键(更多按键修饰符可查看官方文档)
		.lazy 		使得input中的值与数据在change事件中同步。
		.trim 		自动过滤用户输入值的首尾空格。
		.number 	自动将用户输入的值转化为Number类型。

---
### 指令(vue指令都带有'v-'前缀,类比于ng指令)：
	1) v-bind 		绑定动态变化的指令(多应用于列表中)。。(缩写可用':'表示)
	2-1) v-if   	假设指令。。其值是一个布尔值(使用切换次数少场景)。
	2-2) v-else		与if或者else-if连用，否则不识别。
	3) v-for  		遍历（item in item）。
	4) v-on   		绑定事件的方法(缩写可用'@')。
	5) v-model 		双向数据绑定
	6) v-once 		只能绑定一次插值。当数据改变时，插入的值不会随之改变。慎用。。
	7) v-html       html文本。
	8) {{exam}}   纯文本。。(没有html标签包裹的文本,它可放在html标签里面,转化为html文本)。
	9) v-show		根据条件显示指令(不支持template语法,适用于频繁切换场景)。
---
### 组件
	1. 组件（Component）是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素， Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。
	2. 要注册一个全局组件，你可以使用 Vue.component(tagName, options)。
	3. 组件在注册之后，便可以在父实例的模块中以自定义元素 <my-component></my-component> 的形式使用。要确保在初始化根实例 之前 注册了组件。
	4. 在一部分标签中,如 ul ol select tr等。。严格限定了子标签的格式。这时直接设置<my-name>自定义标签会无效。相对的我们可用 is来转化。。如<li is='my-name'></li>。(字符串模板除外)。
	5. 在父子组件中它们的关系通常是props down 和 events up ,父组件向子组件传递数据用props ,子组件向父组件通讯用events。(组件实例的作用域是孤立的)。
	6. 使用v-on绑定自定义事件,使用$on(eventName)监听事件,使用$emit(eventName)触发事件。。
	7. slot内容分发。。(分发内容是在父组件内编译)。。
	8. vue组件的api来自slots,props,Events三部分,其中,props允许外部环境传递数据给组件,Events允许触发外部环境的副作用,slots允许将外部环境的内容组合在组件中。
	9. 子组件索引。。ref可为子组件指定一个索引id ($refs.id)..它是在组件渲染完成后才会填充,应当避免在模板或计算属性中使用。。

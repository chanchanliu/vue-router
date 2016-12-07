# vue-router 学习笔记

## 目录

### 绑定一个元素

- 

    > 如果new Vue不写在$(document).ready(function() {}里面的话，就必须写在最后面，这样才能保证页面元素是先于js加载的

``` 
<script>
	$(document).ready(function() {
	    new Vue({
	        el: '#app',
	        data: {
	            message: 'Hello Vue.js!'
	        }
	    })
	});
</script>

<div id="app">
  {{ message }}
</div>
 ```

### 双向绑定

- 

    > v-model绑定input

``` 
<!-- 同时绑定message和v-modle="messsage"的两个元素，名为双向绑定。 -->
<script>
$(document).ready(function() {
    new Vue({
        el: '#app',
        data: {
            message: 'Hello Vue.js!'
        }
    })
});
</script>
<div id="app">
<!-- 因为是在Django的模板中调试，Django和Vue的{{info}}都是关键字，所以使用{% templatetag openvariable %} info {% templatetag closevariable %} 来包裹信息。这样的话被，经过渲染之后，{% templatetag openvariable %} info {% templatetag closevariable %}就变成了{{info}} -->
    {% templatetag openvariable %}message{% templatetag closevariable %}
    <input v-model="message">
</div>
 ```

### 渲染列表

- 

    > v-for绑定列表

```
	<div id="app">
    <div id="app">
        <ul>
            <li v-for="todo in todos">
                {% templatetag openvariable %} todo.text {% templatetag closevariable %}
            </li>
        </ul>
    </div>
</div>
<!-- js中data的todos和li标签中v-for的in todos同一个名称，另外在{{}}中必须todo.txt,才能渲染到， -->
<script>
    new Vue({
      el: '#app',
      data: {
        todos: [
          { text: 'Learn JavaScript' },
          { text: 'Learn Vue.js' },
          { text: 'Build Something Awesome' }
        ]
      }
    })      
</script>
```

### 处理用户输入
	
- 

    > v-on绑定点击事件

```
<script>
    $(document).click(function (){
        new Vue({
            el: '#app',
            data:{
                message:'Hello Vue.js!'
            },
            //在Vue里面方法必须写在methods里面，格式是functionname:function(){}
            methods:{
                reverseMessage:function(){
                    this.message = this.message.split('').reverse().join('')
                }
            }
        })
    })
</script>
<div id="app">
    <p>{% templatetag openvariable %} message {% templatetag closevariable %}</p>
    <!-- 绑定button使用v-on，格式是v-on:触发事件名="方法名" -->
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

### 综合

```
<script>
    $(document).click(function (){
        new Vue({
            el: '#app',
            data:{
                newTodo:'',
                todos:[
                    {text:'Add some todos'}
                ]
            },
            methods:{
                addTodo:function(){
                    var text = this.newTodo.trim()
                    if(text){
                        this.todos.push({text:text})
                        this.newTodo = ''
                    }
                },
                removeTodo:function(index){
                    console.log(index)
                    //splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目。
                    this.todos.splice(index, 1)
                }
            }
        })
    })
</script>

<div id="app">
    <!-- 在input里面敲回车键就触发了addTodo方法，添加了新的li标签 -->
    <input v-model="newTodo" v-on:keyup.enter="addTodo">
    <ul>
        <li v-for="todo in todos">
            <span>{% templatetag openvariable %} todo.text {% templatetag closevariable %}</span>
            <!-- 点击button就触发了removeTodo方法 -->
            <button v-on:click="removeTodo($index)">x</button>
        </li>
    </ul>
</div>
```

### 相应数据的绑定

-

> Vue.js 也提供一个强大的过渡效果系统，可以在 Vue 插入/删除元素时自动应用过渡效果。

```
<div id="example-2">
	<!-- v-if,当greeting为true的时候，hello才显示-->
	<p v-if="greeting">Hello!</p>
</div>
<script>
	var exampleVM2 = new Vue({
		el: '#example-2',
		data: {
			greeting: true
		}
	})
</script>
```

-

 > v-bind 指令用于绑定 HTML 特性


### 组件系统

-

>  组件系统是 Vue.js 另一个重要概念，因为它提供了一种抽象，让我们可以用独立可复用的小组件来构建大型应用。如果我们考虑到这点，几乎任意类型的应用的界面都可以抽象为一个组件树。

### 构造器
	
-

> 每个 Vue.js 应用的起步都是通过构造函数 Vue 创建一个 Vue 的根实例。

> 一个 Vue 实例其实正是一个 MVVM 模式中所描述的 ViewModel - 因此在文档中经常会使用 vm 这个变量名。

> 在实例化 Vue 时，需要传入一个选项对象，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。全部的选项可以在 API 文档中查看。

> 可以扩展 Vue 构造器，从而用预定义选项创建可复用的组件构造器


```
var MyComponent = Vue.extend({
  // 扩展选项
})

// 所有的 MyComponent 实例都将以预定义的扩展选项被创建
var myComponentInstance = new MyComponent()
```
-

> 每个Vue实例都有它的方法（methods）和数据（date），和绑定的元素对象（el）


```
var data = { a: 1 }
var vm = new Vue({
	data: data
})

vm.a === data.a // -> true

// 设置属性也会影响到原始数据
vm.a = 2
data.a // -> 2

// ... 反之亦然
data.a = 3
vm.a // -> 3
```

-

> 每个 Vue 实例都会代理其 data 对象里所有的属性，只有这些被代理的属性是响应的。


### 实例的生命周期

-

> Vue 实例在创建时有一系列初始化步骤——例如，它需要建立数据观察，编译模板，创建必要的数据绑定。在此过程中，它也将调用一些生命周期钩子，给自定义逻辑提供运行机会。例如 created 钩子在实例创建后调用：

```
var vm = new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// -> "a is: 1"
```

#### 也有一些其它的钩子，在实例生命周期的不同阶段调用，如 compiled、 ready 、destroyed。钩子的 this 指向调用它的 Vue 实例。一些用户可能会问 Vue.js 是否有“控制器”的概念？答案是，没有。组件的自定义逻辑可以分割在这些钩子中。 

### 数据绑定语法

#### Vue.js 的模板是基于 DOM 实现的。这意味着所有的 Vue.js 模板都是可解析的有效的 HTML，且通过一些特殊的特性做了增强。Vue 模板因而从根本上不同于基于字符串的模板，请记住这点。

### 插入数据值

-

> 数据绑定最基础的形式是文本插值，使用 “Mustache” 语法（双大括号）：

```
<span>Message: {{ msg }}</span>
<!-- 在django中双大括号是模板的渲染语法，所以要用另一种方法实现双大括号语法。 -->
{% templatetag openvariable %} msg {% templatetag closevariable %}
```

-

> 插入HTML

```
<div>{{{ raw_html }}}</div>
```

-

> 插入到HTML值的属性值里

```
<div id="item-{{ id }}"></div>
```

### 绑定表达式

-

> 

** JavaScript 表达式 **

> 可以直接插入加减乘除、三元运算、以及javascript的函数

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<!-- 一个限制是每个绑定只能包含单个表达式  -->
<!-- 这是一个语句，不是一个表达式： -->
{{ var a = 1 }}

<!-- 流程控制也不可以，可改用三元表达式 -->
{{ if (ok) { return message } }}
```

### 指令
### 计算属性
### 绑定Class和CSS
### 绑定HTML class
### 绑定内联样式CSS
### 条件渲染
### if-else结构
### 使用template标签包装多个元素实现if-else的多元素切换
### v-show指令实现依赖条件决定是否展示数据
### 组件警告
### v-for
### template v-for
### 数组变动检测
### v-for对象
### 值域 v-for
### 显示过滤排序的结果
### 方法与事件处理器
### 可以用 v-on 指令监听 DOM 事件
### 内联 JavaScript 语句可以传递参数
### 事件修饰符
### 按键修饰符
### 为什么在 HTML 中监听事件
### 表单控件绑定
### 基础用法
### 绑定value
### 参数特性
### 组件
### 使用组件extend-component
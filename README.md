# vue-router 学习笔记

## 目录

### 绑定一个元素 

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

###  双向绑定

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

 > v-bind 指令用于绑定 HTML 特性

### 组件系统

>  **组件系统是 Vue.js 另一个重要概念，因为它提供了一种抽象，让我们可以用独立可复用的小组件来构建大型应用。如果我们考虑到这点，几乎任意类型的应用的界面都可以抽象为一个组件树。**

### 构造器

> **每个 Vue.js 应用的起步都是通过构造函数 Vue 创建一个 Vue 的根实例。**

> **一个 Vue 实例其实正是一个 MVVM 模式中所描述的 ViewModel - 因此在文档中经常会使用 vm 这个变量名。**

> **在实例化 Vue 时，需要传入一个选项对象，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。全部的选项可以在 API 文档中查看。**

> **可以扩展 Vue 构造器，从而用预定义选项创建可复用的组件构造器**

```
var MyComponent = Vue.extend({
  // 扩展选项
})

// 所有的 MyComponent 实例都将以预定义的扩展选项被创建
var myComponentInstance = new MyComponent()
```

> **每个Vue实例都有它的方法（methods）和数据（date），和绑定的元素对象（el）**


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

> **每个 Vue 实例都会代理其 data 对象里所有的属性，只有这些被代理的属性是响应的。**


### 实例的生命周期

> **Vue 实例在创建时有一系列初始化步骤——例如，它需要建立数据观察，编译模板，创建必要的数据绑定。在此过程中，它也将调用一些生命周期钩子，给自定义逻辑提供运行机会。例如 created 钩子在实例创建后调用：**

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

**也有一些其它的钩子，在实例生命周期的不同阶段调用，如 compiled、 ready 、destroyed。钩子的 this 指向调用它的 Vue 实例。一些用户可能会问 Vue.js 是否有“控制器”的概念？答案是，没有。组件的自定义逻辑可以分割在这些钩子中。** 

### 数据绑定语法

**Vue.js 的模板是基于 DOM 实现的。这意味着所有的 Vue.js 模板都是可解析的有效的 HTML，且通过一些特殊的特性做了增强。Vue 模板因而从根本上不同于基于字符串的模板，请记住这点。**

### 插入数据值

> **数据绑定最基础的形式是文本插值，使用 “Mustache” 语法（双大括号）：**

```
<span>Message: {{ msg }}</span>
<!-- 在django中双大括号是模板的渲染语法，所以要用另一种方法实现双大括号语法。 -->
{% templatetag openvariable %} msg {% templatetag closevariable %}
```

> **插入HTML**

```
<div>{{{ raw_html }}}</div>
```

> **插入到HTML值的属性值里**

```
<div id="item-{{ id }}"></div>
```

### 绑定表达式

> **JavaScript 表达式** 

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

> **过滤器（与javascript表达式相互结合，过滤器只能跟在js表达式后面）**

> **Vue.js 允许在表达式后添加可选的“过滤器 (Filter) ”，以“管道符”指示：**

```{{ message | capitalize }}```

这里我们将表达式 message 的值“管输（pipe）”到内置的 capitalize 过滤器，这个过滤器其实只是一个 JavaScript 函数，返回大写化的值。Vue.js 提供数个内置过滤器。

**过滤器可以串联：**

```{{ message | filterA | filterB }}```

**过滤器也可以接受参数：**

```{{ message | filterA 'arg1' arg2 }}```

**过滤器函数始终以表达式的值作为第一个参数。**带引号的参数视为字符串，而不带引号的参数按表达式计算。这里，字符串 ‘arg1’ 将传给过滤器作为第二个参数，表达式 arg2 的值在计算出来之后作为第三个参数。

### 指令

> **参数**
有些指令可以在其名称后面带一个“参数” (Argument)，中间放一个冒号隔开。例如，**v-bind 指令用于响应地更新 HTML 特性：**

```<a v-bind:href="url"></a>```

用特性插值 href=”{{url}}” 获得同样的结果：这样没错，并且实际上在**内部特性插值会转为 v-bind 绑定**。

另一个例子是 **v-on 指令，它用于监听 DOM 事件：**

```<a v-on:click="doSomething">```

> **修饰器**

**修饰符 (Modifiers) 是以半角句号 . 开始的特殊后缀**，用于表示指令应当以特殊方式绑定。例如 .literal 修饰符告诉指令将它的值解析为一个字面字符串而不是一个表达式：

```<a v-bind:href.literal="/a/b/c"></a>```

> **缩写**

针对常用v-bind和v-on是有一些缩写的

v-bind

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>

<!-- 缩写 -->
<a :href="url"></a>

<!-- 完整语法 -->
<button v-bind:disabled="someDynamicCondition">Button</button>

<!-- 缩写 -->
<button :disabled="someDynamicCondition">Button</button>
```

v-on

```
<a v-on:click="doSomething"></a>
<a @click="doSomething"></a>
```

### 计算属性

在模板中绑定表达式是非常便利的，但是它们实际上只用于简单的操作。模板是为了描述视图的结构。在模板中放入太多的逻辑会让模板过重且难以维护。这就是为什么 Vue.js 将绑定表达式限制为一个表达式。如果需要多于一个表达式的逻辑，应当使用计算属性。

```
<div id='exmple'>
    a = {% templatetag openvariable %} a {% templatetag closevariable %},b = {% templatetag openvariable %} b {% templatetag closevariable %}
</div>

<script>
    var vm = new Vue({
        el:'#exmple',
        data:{
            a:1  //a的属性值
        },
        computed:{ //这个computed是随便起的名字吗？
            //一个计算属性的getter，这里我们声明了一个计算属性 b。我们提供的函数将用作属性 vm.b的 getter。
            b:function(){
                return this.a + 1
            }
        }
    })
</script>
```

**vm.b 依赖于 vm.a，因此当 vm.a 发生改变时，依赖于 vm.b 的绑定也会更新。**

> **$watch**

Vue.js 提供了一个方法 watch，它用于观察Vue实例上的数据变动。当一些数据需要根据其它数据变化时，watch 很诱人 —— 特别是如果你来自 AngularJS。**不过，通常更好的办法是使用计算属性而不是一个命令式的 $watch 回调。**

```
<div id="demo">{{fullName}}</div>
<script>
    var vm = new Vue({
        el: '#demo',
        data: {
            firstName: 'Foo',
            lastName: 'Bar',
            fullName: 'Foo Bar'
        }
    })

    vm.$watch('firstName', function(val) {
        this.fullName = val + ' ' + this.lastName
    })

    vm.$watch('lastName', function(val) {
        this.fullName = this.firstName + ' ' + val
    })
</script>
```

**上面代码是命令式的重复的。跟计算属性对比**

```
var vm = new Vue({
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

> **计算属性默认只是 getter，不过在需要时你也可以提供一个 setter：**

```
<div id="demo">
    {% templatetag openvariable %} fullName {% templatetag closevariable %}
</div>
<script>
    var vm = new Vue({
        el:'#demo',
        data: {
          firstName: 'Foo',
          lastName: 'Bar'
        },
        computed: {
          fullName: {
            // getter
            get: function () {
              return this.firstName + ' ' + this.lastName
            },
            // setter
            set: function (newValue) {
              var names = newValue.split(' ')
              this.firstName = names[0]
              this.lastName = names[names.length - 1]
            }
          }
        }
    })
</script>
```

**使用setter方法之后，就是firstName和lastName就会随着fullname动态变化了。**

```
vm.fullName = 'Tony Dandelion'
"Tony Dandelion"
vm.firstName
"Tony"
vm.lastName
"Dandelion"
```

### 绑定Class和CSS

### 绑定HTML class

尽管可以用 Mustache 标签绑定 class，比如 class=”{{ className }}”，但是我们不推荐这种写法和 v-bind:class 混用。两者只能选其一！

> **面向对象的绑定**

```
<div class="static" v-bind:class="{ 'class-a': isA, 'class-b': isB }" qq></div>
<script>
    var vm = new Vue({
        el:'#demo',
        data: {
            isA: true,
            isB: false
        }
    })
</script>
<!-- 最终效果是<div class="static class-a"></div> -->
```

你也可以直接绑定数据里的一个对象：

```
<div v-bind:class="classObject"></div>

data: {
  classObject: {
    'class-a': true,
    'class-b': false
  }
}
```

> **数组绑定**

我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：

```
<div v-bind:class="[classA, classB]">
data: {
  classA: 'class-a',
  classB: 'class-b'
}
```

渲染为：

```
<div class="class-a class-b"></div>
```

如果你也想根据条件切换列表中的 class，可以用三元表

```<div v-bind:class="[classA, isB ? classB : '']">```

终添加 classA，但是只有在 isB 是 true 时添加 classB 。

不过，当有多个条件 class 时这样写有些繁琐。在 1.0.19+ 中，可以在数组语法中使用对象语法：

```<div v-bind:class="[classA, { classB: isB, classC: isC }]">```

### 绑定内联样式CSS

> **面向对象绑定样式**

v-bind:style 的对象语法十分直观——看着非常像 CSS，其实它是一个 JavaScript 对象。CSS 属性名可以用驼峰式（camelCase）或短横分隔命名（kebab-case）：

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
data: {
  activeColor: 'red',
  fontSize: 30
}
```

**直接绑定到一个样式对象通常更好**，让模板更清晰：

```
<div v-bind:style="styleObject"></div>
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

同样的，对象语法常常结合返回对象的计算属性使用。

> **数组语法**

v-bind:style 的数组语法可以将多个样式对象应用到一个元素上：

```<div v-bind:style="[styleObjectA, styleObjectB]">```

> **自动添加前缀**

**当 v-bind:style 使用需要厂商前缀的 CSS 属性时，如 transform，Vue.js 会自动侦测并添加相应的前缀。**

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
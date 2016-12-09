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

在 Vue.js，我们使用 v-if 指令实现同样的功能：

```<h1 v-if="ok">Yes</h1>```

也可以用 v-else 添加一个 “else” 块：

```
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```
```
<div id="demo">
    <h1 v-if="is">Yes</h1>
    <h1 v-else>No</h1>
</div>

<script>
    var boolea = false
    var vm = new Vue({
        el:'#demo',
        data: {
            is: boolea,
        }
    })
</script>
```

### 使用template标签包装多个元素实现if-else的多元素切换

```
<div id="demo">
    <template v-if="is">
        <h1>Yes</h1>
        <h1> you are right!</h1>
    </template>
    <template v-else>
        <h1>No</h1>
        <h1>you are wrong!</h1>
    </template>
</div>
<script>
var boolea = true
var vm = new Vue({
    el: '#demo',
    data: {
        is: boolea,
    }
})
</script>
```

### v-show指令实现依赖条件决定是否展示数据

**v-show是不支持template标签对多个元素进行包装的 
也可以使用v-else给v-show设置else块**

```
<div id="demo">
    <h1 v-show='is'>Yes</h1>
</div>
<script>
var boolea = false
var vm = new Vue({
    el: '#demo',
    data: {
        is: boolea,
    }
})
</script>
```

### 组件警告

将 v-show 用在组件上时，因为指令的优先级 v-else 会出现问题。因此不要这样做：

```
<custom-component v-show="condition"></custom-component>
<p v-else>这可能也是一个组件</p>
```

用另一个 v-show 替换 v-else：

```
<custom-component v-show="condition"></custom-component>
<p v-show="!condition">这可能也是一个组件</p>
```

这样就可以达到 v-if 的效果。

> **一下是警告内容**

**vue.js:1023 [Vue warn]: Unknown custom element: - did you register the component correctly? For recursive components, make sure to provide the “name” option.**

**一般来说，v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好。**

**列表渲染(data不同数据名之间是用 , 相互间隔的)**

### v-for

**可以使用 v-for 指令基于一个数组渲染一个列表。这个指令使用特殊的语法，形式为 item in items，items 是数据数组，item 是当前数组元素的别名：**

列表渲染使用的都是数组。在data中的申明格式是：

```
数组名:[
    {元素名1:数据1,元素名2:数据5,元素3.....}
    {元素名1:数据2,元素名2:数据6,元素3.....}
    {元素名1:数据3,元素名2:数据7,元素3.....}        
]

example：
items:[
    {A:1,b:6,c:10},
    {A:2,b:7,c:11},
    {A:3,b:8,c:12}
]
```

使用方法

```
<li v-for='当前数组元素的别名 in 数组名'>
    {% templatetag openvariable %} 当前数组元素的别名.当前数组元素中具体要遍历的元素名 {% templatetag closevariable %}
</li>

example：
<li v-for='item in items'>
    {% templatetag openvariable %} item.b {% templatetag closevariable %}
</li>
```

**在 v-for 块内我们能完全访问父组件作用域内的属性，另有一个特殊变量 $index，正如你猜到的，它是当前数组元素的索引：**

```
<ol id="demo">
    <li v-for="item in items">
        {% templatetag openvariable %} parentMessage {% templatetag closevariable %} - {% templatetag openvariable %} $index {% templatetag closevariable %} - {% templatetag openvariable %} item.c {% templatetag closevariable %}
    </li>
</ol>

<script>
    new Vue({
        el:'#demo',
        data: {
            parentMessage:'Parent',
            items:[
                {A:1,b:6,c:10},
                {A:2,b:7,c:11},
                {A:3,b:8,c:12}
            ]
        }
    })
</script>

<!-- 数组下标从0开始 -->
Parent - 0 - 10
Parent - 1 - 11
Parent - 2 - 12
```

### template v-for

**使用template标签，将多个数据包装成块。**

### 数组变动检测

> **变异方法(修改原始数组，影响页面的渲染效果。)**

```
push()  #从最后开始添加
pop() #从后往前删除
shift()  #从前往后删除
unshift() 
splice()  #splice() 方法用于插入、删除或替换数组的元素。
sort()  #排序
reverse() #逆序
```

> **替换数组（不修改原始数据）**

变异方法，如名字所示，修改了原始数组。相比之下，也有非变异方法，如 filter(), concat() 和 slice()，不会修改原始数组而是返回一个新数组。在使用非变异方法时，可以直接用新数组替换旧数组：

```
slice() #可提取字符串的某个部分,并以新的字符串返回被提取的部分
filter() #过滤
concat() #连接两个或多个数组
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

可能你觉得这将导致 Vue.js 弃用已有 DOM 并重新渲染整个列表——幸运的是并非如此。 Vue.js 实现了一些启发算法，以最大化复用 DOM 元素，因而**用另一个数组替换数组是一个非常高效的操作。**

> **track-by**

有时需要用全新对象（例如通过 API 调用创建的对象）替换数组。因为 **v-for 默认通过数据对象的特征来决定对已有作用域和 DOM 元素的复用程度**，这可能导致重新渲染整个列表。但是，**如果每个对象都有一个唯一 ID 的属性，便可以使用 track-by 特性给 Vue.js 一个提示，Vue.js 因而能尽可能地复用已有实例。**

```
<ol id="demo">
    <div v-for="item in items" track-by="_uid">
        {% templatetag openvariable %} item._uid {% templatetag closevariable %}
    </div>
</ol>

<script>
var example1 = new Vue({
    el: '#demo',
    data: {
        items: [
          { _uid: '88f869d'},
          { _uid: '7496c10'}
        ]
    }
})
</script>
输出：
88f869d
7496c10
```

**然后在替换数组 items 时，如果 Vue.js 遇到一个包含 _uid: ‘88f869d’ 的新对象，它知道它可以复用这个已有对象的作用域与 DOM 元素。**

> **track-by $index**

如果没有唯一的键供追踪，**可以使用 track-by=”$index”，它强制让 v-for 进入原位更新模式：片断不会被移动，而是简单地以对应索引的新值刷新。**这种模式也能处理数据数组中重复的值。

```
<ol id="demo">
    <div v-for="item in items" track-by="$index">
        {% templatetag openvariable %} item.messge {% templatetag closevariable %}
    </div>
</ol>

<script>
var example1 = new Vue({
    el: '#demo',
    data: {
        items: [
          { messge:'Tom'},
          { messge:'Jack'}
        ]
    }
})
</script>
```

这让数据替换非常高效，但是也会付出一定的代价。**因为这时 DOM 节点不再映射数组元素顺序的改变，不能同步临时状态（比如 元素的值）以及组件的私有状态。因此，如果 v-for 块包含 元素或子组件，要小心使用 track-by=”$index”**

> **问题**

因为 JavaScript 的限制，Vue.js 不能检测到下面数组变化：

1. 直接用索引设置元素，如 vm.items[0] = {}；
2. 修改数据的长度，如 vm.items.length = 0。

为了解决问题 (1)，Vue.js 扩展了观察数组，为它添加了一个 $set() 方法：

```
// 与 `example1.items[0] = ...` 相同，但是能触发视图更新
example1.items.$set(0, { childMsg: 'Changed!'})
```

至于问题 (2)，只需用一个空数组替换 items。

```example1.items = []```

除了 $set()， Vue.js 也为观察数组添加了 $remove() 方法，用于从目标数组中查找并删除元素，在内部它调用 splice() 。因此，不必这样：

```
var index = this.items.indexOf(item)
if (index !== -1) {
  this.items.splice(index, 1)
}
```

只用这样：

```
this.items.$remove(item)
```

使用 Object.freeze()

在遍历一个数组时，如果数组元素是对象并且对象用 Object.freeze() 冻结，**你需要明确指定 track-by**。在这种情况下如果 Vue.js 不能自动追踪对象，将给出一条警告。

### v-for对象

也可以使用 v-for 遍历对象。除了 $index 之外，**作用域内还可以访问另外一个特殊变量 $key。**

```
<ul id="repeat-object" class="demo">
  <li v-for="value in object">
    {{ $key }} : {{ value }}
  </li>
</ul>
new Vue({
  el: '#repeat-object',
  data: {
    object: {
      FirstName: 'John',
      LastName: 'Doe',
      Age: 30
    }
  }
})
```

### 值域 v-for

v-for 也可以接收一个整数，此时它将重复模板数次。

```
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
结果：
0 1 2 3 4 5 6 7 8 9
```

### 显示过滤排序的结果

有时我们想显示过滤/排序过的数组，同时不实际修改或重置原始数据。有两个办法：

1. 创建一个计算属性，返回过滤/排序过的数组；
2. 使用内置的过滤器 filterBy 和 orderBy。

计算属性有更好的控制力，也更灵活，因为它是全功能 JavaScript。但是通常过滤器更方便，详细见 API。

### 方法与事件处理器
### 可以用 v-on 指令监听 DOM 事件

```
<div id="example">
  <button v-on:click="greet">Greet</button>
</div>
```

我们绑定了一个单击事件处理器到一个方法 greet。下面在 Vue 实例中定义这个方法：

```
var vm = new Vue({
  el: '#example',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // 方法内 `this` 指向 vm
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      alert(event.target.tagName)
    }
  }
})
```

### 内联 JavaScript 语句可以传递参数

```
<div id="example-2">
  <button v-on:click="say('hi')">Say Hi</button>
  <button v-on:click="say('what')">Say What</button>
</div>
new Vue({
  el: '#example-2',
  methods: {
    say: function (msg) {
      alert(msg)
    }
  }
})
Result:
Say Hi  Say What
```

类似于内联表达式，**事件处理器限制为一个语句。**

有时也需要在内联语句处理器中访问原生 DOM 事件。**可以用特殊变量 $event 把它传入方法：**

```
<button v-on:click="say('hello!', $event)">Submit</button>
// ...
methods: {
  say: function (msg, event) {
    // 现在我们可以访问原生事件对象
    event.preventDefault()
  }
}
```

### 事件修饰符

在事件处理器中经常需要调用 event.preventDefault() 或 event.stopPropagation()。尽管我们在方法内可以轻松做到，不过让**方法是纯粹的数据逻辑而不处理 DOM 事件细节会更好**。

为了解决这个问题，**Vue.js 为 v-on 提供两个 事件修饰符：.prevent 与 .stop**。你是否还记得修饰符是点号打头的指令后缀？

```
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat">

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

1.0.16 添加了两个额外的修饰符：

<!-- 添加事件侦听器时使用 capture 模式 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>
```

### 按键修饰符

在监听键盘事件时，我们经常需要检测 keyCode。Vue.js 允许为 v-on 添加按键修饰符：

```
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
记住所有的 keyCode 比较困难，Vue.js 为最常用的按键提供别名：

<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
全部的按键别名：

enter
tab
delete
esc
space
up
down
left
right

1.0.8+： 支持单字母按键别名。
1.0.17+： 可以自定义按键别名：
```

```
// 可以使用 @keyup.f1
Vue.directive('on').keyCodes.f1 = 112
```

### 为什么在 HTML 中监听事件

你可能注意到这种事件监听的方式违背了传统理念 “separation of concern”。不必担心，因为所有的 Vue.js 事件处理方法和表达式都严格绑定在当前视图的 ViewModel 上，它不会导致任何维护困难。实际上，**使用 v-on 有几个好处：**

* 扫一眼 HTML 模板便能轻松定位在 JavaScript 代码里对应的方法。
* 因为你无须在 JavaScript 里手动绑定事件，你的 ViewModel 代码可以是非常纯粹的逻辑，和 DOM 完全解耦，更易于测试。
* 当一个 ViewModel 被销毁时，所有的事件处理器都会自动被删除。你无须担心如何自己清理它们。

### 表单控件绑定
### 基础用法

> **Text**

```
<span>Message is: {{ message }}</span>
<br>
<input type="text" v-model="message" placeholder="edit me">
```

> **checkbox**

**单个勾选框，逻辑值：**

```
<div id="demo">
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{% templatetag openvariable %} checked {% templatetag closevariable %}</label>
</div>
<script>
var bool = true;
new Vue({
    el: "#demo",
    data: {
        checked: bool
    }
})
</script>
```

> **Radio**

```
<div id="demo">
    <input type="radio" id="one" value="One" v-model="picked">
    <label for="one">One</label>
    <br>
    <input type="radio" id="<two></two>" value="Two" v-model="picked">
    <label for="two">Two</label>
    <br>
    <span>Picked: {% templatetag openvariable %} picked {% templatetag closevariable %}</span>
</div>
<script>
var bool = true;
new Vue({
    el: "#demo",
    data: {
        picked: 'One'
    }
})
</script>
```

> **Select**

**单选**

```
<div id="demo">
    <select v-model="selected">
        <option selected>A</option>
        <option>B</option>
        <option>C</option>
    </select>
    <span>Selected: {% templatetag openvariable %} selected {% templatetag closevariable %} </span>
</div>
<script>
var bool = true;
new Vue({
    el: "#demo",
    data: {
        selected: ''
    }
})
```

**多选（绑定到一个数组）**

**多了一个multiple**

```
<div id="demo">
<select v-model="selected" multiple>
  <option selected>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br>
<span>Selected: {% templatetag openvariable %}  selected | json  {% templatetag closevariable %}</span>
</div>
<script>
var bool = true;
new Vue({
    el: "#demo",
    data: {
        selected: ''
    }
})
</script>
```

**动态选项，用 v-for 渲染**

```
<div id="demo">
    <select v-model="selected">
        <option v-for="option in options" v-bind:value="option.value">
            {% templatetag openvariable %} option.text {% templatetag closevariable %}
        </option>
    </select>
    <span>Selected: {% templatetag openvariable %} selected  {% templatetag closevariable %}</span>
</div>
<script>
new Vue({
  el: '#demo',
  data: {
    selected: 'A',
    options: [
      { text: 'One', value: 'A' },
      { text: 'Two', value: 'B' },
      { text: 'Three', value: 'C' }
    ]
  }
})
</script>
```

### 绑定value

```
<!-- 当选中时，`picked` 为字符串 "a" -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` 为 true 或 false -->
<input type="checkbox" v-model="toggle">

<!-- 当选中时，`selected` 为字符串 "abc" -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

但是有时我们想**绑定 value 到 Vue 实例的一个动态属性上，这时可以用 v-bind 实现**，并且这个属性的值可以不是字符串。

> **Checkbox**

```
<input
  type="checkbox"
  v-model="toggle"
  v-bind:true-value="a"
  v-bind:false-value="b">
// 当选中时
vm.toggle === vm.a
// 当没有选中时
vm.toggle === vm.b
```

> **Radio**

```
<input type="radio" v-model="pick" v-bind:value="a">
// 当选中时
vm.pick === vm.a
```

> **Select Options**

```
<select v-model="selected">
  <!-- 对象字面量 -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
// 当选中时
typeof vm.selected // -> 'object'
vm.selected.number // -> 123
```

### 参数特性

> **lazy**

在默认情况下，v-model 在input 事件中同步输入框值与数据，可以添加一个特性 lazy，从而改到在 change 事件中同步：

```
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model="msg" lazy>
```

> **number**

如果想自动将用户的输入转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个特性 number

```
<input v-model="age" number>
```

> **debounce**

debounce 设置一个最小的延时，在每次敲击之后延时同步输入框的值与数据。如果每次更新都要进行高耗操作（例如在输入提示中 Ajax 请求），它较为有用。

```
<div id="demo">
    <input type="text" v-model="toggle" debounce="500">
    <span> {% templatetag openvariable %} toggle {% templatetag closevariable %} </span>
</div>
<script>
new Vue({
    el: '#demo',
    data: {
        toggle:""
    }
})
</script>
```

**注意** debounce 参数不会延迟 input 事件：它延迟“写入”底层数据。因此在使用 debounce 时应当用 vm.$watch() 响应数据的变化。若想延迟 DOM 事件，应当使用 debounce 过滤器。

### 组件

组件（Component）是 Vue.js 最强大的功能之一。**组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能。**在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。

### 使用组件extend-component

**页面渲染的时候**

```<my-component></my-component> --> my-component --> MyComponent --> <div>A custom component!</div>```

**使用的时候**

```
创建一个组件构造器 -----> 得到<div>A custom component!</div>-->MyComponent的关联关系，然后进行注册。 -----> 得到MyComponent-->my-component的关系。    这样一来，使用<my-component></my-component>就得到<div>A custom component!</div>了。
```

> **1、注册**

可以用 Vue.extend() 创建一个组件构造器：

```
var MyComponent = Vue.extend({
  // 选项...
})
```

要把这个构造器用作组件，需要用 Vue.component(tag, constructor) 注册 ：

```
// 全局注册组件，tag 为 my-component
Vue.component('my-component', MyComponent)
```

实例：**注意，使用的是extend不是extends。**

```
<div id="example">
    <my-component></my-component>
</div>
<script>
    //创建一个组件构造器
    var MyComponent = Vue.extend({
        template:'<div>A custom component!</div>'
    })
    //注册，把MyComponent注册成my-componen这个名字
    Vue.component('my-component',MyComponent)
    new Vue({
        el:'#example'
    })
</script>
```

注意组件的模板替换了自定义元素，**自定义元素的作用只是作为一个挂载点。**可以用实例选项 replace 决定是否替换。

> **2、局部注册**

不需要全局注册每个组件。可以让组件只能用在其它组件内，用实例选项 components 注册，局部注册和全局注册的区别是，局部注册是在父类组件的components中注册

```
var Child = Vue.extend({ /* ... */ })

var Parent = Vue.extend({
  template: '...',
  components: {
    // <my-component> 只能用在父组件模板内
    'my-component': Child
  }
})
```

这种封装也适用于其它资源，如**指令、过滤器和过渡。**

> **3、注册语法糖**

为了让事件更简单，可以直接传入选项对象而不是构造器给 Vue.component() 和 component 选项。Vue.js 在背后自动调用 Vue.extend()：

```
// 在一个步骤中扩展与注册
Vue.component('my-component', {
  template: '<div>A custom component!</div>'
})

// 局部注册也可以这么做
var Parent = Vue.extend({
  components: {
    'my-component': {
      template: '<div>A custom component!</div>'
    }
  }
})
```

> **4、组件选项问题**

传入 Vue 构造器的多数选项也可以用在 Vue.extend() 中，不过有两个特例： **data 和 el。**试想如果我们简单地把一个对象作为 data 选项传给 Vue.extend()：

```
var data = { a: 1 }
var MyComponent = Vue.extend({
  data: data
})
```

这么做的问题是 **MyComponent 所有的实例将共享同一个 data 对象！**这基本不是我们想要的，因此我们应当**使用一个函数作为 data 选项，让这个函数返回一个新对象：**

```
var MyComponent = Vue.extend({
  data: function () {
    return { a: 1 }
  }
})
```

同理，**el 选项用在 Vue.extend() 中时也须是一个函数。**

> **5、模板解析问题**

Vue 的模板是 DOM 模板，使用浏览器原生的解析器而不是自己实现一个。相比字符串模板，DOM 模板有一些好处，但是也有问题，它必须是有效的 HTML 片段。一些 HTML 元素对什么元素可以放在它里面有限制。常见的限制：

1. a 不能包含其它的交互元素（如按钮，链接）
2. ul 和 ol 只能直接包含 li
3. select 只能包含 option 和 optgroup
4. table 只能直接包含 thead, tbody, tfoot, tr, caption, col, colgroup
5. tr 只能直接包含 th 和 td

在实际中，这些限制会导致意外的结果。尽管在简单的情况下它可能可以工作，但是你不能依赖自定义组件在浏览器验证之前的展开结果。例如 … 不是有效的模板，即使 my-select 组件最终展开为 …。

另一个结果是，**自定义标签（包括自定义元素和特殊标签，如 <component>、<template>、 <partial> ）不能用在 ul, select, table 等对内部元素有限制的标签内。**放在这些元素内部的自定义标签将被提到元素的外面，因而渲染不正确。

**对于自定义元素，应当使用 is 特性：**

```
<table>
  <tr is="my-component"></tr>
</table>
<template> 不能用在 <table> 内，这时应使用 <tbody>，<table> 可以有多个 <tbody>：

<table>
  <tbody v-for="item in items">
    <tr>Even row</tr>
    <tr>Odd row</tr>
  </tbody>
</table>
```

> **6、Props**

使用 Props 传递数据

组件实例的作用域是孤立的。这意味着不能并且不应该在子组件的模板内直接引用父组件的数据。**可以使用 props 把数据传给子组件。**

**“prop” 是组件数据的一个字段，期望从父组件传下来。子组件需要显式地用 props 选项 声明 props：**

```
Vue.component('child', {
  // 声明 props
  props: ['msg'],
  // prop 可以用在模板内
  // 可以用 `this.msg` 设置
  template: '<span>{{ msg }}</span>'
})
```

然后向它传入一个普通字符串：

```
<child msg="hello!"></child>
```

> **7、camelCase vs. kebab-case**

HTML 特性不区分大小写。**名字形式为 camelCase 的 prop 用作特性时，需要转为 kebab-case（短横线隔开）：**

```
Vue.component('child', {
  // camelCase in JavaScript
  props: ['myMessage'],
  template: '<span>{{ myMessage }}</span>'
})
<!-- kebab-case in HTML -->
<child my-message="hello!"></child>
```

> **8、动态 Props**

类似于用 v-bind 绑定 HTML 特性到一个表达式，**也可以用 v-bind 绑定动态 Props 到父组件的数据。每当父组件的数据变化时，也会传导给子组件：**

```
<div>
  <input v-model="parentMsg">
  <br>
  <child v-bind:my-message="parentMsg"></child>
</div>
```

使用 v-bind 的缩写语法通常更简单：

```
<child :my-message="parentMsg"></child>
```

> **9、字面量语法 vs. 动态语法**

初学者常犯的一个错误是使用字面量语法传递数值：

```
<!-- 传递了一个字符串 "1" -->
<comp some-prop="1"></comp>
```

因为它是一个字面 prop，它的值以字符串 “1” 而不是以实际的数字传下去。如果想传递一个实际的 JavaScript 数字，需要使用动态语法，从而让它的值被当作 JavaScript 表达式计算：

```
<!-- 传递实际的数字  -->
<comp :some-prop="1"></comp>
```

> **10、Prop绑定类型**

prop 默认是单向绑定：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意修改了父组件的状态——这会让应用的数据流难以理解。不过，**也可以使用 .sync 或 .once 绑定修饰符显式地强制双向或单次绑定：**

比较语法：

```
<!-- 默认为单向绑定 -->
<child :msg="parentMsg"></child>

<!-- 双向绑定 -->
<child :msg.sync="parentMsg"></child>

<!-- 单次绑定 -->
<child :msg.once="parentMsg"></child>
```

双向绑定**会把子组件的 msg 属性同步回父组件的 parentMsg 属性。**单次绑定在建立之后不会同步之后的变化。

注意如果 prop 是一个对象或数组，是按引用传递。在子组件内修改它会影响父组件的状态，不管是使用哪种绑定类型。


> **11、Prop 验证**

组件可以为 props 指定验证要求。当组件给其他人使用时这很有用，因为这些验证要求构成了组件的 API，确保其他人正确地使用组件。此时 props 的值是一个对象，包含验证要求：

```
Vue.component('example', {
  props: {
    // 基础类型检测 （`null` 意思是任何类型都可以）
    propA: Number,
    // 多种类型 (1.0.21+)
    propM: [String, Number],
    // 必需且是字符串
    propB: {
      type: String,
      required: true
    },
    // 数字，有默认值
    propC: {
      type: Number,
      default: 100
    },
    // 对象/数组的默认值应当由一个函数返回
    propD: {
      type: Object,
      default: function () {
        return { msg: 'hello' }
      }
    },
    // 指定这个 prop 为双向绑定
    // 如果绑定类型不对将抛出一条警告
    propE: {
      twoWay: true
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        return value > 10
      }
    },
    // 转换函数（1.0.12 新增）
    // 在设置值之前转换值
    propG: {
      coerce: function (val) {
        return val + '' // 将值转换为字符串
      }
    },
    propH: {
      coerce: function (val) {
        return JSON.parse(val) // 将 JSON 字符串转换为对象
      }
    }
  }
})
```

type 可以是下面原生构造器：

1. String
2. Number
3. Boolean
4. Function
5. Object
6. Array

**type 也可以是一个自定义构造器，使用 instanceof 检测。**

当 prop 验证失败了，Vue 将拒绝在子组件上设置此值，如果使用的是开发版本会抛出一条警告。

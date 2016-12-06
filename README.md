# vue-router 学习笔记

### 目录

- 绑定一个元素

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

- 双向绑定

	> **v-model绑定input**

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

- 渲染列表

	> **v-for绑定列表**

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

- 处理用户输入
	
	> **v-on绑定点击事件**

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

- 综合

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

- 相应数据的绑定
- 组件系统
- 构造器
- 实例的生命周期
- 数据绑定语法
- 插入数据值
- 绑定表达式
- 指令
- 计算属性
- 绑定Class和CSS
- 绑定HTML class
- 绑定内联样式CSS
- 条件渲染
- if-else结构
- 使用template标签包装多个元素实现if-else的多元素切换
- v-show指令实现依赖条件决定是否展示数据
- 组件警告
- v-for
- template v-for
- 数组变动检测
- v-for对象
- 值域 v-for
- 显示过滤排序的结果
- 方法与事件处理器
- 可以用 v-on 指令监听 DOM 事件
- 内联 JavaScript 语句可以传递参数
- 事件修饰符
- 按键修饰符
- 为什么在 HTML 中监听事件
- 表单控件绑定
- 基础用法
- 绑定value
- 参数特性
- 组件
- 使用组件extend-component
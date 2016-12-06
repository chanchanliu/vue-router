# vue-router 学习笔记

**目录**

- 绑定一个元素

	> 如果new Vue不写在$(document).ready(function() {}里面的话，就必须写在最后面，这样才能保证页面元素是先于js加载的

` <script>
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
</div> `

- 双向绑定
- 渲染列表
- 处理用户输入
- 综合
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
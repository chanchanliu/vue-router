# vue-router ѧϰ�ʼ�

## Ŀ¼

### ��һ��Ԫ�� 

> ���new Vue��д��$(document).ready(function() {}����Ļ����ͱ���д������棬�������ܱ�֤ҳ��Ԫ��������js���ص�


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

###  ˫���

> v-model��input

``` 

<!-- ͬʱ��message��v-modle="messsage"������Ԫ�أ���Ϊ˫��󶨡� -->
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
<!-- ��Ϊ����Django��ģ���е��ԣ�Django��Vue��{{info}}���ǹؼ��֣�����ʹ��{% templatetag openvariable %} info {% templatetag closevariable %} ��������Ϣ�������Ļ�����������Ⱦ֮��{% templatetag openvariable %} info {% templatetag closevariable %}�ͱ����{{info}} -->
    {% templatetag openvariable %}message{% templatetag closevariable %}
    <input v-model="message">
</div>
```

### ��Ⱦ�б�

> v-for���б�

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
<!-- js��data��todos��li��ǩ��v-for��in todosͬһ�����ƣ�������{{}}�б���todo.txt,������Ⱦ���� -->
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

### �����û�����

> v-on�󶨵���¼�

```
<script>
    $(document).click(function (){
        new Vue({
            el: '#app',
            data:{
                message:'Hello Vue.js!'
            },
            //��Vue���淽������д��methods���棬��ʽ��functionname:function(){}
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
    <!-- ��buttonʹ��v-on����ʽ��v-on:�����¼���="������" -->
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

### �ۺ�

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
                    //splice() ������/�����������/ɾ����Ŀ��Ȼ�󷵻ر�ɾ������Ŀ��
                    this.todos.splice(index, 1)
                }
            }
        })
    })
</script>

<div id="app">
    <!-- ��input�����ûس����ʹ�����addTodo������������µ�li��ǩ -->
    <input v-model="newTodo" v-on:keyup.enter="addTodo">
    <ul>
        <li v-for="todo in todos">
            <span>{% templatetag openvariable %} todo.text {% templatetag closevariable %}</span>
            <!-- ���button�ʹ�����removeTodo���� -->
            <button v-on:click="removeTodo($index)">x</button>
        </li>
    </ul>
</div>
```

### ��Ӧ���ݵİ�

> Vue.js Ҳ�ṩһ��ǿ��Ĺ���Ч��ϵͳ�������� Vue ����/ɾ��Ԫ��ʱ�Զ�Ӧ�ù���Ч����

```
<div id="example-2">
    <!-- v-if,��greetingΪtrue��ʱ��hello����ʾ-->
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

 > v-bind ָ�����ڰ� HTML ����

### ���ϵͳ

>  **���ϵͳ�� Vue.js ��һ����Ҫ�����Ϊ���ṩ��һ�ֳ��������ǿ����ö����ɸ��õ�С�������������Ӧ�á�������ǿ��ǵ���㣬�����������͵�Ӧ�õĽ��涼���Գ���Ϊһ���������**

### ������

> **ÿ�� Vue.js Ӧ�õ��𲽶���ͨ�����캯�� Vue ����һ�� Vue �ĸ�ʵ����**

> **һ�� Vue ʵ����ʵ����һ�� MVVM ģʽ���������� ViewModel - ������ĵ��о�����ʹ�� vm �����������**

> **��ʵ���� Vue ʱ����Ҫ����һ��ѡ����������԰������ݡ�ģ�塢����Ԫ�ء��������������ڹ��ӵ�ѡ�ȫ����ѡ������� API �ĵ��в鿴��**

> **������չ Vue ���������Ӷ���Ԥ����ѡ����ɸ��õ����������**

```
var MyComponent = Vue.extend({
  // ��չѡ��
})

// ���е� MyComponent ʵ��������Ԥ�������չѡ�����
var myComponentInstance = new MyComponent()
```

> **ÿ��Vueʵ���������ķ�����methods�������ݣ�date�����Ͱ󶨵�Ԫ�ض���el��**


```
var data = { a: 1 }
var vm = new Vue({
    data: data
})

vm.a === data.a // -> true

// ��������Ҳ��Ӱ�쵽ԭʼ����
vm.a = 2
data.a // -> 2

// ... ��֮��Ȼ
data.a = 3
vm.a // -> 3
```

> **ÿ�� Vue ʵ����������� data ���������е����ԣ�ֻ����Щ���������������Ӧ�ġ�**


### ʵ������������

> **Vue ʵ���ڴ���ʱ��һϵ�г�ʼ�����衪�����磬����Ҫ�������ݹ۲죬����ģ�壬������Ҫ�����ݰ󶨡��ڴ˹����У���Ҳ������һЩ�������ڹ��ӣ����Զ����߼��ṩ���л��ᡣ���� created ������ʵ����������ã�**

```
var vm = new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` ָ�� vm ʵ��
    console.log('a is: ' + this.a)
  }
})
// -> "a is: 1"
```

**Ҳ��һЩ�����Ĺ��ӣ���ʵ���������ڵĲ�ͬ�׶ε��ã��� compiled�� ready ��destroyed�����ӵ� this ָ��������� Vue ʵ����һЩ�û����ܻ��� Vue.js �Ƿ��С����������ĸ�����ǣ�û�С�������Զ����߼����Էָ�����Щ�����С�** 

### ���ݰ��﷨

**Vue.js ��ģ���ǻ��� DOM ʵ�ֵġ�����ζ�����е� Vue.js ģ�嶼�ǿɽ�������Ч�� HTML����ͨ��һЩ���������������ǿ��Vue ģ������Ӹ����ϲ�ͬ�ڻ����ַ�����ģ�壬���ס��㡣**

### ��������ֵ

> **���ݰ����������ʽ���ı���ֵ��ʹ�� ��Mustache�� �﷨��˫�����ţ���**

```
<span>Message: {{ msg }}</span>
<!-- ��django��˫��������ģ�����Ⱦ�﷨������Ҫ����һ�ַ���ʵ��˫�������﷨�� -->
{% templatetag openvariable %} msg {% templatetag closevariable %}
```

> **����HTML**

```
<div>{{{ raw_html }}}</div>
```

> **���뵽HTMLֵ������ֵ��**

```
<div id="item-{{ id }}"></div>
```

### �󶨱��ʽ

> **JavaScript ���ʽ** 

> ����ֱ�Ӳ���Ӽ��˳�����Ԫ���㡢�Լ�javascript�ĺ���

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<!-- һ��������ÿ����ֻ�ܰ����������ʽ  -->
<!-- ����һ����䣬����һ�����ʽ�� -->
{{ var a = 1 }}

<!-- ���̿���Ҳ�����ԣ��ɸ�����Ԫ���ʽ -->
{{ if (ok) { return message } }}
```

> **����������javascript���ʽ�໥��ϣ�������ֻ�ܸ���js���ʽ���棩**

> **Vue.js �����ڱ��ʽ����ӿ�ѡ�ġ������� (Filter) �����ԡ��ܵ�����ָʾ��**

```{{ message | capitalize }}```

�������ǽ����ʽ message ��ֵ�����䣨pipe���������õ� capitalize �������������������ʵֻ��һ�� JavaScript ���������ش�д����ֵ��Vue.js �ṩ�������ù�������

**���������Դ�����**

```{{ message | filterA | filterB }}```

**������Ҳ���Խ��ܲ�����**

```{{ message | filterA 'arg1' arg2 }}```

**����������ʼ���Ա��ʽ��ֵ��Ϊ��һ��������**�����ŵĲ�����Ϊ�ַ��������������ŵĲ��������ʽ���㡣����ַ��� ��arg1�� ��������������Ϊ�ڶ������������ʽ arg2 ��ֵ�ڼ������֮����Ϊ������������

### ָ��

> **����**
��Щָ������������ƺ����һ���������� (Argument)���м��һ��ð�Ÿ��������磬**v-bind ָ��������Ӧ�ظ��� HTML ���ԣ�**

```<a v-bind:href="url"></a>```

�����Բ�ֵ href=��{{url}}�� ���ͬ���Ľ��������û������ʵ������**�ڲ����Բ�ֵ��תΪ v-bind ��**��

��һ�������� **v-on ָ������ڼ��� DOM �¼���**

```<a v-on:click="doSomething">```

> **������**

**���η� (Modifiers) ���԰�Ǿ�� . ��ʼ�������׺**�����ڱ�ʾָ��Ӧ�������ⷽʽ�󶨡����� .literal ���η�����ָ�����ֵ����Ϊһ�������ַ���������һ�����ʽ��

```<a v-bind:href.literal="/a/b/c"></a>```

> **��д**

��Գ���v-bind��v-on����һЩ��д��

v-bind

```
<!-- �����﷨ -->
<a v-bind:href="url"></a>

<!-- ��д -->
<a :href="url"></a>

<!-- �����﷨ -->
<button v-bind:disabled="someDynamicCondition">Button</button>

<!-- ��д -->
<button :disabled="someDynamicCondition">Button</button>
```

v-on

```
<a v-on:click="doSomething"></a>
<a @click="doSomething"></a>
```

### ��������

��ģ���а󶨱��ʽ�Ƿǳ������ģ���������ʵ����ֻ���ڼ򵥵Ĳ�����ģ����Ϊ��������ͼ�Ľṹ����ģ���з���̫����߼�����ģ�����������ά���������Ϊʲô Vue.js ���󶨱��ʽ����Ϊһ�����ʽ�������Ҫ����һ�����ʽ���߼���Ӧ��ʹ�ü������ԡ�

```
<div id='exmple'>
    a = {% templatetag openvariable %} a {% templatetag closevariable %},b = {% templatetag openvariable %} b {% templatetag closevariable %}
</div>

<script>
    var vm = new Vue({
        el:'#exmple',
        data:{
            a:1  //a������ֵ
        },
        computed:{ //���computed��������������
            //һ���������Ե�getter����������������һ���������� b�������ṩ�ĺ������������� vm.b�� getter��
            b:function(){
                return this.a + 1
            }
        }
    })
</script>
```

**vm.b ������ vm.a����˵� vm.a �����ı�ʱ�������� vm.b �İ�Ҳ����¡�**

> **$watch**

Vue.js �ṩ��һ������ watch�������ڹ۲�Vueʵ���ϵ����ݱ䶯����һЩ������Ҫ�����������ݱ仯ʱ��watch ������ ���� �ر������������ AngularJS��**������ͨ�����õİ취��ʹ�ü������Զ�����һ������ʽ�� $watch �ص���**

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

**�������������ʽ���ظ��ġ����������ԶԱ�**

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

> **��������Ĭ��ֻ�� getter����������Ҫʱ��Ҳ�����ṩһ�� setter��**

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

**ʹ��setter����֮�󣬾���firstName��lastName�ͻ�����fullname��̬�仯�ˡ�**

```
vm.fullName = 'Tony Dandelion'
"Tony Dandelion"
vm.firstName
"Tony"
vm.lastName
"Dandelion"
```

### ��Class��CSS

### ��HTML class

���ܿ����� Mustache ��ǩ�� class������ class=��{{ className }}�����������ǲ��Ƽ�����д���� v-bind:class ���á�����ֻ��ѡ��һ��

> **�������İ�**

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
<!-- ����Ч����<div class="static class-a"></div> -->
```

��Ҳ����ֱ�Ӱ��������һ������

```
<div v-bind:class="classObject"></div>

data: {
  classObject: {
    'class-a': true,
    'class-b': false
  }
}
```

> **�����**

���ǿ��԰�һ�����鴫�� v-bind:class����Ӧ��һ�� class �б�

```
<div v-bind:class="[classA, classB]">
data: {
  classA: 'class-a',
  classB: 'class-b'
}
```

��ȾΪ��

```
<div class="class-a class-b"></div>
```

�����Ҳ����������л��б��е� class����������Ԫ��

```<div v-bind:class="[classA, isB ? classB : '']">```

����� classA������ֻ���� isB �� true ʱ��� classB ��

���������ж������ class ʱ����д��Щ�������� 1.0.19+ �У������������﷨��ʹ�ö����﷨��

```<div v-bind:class="[classA, { classB: isB, classC: isC }]">```

### ��������ʽCSS

> **����������ʽ**

v-bind:style �Ķ����﷨ʮ��ֱ�ۡ������ŷǳ��� CSS����ʵ����һ�� JavaScript ����CSS �������������շ�ʽ��camelCase����̺�ָ�������kebab-case����

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
data: {
  activeColor: 'red',
  fontSize: 30
}
```

**ֱ�Ӱ󶨵�һ����ʽ����ͨ������**����ģ���������

```
<div v-bind:style="styleObject"></div>
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

ͬ���ģ������﷨������Ϸ��ض���ļ�������ʹ�á�

> **�����﷨**

v-bind:style �������﷨���Խ������ʽ����Ӧ�õ�һ��Ԫ���ϣ�

```<div v-bind:style="[styleObjectA, styleObjectB]">```

> **�Զ����ǰ׺**

**�� v-bind:style ʹ����Ҫ����ǰ׺�� CSS ����ʱ���� transform��Vue.js ���Զ���Ⲣ�����Ӧ��ǰ׺��**

### ������Ⱦ
### if-else�ṹ
### ʹ��template��ǩ��װ���Ԫ��ʵ��if-else�Ķ�Ԫ���л�
### v-showָ��ʵ���������������Ƿ�չʾ����
### �������
### v-for
### template v-for
### ����䶯���
### v-for����
### ֵ�� v-for
### ��ʾ��������Ľ��
### �������¼�������
### ������ v-on ָ����� DOM �¼�
### ���� JavaScript �����Դ��ݲ���
### �¼����η�
### �������η�
### Ϊʲô�� HTML �м����¼�
### ���ؼ���
### �����÷�
### ��value
### ��������
### ���
### ʹ�����extend-component
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

�� Vue.js������ʹ�� v-if ָ��ʵ��ͬ���Ĺ��ܣ�

```<h1 v-if="ok">Yes</h1>```

Ҳ������ v-else ���һ�� ��else�� �飺

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

### ʹ��template��ǩ��װ���Ԫ��ʵ��if-else�Ķ�Ԫ���л�

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

### v-showָ��ʵ���������������Ƿ�չʾ����

**v-show�ǲ�֧��template��ǩ�Զ��Ԫ�ؽ��а�װ�� 
Ҳ����ʹ��v-else��v-show����else��**

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

### �������

�� v-show ���������ʱ����Ϊָ������ȼ� v-else ��������⡣��˲�Ҫ��������

```
<custom-component v-show="condition"></custom-component>
<p v-else>�����Ҳ��һ�����</p>
```

����һ�� v-show �滻 v-else��

```
<custom-component v-show="condition"></custom-component>
<p v-show="!condition">�����Ҳ��һ�����</p>
```

�����Ϳ��Դﵽ v-if ��Ч����

> **һ���Ǿ�������**

**vue.js:1023 [Vue warn]: Unknown custom element: - did you register the component correctly? For recursive components, make sure to provide the ��name�� option.**

**һ����˵��v-if �и��ߵ��л����Ķ� v-show �и��ߵĳ�ʼ��Ⱦ���ġ���ˣ������ҪƵ���л� v-show �Ϻã����������ʱ����������ܸı� v-if �Ϻá�**

**�б���Ⱦ(data��ͬ������֮������ , �໥�����)**

### v-for

**����ʹ�� v-for ָ�����һ��������Ⱦһ���б����ָ��ʹ��������﷨����ʽΪ item in items��items ���������飬item �ǵ�ǰ����Ԫ�صı�����**

�б���Ⱦʹ�õĶ������顣��data�е�������ʽ�ǣ�

```
������:[
    {Ԫ����1:����1,Ԫ����2:����5,Ԫ��3.....}
    {Ԫ����1:����2,Ԫ����2:����6,Ԫ��3.....}
    {Ԫ����1:����3,Ԫ����2:����7,Ԫ��3.....}        
]

example��
items:[
    {A:1,b:6,c:10},
    {A:2,b:7,c:11},
    {A:3,b:8,c:12}
]
```

ʹ�÷���

```
<li v-for='��ǰ����Ԫ�صı��� in ������'>
    {% templatetag openvariable %} ��ǰ����Ԫ�صı���.��ǰ����Ԫ���о���Ҫ������Ԫ���� {% templatetag closevariable %}
</li>

example��
<li v-for='item in items'>
    {% templatetag openvariable %} item.b {% templatetag closevariable %}
</li>
```

**�� v-for ������������ȫ���ʸ�����������ڵ����ԣ�����һ��������� $index��������µ��ģ����ǵ�ǰ����Ԫ�ص�������**

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

<!-- �����±��0��ʼ -->
Parent - 0 - 10
Parent - 1 - 11
Parent - 2 - 12
```

### template v-for

**ʹ��template��ǩ����������ݰ�װ�ɿ顣**

### ����䶯���

> **���췽��(�޸�ԭʼ���飬Ӱ��ҳ�����ȾЧ����)**

```
push()  #�����ʼ���
pop() #�Ӻ���ǰɾ��
shift()  #��ǰ����ɾ��
unshift() 
splice()  #splice() �������ڲ��롢ɾ�����滻�����Ԫ�ء�
sort()  #����
reverse() #����
```

> **�滻���飨���޸�ԭʼ���ݣ�**

���췽������������ʾ���޸���ԭʼ���顣���֮�£�Ҳ�зǱ��췽������ filter(), concat() �� slice()�������޸�ԭʼ������Ƿ���һ�������顣��ʹ�÷Ǳ��췽��ʱ������ֱ�����������滻�����飺

```
slice() #����ȡ�ַ�����ĳ������,�����µ��ַ������ر���ȡ�Ĳ���
filter() #����
concat() #����������������
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

����������⽫���� Vue.js �������� DOM ��������Ⱦ�����б������˵��ǲ�����ˡ� Vue.js ʵ����һЩ�����㷨������󻯸��� DOM Ԫ�أ����**����һ�������滻������һ���ǳ���Ч�Ĳ�����**

> **track-by**

��ʱ��Ҫ��ȫ�¶�������ͨ�� API ���ô����Ķ����滻���顣��Ϊ **v-for Ĭ��ͨ�����ݶ��������������������������� DOM Ԫ�صĸ��ó̶�**������ܵ���������Ⱦ�����б����ǣ�**���ÿ��������һ��Ψһ ID �����ԣ������ʹ�� track-by ���Ը� Vue.js һ����ʾ��Vue.js ����ܾ����ܵظ�������ʵ����**

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
�����
88f869d
7496c10
```

**Ȼ�����滻���� items ʱ����� Vue.js ����һ������ _uid: ��88f869d�� ���¶�����֪�������Ը���������ж������������ DOM Ԫ�ء�**

> **track-by $index**

���û��Ψһ�ļ���׷�٣�**����ʹ�� track-by=��$index������ǿ���� v-for ����ԭλ����ģʽ��Ƭ�ϲ��ᱻ�ƶ������Ǽ򵥵��Զ�Ӧ��������ֵˢ�¡�**����ģʽҲ�ܴ��������������ظ���ֵ��

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

���������滻�ǳ���Ч������Ҳ�Ḷ��һ���Ĵ��ۡ�**��Ϊ��ʱ DOM �ڵ㲻��ӳ������Ԫ��˳��ĸı䣬����ͬ����ʱ״̬������ Ԫ�ص�ֵ���Լ������˽��״̬����ˣ���� v-for ����� Ԫ�ػ��������ҪС��ʹ�� track-by=��$index��**

> **����**

��Ϊ JavaScript �����ƣ�Vue.js ���ܼ�⵽��������仯��

1. ֱ������������Ԫ�أ��� vm.items[0] = {}��
2. �޸����ݵĳ��ȣ��� vm.items.length = 0��

Ϊ�˽������ (1)��Vue.js ��չ�˹۲����飬Ϊ�������һ�� $set() ������

```
// �� `example1.items[0] = ...` ��ͬ�������ܴ�����ͼ����
example1.items.$set(0, { childMsg: 'Changed!'})
```

�������� (2)��ֻ����һ���������滻 items��

```example1.items = []```

���� $set()�� Vue.js ҲΪ�۲���������� $remove() ���������ڴ�Ŀ�������в��Ҳ�ɾ��Ԫ�أ����ڲ������� splice() ����ˣ�����������

```
var index = this.items.indexOf(item)
if (index !== -1) {
  this.items.splice(index, 1)
}
```

ֻ��������

```
this.items.$remove(item)
```

ʹ�� Object.freeze()

�ڱ���һ������ʱ���������Ԫ���Ƕ����Ҷ����� Object.freeze() ���ᣬ**����Ҫ��ȷָ�� track-by**���������������� Vue.js �����Զ�׷�ٶ��󣬽�����һ�����档

### v-for����

Ҳ����ʹ�� v-for �������󡣳��� $index ֮�⣬**�������ڻ����Է�������һ��������� $key��**

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

### ֵ�� v-for

v-for Ҳ���Խ���һ����������ʱ�����ظ�ģ�����Ρ�

```
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
�����
0 1 2 3 4 5 6 7 8 9
```

### ��ʾ��������Ľ��

��ʱ��������ʾ����/����������飬ͬʱ��ʵ���޸Ļ�����ԭʼ���ݡ��������취��

1. ����һ���������ԣ����ع���/����������飻
2. ʹ�����õĹ����� filterBy �� orderBy��

���������и��õĿ�������Ҳ������Ϊ����ȫ���� JavaScript������ͨ�������������㣬��ϸ�� API��

### �������¼�������
### ������ v-on ָ����� DOM �¼�

```
<div id="example">
  <button v-on:click="greet">Greet</button>
</div>
```

���ǰ���һ�������¼���������һ������ greet�������� Vue ʵ���ж������������

```
var vm = new Vue({
  el: '#example',
  data: {
    name: 'Vue.js'
  },
  // �� `methods` �����ж��巽��
  methods: {
    greet: function (event) {
      // ������ `this` ָ�� vm
      alert('Hello ' + this.name + '!')
      // `event` ��ԭ�� DOM �¼�
      alert(event.target.tagName)
    }
  }
})
```

### ���� JavaScript �����Դ��ݲ���

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

�������������ʽ��**�¼�����������Ϊһ����䡣**

��ʱҲ��Ҫ��������䴦�����з���ԭ�� DOM �¼���**������������� $event �������뷽����**

```
<button v-on:click="say('hello!', $event)">Submit</button>
// ...
methods: {
  say: function (msg, event) {
    // �������ǿ��Է���ԭ���¼�����
    event.preventDefault()
  }
}
```

### �¼����η�

���¼��������о�����Ҫ���� event.preventDefault() �� event.stopPropagation()�����������ڷ����ڿ�������������������**�����Ǵ���������߼��������� DOM �¼�ϸ�ڻ����**��

Ϊ�˽��������⣬**Vue.js Ϊ v-on �ṩ���� �¼����η���.prevent �� .stop**�����Ƿ񻹼ǵ����η��ǵ�Ŵ�ͷ��ָ���׺��

```
<!-- ��ֹ�����¼�ð�� -->
<a v-on:click.stop="doThis"></a>

<!-- �ύ�¼���������ҳ�� -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- ���η����Դ��� -->
<a v-on:click.stop.prevent="doThat">

<!-- ֻ�����η� -->
<form v-on:submit.prevent></form>

1.0.16 �����������������η���

<!-- ����¼�������ʱʹ�� capture ģʽ -->
<div v-on:click.capture="doThis">...</div>

<!-- ֻ���¼��ڸ�Ԫ�ر�����������Ԫ�أ�����ʱ�����ص� -->
<div v-on:click.self="doThat">...</div>
```

### �������η�

�ڼ��������¼�ʱ�����Ǿ�����Ҫ��� keyCode��Vue.js ����Ϊ v-on ��Ӱ������η���

```
<!-- ֻ���� keyCode �� 13 ʱ���� vm.submit() -->
<input v-on:keyup.13="submit">
��ס���е� keyCode �Ƚ����ѣ�Vue.js Ϊ��õİ����ṩ������

<!-- ͬ�� -->
<input v-on:keyup.enter="submit">

<!-- ��д�﷨ -->
<input @keyup.enter="submit">
ȫ���İ���������

enter
tab
delete
esc
space
up
down
left
right

1.0.8+�� ֧�ֵ���ĸ����������
1.0.17+�� �����Զ��尴��������
```

```
// ����ʹ�� @keyup.f1
Vue.directive('on').keyCodes.f1 = 112
```

### Ϊʲô�� HTML �м����¼�

�����ע�⵽�����¼������ķ�ʽΥ���˴�ͳ���� ��separation of concern�������ص��ģ���Ϊ���е� Vue.js �¼��������ͱ��ʽ���ϸ���ڵ�ǰ��ͼ�� ViewModel �ϣ������ᵼ���κ�ά�����ѡ�ʵ���ϣ�**ʹ�� v-on �м����ô���**

* ɨһ�� HTML ģ��������ɶ�λ�� JavaScript �������Ӧ�ķ�����
* ��Ϊ�������� JavaScript ���ֶ����¼������ ViewModel ��������Ƿǳ�������߼����� DOM ��ȫ��������ڲ��ԡ�
* ��һ�� ViewModel ������ʱ�����е��¼������������Զ���ɾ���������뵣������Լ��������ǡ�

### ���ؼ���
### �����÷�

> **Text**

```
<span>Message is: {{ message }}</span>
<br>
<input type="text" v-model="message" placeholder="edit me">
```

> **checkbox**

**������ѡ���߼�ֵ��**

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

**��ѡ**

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

**��ѡ���󶨵�һ�����飩**

**����һ��multiple**

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

**��̬ѡ��� v-for ��Ⱦ**

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

### ��value

```
<!-- ��ѡ��ʱ��`picked` Ϊ�ַ��� "a" -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` Ϊ true �� false -->
<input type="checkbox" v-model="toggle">

<!-- ��ѡ��ʱ��`selected` Ϊ�ַ��� "abc" -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

������ʱ������**�� value �� Vue ʵ����һ����̬�����ϣ���ʱ������ v-bind ʵ��**������������Ե�ֵ���Բ����ַ�����

> **Checkbox**

```
<input
  type="checkbox"
  v-model="toggle"
  v-bind:true-value="a"
  v-bind:false-value="b">
// ��ѡ��ʱ
vm.toggle === vm.a
// ��û��ѡ��ʱ
vm.toggle === vm.b
```

> **Radio**

```
<input type="radio" v-model="pick" v-bind:value="a">
// ��ѡ��ʱ
vm.pick === vm.a
```

> **Select Options**

```
<select v-model="selected">
  <!-- ���������� -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
// ��ѡ��ʱ
typeof vm.selected // -> 'object'
vm.selected.number // -> 123
```

### ��������

> **lazy**

��Ĭ������£�v-model ��input �¼���ͬ�������ֵ�����ݣ��������һ������ lazy���Ӷ��ĵ��� change �¼���ͬ����

```
<!-- �� "change" ������ "input" �¼��и��� -->
<input v-model="msg" lazy>
```

> **number**

������Զ����û�������תΪ Number ���ͣ����ԭֵ��ת�����Ϊ NaN �򷵻�ԭֵ�����������һ������ number

```
<input v-model="age" number>
```

> **debounce**

debounce ����һ����С����ʱ����ÿ���û�֮����ʱͬ��������ֵ�����ݡ����ÿ�θ��¶�Ҫ���иߺĲ�����������������ʾ�� Ajax ���󣩣�����Ϊ���á�

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

**ע��** debounce ���������ӳ� input �¼������ӳ١�д�롱�ײ����ݡ������ʹ�� debounce ʱӦ���� vm.$watch() ��Ӧ���ݵı仯�������ӳ� DOM �¼���Ӧ��ʹ�� debounce ��������

### ���

�����Component���� Vue.js ��ǿ��Ĺ���֮һ��**���������չ HTML Ԫ�أ���װ�����õĴ��롣�ڽϸ߲����ϣ�������Զ���Ԫ�أ�Vue.js �ı�����Ϊ��������⹦�ܡ�**����Щ����£����Ҳ������ԭ�� HTML Ԫ�ص���ʽ���� is ������չ��

### ʹ�����extend-component

**ҳ����Ⱦ��ʱ��**

```<my-component></my-component> --> my-component --> MyComponent --> <div>A custom component!</div>```

**ʹ�õ�ʱ��**

```
����һ����������� -----> �õ�<div>A custom component!</div>-->MyComponent�Ĺ�����ϵ��Ȼ�����ע�ᡣ -----> �õ�MyComponent-->my-component�Ĺ�ϵ��    ����һ����ʹ��<my-component></my-component>�͵õ�<div>A custom component!</div>�ˡ�
```

> **1��ע��**

������ Vue.extend() ����һ�������������

```
var MyComponent = Vue.extend({
  // ѡ��...
})
```

Ҫ����������������������Ҫ�� Vue.component(tag, constructor) ע�� ��

```
// ȫ��ע�������tag Ϊ my-component
Vue.component('my-component', MyComponent)
```

ʵ����**ע�⣬ʹ�õ���extend����extends��**

```
<div id="example">
    <my-component></my-component>
</div>
<script>
    //����һ�����������
    var MyComponent = Vue.extend({
        template:'<div>A custom component!</div>'
    })
    //ע�ᣬ��MyComponentע���my-componen�������
    Vue.component('my-component',MyComponent)
    new Vue({
        el:'#example'
    })
</script>
```

ע�������ģ���滻���Զ���Ԫ�أ�**�Զ���Ԫ�ص�����ֻ����Ϊһ�����ص㡣**������ʵ��ѡ�� replace �����Ƿ��滻��

> **2���ֲ�ע��**

����Ҫȫ��ע��ÿ����������������ֻ��������������ڣ���ʵ��ѡ�� components ע�ᣬ�ֲ�ע���ȫ��ע��������ǣ��ֲ�ע�����ڸ��������components��ע��

```
var Child = Vue.extend({ /* ... */ })

var Parent = Vue.extend({
  template: '...',
  components: {
    // <my-component> ֻ�����ڸ����ģ����
    'my-component': Child
  }
})
```

���ַ�װҲ������������Դ����**ָ��������͹��ɡ�**

> **3��ע���﷨��**

Ϊ�����¼����򵥣�����ֱ�Ӵ���ѡ���������ǹ������� Vue.component() �� component ѡ�Vue.js �ڱ����Զ����� Vue.extend()��

```
// ��һ����������չ��ע��
Vue.component('my-component', {
  template: '<div>A custom component!</div>'
})

// �ֲ�ע��Ҳ������ô��
var Parent = Vue.extend({
  components: {
    'my-component': {
      template: '<div>A custom component!</div>'
    }
  }
})
```

> **4�����ѡ������**

���� Vue �������Ķ���ѡ��Ҳ�������� Vue.extend() �У����������������� **data �� el��**����������Ǽ򵥵ذ�һ��������Ϊ data ѡ��� Vue.extend()��

```
var data = { a: 1 }
var MyComponent = Vue.extend({
  data: data
})
```

��ô���������� **MyComponent ���е�ʵ��������ͬһ�� data ����**���������������Ҫ�ģ��������Ӧ��**ʹ��һ��������Ϊ data ѡ��������������һ���¶���**

```
var MyComponent = Vue.extend({
  data: function () {
    return { a: 1 }
  }
})
```

ͬ��**el ѡ������ Vue.extend() ��ʱҲ����һ��������**

> **5��ģ���������**

Vue ��ģ���� DOM ģ�壬ʹ�������ԭ���Ľ������������Լ�ʵ��һ��������ַ���ģ�壬DOM ģ����һЩ�ô�������Ҳ�����⣬����������Ч�� HTML Ƭ�Ρ�һЩ HTML Ԫ�ض�ʲôԪ�ؿ��Է��������������ơ����������ƣ�

1. a ���ܰ��������Ľ���Ԫ�أ��簴ť�����ӣ�
2. ul �� ol ֻ��ֱ�Ӱ��� li
3. select ֻ�ܰ��� option �� optgroup
4. table ֻ��ֱ�Ӱ��� thead, tbody, tfoot, tr, caption, col, colgroup
5. tr ֻ��ֱ�Ӱ��� th �� td

��ʵ���У���Щ���ƻᵼ������Ľ���������ڼ򵥵�����������ܿ��Թ����������㲻�������Զ���������������֤֮ǰ��չ����������� �� ������Ч��ģ�壬��ʹ my-select �������չ��Ϊ ����

��һ������ǣ�**�Զ����ǩ�������Զ���Ԫ�غ������ǩ���� <component>��<template>�� <partial> ���������� ul, select, table �ȶ��ڲ�Ԫ�������Ƶı�ǩ�ڡ�**������ЩԪ���ڲ����Զ����ǩ�����ᵽԪ�ص����棬�����Ⱦ����ȷ��

**�����Զ���Ԫ�أ�Ӧ��ʹ�� is ���ԣ�**

```
<table>
  <tr is="my-component"></tr>
</table>
<template> �������� <table> �ڣ���ʱӦʹ�� <tbody>��<table> �����ж�� <tbody>��

<table>
  <tbody v-for="item in items">
    <tr>Even row</tr>
    <tr>Odd row</tr>
  </tbody>
</table>
```

> **6��Props**

ʹ�� Props ��������

���ʵ�����������ǹ����ġ�����ζ�Ų��ܲ��Ҳ�Ӧ�����������ģ����ֱ�����ø���������ݡ�**����ʹ�� props �����ݴ����������**

**��prop�� ��������ݵ�һ���ֶΣ������Ӹ�������������������Ҫ��ʽ���� props ѡ�� ���� props��**

```
Vue.component('child', {
  // ���� props
  props: ['msg'],
  // prop ��������ģ����
  // ������ `this.msg` ����
  template: '<span>{{ msg }}</span>'
})
```

Ȼ����������һ����ͨ�ַ�����

```
<child msg="hello!"></child>
```

> **7��camelCase vs. kebab-case**

HTML ���Բ����ִ�Сд��**������ʽΪ camelCase �� prop ��������ʱ����ҪתΪ kebab-case���̺��߸�������**

```
Vue.component('child', {
  // camelCase in JavaScript
  props: ['myMessage'],
  template: '<span>{{ myMessage }}</span>'
})
<!-- kebab-case in HTML -->
<child my-message="hello!"></child>
```

> **8����̬ Props**

�������� v-bind �� HTML ���Ե�һ�����ʽ��**Ҳ������ v-bind �󶨶�̬ Props ������������ݡ�ÿ������������ݱ仯ʱ��Ҳ�ᴫ�����������**

```
<div>
  <input v-model="parentMsg">
  <br>
  <child v-bind:my-message="parentMsg"></child>
</div>
```

ʹ�� v-bind ����д�﷨ͨ�����򵥣�

```
<child :my-message="parentMsg"></child>
```

> **9���������﷨ vs. ��̬�﷨**

��ѧ�߳�����һ��������ʹ���������﷨������ֵ��

```
<!-- ������һ���ַ��� "1" -->
<comp some-prop="1"></comp>
```

��Ϊ����һ������ prop������ֵ���ַ��� ��1�� ��������ʵ�ʵ����ִ���ȥ������봫��һ��ʵ�ʵ� JavaScript ���֣���Ҫʹ�ö�̬�﷨���Ӷ�������ֵ������ JavaScript ���ʽ���㣺

```
<!-- ����ʵ�ʵ�����  -->
<comp :some-prop="1"></comp>
```

> **10��Prop������**

prop Ĭ���ǵ���󶨣�������������Ա仯ʱ��������������������Ƿ��������ᡣ����Ϊ�˷�ֹ����������޸��˸������״̬���������Ӧ�õ�������������⡣������**Ҳ����ʹ�� .sync �� .once �����η���ʽ��ǿ��˫��򵥴ΰ󶨣�**

�Ƚ��﷨��

```
<!-- Ĭ��Ϊ����� -->
<child :msg="parentMsg"></child>

<!-- ˫��� -->
<child :msg.sync="parentMsg"></child>

<!-- ���ΰ� -->
<child :msg.once="parentMsg"></child>
```

˫���**���������� msg ����ͬ���ظ������ parentMsg ���ԡ�**���ΰ��ڽ���֮�󲻻�ͬ��֮��ı仯��

ע����� prop ��һ����������飬�ǰ����ô��ݡ�����������޸�����Ӱ�츸�����״̬��������ʹ�����ְ����͡�


> **11��Prop ��֤**

�������Ϊ props ָ����֤Ҫ�󡣵������������ʹ��ʱ������ã���Ϊ��Щ��֤Ҫ�󹹳�������� API��ȷ����������ȷ��ʹ���������ʱ props ��ֵ��һ�����󣬰�����֤Ҫ��

```
Vue.component('example', {
  props: {
    // �������ͼ�� ��`null` ��˼���κ����Ͷ����ԣ�
    propA: Number,
    // �������� (1.0.21+)
    propM: [String, Number],
    // ���������ַ���
    propB: {
      type: String,
      required: true
    },
    // ���֣���Ĭ��ֵ
    propC: {
      type: Number,
      default: 100
    },
    // ����/�����Ĭ��ֵӦ����һ����������
    propD: {
      type: Object,
      default: function () {
        return { msg: 'hello' }
      }
    },
    // ָ����� prop Ϊ˫���
    // ��������Ͳ��Խ��׳�һ������
    propE: {
      twoWay: true
    },
    // �Զ�����֤����
    propF: {
      validator: function (value) {
        return value > 10
      }
    },
    // ת��������1.0.12 ������
    // ������ֵ֮ǰת��ֵ
    propG: {
      coerce: function (val) {
        return val + '' // ��ֵת��Ϊ�ַ���
      }
    },
    propH: {
      coerce: function (val) {
        return JSON.parse(val) // �� JSON �ַ���ת��Ϊ����
      }
    }
  }
})
```

type ����������ԭ����������

1. String
2. Number
3. Boolean
4. Function
5. Object
6. Array

**type Ҳ������һ���Զ��幹������ʹ�� instanceof ��⡣**

�� prop ��֤ʧ���ˣ�Vue ���ܾ�������������ô�ֵ�����ʹ�õ��ǿ����汾���׳�һ�����档

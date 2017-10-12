# 第一章 Vue.js简介
## 1.1 Vue.js是什么
&emsp;&emsp;单独来讲，Vue.js被定义成一个用来开发Web界面的前端库，是个非常轻量级的工具。Vue.js本身具有响应式和组件化的特定。<br/>
&emsp;&emsp;所谓响应式编程，即为保持状态和视图的同步，这个在大多数前端MV*(MVC/MVVM/MVW)框架，不管是早期的backbone.js还是现在的AngularJS都对这一特性进行了实现(也称之为数据绑定),但这几者的实现方式和使用方式都不相同。相比而言，Vue.js使用起来更为简单，也无需引入太多新的概念，声明实例new Vue({ data:data })后自然对data里面的数据进行了视图上的绑定。修改data数据，视图中对应数据也会随之更改。<br/>
&emsp;&emsp;Vue.js的组件化理念和ReactJS异曲同工——"一切都是组件",可以将任意封装好的代码注册成标签，例如:Vue:component('example',Example),可以在模板中以<example></example>的形式调用。如果组件抽象的合理，这在很大程度上能减少重复开发，而且配合Vue.js的周边工具vue-loader,我们可以将一个组件的CSS、HTML和js都写在一个文件里，做到模块化开发。<br/>
&emsp;&emsp;除此之外，Vue.js也可以和一些周边工具配合起来，例如vue-router和vue-resource,支持了路由和异步请求，这样满足了开发单页面应用的基本条件。<br/>
## 1.2 为什么要用Vue.js
&emsp;&emsp;相比较AngularJS和ReactJS，Vue.js一直以轻量级，易上手被称道。MVVM的开发模式也使前端从原先的DOM操作中解放出来，我们不再需要在维护视图和数据的统一上花大量的时间，只需要关注与data的变化，代码变得更加容易维护。虽然社区和插件并没有一些老牌的开源项目那么丰富，但满足日常的开发是没有问题的。Vue.js2.0也已经发布了beta版本，渲染层基于一个轻量级的virtual-DOM实现，在大多数场景下初始化渲染速度和内存消耗都提升了2~4倍。而阿里也开源了weex(可以理解成ReactJS-Native和ReactJS的关系)，这也意味着Vue.js在移动端有了更多的可能性。<br/>
&emsp;&emsp;不过，对于为什么要选择使用一个框架，都需要建立在一定的项目基础上。如果脱离实际项目情况我们来谈某个框架的优劣，以及是否采用这种框架，我觉得是不够严谨的。<br/>
&emsp;&emsp;作为新兴的前端框架，Vue.js也抛弃了对IE8的支持，在移动端支持到Android 4.2+和IOS 7+。所以如果你在一家比较传统，还需要使用IE6的公司的话，你或许可以考虑其他的解决方案了。另外，在传统的前后端混合(通过后端模板引擎渲染)的项目中，Vue.js也会受到一定的限制，Vue实例只能和后端模板文件混合在一起，获取的数据也需要依赖于后端的渲染，这在处理一些JSON对象和数组的时候会有些麻烦。<br/>
&emsp;&emsp;理想状态下，我们能直接在前后端分离的项目中使用Vue.js最合适。这能最大程度上发挥Vue.js的优势和特性，熟悉后能极大的提升我们开发效率以及代码的复用率。尤其是移动浏览器上，Vue.js压缩后只有18KB,而且没有其他的依赖。<br/>
## 1.3 Vue.js的Hello world
&emsp;&emsp;现在来看一下我们第一个Vue.js项目，按照传统，我们来写一个Hello World。<br/>
&emsp;&emsp;首先，引入Vue.js的方式有很多，你可以直接使用CDN，例如：<br/>
&emsp;&emsp;`<script src="http://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.min.js"></script>`<br/>
&emsp;&emsp;也可以通过NPM进行安装：<br/>
&emsp;&emsp;`npm install vue`//最新稳定版本<br/>
&emsp;&emsp;正确引入Vue.js之后，我们在HTML文件中的内容为：<br/>
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue.js的Hello world</title>
    <script src="../js/vue.min.js" type="text/javascript"></script>
</head>
<body>
<div id="app">
    <h1>{{message}}</h1>
</div>
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        data:{
            message:'Hello world,I am Vue.js'
        }
    });
</script>
</body>
</html>
```
&emsp;&emsp;输出结果为：
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/1.3.PNG)
&emsp;&emsp;这种形式类似于前端模板引擎，我们把js中message值替换了HTML模板中{{message}}这部分。<br/>
&emsp;&emsp;不过，如果仅仅是这样的例子，我相信你也不会有什么兴趣去使用Vue.js。根据上文对Vue.js的说明，我们继续写两个有关于它特性的例子。<br/>
&emsp;&emsp;第一个特性是数据绑定，我们可以在运行上述例子的浏览器控制台(console)环境中输入vm.message='Hello Vue.js',输出结果就变为了Hello Vue.js。也就说明vm.message和视图中的{{message}}是绑定的，我们无需手动去获取``<h1>``标签来修改里面的innerHTML。<br/>
&emsp;&emsp;同样,我们也可以绑定用户输入的数据，视图会随着用户的输入而变化，例如：<br/>
```html
<div id="app">
    <h1>Your input is {{message}}</h1>
    <input type="text" v-model="message">
</div>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/1.3.1.PNG)
&emsp;&emsp;vm.message的值会随着用户在input中输入的值的变化而变化，而无需我们手动去获取DOM元素的值再同步到js中。<br/>
&emsp;&emsp;第二个特性是组件化，简单来说我们可以自己定义HTML标签，并在模板中使用它，例如：<br/>
```html
<div id="app">
    <message content='Hello World'></message>
</div>
<script type="text/javascript">
    var Message=Vue.extend({
        props:['content'],
        template:'<h1>{{content}}</h1>'
    });
    Vue.component('message',Message);
    var vm=new Vue({
        el:'#app',
    });
</script>
```
&emsp;&emsp;我们在浏览器里最终看到的HTML结果为：<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/1.3.2.PNG)
&emsp;&emsp;可以看到自定义的标签<message>被替换成了``<h1>Hello World</h1>``,当然，实际中的组件远比示例复杂，我们会给组件添加参数及方法，使之能更好地被复用。<br/>
# 第二章 基础特性
## 2.1 实例及选项
&emsp;&emsp;从以前的例子中可以看出，Vue.js的使用都是通过构造函数Vue{{option}}创建一个Vue的实例：var vm=new Vue({})。一个Vue实例相当于一个MVVM模式中的ViewModel。如图2-1所示。<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.1.PNG)
>图2-1
                
&emsp;&emsp;在实例化的时候，我们可以传入一个选项对象，包含数据、模板、挂载元素、方法、生命周期钩子等选项。下面就对一些常用的选项对象属性进行具体的说明。<br/>
### 2.1.1 模板
&emsp;&emsp;选项中主要影响模板或DOM的选项有el和template，属性replace和template需要一起使用。<br/>
&emsp;&emsp;el:类型为字符串，DOM元素或函数。其作用是为实例提供挂载元素。一般来说我们会使用css选择符，或者原生的DOM元素。例如``el:'#app'``。在初始项中指定了el，实例将立即进入编译过程。<br/>
&emsp;&emsp;template:类型为字符串。默认会将template值替换挂载元素(即el值对应的元素)，并合并挂载元素和模板根节点的属性(如果属性具有唯一性，类似id，则以模板根节点为准)。如果replace为false，模板template的值将插入挂载元素内。通过template插入模板的时候，挂载元素的内容都将被互联，除非使用slot进行分发。在使用template时，我们往往不会把所有的HTML字符串直接写在js里面，这样影响可读性而且也不利于维护。所以经常用``'#tpl'``的方式赋值，并且在body内容添加``<scrip id="tpl" type="x-template">``为标签包含的HTML内容，这样就能将HTML从js中分离开来，示例如下：<br/>
```html
<div id="app">
    <p>123</p>
</div>
<script id="tpl" type="x-template">
    <div class="tpl">
        <p>This is a tpl from script tag</p>
    </div>
</script>
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        template:'#tpl'
    });
</script>
```
最终输出HTML结构为:<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.2.PNG)
&emsp;&emsp;Vue.js 2.0中废除了replace这个参数，并且强制要求每一个Vue.js实例需要有一个根元素，即不允许组件模板为：<br/>
```html
<script id="tpl" type="x-template">
    <div class="tpl">
        ...
    </div>
    <div class="tpl">
        ...
    </div>
</script>
```
&emsp;&emsp;这样的兄弟节点为根节点的模板形式，需要改写成：<br/>
```html
<script id="tpl" type="x-template">
    <div class="wrapper">
        <div class="tpl">
            ...
        </div>
        <div class="tpl">
            ...
        </div>
    </div>
</script>
```
### 2.1.2 数据
&emsp;&emsp;Vue.js实例中可以通过data属性定义数据，这些数据可以在实例对应的模板中进行绑定并使用。需要注意的是，如果传入data的是一个对象，Vue实例会代理起data对象里的所有属性，而不会传入对象进行深拷贝。另外，我们也可以用Vue实例vm中的$data来获取声明的数据，例如：<br/>
```html
var data={a:1}
var vm=new Vue({
    data:data
});
vm.$data===data//->true
vm.a===data.a//->true
//设置属性也会影响原始数据
vm.a=2
data.a// ->2
//反之亦然
data.a=3
vm.a // ->3
```
&emsp;&emsp;然后在模板中使用{{a}}就会输出vm.a的值，并且修改vm.a的值，模板中的值会随之改变，我们也称这个数据为响应式(responsive)数据。<br/>
&emsp;&emsp;需要注意的是，只有初始化时传入的对象才是响应式的，即在声明完实例后，再加上一句``vm.$data.b='2'``,并在模板中使用{{b}},这时是不会输出字符串'2'的，例如:<br/>
```html
<div id="app">
    <h1>{{a}}</h1>
    <h1>{{b}}</h1>
</div>
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        data:{
            a:1
        }
    });
    vm.$data.b=2;
</script>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.3.PNG)
&emsp;&emsp;如果需要在实例化之后加入响应式变量，需要调用实例方法$set,例如：<br/>
``vm.$set('b',2);``<br/>
```html
<div id="app">
    <h1>{{a}}</h1>
    <h1>{{b}}</h1>
</div>
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        data:{
            a:1
        }
    });
    vm.$set('b',2);
</script>
```
&emsp;&emsp;不过Vue.js并不推荐这么做，这样会抛出一个异常(事实上，我并没有发现异常)：<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.4.PNG)
&emsp;&emsp;所以，我们应尽量在初始化的时候，把所有的变量都设定好，如果没有值，也可以用undefined或null占位。<br/>
&emsp;&emsp;另外，组件类型的实例可以通过props获取数据，同data一样，也需要在初始化时预设好。示例：<br/>
```javascript
<my-component title="myTitle" content="myContent"></my-component>
    var myComponent=Vue.component('my-component', {
        props: ['title', 'content'],
        template: '<h1>{{title}}</h1><p>{{content}}</p>'
    });
```
&emsp;&emsp;我们也可以在上述类型实例中同时使用data，但有两个地方需要注意：(1)data的值必须是一个函数，并且返回值是原始对象。如果传给组件的data是一个原始对象的话，则在建立多个组件实例时它们就会共用这个data对象，修改其中一个组件实例的数据就会影响到其他组件实例的数据，这显然不是我们所期望的。(2)data中的属性和props中的不能重名。这两者都会抛出异常。<br/>
&emsp;&emsp;所以正确的使用方法如下：<br/>
```javascript
<script type="text/javascript">
    var MyComponent=Vue.component('my-component',{
        props:['title','content'],
        data:function () {
            return{
                desc:'123'
            }
        },
        template:'<div><h1>{{title}}</h1><p>{{content}}</p><p>{{desc}}</p></div>'
    })
</script>
```
### 2.1.3 方法
&emsp;&emsp;我们可以通过选项属性methods对象来定义方法，并且通过v-on指令来监听DOM事件，例如：<br/>
```html
<button v-on:click="alert"/>alert</button>
<script type="text/javascript">
    new Vue({
        el:'#app',
        data:{a:1},
        methods:{
            alert:function () {
                alert(this.a);
            }
        }
    });
</script>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.5.PNG)
&emsp;&emsp;另外，Vue.js也支持自定义事件，可以在初始化时传入events对象，通过实例的$emit方法进行触发。这套通信机制常用在组件间相互通信的情况中，例如子组件冒泡触发父组件事件方法，或者父组件广播某个事件，子组件对其进行监听等。<br/>
```javascript
var vm=new Vue({
        el:'#app',
        data:data,
        events:{
            'event.alert':function () {
                alert('this is event alert:'+this.a);
            }
        }
    });
    vm.$emit('event.alert');
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.6.PNG)
&emsp;&emsp;而Vue.js 2.0中废除了events选项属性，不再支持事件广播的这类特性，推荐直接使用Vue实例的全局方法$on()/$emit(),或者使用插件Vuex来处理。<br/>
### 2.1.4 生命周期
&emsp;&emsp;Vue.js实例在创建时有一系列的初始化步骤，例如建立数据观察，编译模板，创建数据绑定等。在此过程中，我们可以通过一些定义好的生命周期钩子函数来运行业务逻辑。例如：
<br/>
```javascript
var vm=new Vue({
        data:{
            a:1
        },
        created:function () {
            console.log('created')
        }
    })
```
&emsp;&emsp;运行上述例子时，浏览器console中就会打印出created。<br/>
&emsp;&emsp;下图是实例的生命周期。<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.7.PNG)<br/>
&emsp;&emsp;init:在实例开始初始化时同步调用。此时已完成数据观测、事件等都尚未初始化。2.0中更名为beforeCreate。<br/>
&emsp;&emsp;created:在实例创建之后调用。此时已完成数据绑定、事件方法，但尚未开始DOM编译，即未挂载到document中。<br/>
&emsp;&emsp;beforeCompile:在DOM编译前调用。2.0废除了该方法，推荐使用created。<br/>
&emsp;&emsp;beforeMount:2.0新增的声明钩子函数，在mounted之前运行。<br/>
&emsp;&emsp;compiled:在编译结束时调用。此时所有指令已生效，数据变化已能触发DOM更新，但不保证$el已插入文档。2.0中更名为mounted。<br/>
&emsp;&emsp;ready:在编译结束和$el第一次插入文档之后调用。2.0废弃了该方法，推荐使用mounted。这个变化其实已经改变了ready这个生命周期状态，相当于取消了在$el首次插入文档后的钩子函数。<br/>
&emsp;&emsp;attached:在vm.$el插入DOM时调用，ready会在第一次attached后调用。操作$el必须使用指令或实例方法(例如$appendTo()),直接操作vm.$el不会触发这个钩子。2.0废弃了该方法，推荐在其他钩子函数中自定义方法检查是否已挂载。<br/>
&emsp;&emsp;detached:同attached类似，该钩子在vm.$el从DOM删除时调用，而且必须是指令或实例方法。2.0中同样废弃了该方法。<br/>
&emsp;&emsp;beforeDestroy:在开始销毁实例时调用，此刻实力仍然有效。<br/>
&emsp;&emsp;destroyed:在实例被销毁之后调用。此时所有绑定和实例指令都已经解绑，子实例也被销毁。<br/>
&emsp;&emsp;beforeUpdate:2.0新增的生命周期钩子，在实例挂载之后，再次更新实例(例如更新data)时会调用该方法，此时尚未更新DOM结构。<br/>
&emsp;&emsp;updated:2.0新增的生命周期钩子，在实例挂载之后，再次更新实例并更新完DOM结构后调用。<br/>
&emsp;&emsp;activated:2.0新增的生命周期钩子，需要配合动态组件keep-live属性使用。在动态组件初始化渲染的过程中调用该方法。<br/>
&emsp;&emsp;deactivated:2.0新增的生命周期钩子，需要配合动态组件keep-live属性使用。在动态组件移出的过程中调用该方法。<br/>
&emsp;&emsp;可以通过一个简单的demo来更清楚地了解内部的运行机制，代码如下：<br/>
```javascript
var vm=new Vue({
        el:'#app',
        init:function () {
            console.log('init');
        },
        created:function () {
            console.log('created');
        },
        beforeCompile:function () {
            console.log('beforeCompile');
        },
        compiled:function () {
            console.log('compiled');
        },
        attached:function () {
            console.log('attached');
        },
        dettached:function () {
            console.log('dettached');
        },
        beforeDestroy:function () {
            console.log('beforeDestroy');
        },
        destroyed:function () {
            console.log('destroyed');
        },
        ready:function () {
            console.log('ready');
            //组件完成后调用$destroy函数，进行销毁
            this.$destroy();
        }
    });
```
&emsp;&emsp;输出结果为:<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.8.PNG)
## 2.2 数据绑定
### 2.2.1 数据绑定语法
&emsp;&emsp;本小节主要介绍Vue.js的数据绑定语法，出现的例子会基于以下js代码：<br/>
```javascript
var vm=new Vue({
        el:'#app',
        data:{
            id:1,
            index:0,
            name:'Vue',
            avatar:'http://......',
            count:[1,2,3,4,5],
            names:['Vue1.0','Vue2.0'],
            items:[
                {name:'Vue1.0',version:'1.0'},
                {name:'Vue1.1',version:'1.0'}
            ]
        }
    });
```
#### 1.文本插值
&emsp;&emsp;数据绑定最基础的形式就是文本插值，使用的是双大括号{{}},为"Mustache"语法(源自前端模板引擎Mustache.js),示例如下：<br/>
```javascript
<span>Hello {{name}}</span>//->Hello Vue;
```
&emsp;&emsp;Vue.js实例vm中的name属性的值将会替换Mustache标签中的name,并且修改数据对象中的name属性，DOM也会随之更新。在浏览器console中运行vm.name='Vue 1.0',输出结果为Hello Vue 1.0。<br/>
&emsp;&emsp;模板语法同时也支持单次插值，即首次赋值后再更改vm实例属性值不会引起DOM变化，例如以下模板在运行vm.name='Vue 1.0'后，依旧输出Hello Vue:<br/>
```javascript
<span>Hello {{* name }}</span>//->Hello Vue
```
&emsp;&emsp;Vue.js2.0去除了{{*}}这种写法，采用v-once代替。以上模板需要改写为`<span v-once="name">{{name}}</span>`
#### 2.HTML属性
&emsp;&emsp;Mustache标签也同样适用于HTML属性中，例如：<br/>
`<div id="id-{{id}}"></div>  //<div id="id-1"></div>`<br/>
&emsp;&emsp;Vue.js2.0中废除了这种写法，用v-bind指令代替，`<div v-bind:id="'id-'+id"/></div>`代替，或简写为`<div :id="'id-'+id"></div>`
#### 3.绑定表达式
&emsp;&emsp;放在Mustache标签内的文本内容称为绑定表达式。除了直接输出属性值之外，一段绑定表达式可以由一个简单的JavaScript表达式和可选的一个或多个过滤器构成。例如：<br/>
```javascript
{{ index + 1 }} //1
{{ index == 0 ? 'a':'b' }} //a
{{ name.split('').join('|') }} //V|u|e
```
&emsp;&emsp;每个绑定中只能包含单个表达式，并不支持JavaScript语句，否则Vue.js就会抛出warning异常。并且绑定表达式里不支持正则表达式，如果需要进行复杂的转换，可以使用过滤器或者计算属性来进行处理，以下的例子即为无效的表达式:<br/>
```javascript
{{ var a = 1 }} //无效
{{ if(ok) { return name } }} //无效，但可以写成ok ? name : '' 或者 ok && name这样的写法
```
#### 4.过滤器
&emsp;&emsp;Vue.js允许在表达式后添加可选的过滤器，以管道符"|"指示。示例<br/>
&emsp;&emsp;`{{ name | uppercase }} //VUE` <br/>
&emsp;&emsp;Vue.js将name的值传入给uppercase这个内置的过滤器中(本质是一个函数),返回字符串的最大值。同时也允许多个过滤器链式使用，例如：<br/>
&emsp;&emsp;`{{ name | filterA | filterB }}` <br/>
&emsp;&emsp;也允许传入多个参数，例如：<br/>
&emsp;&emsp;`{{ name | filterA arg1 arg2 }}` <br/>
&emsp;&emsp;此时，filterA将name的值作为第一个参数，arg1,arg2作为第二，第三个参数传入过滤器函数中。最终函数的返回值即为输出结果。arg1,arg2可以使用表达式，也可以加上单引号，直接传入字符串。例如：<br/>
&emsp;&emsp;`{{ name.split('') | limitBy 3 1 }} //->u,e` <br/>
&emsp;&emsp;过滤器limitBy可以接受两个参数，第一个参数是设置显示个数，第二个参数为可选，指从开始元素的数组下标。<br/>
&emsp;&emsp;Vue.js内置了10个过滤器，下面简单介绍它们的功能和用法。<br/>
* capitalize:字符串字符转化为大写
* uppercase:字符串转化成大写
* lowercase:字符串转化为小写
* currency 参数为{String}[货币符号]，{Number}[小数位]，将数字转化为货币符号，并且会自动添加数字分节号。例如：
`{{ amount | currency '￥' 2 }}` // ->若amount值为10000,则输出￥10000.00
* pluralize参数为{String}single,[double,triple],字符串复数化。如果接收的是一个参数，那复数形式就是在字符串末尾直接加一个"s"。如果接收多个参数，则会被当成数组处理，字符串会添加对应数组下标的值。如果字符串的个数多于参数个数，多出部分会都添加最后一个参数的值。例如：
`<p  v-for="c in count"> {{ c | pluralize 'item' }} {{ c | pluralize 'st' 'nd' 'rd' 'th' }}</p>`
&emsp;&emsp;输出结果:<br/>
```html
1item 1st
2items 2nd
3items 3rd
4items 4th
```
* json参数为{Number}[indent]空格缩进数，与JSON.stringify()作用相同，将json对象数据输出成符合json格式的字符串。
* debounce传入值必须是函数，参数可选，为{Number}[wait],即延时时长。作用是当调用函数n毫秒后，才会执行该动作，若在这n毫秒内有调用此动作则将重新计算执行时间。例如：
```javascript
<input v-on:keyup="onKeyup | debounce 500"> //input元素上监听了keyup事件，并且延迟了500ms触发
```
* limitBy 传入值必须是数组，参数为{Number}limit,{Number}[offset],limit为显示个数，offset为开始显示数组下标。例如：
```javascript
<div v-for="item in items | limitBy 10"></div> //items为数组，且只显示数组中的前十个元素
```
* filterBy传入值必须是数组，参数为{String | Function} targetStringOrFunction,即需要匹配的字符串或函数(通过函数返回值为true或false来判断匹配结果);"in"(可选分隔符);{String}[...searchKeys],为检索的属性区域。示例：
```javascript
 <p v-for="item in items | filterBy '1.0' in 'name'">{{item | json}}</p> //检索items数组中属性name值为1.0的元素输出。检索区域也可以为数组，即in [name,version],在多个属性中进行检索
```
上述两个例子的输出结果为:
Vue1.0
{"name":"Vue1.0","version":"1.0"}
```javascript
<p v-for="item in items | filterBy customFilter">{{item | json}}</p>//使用自定义的过滤函数，函数可以在选项methods中定义
    methods:{
        customFilter:function(item){
            if(item.name) return true //检索所有元素中包含name属性的元素
        }
    }
```
* orderBy传入值必须是数组，参数为{String|Array|Function}sortKeys,即指定排序策略。这里可以使用单个键名，也可以传入包含多个排序键名的数组。也可以像Array.Sort()那样传入自己的排序策略函数。第二个参数为可选参数{Stirng}[order],即选择升序或降序，order>=0为升序，order<0为降序。
```javascript
单个键名：<p v-for="item in items | orderBy 'name' -1">{{item.name}}</p>//items数组中以键名name进行降序排列
    多个键名：<p v-for="item in items | orderBy [name,version]">{{item.name}}</p> //使用items里的两个键名进行排序
    自定义排序函数：<p v-for="item in items | orderBy customOrder">{{item.name}}</p>
    methods:{
        customOrder:function(a,b){
            return parseFloat(a.version) > parseFloat(b.version) //对比item中version的值的大小进行排序
        }
    }
```
#### 5.指令
&emsp;&emsp;Vue.js也提供指令(Directives)这一概念，可以理解为当表达式的值发生改变时，会有特殊行为作用到绑定的DOM上。指令通常会直接书写在模板的HTML元素中，而为了有别于普通的属性，Vue.js指令是带有前缀v-的属性。写法上来说，指令的限定为绑定表达式。<br/>
* 参数<br/>
`<img v-bind:src="avatar"/>`<br/>
&emsp;&emsp;指令v-bind可以在后面带一个参数，用冒号(:)隔开，src即为参数。此时img标签中的src会与vm实例中的avatar绑定，等同于:<br/>
`<img src="{{avatar}}" />`
* 修饰符<br/>
&emsp;&emsp;修饰符(Modifiers)是以半角句号.开始的特殊后缀，用于表示指令应该以特殊方式绑定。<br/>
&emsp;&emsp;`<button v-on:click.stop="doClick"></button>`<br/>
&emsp;&emsp;v-on的作用是在对应的DOM元素上绑定时间监听器，doClick为函数名，而stop即为修饰符，作用是停止冒泡，相当于调用了e.stopPropagation()。
### 2.2.2 计算属性
&emsp;&emsp;在项目开发中,我们展示的数据往往需要经过一些处理。除了在模板中绑定表达式或者利用过滤器外,Vue.js还提供了计算属性这种方法,避免在模板中加入过重的业务逻辑,保证模板的结果清晰和可维护性。<br/>
#### 1.基础例子
```javascript
<div id="app">
    <p>{{firstName}}</p>//Gavin
    <p>{{lastName}}</p>//CLY
    <p>{{fullName}}</p>//Gavin CLY
</div>
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        data:{
            firstName:'Gavin',
            lastName:'CLY'
        },
        computed:{
            fullName:function () {
                //this指向vm实例
                return this.firstName+' '+this.lastName
            }
        }
    });
</script>
```
&emsp;&emsp;此时你对vm.firstName和vm.lastName修改，始终会影响vm.fullName。<br/>
#### 2.Setter
```javascript
<script type="text/javascript">
    var vm=new Vue({
        el:'#el',
        data:{
            cents:100,
        },
        computed:{
            price:{
                set:function (newValue) {
                    this.cents=newValue*100;
                },
                get:function () {
                    return (this.cents/100).toFixed(2);
                }
            }
        }
    });
</script>
```
&emsp;&emsp;在处理商品价格的时候，后端往往会把价钱定义成以分为单位的整型，避免在处理浮点类型数据时产生的问题。而前端则需要把价钱在转换成元进行展示，而且如果需要对价钱进行修改的话，则又要把输入的价格在恢复到分传给后端，很是繁琐。<br/>
&emsp;&emsp;而在使用Vue.js的计算属性后，我们可以将vm.cents设置为后端所存的数据，计算属性price为前端展示和更新的数据。<br/>
```<p>&yen;{{price}}</p> //￥1.00```<br/>
&emsp;&emsp;此时更改vm.price=2,vm.cents会被更新为200，在传递给后端时无需再手动转化一遍数据。<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.9.PNG)
### 2.2.3 表单控件
&emsp;&emsp;Vue.js中提供v-model的指令对表单元素进行双向数据绑定，在修改表单元素值的同时，实例vm中对应的属性值也同时更新，反之亦然。本小节会介绍主要input元素绑定v-model后的具体用法和处理方式，示例所依赖的js代码如下:<br/>
```javascript
<script type="text/javascript">
    var vm=new Vue({
        el:'#app',
        data:{
            message:'',
            gender:'',
            checked:'',
            multiChecked:[],
            selected:'',
            multiSelected:[]
        }
    });
</script>
```
#### 1.Text
&emsp;&emsp;输入框提示，用户输入的内容和vm.message直接绑定。<br/>
```javascript
<div id="app">
    <input type="text" v-model="message"/>
    <span>Your input is:{{message}}</span>
</div>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.10.PNG)<br/>
#### 2.Radio
```javascript
<label><input type="radio" value="male" v-model="gender">男 </label>
    <label><input type="radio" value="female" v-model="gender">女 </label>
    <p>{{gender}}</p>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.11.PNG)<br/>
#### 3.Checkbox
&emsp;&emsp;单个勾选框，v-model即为布尔值，此时input的value并不影响v-model的值。<br/>
```javascript
 <input type="checkbox" v-model="checked"/>
    <span>checked:{{checked}}</span>
```
&emsp;&emsp;多个勾选框，v-model使用相同的属性名称。切属性为数组。<br/>
```javascript
<label><input type="checkbox" value="1" v-model="multiChecked">1 </label>
    <label><input type="checkbox" value="2" v-model="multiChecked">2 </label>
    <label><input type="checkbox" value="3" v-model="multiChecked">3 </label>
    <p>MultiChecked:{{multiChecked.join('|')}}</p>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.12.PNG)<br/>
#### 4.Select
```javascript
 <select v-model="selected">
        <option selected>A</option>
        <option>B</option>
        <option>C</option>
    </select>

    <span>Selected:{{selected}}</span>
    <select v-model="multiSelected" multiple>
        <option selected>A</option>
        <option>B</option>
        <option>C</option>
    </select>
    <span>MultiSelected:{{multiSelected.join('|')}}</span>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.13.PNG)<br/>
#### 5.绑定value
&emsp;&emsp;表单控件的值同样可以绑定在Vue实例的动态属性上，用v-bind实现。示例:<br/>
1.Checkbox
```javascript
<input type="checkbox" v-model="checked" v-bind:true-value="a" v-bind:false-value="b">
```
选中:vm.checked==vm.a //->true
未选中:vm.checked==vm.b //->true<br/>
2.Radio
```javascript
<input type="radio" v-model="checked",v-bind:value="a">
```
选中:vm.checked==vm.a //->true <br/>
3.Select Options
```javascript
<select v-model="selected">
    <!--对象字面量-->
    <option v-bind:value="{number:123}">123</option>
</select>
```
选中:typeof vm.selected// -> 'object'
vm.selected.number // ->123
#### 6.参数特性
* lazy
默认情况下，v-model在input事件中同步输入框值与数据，加lazy属性后从会改到在change事件中同步。
```javascript
<input v-model="query" lazy />
```
* nunber
会自动将用户输入转为Number类型，如果原值转换结果为NaN则返回原值。
```javascript
<input v-model="age" number />
```
* debounce
debounce为设置的最小时延，单位为ms,即为单位时间内仅执行一次数据更新。该参数往往应用在高耗操作上，例如在更新时发出ajax请求返回提示信息。
```javascript
<input v-model="query" debounce="500"/>
```
不过Vue.js2.0中取消了lazy和nubmer作为参数，用修饰符(modifier)来代替:
```javascript
<input v-model.lazy="query" /> <input v-model.number="age"/>
```
新增了trim修饰符,去掉输入值首尾空格:
```javascript
<input v-model.trim="name" />
```
去除了debounce这个参数，原因是无法监测到输入新数据，但尚未同步到vm实例属性时这个状态。
### 2.2.4 Class与Style绑定
&emsp;&emsp;在开发过程中，我们经常会遇到动态添加类名或直接修改内联样式（例如 tab 切换）。class 和 style 都是DOM元素的attribute, 我们当然可以直接使用 v-bind 对这两个属性进行
数据绑定，例如 <p v-bind:style='style'><p>，然后通过修改 vm.style 的值对元素样式进行修改。但这样未免过于繁琐而且容易出错，所以 Vue.js 为这两个属性单独做了增强处理，表
达式的结果类型除了字符串之外，还可以是对象和数组。本小节就会对这两个属性具体的用法进行说明。<br/>
#### 1．Class绑定
首先说明的是 class 属性，我们绑定的数据可以是对象和数组，具体的语法如下：<br/>
① 对象语法： v-bind:class 接受参数是一个对象，而且可以与普通的 class 属性共存。<br/>
```javascript
<div class="tab" v-bind:calss="{'active' : active , 'unactive' : !active}">
</div>
vm 实例中需要包含
data : {
active : true
}
```
渲染结果为：``<div class="tab active"></div>``<br/>
② 数组语法： v-bind:class 也接受数组作为参数。
```javascript
<div v-bind:class="[classA, classB]"></div>
vm 实例中需要包含
data : {
classA : 'class-a',
classB : 'class-b'
}
```
渲染结果为： ``<div class="class-a class-b"></div>。``<br/>
也可以使用三元表达式切换数组中的 ``class， <div v-bind:class="[classA, isB ? classB :
'']"></div>``。如果 vm.isB = false, 则渲染结果为`` <div v-bind:class="class-a"></div>``。















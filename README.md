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
#### 2．内联样式绑定
style 属性绑定的数据即为内联样式，同样具有对象和数组两种形式：
① 对象语法：直接绑定符合样式格式的对象。
```javascript
<div v-bind:style="alertStyle"></div>
data : {
alertStyle : {
color : 'red',
fontSize : '20px'
}
}
```
除了直接绑定对象外，也可以绑定单个属性或直接使用字符串。
``<div v-bind:style="{ fontSize : alertStyle.fontSize, color : 'red'}"></div>``<br/>
② 数组语法： v-bind:style 允许将多个样式对象绑定到统一元素上。<br/>
``<div v-bind:style="[ styleObjectA, styleObjectB]" .></div>``
#### 3．自动添加前缀
在使用 transform 这类属性时， v-bind:style 会根据需要自动添加厂商前缀。 :style 在运行时进行前缀探测，如果浏览器版本本身就支持不加前缀的 css 属性，那就不会添加。
## 2.3模板渲染
当获取到后端数据后，我们会把它按照一定的规则加载到写好的模板中，输出成在浏览器中显示的 HTML，这个过程就称之为渲染。而Vue.js是在前端（即浏览器内）进行的模板渲染。本节主要介绍 Vue.js 渲染的基本语法。
### 2.3.1　前后端渲染对比
&emsp;&emsp;早期的Web项目一般是在服务器端进行渲染，服务器进程从数据库获取数据后，利用后端模板引擎，甚至于直接在HTML模板中嵌入后端语言（例如 JSP），将数据加载进来生成HTML，然后通过网络传输到用户的浏览器中,然后被浏览器解析成可见的页面。而前端渲染则是在浏览器里利用JS把数据和HTML 模板进行组合。两种方式各有自己的优缺点，需要更具自己的业务场景来选择技术方案。<br/>
&emsp;&emsp;前端渲染的优点在于：<br/>
&emsp;&emsp;① 业务分离，后端只需要提供数据接口，前端在开发时也不需要部署对应的后端环境，通过一些代理服务器工具就能远程获取后端数据进行开发，能够提升开发效率。<br/>
&emsp;&emsp;② 计算量转移，原本需要后端渲染的任务转移给了前端，减轻了服务器的压力。<br/>
&emsp;&emsp;而后端渲染的优点在于：<br/>
&emsp;&emsp;① 对搜索引擎友好。<br/>
&emsp;&emsp;② 首页加载时间短，后端渲染加载完成后就直接显示HTML，但前端渲染在加载完成后还需要有段 js渲染的时间。Vue.js2.0开始支持服务端渲染，从而让开发者在使用上有了更多的选择。
### 2.3.2　条件渲染
&emsp;&emsp;Vue.js 提供 v-if，v-show，v-else，v-for这几个指令来说明模板和数据间的逻辑关系，这基本就构成了模板引擎的主要部分。下面将详细说明这几个指令的用法和场景。
#### 1．v-if/v-else
&emsp;&emsp;v-if 和 v-else 的作用是根据数据值来判断是否输出该 DOM 元素，以及包含的子元素。例如：<br/>
``<div v-if="yes">yes</div>``<br/>
&emsp;&emsp;如果当前 vm 实例中包含``data.yes=true``，则模板引擎将会编译这个 DOM 节点，输出``<div>yes</div>``。
我们也可以利用 v-else 来配合v-if使用。例如：<br/>
```javascript
<div v-if="yes">yes</div>
<div v-else>no</div>
```
&emsp;&emsp;需要注意的是，v-else必须紧跟v-if，不然该指令不起作用。例如：<br/>
```javascript
<div v-if="yes">yes</div>
<p>the v-else div shows</p>
<div v-else>no</div>
```
&emsp;&emsp;最终这三个元素都会输出显示在浏览器中。<br/>
&emsp;&emsp;v-if 绑定的元素包含子元素则不影响和 v-else 的使用。例如：<br/>
```javascript
<div v-if="yes">
<div v-if="inner">inner</div>
<div v-else>not inner</div>
</div>
<div v-else>no</div>
new Vue({
data : {
yes : true,
inner : false
}
})
```
&emsp;&emsp;输出结果为：<br/>
```javascript
<div>
<div>not inner></div>
</div>
```
#### 2．v-show
&emsp;&emsp;除了v-if，v-show也是可以根据条件展示元素的一种指令。例如：<br/>
``<div v-show="show">show</div>``<br/>
&emsp;&emsp;也可以搭配 v-else 使用，用法和 v-if 一致。例如：<br/>
``<div v-show="show">show</div>``
``<div v-else>hidden</div>``<br/>
&emsp;&emsp;与v-if不同的是，v-show元素的使用会渲染并保持在 DOM 中。 v-show 只是切换元素的 css属性 display。例如：<br/>
``<div v-if="show">if</div>``
``<div v-show="show">show</div>``<br/>
&emsp;&emsp;show 分别为 true 时的结果：<br/>
```javascript
<!-- v-if vs v-show -->
<div>if</div>
<div>show</div>
```
&emsp;&emsp;show 分别为 false 时的结果：<br/>
```javascript
<!-- v-if vs v-show -->
<div style="display:none;">show</div>
```
#### 3．v-if vs v-show
&emsp;&emsp;从上述 v-show 图能够明显看到，当 v-if 和 v-show 的条件发生变化时，v-if引起了dom操作级别的变化，而 v-show仅发生了样式的变化，从切换的角度考虑， v-show 消耗的性能要比 v-if 小。<br/>
&emsp;&emsp;除此之外， v-if 切换时， Vue.js 会有一个局部编译 / 卸载的过程，因为 v-if 中的模板
也可能包括数据绑定或子组件。v-if会确保条件块在切换当中适当地销毁与中间内部的事件监听器和子组件。而且 v-if 是惰性的，如果在初始条件为假时， v-if 本身什么都不会做，而v-show则仍会进行正常的操作，然后把 css 样式设置为 display:none。<br/>
&emsp;&emsp;所以，总的来说，v-if有更高的切换消耗而 v-show 有更高的初始渲染消耗，我们需要根据实际的使用场景来选择合适的指令。
### 2.3.3　列表渲染
&emsp;&emsp;v-for指令主要用于列表渲染，将根据接收到数组重复渲染v-for绑定到的DOM元素及内部的子元素，并且可以通过设置别名的方式，获取数组内数据渲染到节点中。例如：<br/>
```javascript
<ul>
<li v-for="item in items">
<h3>{{item.title}}</h3>
<p>{{item.description}}</p>
</li>
</ul>
var vm = new Vue({
el : '#app',
data: {
items : [
{ title : 'title-1', description : 'description-1'},
{ title : 'title-2', description : 'description-2'},
{ title : 'title-3', description : 'description-3'},
{ title : 'title-4', description : 'description-4'}
]
}
});
```
&emsp;&emsp;其中items为data中的属性名，item为别名，可以通过 item来获取当前数组遍历的每个元素，输出结果为：<br/>
```javascript
<ul>
<li>
<h3>title-1</h3>
<p>description-1</p>
</li><li>
<h3>title-2</h3>
<p>description-2</p>
</li><li>
<h3>title-3</h3>
<p>description-3</p>
</li><li>
<h3>title-4</h3>
<p>description-4</p>
</li>
</ul>
```
&emsp;&emsp;v-for 内置了 $index 变量，可以在 v-for 指令内调用，输出当前数组元素的索引。另
外，我们也可以自己指定索引的别名，如
```javascript
<li v-for="(index,item) in items">{{index}} –
{{$index}} – {{item.title}}</li>
```
，输出结果为：<br/>
```javascript
<ul>
<li>
0 - 0 - title-1
</li><li>
1 - 1 - title-2
</li><li>
2 - 2 - title-3
</li><li>
3 - 3 - title-4
</li>
</ul>
```
&emsp;&emsp;需要注意的是Vue.js对data中数组的原生方法进行了封装，所以在改变数组时能触发视图更新，但以下两种情况是无法触发视图更新的：<br/>
&emsp;&emsp;① 通过索引直接修改数组元素， 例如 ``vm.items[0] = { title : 'title-changed'}``;<br/>
&emsp;&emsp;② 无法直接修改“修改数组”的长度， 例如： ``vm.items.length = 0``<br/>
&emsp;&emsp;对于第一种情况， Vue.js 提供了 \$set 方法，在修改数据的同时进行视图更新，可以写成：<br/>
&emsp;&emsp;``vm.items.$set(0, { title : 'title-changed'}`` 或 者 ``vm.$set('items[0]', { title : 'titlealso-changed'})``，这两种方式皆可以达到效果。<br/>
&emsp;&emsp;在列表渲染的时候，有个性能方面的小技巧，如果数组中有唯一标识 id，例如：<br/>
```javascript
items : [
{ _id : 1, title : 'title-1'},
{ _id : 2, title : 'title-2'},
{ _id : 3, title : 'title-3'}
…
]
```
&emsp;&emsp;通过trace-by给数组设定唯一标识，我们将上述 v-for 作用于的 li 元素修改为：<br/>
&emsp;&emsp;``<li v-for="item in items" track-by="_id"></li>``<br/>
&emsp;&emsp;这样，Vue.js在渲染过程中会尽量复用原有对象的作用域及 DOM 元素。<br/>
&emsp;&emsp;v-for除了可以遍历数组外，也可以遍历对象，与 \$index 类似，作用域内可以访问另一内置变量 \$key，也可以使用（key,value）形式自定义key变量。
```javascript
<li v-for="(key, value) in objectDemo">
{{key}} - {{$key}} : {{value}}
</li>
var vm = new Vue({
el : '#app',
data: {
objectDemo : {
a : 'a-value',
b : 'b-value',
c : 'c-value',
}
}
});
```
&emsp;&emsp;输出结果：<br/>
```javascript
a-a:a-value
b-b:b-value
c-c:c-value
```
&emsp;&emsp;最后，v-for还可以接受单个整数，用作循环次数：<br/>
```javascript
<li v-for="n in 5">
{{ n }}
</li>
```
&emsp;&emsp;输出结果：<br/>
```javascript
0
1
2
3
4
```
### 2.3.4　template标签用法
&emsp;&emsp;上述的例子中，v-show和v-if指令都包含在一个根元素中，那是否有方式可以将指令作用到多个兄弟 DOM 元素上？Vue.js提供了template标签，我们可以将指令作用到这个标签上，但最后的渲染结果里不会有它。例如：<br/>
```javascript
<template v-if="yes">
<p>There is first dom</p>
<p>There is second dom</p>
<p>There is third dom</p>
</template>
```
&emsp;&emsp;输出结果为：<br/>
```javascript
<!-- template -->
<p>There is first dom</p>
<p>There is second dom</p>
<p>There is third dom</p>
```
&emsp;&emsp;同样， template 标签也支持使用 v-for 指令，用来渲染同级的多个兄弟元素。例如：<br/>
```javascript
<template v-for="item in items">
<p>{{item.name}}</p>
<p>{{item.desc}}<p>
</template>
```
## 2.4　事件绑定与监听
&emsp;&emsp;当模板渲染完成之后，就可以进行事件的绑定与监听了。 Vue.js提供了v-on指令用来监听DOM事件，通常在模板内直接使用，而不像传统方式在 js 中获取DOM 元素，然后绑定事件。例如：<br/>
``<button v-on:click="say">Say</button>``<br/>
### 2.4.1 方法及内联语句处理器
&emsp;&emsp;通过 v-on 可以绑定实例选项属性 methods 中的方法作为事件的处理器，v-on:后参数接受所有的原生事件名称。例如：<br/>
```javascript
<button v-on:click="say">Say</button>
var vm = new Vue({
el : '#app',
data: {
msg : 'Hello Vue.js'
},
methods : {
say : function() {
alert(this.msg);
}
}
});
```
&emsp;&emsp;单击 button，即可触发 say 函数，弹出 alert 框 'Hello Vue.js'。<br/>
&emsp;&emsp;Vue.js 也 提 供 了 v-on 的 缩 写 形 式， 我 们 可 以 将 模 板 中 的 内 容 改 写 为 ``<button @click='say'>Say</button>``，这两句语句是等价的。<br/>
&emsp;&emsp;除了直接绑定 methods 函数外， v-on 也支持内联 JavaScript语句，但仅限一个语句。例如：<br/>
```javascript
<button v-on:click="sayFrom ('from param')">Say</button>
var vm = new Vue({
el : '#app',
data: {
msg : 'Hello Vue.js'
},
methods : {
sayFrom: function(from) {
alert(this.msg + '' + from);
}
}
});
```
&emsp;&emsp;在直接绑定methods函数和内联JavaScript 语句时，都有可能需要获取原生DOM事件对象，以下两种方式都可以获取：<br/>
```javascript
<button v-on:click="showEvent">Event</button>
<button v-on:click="showEvent($event)">showEvent</button>
<button v-on:click="showEvent()">showEvent</button> // 这样写获取不到 event
var vm = new Vue({
el : '#app',
methods : {
showEvent : function(event) {
console.log(event);
}
}
});
```
&emsp;&emsp;同一元素上也可以通过v-on绑定多个相同事件函数，执行顺序为顺序执行，例如：<br/>
``<div v-on:click="sayFrom('first')" v-on:click ="sayFrom('second)">``
### 2.4.2　修饰符
&emsp;&emsp;Vue.js为指令v-on提供了多个修饰符，方便我们处理一些DOM事件的细节，并且修饰符可以串联使用。主要的修饰符如下。<br/>
&emsp;&emsp;.stop:等同于调用event.stopPropagation()。<br/>
&emsp;&emsp;.prevent:等同于调用event.preventDefault()。<br/>
&emsp;&emsp;.capture:使用capture模式添加事件监听器。<br/>
&emsp;&emsp;.self:只当事件是从监听元素本身触发时才触发回调。<br/>
&emsp;&emsp;使用方式如下：
```javascript
<a v-on:click.stop='doThis'></a>
<form v-on:submit.prevent="onSubmit"></form> // 阻止表单默认提交事件
<form v-on:submit.stop.prevent="onSubmit"></form> // 阻止默认提交事件且阻止冒泡
<form v-on:submit.stop.prevent></form> // 也可以只有修饰符，并不绑定事件
```
&emsp;&emsp;可以尝试运行以下这个例子，更好地理解修饰符在其中起到的作用。
```javascript
var vm = new Vue({
el : '#app',
methods : {
saySelf(msg) {
alert(msg);
}
}
});
<div v-on:click="saySelf('click from inner')" v-on:click.self="saySelf('click
from self')">
<button v-on:click="saySelf('button click')">button</button>
<button v-on:click.stop="saySelf('just button click')">button</button>
</div>
```
&emsp;&emsp;除了事件修饰符之外，v-on还提供了按键修饰符，方便我们监听键盘事件中的按键。例如：<br/>
```javascript
<input v-on:keyup.13="submit"/> // 监听 input 的输入，当输入回车时触发 Submit 函
数（回车的 keycode 值为 13），用于处理常见的用户输入完直接按回车键提交）
```
&emsp;&emsp;Vue.js 给一些常用的按键名提供了别称，这样就省去了一些记 keyCode 的事件。全部按键别名为： enter、 tab、 delete、 esc、space、up、down、left、right。例如：<br/>
``<input v-on:keyup.enter="submit" />``<br/>
&emsp;&emsp;Vue.js也允许我们自己定义按键别名，例如：<br/>
```javascript
Vue.directive('on').keyCodes.f1 = 112; // 即可以使用 <input v-on:keyup.f1="help" />
```
&emsp;&emsp;Vue.js2.0中可以直接在``Vue.config.keyCodes``里添加自定义按键别名，无需修改v-on指令，例如：<br/>
``Vue.config.keyCodes.f1 = 12。``
### 2.4.3　与传统事件绑定的区别
&emsp;&emsp;如果你之前没有接触过Angularjs，ReactJS 这类框架，或许会对Vue.js这种事件监听方式感到困惑。毕竟我们一开始接受的理念就是将HTML和JS隔离开编写。但其实 Vue.js事件处理方法和表达式都严格绑定在当前视图的 ViewModel上，所以并不会导致维护困难。<br/>
&emsp;&emsp;而这么写的好处在于：<br/>
&emsp;&emsp;①无需手动管理事件。ViewModal被销毁时，所有的事件处理器都会自动被删除，让我们从获取DOM 绑定事件然后在特定情况下再解绑这样的事情中解脱出来。<br/>
&emsp;&emsp;②解耦。ViewModel代码是纯粹的逻辑代码，和 DOM 无关，有利于我们写自动化测试用例<br/>
&emsp;&emsp;还有个与以往不同的细节是，我们在处理 ul、 li 这种列表，尤其是下拉刷新这种需要异步加载数据的列表时，往往会把li事件代理到ul上，这样异步加载进来的新数据就不需要再次绑定事件。而 Vue.js 这类的框架由于不需要手动添加事件，往往直接会把事件绑定在 li 上，类似这样 :``<li v-repeat="item in items" v-on:click="clickLi"></li>``，理论上每次新增 li 的时候都会进行同li个数的事件绑定，比用事件代理多耗了些性能。但在实际运用中并没有什么特别的性能瓶颈影响，而且我们也省去在代理中处理 e.target 的步骤，让事件和 DOM 元素关系更紧密、简单。
## 2.5　Vue.extend()
&emsp;&emsp;组件化开发也是Vue.js中非常重要的一个特性，我们可以将一个页面看成一个大的根组件，里面包含的元素就是不同的子组件，子组件也可以在不同的根组件里被调用。在上述例子中，可以看到在一个页面中通常会声明一个Vue的实例newVue({})作为根组件，那么如何生成可被重复使用的子组件呢？ Vue.js 提供了 Vue.extend(options)方法，创建基础Vue构造器的“子类”，参数 options对象和直接声明Vue实例参数对象基本一致，使用方法如下：<br/>
```javascript
var Child = Vue.extend({
template : '#child',
// 不同的是， el 和 data 选项需要通过函数返回值赋值，避免多个组件实例共用一个数据
data : function() {
return {
….
}
}
….
})
Vue.component('child', Child) // 全局注册子组件
<child ….></child> // 子组件在其他组件内的调用方式
```
# 第三章 指令
&emsp;&emsp;指令是 Vue.js中一个重要的特性，主要提供了一种机制将数据的变化映射为DOM行为。那什么叫数据的变化映射为DOM行为？前文中阐述过Vue.js是通过数据驱动的，所以我们不会直接去修改DOM结构，不会出现类似于``$('ul').append('<li>one</li>')`` 这样的操作。当数据变化时，指令会依据设定好的操作对DOM进行修改，这样就可以只关注数据的变化，而不用去管理DOM的变化和状态，使得逻辑更加清晰，可维护性更好。<br/>
&emsp;&emsp;Vue.js 本身就提供了大量的内置指令来进行对DOM的操作，我们也可以开发自定义指令。本章主要介绍部分常见指令的使用及场景以及自定义指令的开发和指令相关的参数。
## 3.1 内置指令
### 3.1.1 v-bind
&emsp;&emsp;v-bind 主要用于动态绑定DOM元素属性（attribute），即元素属性实际的值是由 vm实例中的 data 属性提供的。例如：
```javascript
<img v-bind:src='avatar' />
new Vue({
data : {
avatar : 'http://….'
}
})
```
&emsp;&emsp;v-bind 可以简写为：，上述例子即可简写为 ``<img :src='avatar' />。``<br/>
&emsp;&emsp;v-bind 还拥有三种修饰符，分别为.sync、.once、.camel，作用分别如下。<br/>
&emsp;&emsp;.sync ：用于组件props属性，进行双向绑定，即父组件绑定传递给子组件的值，无论在哪个组件中对其进行了修改，其他组件中的这个值也会随之更新。例如： ``<my-child:parent.sync='parent'></my-child>``。父组件实例vm.parent将通过prop选项传递给子组件 mychild，即my-child组件构造函数需要定义选项 props:['parent']，便可通过子组件自身实例vm.parent获取父组件传递的数据。两个组件都共享这一份数据，不论谁修改了这份数据，组件获取的数据都是一致的。但一般不推荐子组件直接修改父组件数据，这样会导致耦合且组件
内的数据不容易维护。<br/>
&emsp;&emsp;.once ：同.synce一样，用于组件props属性，但进行的是单次绑定。和双向绑定正好相反，单次绑定是将绑定数据传递给子组件后，子组件单独维护这份数据，和父组件的数据再无关系，父组件的数据发生变化也不会影响子组件中的数据。例如：``<my-child :parent.once='parent'></my-child>``<br/>
&emsp;&emsp;.camel ：将绑定的特性名字转回驼峰命名。只能用于普通HTML属性的绑定，通常会用于svg 标签下的属性，例如：`` <svg width='400' height='300' :view-box.camel='viewBox'></svg>``，输出结果即为``<svgwidth="400"height="300" viewBox="….."></svg>``<br/>
&emsp;&emsp;不过在 Vue.js2.0中，修饰符.syce和.once均被废弃，规定组件间仅能单向传递，如果子组件需要修改父组件，则必须使用事件机制来进行处理。
### 3.1.2 v-model
&emsp;&emsp;v-model指令在第2.2.3小节中的表单控件中已经说明过了，这里就不再赘述了。该指令主要用于 input、 select、 textarea 标签中，具有 lazy、 number、 debounce（2.0 废除）、trim（2.0 新增）这些修饰符。
### 3.1.3　v-if/v-else/v-show
&emsp;&emsp;v-if/v-else/v-show这三个指令主要用于根据条件展示对应的模板内容，这在第2.3.2 小节的渲染语法中也进行了说明。v-if和v-show的主要区别就在于， v-if 在条件为 false的情况下并不进行模板的编译，而v-show则会在模板编译好之后将元素隐藏掉。 v-if 的切换消耗要比 v-show 高，但初始条件为 false 的情况下， v-if 的初始渲染要稍快。
### 3.1.4　v-for
&emsp;&emsp;v-for 也是用于模板渲染的指令，在第2.3.3小节列表渲染中我们也已说明过，这里就不再赘述。常见用法如下：
```javascript
<ul>
<li v-for='(index, item) in items'>
<p>{{ item.name }}</p>
…..
</li>
</ul>
```
&emsp;&emsp;v-for 指令用法在Vue.js2.0中做了些细微的调整，大致包含以下几个方面：
#### 1．参数顺序变化
&emsp;&emsp;当包含参数index或key时，对象参数修改为（item,index）或（value, key），这样与 JS Array对象的新方法forEach和map，以及一些对象迭代器（例如 lodash）的参数能保持一致。
#### 2．v-bind:key
&emsp;&emsp;属性`` track-by ``被 ``v-bind ： key ``代替，`` <div v-for="item in items" tranck-by="id">`` 需要改写成`` <div v-for="item in items" v-bind:key="item.id">``。
#### 3.n in 10
&emsp;&emsp;``v-for="n in 10" ``中的 n 由原来的 0 ～ 9 迭代变成 1 ～ 10 迭代。
### 3.1.5 v-on
&emsp;&emsp;v-on 指令主要用于事件绑定，在第2.4节中我们已经说明。回顾一下用法：<br/>
&emsp;&emsp;``<button v-on:click='onClick'></button>``<br/>
&emsp;&emsp;v-on 可以简写为：<br/>
&emsp;&emsp;``<button @click='onClick'></button>``<br/>
&emsp;&emsp;修饰符包括 .stop、 .prevent、 .capture、 .self 以及指定按键 ``.{keyCode|keyAlias}``。<br/>
&emsp;&emsp;在 Vue.js 2.0中，在组件上使用v-on指令只监听自定义事件，即使用 $emit 触发的事件；如果要监听原生事件，需要使用修饰符.native，例如``<my-component v-on:click.native="onClick"></my-component>``。
### 3.1.6　v-text
&emsp;&emsp;v-text，参数类型为 String，作用是更新元素的 textContent。 {{}} 文本插值本身也会被编译成 textNode 的一个 v-text 指令。而与直接使用 {{}} 不同的是， v-text 需要绑定在某个元素上，能避免未编译前的闪现问题。例如：
&emsp;&emsp;``<span v-text="msg"></span>``
&emsp;&emsp;如果直接使用 <span>{{msg}}</span>，在生命周期 beforeCompile 期间，此刻 msg 数据尚未编译至{{msg}}中，用户能看到一瞬间的{{msg}}，然后闪现为 There is a message，而用 v-text 的话则不会有这个问题，如图 3-1 所示。<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.14.PNG)<br/>
### 3.1.7　v-HTML
&emsp;&emsp;v-HTML,参数类型为String，作用为更新元素的innerHTML，接受的字符串不会进行编译等操作，按普通HTML处理。同v-text类似，{{{}}}插值也会编译为节点的 v-HTML指令， v-HTML也需要绑定在某个元素上且能避免编译前闪现问题。例如：<br/>
``<div>{{{HTML}}}</div>``
``<div v-HTML="HTML"></div>``
### 3.1.8 v-el
&emsp;&emsp;v-el 指令为 DOM 元素注册了一个索引，使得我们可以直接访问 DOM 元素。语法上说，可以通过所属实例的\$els属性调用。例如：<br/>
&emsp;&emsp;``<div v-el:demo>there is a el demo</div>``<br/>
&emsp;&emsp;``vm.$els.demo.innerText // -> there is a el demo``<br/>
&emsp;&emsp;或者在 vm 内部通过 this 进行调用。<br/>
&emsp;&emsp;另外，由于HMTL不区分大小写，在v-el中如果使用了驼峰式命名，系统会自动转成小写。但可以使用“-” 来连接你期望大写的字母。例如：<br/>
```javascript
<div v-el:camelCase>There is a camelcase</div>
<div v-el:camel-case>There is a camelCase</div>
vm.$els.camelcase.innerText // -> There is a camelcase
vm.$els.camelCase.innerText // -> There is a camelCase
```
### 3.1.9 v-ref
&emsp;&emsp;v-ref 指令与v-el类似，只不过v-ref作用于子组件上，实例可以通过 \$refs 访问子组件。命名方式也类似，想使用驼峰式命名的话用“-”来做连接。例如：<br/>
```javascript
<message v-ref:title content="title"></message>
<message v-ref:sub-title content="subTitle"></message>
var Message = Vue.extend({
props : ['content'],
template : '<h1>{{content}}</h1>'
});
Vue.component('message', Message);
```
&emsp;&emsp;我们最终将 ``vm.$refs.title`` 和 ``vm.$refs.subTitle ``用 console.log 的方式打印到控制台中，结果为：
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.15.PNG)<br/>
&emsp;&emsp;输出了两个子组件的实例。<br/>
&emsp;&emsp;从理论上来说，我们可以通过父组件对子组件进行任意的操作，但实际上尽量还是会采用props数据绑定，用组件间通信的方式去进行逻辑上的交互，尽量让组件只操作自己内部的数据和状态，如果组件间有通信，也通过调用组件暴露出来的接口进行通信，而不是直接跨组件修改数据。
### 3.1.10　v-pre
&emsp;&emsp;v-pre 指令相对简单，就是跳过编译这个元素和子元素，显示原始的 {{}}Mustache 标签，用来减少编译时间。例如：
```javascript
<div v-pre>{{ uncompiled}}</div>
var vm = new Vue({
el : '#app',
data: {
uncompiled : 'Thers is an uncompiled element'
}
});
```
&emsp;&emsp;最后输入:
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.16.PNG)<br/>
### 3.1.11　v-cloak
&emsp;&emsp;v-cloak指令相当于在元素上添加了一个[v-cloak]的属性，直到关联的实例结束编译。官方推荐可以和css规则[v-cloak]{display:none}一起使用，可以隐藏未编译的 Mustache标签直到实例准备完毕。例如：<br/>
&emsp;&emsp;``<div v-cloak>{{ msg }}</div>``
### 3.1.12　v-once
&emsp;&emsp;v-once 指令是Vue.js2.0中新增的内置指令，用于标明元素或组件只渲染一次，即使随后发生绑定数据的变化或更新，该元素或组件及包含的子元素不会再次被编译和渲染。这样就相当于我们明确标注了这些元素不需要被更新，所以 v-once 的作用是最大程度地提升了更新行为中页面的性能，可以略过一些明确不需要变化的步骤。使用方式如下：<br/>
``<span v-once>{{msg}}</span>``
``<my-component v-once :msg='msg'></my-component>``
## 3.2 自定义指令基础
&emsp;&emsp;除了内置指令外，Vue.js也提供了方法让我们可以注册自定义指令，以便封装对 DOM元素的重的处理行为，提高代码复用率。本小节主要说明了如何创建、注册自定义指令，以及讲述指令的相关属性钩子函数，更深一步地了解指令在 Vue.js 中起到的作用。
### 3.2.1　指令的注册
&emsp;&emsp;我们可以通过``Vue.directive(id,definition)``方法注册一个全局自定义指令，接收参数id和定义对象。id是指令的唯一标识，定义对象则是指令的相关属性及钩子函数。例如：<br/>
&emsp;&emsp;``Vue.directive(‘global-directive’,definition)``;//我们暂时只注册了这个指令，并没有赋予这个指令任何功能。
&emsp;&emsp;我们可以在模板中这么使用：<br/>
&emsp;&emsp;``<div v-global-directive></div>``<br/>
&emsp;&emsp;而除了全局注册指令外，我们也可以通过在组件的directives选项注册一个局部的自定义指令。例如：<br/>
```javascript
var comp = Vue.extend({
directives : {
'localDirective' : {} // 可以采用驼峰式命名
}
});
```
&emsp;&emsp;该指令就只能在当前组件内通过``v-local-directive``的方式调用，而无法被其他组件调用。
### 3.2.2　指令的定义对象
&emsp;&emsp;我们在注册指令的同时，可以传入definition定义对象，对指令赋予一些特殊的功能。这个定义对象主要包含三个钩子函数： bind、 update 和 unbind。<br/>
&emsp;&emsp;bind: 只被调用一次，在指令第一次绑定到元素上时调用。<br/>
&emsp;&emsp;update：指令在bind之后以初始值为参数进行第一次调用，之后每次当绑定值发生变化时调用， update 接收到的参数为 newValue和oldValue
<br/>
&emsp;&emsp;unbind：指令从元素上解绑时调用，只调用一次。<br/>
&emsp;&emsp;这三个函数都是可选函数，但注册一个空指令肯定没有意义，来看下面这个例子，会使我们对整个指令周期有更明确的认识。
```javascript
<div v-if="isExist" v-my-directive="param"></div>
Vue.directive('my-directive', {
bind : function() {
console.log('bind', arguments);
},
update : function(newValue, oldValue) {
console.log('update', newValue, oldValue)
},
unbind : function() {
console.log('unbind', arguments);
}
})
var vm = new Vue({
el : '#app',
data : {
param : 'first',
isExist : true
}
});
```
&emsp;&emsp;我们在控制台里先后输入 ``vm.param ='second' ``和 ``vm.isExist = false``，整体输出如下：
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.17.PNG)<br/>
&emsp;&emsp;另外，如果我们只需要使用update函数时，可以直接传入一个函数代替定义对象：
```javascript
Vue.directive('my-directive', function(value) {
// 该函数即为 update 函数
});
```
&emsp;&emsp;上述例子中，可以使用 my-directive 指令绑定的值是 data 中的 param 属性。也可以直接绑定字符串常量，或使用字面修饰符，但这样的话需要注意 update 方法将只调用一次，因为普通字符串不能响应数据变化。例如：
```javascript
<div v-my-directive="constant string"/></div> // -> value 为 undefined，因
为 data 中没有对应的属性
<div v-my-direcitve="'constant string'"></div> // -> value 为 constant
string，绑定字符串需要加单引号
<div v-my-directive.literal="constant string"></div> // -> value 为 constant
string，利用字面修饰符后无需使用单引号
```
&emsp;&emsp;除了字符串外，指令也能接受对象字面量或任意合法的JavaScript 表达式。例如：
```javascript
<div v-my-directive="{ title : 'Vue.js', author : 'You'}" ></div>
<div v-my-directive="isExist ? 'yes' : 'no'" ></div>
```
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.18.PNG)<br/><br/>
&emsp;&emsp;注意此时对象字面量不需要用单引号括起来，这和字符串常量不一样。
### 3.2.3　指令实例属性
&emsp;&emsp;除了了解指令的生命周期外，还需要知道指令中能调用的相关属性，以便我们对相关DOM进行操作。在指令的钩子函数内，可以通过this来调用指令实例。下面就详细说明指令的实例属性。<br/>
&emsp;&emsp;el ：指令绑定的元素。<br/>
&emsp;&emsp;vm ：该指令的上下文ViewModel，可以为newVue()的实例，也可以为组件实例。<br/>
&emsp;&emsp;expression ：指令的表达式，不包括参数和过滤器。<br/>
&emsp;&emsp;arg ：指令的参数。<br/>
&emsp;&emsp;name ：指令的名字，不包括 v- 前缀。<br/>
&emsp;&emsp;modifiers ：一个对象，包含指令的修饰符。<br/>
&emsp;&emsp;descriptor ：一个对象，包含指令的解析结果。<br/>
&emsp;&emsp;我们可以通过以下这个例子，更直观地了解到这些属性：<br/>
```javascript
<div v-my-msg:console.log="content"></div>
Vue.directive('my-msg', {
bind : function() {
console.log('~~~~~~~~~~~bind~~~~~~~~~~~~~');
console.log('el', this.el);
console.log('name', this.name);
console.log('vm', this.vm);
console.log('expression', this.expression);
console.log('arg', this.arg);
console.log('modifiers', this.modifiers);
console.log('descriptor', this.descriptor);
},
update : function(newValue, oldValue) {
var keys = Object.keys(this.modifiers);
window[this.arg][keys[0]](newValue);
},
unbind : function() {
}
});
var vm = new Vue({
el : '#app',
data : {
content : 'there is the content'
}
});
```
&emsp;&emsp;输出结果如下：<br/>
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.19.PNG)<br/><br/>
### 3.2.4　元素指令
&emsp;&emsp;元素指令是Vue.js的一种特殊指令，普通指令需要绑定在某个具体的DOM元素上，但元素指令可以单独存在，从使用方式上看更像是一个组件，但本身内部的实例属性和钩子函数是和指令一致的。例如：
```javascript
<div v-my-directive></div> // -> 普通指令使用方式
<my-directive></my-directive> // -> 元素指令使用方式
```
&emsp;&emsp;元素指令的注册方式和普通指令类似，也有全局注册和局部注册两种。
```javascript
Vue.elementDirective('my-ele-directive') // 全局注册方式
var Comp = Vue.extend({ // 局部注册，仅限该组件内使用
… // 省略了其他参数
elementDirectives : {
'eleDirective' : {}
}
});
Vue.component('comp', Comp);
```
&emsp;&emsp;元素指令不能接受参数或表达式，但可以读取元素特性从而决定行为。而且当编译过程中遇到一个元素指令时，Vue.js将忽略该元素及其子元素，只有元素指令本身才可以操作该元素及其子元素。<br/>
&emsp;&emsp;Vue.js2.0中取消了这个特性，推荐使用组件来实现需要的业务。









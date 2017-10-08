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
## 2.1.2 数据
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
## 2.1.3 方法
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
## 2.1.4 生命周期
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
![image](https://github.com/15529343201/Vue.js/blob/master/%E5%9B%BE%E7%89%87/2.7.PNG)
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












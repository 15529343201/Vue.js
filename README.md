#第一章 Vue.js简介
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
&emsp;&emsp;<code><script src="http://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.min.js"></script></code><br/>
&emsp;&emsp;也可以通过NPM进行安装：<br/>
&emsp;&emsp;<code>npm install vue</code>//最新稳定版本<br/>
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







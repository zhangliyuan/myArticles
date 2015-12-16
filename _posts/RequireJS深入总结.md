title: RequireJS深入总结
date: 2015-11-28 09:56:19
tags: RequireJS
---

![](http://7xlxb6.com1.z0.glb.clouddn.com/hubidankanRequireJS_logo.png)
## RequireJS是什么
”RequireJS是一个JavaScript文件和模块加载器，适合在浏览器中使用，当然也可在其它脚本环境中使用。“。这是官方给出的定义，简洁明了的指出了RequireJS是什么——**加载器**。什么加载器，**JavaScript模块**的加载器。

*那么为什么JavaScript模块需要这么一个加载器呢？*<!--more-->

## RequireJS出现的背景
随着Web站点的发展，难免会出现这样的情况：

```html
<script src="1.js"></script>
<script src="2.js"></script>
<script src="3.js"></script>
```

这段代码依次加载多个js文件。
这样的写法有很大的缺点。首先，加载的时候，浏览器会停止网页渲染，加载文件越多，网页失去响应的时间就会越长；其次，由于js文件之间存在依赖关系，因此必须严格保证加载顺序（比如上例的1.js要在2.js的前面），依赖性最大的模块一定要放到最后加载，当依赖关系很复杂的时候，代码的编写和维护都会变得困难。

总的来说，当时的Web Site面临这下面这些问题：

* Web site越来越像 Web app
* 随着站点的变大，代码越来越复杂
* 编译JS越来越困难
* 开发者希望 JS 文件模块化
* 部署时希望将所有的代码压缩一个文件中减少http请求

以上问题的解决方案：
* 使用类似于`#include`/`import`/`require`这样的指令，实现随时随地引用
* 加载嵌套依赖
* 易于开发人员使用且优化工具有助于部署

*RequireJS就是在这样的背景下出现的，那么RequireJS是如何解决上述问题的？*
## RequireJS的特性
* 使JS文件模块化，一个JS文件即可认为是一个JS模块
* 模块可异步按需加载，减少了传统JS Script加载导致的页面阻塞问题
* 提供命名空间，减少变量命名冲突的问题
* 配置简单，易上手 

模块化的Javascript代码解决了各个功能组件的松耦合性，复用性和可维护性。

## RequireJS使用的场景
RequireJS比较适合浏览器端，这是相对于CommonJS而言。因为RequireJS遵循AMD模范，它异步加载js，避免浏览器因为加载某个js而阻塞导致白屏出现。当然，这并不是说RequireJS就不可以在服务端使用了，所有的可用不可用都是相对而言的。


## RequireJS的简单使用
### 在页面中引用
```html
<script data-main="scripts/main.js" src="scripts/require.js"></script>
```
RequireJS以一个相对于baseUrl的地址来加载所有的代码。 页面顶层`<script>`标签含有一个特殊的属性`data-main`，`require.js`使用它来启动脚本加载过程，而`baseUrl`一般设置到与该属性相一致的目录。`baseUrl`亦可通过RequireJS config手动设置。如果没有显式指定config及data-main，则默认的baseUrl为包含RequireJS的那个HTML页面的所属目录。

### RequireJS的API
require会定义三个变量： define , require , requirejs ，
其中require === requirejs，一般使用require更简短
‘define’提供命名空间来定义新的模块，并声明其所要依赖的模块。
‘require’加载依赖模块，并执行加载完后的回调函数。

### RequireJS config配置
如果你想改变RequireJS的默认配置来使用自定义的配置，可以使用require.config函数。 
config函数需要传入一个可选的参数对象，这个可选参数对象包含了许多的配置参数选项。 
下面时一些常用的配置项： 
* baseUrl: 用于加载模块的根路径。 
* paths: 用于映射不存在根路径下面的模块路径。 
* shims: 配置在脚本/模块外面并没有使用RequireJS的函数依赖并且初始化函数。假如underscore并没有使用 
RequireJS定义，但是你还想通过RequireJS来使用它，那么你就需要在配置中把它定义为一个shim。 
* deps: 加载依赖关系数组。

```javascript
require.config({
  //By default load any module IDs from scripts/app
  baseUrl: 'scripts/app',
  //except, if the module ID starts with "lib"
  paths: {
    lib: '../lib'
  },
  // load backbone as a shim
  shim: {
    'backbone': {
    //The underscore script dependency should be loaded before loading backbone.js
    deps: ['underscore'],
    // use the global 'Backbone' as the module name.
    exports: 'Backbone'
    }
  }
});
```


## RequireJS有什么坑
* 由于在开发中模块加载过多，导致http请求过多，因此RequireJS提供了一个名为 optimizer的工具以优化。 
* 由于AMD是模块依赖预加载，即被依赖的模块需要先被加载，而不是使用时再加载，其灵活性不及CMD规范的SeaJS

## RequireJS与ECMAScript 6
在最新的ECMAScript 6中，已经引入了Module概念。在其模块系统中，每个JavaScript代码文件在ES6中都是一个模块。只有模块中的对象需要被外部调用时，模块才会输出对象，其余则都是模块的私有对象。该处理方式将细节进行封装，仅导出必要的功能。但是，在浏览器对这一特性实现支持前，我们还需要等待一段时间。所以之前的模块化实现方案RequireJS（也包括SeaJS，TypeScript等），还是我们目前需要使用的工具。


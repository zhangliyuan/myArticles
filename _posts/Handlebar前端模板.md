title: Handlebar的基础语法
date: 2015-12-18 22:29:19
tags: 前端,模板
---

## 简介
*什么是Handlebar*
Handlebars.js 是对 `Mustache模板语言`的扩展，所以你可以将Mustache导入Handlebars以使用 Handlebars 强大的功能。<!--more-->

## Handlebar与其它前端模板的区别
Handlebars可以对模板进行预编译和加载，不确定其它模板是否有同样的机制。
目前发现和其它模板没有太大区别，只是语法不同，但都是**少逻辑**和**代码与视图**分离的模板语言。

## Handlebar的基础语法
看个简单的代码Demo

```javascript
var source = "<p>Hello, my name is {{name}}. I am from {{hometown}}. I have " +
             "{{kids.length}} kids:</p>" +
             "<ul>{{#kids}}<li>{{name}} is {{age}}</li>{{/kids}}</ul>";
var template = Handlebars.compile(source);
var data = { "name": "Alan", "hometown": "Somewhere, TX",
             "kids": [{"name": "Jimmy", "age": "12"}, {"name": "Sally", "age":}]};
var result = template(data);
// Would render:
// <p>Hello, my name is Alan. I am from Somewhere, TX. I have 2 kids:</p>
// <ul>
//   <li>Jimmy is 12</li>
//   <li>Sally is 4</li>
// </ul>
```

### HTML编码
在handlebars里，`{{expression}}`会返回一个经过编码的HTML，如果你不希望被编码，可以使用"\{ \{ \{"

```html
<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{{body}}}
  </div>
</div>
```
使用这样的数据上下文：

```javascript
{
  title: "All about <p> Tags",
  body: "<p>This is a post about &lt;p&gt; tags</p>"
}
```
结果是：

```html
<div class="entry">
  <h1>All About &lt;p&gt; Tags</h1>
  <div class="body">
    <p>This is a post about &lt;p&gt; tags</p>
  </div>
</div>
```
handlebars不会编码`Handlebars.SafeString`。可以自定义一个helper，手动对内容进行编码，这时返回`new Handlebars.SafeString(result)`。

```javascript
Handlebars.registerHelper('link', function(text, url) {
  text = Handlebars.Utils.escapeExpression(text);
  url  = Handlebars.Utils.escapeExpression(url);
 
  var result = '<a href="' + url + '">' + text + '</a>';
 
  return new Handlebars.SafeString(result);
});
```

这里将会对传入的参数进行编码，返回值是“安全的”，所以就算你不使用"\{ \{ \{"，handlebars也不会再次编码了。

### Handlebars中的helper
在上面提到的 HTML编码 中，我们使用了`Handlebars.registerHelper`。下面我们可以讲一讲这个`helper`了。
//TODO 

### 块表达式


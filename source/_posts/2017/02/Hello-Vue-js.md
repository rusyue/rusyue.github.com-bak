---
title: Hello Vue.js
date: 2017-02-02 00:35:50
categories:
    - 前端
tags:
    - 前端
    - 随笔
    - JavaScript
    - Vue.js
---

<!-- 为了取消预览图片的边框所以直接用HTML插入图片 -->
<img src="https://cn.vuejs.org/images/logo.png" alt="LOGO" class="img-no-bd">

Vue.js（读音 /vjuː/, 类似于 view） 是一套构建用户界面的 渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，并且非常容易学习，非常容易与其它库或已有项目整合。另一方面，Vue 完全有能力驱动采用单文件组件和 Vue 生态系统支持的库开发的复杂单页应用。

Vue.js 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。

<!-- more -->

## 起步

尝试 Vue.js 最简单的方法是使用 [JSFiddle Hello World](#)例子。你可以在浏览器新标签页中打开它，跟着我们学习一些基础示例。或者你也可以创建一个本地的 `.html` 文件，然后通过如下方式引入 Vue:

```html
<script src="https://unpkg.com/vue"></script>
```

你可以查看[安装指南](#)来了解其他安装 Vue 的选项。请注意我们**不推荐**新手直接使用 `vue-cli`，尤其是对 `Node.js` 构建工具不够了解的同学。


## 声明式渲染

`Vue.js` 的核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 `DOM` 的系统：

```html
<div id="app">
    {{ message }}
</div>
```

```js
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello Vue!'
    }
})
```

我们已经生成了我们的第一个 `Vue` 应用！看起来这跟单单渲染一个字符串模板非常类似，但是 `Vue.js` 在背后做了大量工作。现在数据和 DOM 已经被绑定在一起，所有的元素都是**响应式**的。我们如何知道？打开你的浏览器的控制台，并修改 `app.message`，你将看到上例相应地更新。

除了绑定插入的文本内容，我们还可以采用这样的方式绑定 DOM 元素属性：

```html
<div id="app-2">
    <span v-bind:title="message">
        Hover your mouse over me for a few seconds
        to see my dynamically bound title!
    </span>
</div>
```

```js
var app2 = new Vue({
    el: '#app-2',
    data: {
        message: 'You loaded this page on ' + new Date()
    }
})
```

这里我们遇到点新东西。你看到的 `v-bind` 属性被称为**指令**。指令带有前缀 `v-`，以表示它们是 Vue.js 提供的特殊属性。可能你已经猜到了，它们会在渲染过的 DOM 上应用特殊的响应式行为。这个指令的简单含义是说：将这个元素节点的 title 属性和 Vue 实例的 `message` 属性绑定到一起。

你再次打开浏览器的控制台输入 `app2.message = 'some new message'`，你就会再一次看到这个绑定了`title`属性的HTML已经进行了更新。

## 用组件构建（应用）

组件系统是 Vue.js 另一个重要概念，因为它提供了一种抽象，让我们可以用独立可复用的小组件来构建大型应用。如果我们考虑到这点，几乎任意类型的应用的界面都可以抽象为一个组件树：

![example](https://vuejs.org/images/components.png)

在 Vue 里，一个组件实质上是一个拥有预定义选项的一个 Vue 实例：

```js
// Define a new component called todo-item
Vue.component('todo-item', {
    template: '<li>This is a todo</li>'
})
```

现在你可以在另一个组件模板中写入它：

```html
<ol>
    <!-- Create an instance of the todo-item component -->
    <todo-item></todo-item>
</ol>
```

但是这样会为每个 todo 渲染同样的文本，这看起来并不是很酷。我们应该将数据从父作用域传到子组件。让我们来修改一下组件的定义，使得它能够接受一个[属性](#)字段：

```js
Vue.component('todo-item', {
    // The todo-item component now accepts a
    // "prop", which is like a custom attribute.
    // This prop is called todo.
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
})
```

现在，我们可以使用 `v-bind` 指令将 todo 传到每一个重复的组件中：

```html
<div id="app-7">
    <ol>
        <!-- Now we provide each todo-item with the todo object    -->
        <!-- it's representing, so that its content can be dynamic -->
        <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
    </ol>
</div>
```

```js
Vue.component('todo-item', {
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
    el: '#app-7',
    data: {
        groceryList: [
            { text: 'Vegetables' },
            { text: 'Cheese' },
            { text: 'Whatever else humans are supposed to eat' }
        ]
    }
})
```

这只是一个假设的例子，但是我们已经将应用分割成了两个更小的单元，子元素通过 `props` 接口实现了与父亲元素很好的解耦。我们现在可以在不影响到父应用的基础上，进一步为我们的 `todo` 组件改进更多复杂的模板和逻辑。

在一个大型应用中，为了使得开发过程可控，有必要将应用整体分割成一个个的组件。在后面的教程中我们将详述组件，不过这里有一个（假想）的例子，看看使用了组件的应用模板是什么样的：

```html
<div id="app">
    <app-nav></app-nav>
    <app-view>
        <app-sidebar></app-sidebar>
        <app-content></app-content>
    </app-view>
</div>
```

准备好探索更广阔的世界了？

---

我们刚才简单介绍了 Vue.js 核心的一些最基本的特征 - 本指南的其余部分将用更详尽的篇幅去描述其他的一些高级特性，所以一定要阅读完所有的内容哦！

---

> **原文**：http://vuejs.org/guide/index.html
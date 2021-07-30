- [模板动态参数](#模板动态参数)
- [v-for和v-if同时使用](#v-for和v-if同时使用)
- [事件](#事件)
  - [事件中的event对象](#事件中的event对象)
  - [有参数的情况下使用event](#有参数的情况下使用event)
  - [一个按钮调用两个方法](#一个按钮调用两个方法)
  - [事件修饰符](#事件修饰符)
    - [stop修饰符](#stop修饰符)
    - [self修饰符](#self修饰符)

# 模板动态参数

```js
const app = Vue.createApp({
  data () {
    return {
      message: 'hello vue',
      name: 'title',
      event: 'click'
    }
  },
  template: `
    <h2
      @[event]="handleClick"
      :[name]="message"
    >
      {{ message }}
    </h2>
  `
})
```

# v-for和v-if同时使用

由于v-for优先级高于v-if，因此需要用`<template>`标签(最终不会渲染到页面)

```js
<ul>
  <template v-for="(item, index) in listArray" :key="item+item" >
    <li v-if="item != xxx"> {{index}}--- {{item}} </li>
  </template>
</ul>
```

v-for循环对象

```js
<ul>
  <li v-for="(value, key, index) in obj" :key="key+value">
    {{ index }} : {{ key }}: {{ value }}
  </li>
</ul>
```

# 事件

## 事件中的event对象

```js
methods: {
  handleClick (event) {
    console.log(event.target) // 触发事件的DOM元素
  }
}
```

## 有参数的情况下使用event

```js
methods: {
  handleClick (num, event) {
    
  }
},
template: `
  <button @click="handleClick(2, $event)>按钮</button>
`
```

## 一个按钮调用两个方法

```js
methods: {
  handleClick1 () {
    // ...
  },
  handleClick2 () {
    // ...
  }
},
template: `
  <button @click="handleClick2(), handleClick2()>按钮</button>
`
```

总结：如果想在模板中一次触发两个事件方法，需要 用`,`逗号，把事件隔开，然后每个事件后边必须加上`( )`才能起作用。

## 事件修饰符

- stop
- prevent
- capture
- self
- once
- passive

### stop修饰符

停止冒泡

```js
<button @click.stop="handleClick()"></button>
```

### self修饰符

停止冒泡

除了使用stop修饰符，还有一种修饰符self，意思是只有点击自己的时候才会被执行。 只不过加的位置要在家外层DOM元素的事件上。

```js
template:`
        <div @click.self="handleBtnClick1">
            <div>目前已点佳丽数量{{count}}.</div>
            <button @click=" addCountClick()">增加一位佳丽</button>
       </div>
        `
```

这时候你会发现点击那里，都没办法触发hanldeBtnClick1方法了，这是因为目前最外层div下都是独立的DOM元素，就是都有成对标签出现，都不属于最外自己，都是他们的子元素。

可以编写一段专属最外层DIV的文字。

```js
template:`
        <div @click.self="handleBtnClick1">
            我是最外层的DIV文字
            <div>目前已点佳丽数量{{count}}.</div>
            <button @click=" addCountClick()">增加一位佳丽</button>
       </div>
        `
```

这样当点击我是最外层的DIV文字时，就会触犯handleBtnClick1方法了。
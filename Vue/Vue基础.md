- [模板动态参数](#模板动态参数)
- [v-for和v-if同时使用](#v-for和v-if同时使用)
- [事件](#事件)
  - [事件中的event对象](#事件中的event对象)
  - [有参数的情况下使用event](#有参数的情况下使用event)
  - [一个按钮调用两个方法](#一个按钮调用两个方法)
  - [事件修饰符](#事件修饰符)
    - [stop修饰符](#stop修饰符)
    - [self修饰符](#self修饰符)
- [Non-props属性](#non-props属性)
- [`$emit用法`](#emit用法)
  - [对传递值的校验](#对传递值的校验)
- [插槽slot](#插槽slot)
- [插槽默认值](#插槽默认值)
  - [具名插槽](#具名插槽)
  - [作用域插槽](#作用域插槽)
- [动态组件](#动态组件)
- [异步组件](#异步组件)
- [多级组件传值provide和inject](#多级组件传值provide和inject)
- [动画](#动画)
  - [使用JS编写动画效果](#使用js编写动画效果)
  - [双DOM元素动画实现](#双dom元素动画实现)
    - [mode属性](#mode属性)
    - [appear属性](#appear属性)

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

# Non-props属性

父组件传递的属性，且子组件没有用props接收（可用inheritAttrs: false进制子组件接收父组件传递的属性）

`$attrs`包含父组件传递的所有属性

# `$emit用法`

子组件调用父组件方法，且可以传值：

```js
emit: ['响应事件名'],
methods: {
  childClick() {
    this.$emit('响应事件名', '传给父组件的值')
  }
},
template: `<button @click="childClick">子组件按钮</button>`
```

父组件：

```js
methods: {
  handleClick(params) {
    // params是子组件通过$emit传递的值
  }
},
template: `<button @响应事件名="handleClick">父组件按钮</button>`

```

## 对传递值的校验

```js
emits: {
  '响应事件名': (value) => {
    return ...
  }
}
```

# 插槽slot

# 插槽默认值

```js
<div>
  <slot>
    // ... 默认值
  </slot>
</div>
```

## 具名插槽

```js
<div>
  <slot name="one"></slot>
  <slot name="two"></slot>
</div>


// 使用

<template v-slot:one>...</template>
<template #two>...</template>  // 简写方式：用 # 代替v-slot:
```

## 作用域插槽

```js
// 1.基础代码
// List组件
template: `
  <div>
    <div v-for="item in list">{{item}}</div>
  </div>
`

// 2.目前子组件里循环使用的是<div>标签，现在要求这个标签是父组件调用时确定，也就是要使用插槽了。（需要说明，这种情况在你写组件时，经常遇到，所以你要足够的重视）。
// List组件
template: `
  <div>
    <slot v-for="item in list" />
  </div>
`

// 父组件调用
template: `
  <list>
    <span></span> // 传递span标签
  </list>
`

```

- 父组件使用子组件插槽中的值

```js
// 通过 : 绑定的形式进行传递
// List组件
template: `
  <div>
    <slot v-for="item in list" :item="item />
  </div>
`

// 父组件
template: `
  <list v-slot="props">
    <span>{{props.item}}</span>
  </list>
`
// 父组件-使用ES6解构简化
template: `
  <list v-slot="{item}">
    <span>{{item}}</span>
  </list>
`
```

*注意这里的props是子组件传递过来的数据都是对象*

# 动态组件

```js
<keep-alive>
  <component :is="showItem">
</keep-alive>
```

# 异步组件

异步组件就是在调用组件时，这个组件并不立即渲染，而是要等带一些业务逻辑完成后，才会进行执行组件内的逻辑和渲染到页面上。

```js
app.component('async-component', Vue.defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({
        template: `<div>这是一个异步组件</div>`
      })
    }, 3000)
  })
}))
```

# 多级组件传值provide和inject

父组件向子组件传值

```js
// 父组件
provide: {
  name: '测试'
}

// 子组件
inject: ['name']
```


# 动画

```js
<transition
  enter-active-class=""
  leave-active-class=""
  type="animation" or "transition"
  :duration="1000" // 1秒后结束动画和过渡
  // 还可写对象-- :duration="{enter: 1000, leave: 3000}"
  :css="false" // 指定不适用css动画
></transition>
```

## 使用JS编写动画效果

- before-enter钩子函数：动画开始前执行函数
- enter钩子函数：动画进入时
- after-enter钩子函数
- before-leave :离场动画执行之前
- leave：开始执行离场动画
- leave-after: 离场动画执行结束

```js
methods: {
  handleBeforeEnter(element) {
    element.style.color = "red"
  },
  handleEnterActive(element, done) {
    const timer = setInterval(() => {
      const color = element.style.color;
      if (color == 'red') {
        element.style.color = "green"
      } else {
        element.style.color = "red"
      }
    }, 500)

    setTimeout(() => {
      clearInterval(timer);
      done() // 动画执行结束后通知执行下一个钩子函数after-enter
    }, 1500)
  },
  handleEnterEnd() {
    alert('入场动画结束')
  }
},
template: `
<transition
  :css="false"
  @before-enter="handleBeforeEnter"
  @enter="handleEnterActive"
  @after-enter="handleEnterEnd"
></transition>
`
```

## 双DOM元素动画实现

### mode属性

> mode="out-in"：先显示离场动画，在显示入场动画
> 
> mode="in-out": 先显示入场动画，在显示离场动画


```js
template: `
  <transition mode="out-in">
    <div v-if="isShow">出场</div>
    <div v-else>入场</div>
  </transition>
`
```

### appear属性

appear属性的意思是初次对某一个元素进行默认显示的时候也进行动画显示。

```js
template: `
  <transition
    appear
  ></transition>
`
```


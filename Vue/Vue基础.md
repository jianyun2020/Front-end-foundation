- [模板动态参数](#模板动态参数)

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
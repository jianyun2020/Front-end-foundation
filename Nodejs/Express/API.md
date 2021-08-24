
- [中间件](#中间件)
  - [express.json()](#expressjson)
  - [express.urlencodeed()](#expressurlencodeed)
  - [应用程序级中间件](#应用程序级中间件)
    - [不关心请求路径](#不关心请求路径)
    - [限定请求路径](#限定请求路径)
    - [限定请求方法 + 请求路径](#限定请求方法--请求路径)
    - [多个处理函数](#多个处理函数)
    - [为同一个路径定义多个中间件](#为同一个路径定义多个中间件)
    - [中间件可以在数组中声明为可重用](#中间件可以在数组中声明为可重用)
  - [路由器级中间件](#路由器级中间件)
# 中间件

## express.json()

配置解析json请求体

```js
app.use(express.json())
```

## express.urlencodeed()

配置解析表单请求体

```js
app.use(express.urlencoded())
```

## 应用程序级中间件

### 不关心请求路径

```js
app.use(function (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
```

### 限定请求路径

```js
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type: ', req.method)
  next()
})
```

### 限定请求方法 + 请求路径

```js
app.get('/user/:id', function (req, res, next) {
  res.send('user')
})
```

### 多个处理函数

```js
app.use('/user/:id', function(req, res, next) {
  console.log('Request URL: ', req.originalurl)
  next()
}, function(req, res, next) {
  console.log('Request Method: ', req.method)
  next()
})
```

### 为同一个路径定义多个中间件

```js
app.get('/user/:id', function(req, res, next) {
  console.log('ID: ', req.params.id)
  next()
}, function(req, res, next) {
  res.send('user info')
})

// 可以写，但不会执行，因为上一步已经结束响应了，并且没有调用next()
app.get('/user/:id', function(req, res, next) {
  res.end(req.params.id)
})
````

### `next('route')`

要从中间件堆栈中跳过其余中间件功能，通过调用`next('route')`将控制权传递给下一条路由。

*注意： 仅在使用app.METHOD()或router.METHOD()函数加载的中间件函数有效*

```js
app.get('/user/:id', function(req, res, next) {
  if (req.params.id === 0) {
    next('route')
  } else {
    next()
  }
}, function(req, res, next) {
  res.send('regular')
})

app.get('/user/:id', function(req, res, next) {
  res.send('special')
})

```

### 中间件可以在数组中声明为可重用

```js
function logOriginalUrl(req, res, next) {
  console.log('Request URL: ', req.originalurl)
  next()
}

function logMethod(req, res, next) {
  console.log('Request Method: ', req.method)
  next()
}

let logStuff = [logOriginalUrl, logMethod]

app.get('/user/:id', logStuff, function(req, res, next) {
  res.send('User Info')
})
```

## 路由器级中间件

```js
const express = require('express')

const router = express.Router()
```
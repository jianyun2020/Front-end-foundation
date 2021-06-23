# Axios是什么？

[Axios官方文档](https://axios-http.com/zh/docs/intro)

Axios是一个基于Promise的网络请求库，作用于node.js和浏览器中。它是isomorphic的（即同一套代码可以运行在浏览器和node.js中）。在服务端它使用原生node.js的http模块，而在客户端（浏览端），则使用XMLHttpRequests。

# 特性

- 从浏览器创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF(跨站请求伪造)

# 安装

使用npm:

```js
npm install axios
```

使用bower（用于web的包管理）:

```js
bower install axios
```

使用yarn:

```js
yarn add axios
```

# 基本用例

注意：CommonJS用法

使用require()导入时获得TypeScript类型推断（只能感知/自动完成）：

```js
const axios = requrie('axios').default;

// axios.<method> 能够提供自动完成和参数类型推断功能
```

发送一个GET请求:

```js
const axios = require('axios');

// 向给定ID的用户发起请求
axios.get('/user?ID=12345')
  .then(function (reponse) {
    // 处理成功情况
    console.log(response);
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .then(function () {
    // 总是会执行
  });
```

上述请求也可以按一下方式完成:

```js
axios.get('/user', {
  params: {
    ID: 12345
  }
})
.then(response => {
  console.log(response);
})
.catch(error => {
  console.log(error);
})
.then(() => {
  // 总是会执行
});
```

支持async/await用法

```js
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

*注意: 由于async/await 是ECMAScript 2017中的一部分，而且在IE和一些旧的浏览器中不支持，所以使用时务必要小心。*

# POST请求

```js
axios.post('/user', {
  firstName: 'Ai',
  lastName: 'Haibara'
})
.then(function (response) {
  console.log(response);
})
.catch(function (error) {
  console.log(error)
})
```

发起多个并发请求:

```js
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

Promise.all([getUserAccount(), getUserPermissions()])
.then(function (results) {
  const acct = result[0];
  const perm = result[1];
});
```

# Axios API

可以向axios传递相关配置来创建请求

- axios(config)

```js
// 发起一个post请求
axios({
  method: 'post',
  url: '/user/123',
  data: {
    firstName: 'Ai',
    lastName: 'Haibara'
  }
})
```

```js
// 在node.js用GET请求获取远程图片
axios({
  method: 'get',
  url: 'http://bit.ly/2mTM3nY',
  responseType: 'stream'
})
.then(function (response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
})
```

- axios(url[, config])

```js
// 发起一个GET请求（默认请求方式）
axios('/user/12345');
```

## 请求方式别名

*注意：在使用别名方法时， url、method、data 这些属性都不必在配置中指定。*

- axios.request(config)
- axios.get(url[, config])
- axios.delete(url[, config])
- axios.head(url[, config])
- axios.options(url[, config])
- axios.post(url[, data[, config]])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[, config]])

# Axios实例

## 创建实例

通过自定义配置新建一个实例：

axios.create([config])

```js
const instance = axios.create({
  baseURL: 'https://example.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

## 实例方法

指定的配置将与实例的配置合并

- axios#request(config)
- axios#get(url[, config])
- axios#delete(url[, config])
- axios#head(url[, config])
- axios#options(url[, config])
- axios#post(url[, data[, config]])
- axios#put(url[, data[, config]])
- axios#patch(url[, data[, config]])
- axios#getUri([config])

# 请求配置

只有url是必须的，如果没有指定method，请求将默认使用GET方法

```js
{
  url: '/user', // 用于请求的服务器的URL
  method: 'get', // 创建请求时使用的方法，默认get
  baseURL: 'https://example.com/api/', // 会自动加在url前面，除非url是绝对URL

  // transformRequest可以在向服务器发送前修改请求数据
  // 只能用于PUT, POST, PATCH
  // 数组中最后一个函数必须返回一个字符串，一个Buffer实例，ArrayBuffer, FormData 或 Stream
  // 可以修改请求头
  transformRequest: [function (data, headers) {
    // 对发送的data进行任意转换处理
    return data;
  }],
  
  // transformResponse在传递给then/catch前，允许修改响应数据
  transformResponse: [function (data) {
    // 对接收的data进行任意转换处理
    return data;
  }],

  // 自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},
  
  // params是与请求一起发送的URL参数
  // 必须是一个简单的对象或URLSearchParams对象
  params: {
    ID: 12345
  },

  // 主要用于序列化params，可选
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, { arrayFormat: 'brackets' })
  }
}
```
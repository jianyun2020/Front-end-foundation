# 获取浏览器地址栏查询参数

let params =  new URLSearchParams(location.search);
// 主标题
let mainHeading = params.get('mainHeading');
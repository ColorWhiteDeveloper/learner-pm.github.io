js 类型和强类型语言区分 number 的 bigint 深入
深拷贝包含 js 内置对象 变量命名
普通函数相关知识，函数一等公民，es6 函数增加 箭头函数的 this
原型链和继承，方法来源，js 内置对象来源
this 指向，js 没有编译，只有运行时
异步，浏览器内置线程，线程和进程，一个页面相关，出发异步方式。时间片
模块，面向未来的前端开发
前端工程化开发，单 html 页面 解耦 探索打包写写插件

页面渲染机制 -> 优化策略 -> vue react 框架优化
前端储存机制，tkoen cookie 身份令牌
网络请求 tcp 模型 -> 现代浏览器对于网络请求的流程 ipv6 https http2.0 http1.0
跨域 和 代理
数据安全，脚本安全
性能优化和合并到渲染，+网络请求优化

基础数据结构，和前端相关重点学习
各种算法 + 实例 leetcode
设计模式使用 + 实习遇到使用 + 自己框架使用

项目 blog loginReact 毕业设计 0-1 简历在线 vue
响应式模板框架 minVue？
封装 ajax 发送请求 -> 发布到 npm GitHub
模拟 promise

使用行业新技术 vite 体验

各种想法 写法 体验

vaios router ajax 作为第一项目开源
blog 作为基础知识储备
毕业项目

实习经历

定义`MyPromise`类

```js
class MyPromise {
  constructor(fun) {
    if (typeof fun !== "function") throw new Error("it need a function");
    fun(this.resolve, this.reject);
  }
  state = PENDING;
  value = undefined;
  errResion = undefined;
  callBackReject = undefined;
  callBackResolve = undefined;
  cache = undefined;
  resolve = (value) => {
    this.state = FULFILED;
    this.value = value;
    this.cache = this.callBackResolve && this.callBackResolve(value);
  };
  reject = (errResion) => {
    this.state = REJECTED;
    this.errResion = errResion;
  };
  then(callResolve, callReject) {
    if (this.state === FULFILED) {
      callResolve(this.value);
    }
    if (this.state === REJECTED) {
      callReject(this.errResion);
    }
    if (this.state === PENDING) {
      this.callBackResolve = callResolve;
      this.callBackReject = callReject;
    }
    // const _promise = new MyPromise((resolve, reject) => {
    //     return
    // });
    return new MyPromise((resolve, reject) => {
      if ((this.state = FULFILED)) {
        const x = callResolve(this.value);
        if (x instanceof MyPromise) {
          x.then(resolve);
        } else {
          resolve(x);
        }
      }
    });
  }
  test() {
    console.log(this.fun);
    console.log("11");
  }
}
```
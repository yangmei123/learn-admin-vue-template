# 学习vue-admin-template笔记

> 结合使用element-ui制作后台基础模版；使用vuex来进行一些状态管理；

> element-ui文档地址

    http://element-cn.eleme.io/#/zh-CN/component/menu
    
> vue-admin-template 文档地址

    https://panjiachen.github.io/vue-element-admin-site/zh/guide/#%E5%8A%9F%E8%83%BD
    
项目启动，调用main.js的入口文件，文件内通过permission.js的方法；
> 在路由进入前，进行登录权限验证；进行重定向等操作；

1. 如果没有token跳转到登录页；
2. 如果有token通过vuex的分发dispatch去触发GetInfo的action方法获取用户信息，如果报错则token有问题，要退出重新登录，如果获取的信息都正常，通过vuex的commit调用mutations修改state的值。
3. 进入页面后，侧边栏的收起关闭状态也使用了state进行管理。
4. 修改loginOut方法，不去请求；
5. 修改页面的请求接口为本地的node接口；对应的github项目地址： https://github.com/yangmei123/node-server-express

页面的http请求使用axios作为项目内所有http请求的预处理，拦截器；

> https://www.kancloud.cn/yunye/axios/234845

> Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。

> 这是一个 极简的 vue admin 管理后台 它只包含了 Element UI & axios & iconfont & permission control & lint，这些搭建后台必要的东西。

[线上地址](http://panjiachen.github.io/vue-admin-template)

[国内访问](https://panjiachen.gitee.io/vue-admin-template)

## Build Setup

```bash
# Clone project
git clone https://github.com/PanJiaChen/vue-admin-template.git

# Install dependencies
npm install

# 建议不要用cnpm  安装有各种诡异的bug 可以通过如下操作解决npm速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# Serve with hot reload at localhost:9528
npm run dev

# Build for production with minification
npm run build

# Build for production and view the bundle analyzer report
npm run build --report
```

## Browsers support

Modern browsers and Internet Explorer 10+.

| [<img src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/edge/edge_48x48.png" alt="IE / Edge" width="24px" height="24px" />](http://godban.github.io/browsers-support-badges/)</br>IE / Edge | [<img src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/firefox/firefox_48x48.png" alt="Firefox" width="24px" height="24px" />](http://godban.github.io/browsers-support-badges/)</br>Firefox | [<img src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/chrome/chrome_48x48.png" alt="Chrome" width="24px" height="24px" />](http://godban.github.io/browsers-support-badges/)</br>Chrome | [<img src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/safari/safari_48x48.png" alt="Safari" width="24px" height="24px" />](http://godban.github.io/browsers-support-badges/)</br>Safari |
| --------- | --------- | --------- | --------- |
| IE10, IE11, Edge| last 2 versions| last 2 versions| last 2 versions


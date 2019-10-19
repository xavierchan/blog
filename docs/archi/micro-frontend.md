---
title: micro-frontend
toc: true
date: 2019-08-20 16:16:19
tags:
- 前端
categories:
---
## 1. 微前端是什么
微前端主要借鉴后端微服务的概念。简单地说，就是将一个巨无霸（Monolith）的前端工程拆分成一个一个的小工程。它们完全具备独立的开发、运行能力。整个系统就将由这些小工程协同合作，实现所有页面的展示与交互。

可以跟微服务这么对比着去理解：

微服务|微前端
---|---:|
一个微服务就是由一组接口构成，接口地址一般是 URL。当微服务收到一个接口的请求时，会进行路由找到相应的逻辑，输出响应内容。	| 一个微前端则是由一组页面构成，页面地址也是 URL。当微前端收到一个页面 URL 的请求时，会进行路由找到相应的组件，渲染页面内容。
后端微服务会有一个网关，作为单一入口接收所有的客户端接口请求，根据接口 URL 与服务的匹配关系，路由到对应的服务。 | 微前端则会有一个加载器，作为单一入口接收所有页面 URL 的访问，根据页面 URL 与微前端的匹配关系，选择加载对应的微前端，由该微前端进行进行路由响应 URL。

---

### 1.1 微前端架构
微前端架构一般可以由以下几种方式进行：
- 使用 HTTP 服务器的路由来重定向多个应用
- 在不同的框架之上设计通讯、加载机制，诸如 Mooa 和 Single-SPA
- 通过组合多个独立应用、组件来构建一个单体应用
- iFrame。使用 iFrame 及自定义消息传递机制
- 使用纯 Web Components 构建应用
- 结合 Web Components 构建




---
## 2. 为什么要用微前端
主要从下面几个角度
- 打包速度
- 页面加载速度
- 多人多地协作
- sass产品定制化
- 产品拆分

---
### 2.1 打包速度
工程越来越大，打包越来越慢。想想edx跑完整个打包流程，需要多少时间？编译一次edx静态资源就需要20-30分钟。


> 在 6 个月前，我们的 B 端工程那会儿还是一个 Monolith。当时已经有 20 多个依赖、60 多个公共组件、200 多个页面，对接 700 多个接口。我们使用了 Webpack 2，并启用 DLL Plugin、HappyPack 4。在我的个人主机上使用 4 线程编译，大概要 5 分钟。而如果不拆分，算下来现在我们已经有近 400 个页面，对接1000 多个接口。这个时间意味着什么？它不仅会耽误我们开发人员的时间，还会影响整个团队的效率。上线时，在 Docker、CI 等环境下，耗时还会被延长。如果部署后出几个 Bug，要线上立即修复，那就不知道要熬到几点了。在使用微前端改造后，目前我们已经有 26 个微前端工程，平均打包时间在 30-45 秒之间。


---
### 2.2 多人多地协作
使用微前端后，代码冲突提交被阻塞的风险，就平摊到各个工程上去了。
> 在协作上，我们在全国有三个地方的前端团队，这么多人在同一个工程里开发，遭遇代码冲突的概率会很频繁，而且冲突的影响面比较大。如果代码中出现问题，导致 CI 失败，所有其他人的代码提交与更新也都会被阻塞。


---
### 2.3 Sass产品 - 定制化与本地化
内心想做 SaaS 产品，但客户总是要做定制化。

*定制化* 往往意味着，在代码里揉进“定制的业务逻辑”。
*本地化* 就会有代码安全方面的考量，怎样不把全部源代码给客户，就能实现定制？

通过微前端技术，我们可以很容易达到本地化代码安全的下限——只给客户他所购买的模块的前端源码。定制化里最简单的独立新模块也变得简单：交付团队增加一个新的微前端工程即可，不需要揉进现有研发工程中。


---
## 3. 怎样整合微前端app
在微前端的方案里，有几个我们必须要解决的问题：
- 一个前端需要对应多个后端
- 提供一套应用注册机制，完成应用的无缝整合

  - 怎样将不同业务子系统集中到一个大平台上，统一对外开放？
  - 如何给不同用户赋予权限让其能够访问平台的特定业务模块同时禁止其访问无权限的业务模块？
  - 如何快速接入新的子系统，并对子系统进行版本管理，保证功能同步？

- 构建时集成应用和应用独立发布部署



---
### 3.1 入口项目
最终线上运行的是一个单页应用，而项目开发中要求应用独立。因此我们新建了一个入口项目，用于整合各个应用。入口项目(Portal)，除了提供“子项目”注册、合并功能外，还提供一些公共支持，如

---
### 3.1.1 *用户登录机制*
将用户的统一登录和认证问题交给了SSO，所有的项目的后端Server都要接入SSO校验登录状态，从而保障业务系统间用户安全认证的一致性。

---
### 3.1.2 *引用公共库*
每一个业务工程都是一个独立的前端工程，所以里面会有一些相同的依赖，如 Vue、moment、lodash 等。如果将这些内容都打包到各自的 vendor.js 里，则势必会导致代码冗余太多，浏览器运行内存压力增大。我们把这些公共依赖、公共组件、CSS、Fonts 等都放到一个工程里，由该工程进行打包，将依赖、组件 export，并以 UMD 的方式注入到全局。

---
- 菜单权限获取
- 全局异常处理
- 全局数据打点






---
### 3.2 路由分发应用
在单页面应用中，我们会依据路由分发组件。而在微前端项目中，我们需要把路由分发到不同的应用中。


---
#### 3.2.1 *Http反向代理*
这通常可以通过HTTP 服务器的反向代理来实现。但是这种方式看上去更像是多个前端应用的聚合，我们只是将这些不同的应用拼凑到一起，使他们看起来像是一个完整的整体。但是，每次用户从 A 应用到 B 应用的时候，都需要刷新一下页面。

---
#### 3.2.2 *客户端javascript异步加载*
这种方式就是在客户端浏览器通过 Ajax 加载应用程序，然后将不同模块的内容插入到对应的 div 中，而且还必须手动克隆每个 script 的标记才能使其工作。
“子项目”对外输出不需要入口HTML页面，只需要输出的资源文件即可，资源文件包括js、css、fonts和imgs等。
```js
function loadPage (element) {
  [].forEach.call(element.querySelectorAll('script'), function (nonExecutableScript) {
    var script = document.createElement("script");
    script.setAttribute("src", nonExecutableScript.src);
    script.setAttribute("type", "text/javascript");
    element.appendChild(script);
  });
}

document.querySelectorAll('.load-app').forEach(loadPage);
```

---
#### 3.2.3 *Web Components*
react，vue的可重用的组件。每个组件都是独立开发的，主应用程序项目利用它们组装成最终的应用程序。
```js
class Header extends HTMLElement {
  attachedCallback() {
    ReactDOM.render(, this.createShadowRoot());
  }
}

document.registerElement('microfrontends-header', Header);
```

---
## 4. 一些框架
#### 4.1 single-spa
single-spa is a framework for bringing together multiple javascript microfrontends in a frontend application. 

【搭建一个single-spa来加载react+vue两个app】 https://dev.to/dabit3/building-micro-frontends-with-react-vue-and-single-spa-52op
【官方文档】https://single-spa.js.org/docs/getting-started-overview.html
【官方Demo】 https://single-spa.surge.sh/
【Demo仓库】 https://github.com/CanopyTax/single-spa-examples

```shell
git clone git@github.com:CanopyTax/single-spa-examples.git
cd single-spa-examples

# Install yarn at https://yarnpkg.com/lang/en/docs/install/
yarn
yarn build
yarn start
open http://localhost:8080

```

## 参考资料

> - [微前端实践](https://juejin.im/post/5cadd7835188251b2f3a4bb0)
> - [前端微服务整合之‘‘插拔式架构’‘实现方案](https://blog.csdn.net/lizhipeng123321/article/details/81868136)
> - [用微前端的方式搭建类单页应用](https://www.cnblogs.com/meituantech/p/9604591.html)
> - [实施微前端的六种方式](https://juejin.im/post/5b45d0ea6fb9a04fa42f9f1a)
> - [「微前端」- 将微服务理念扩展到前端开发（实践篇）](https://www.jianshu.com/p/1f409df7de45)

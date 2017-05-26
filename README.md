# VUE 从快速入门到项目实践
> 阅读例子之前，您需具备以下基础知识：
> * HTML
> * CSS
> * JavaScript

## 安装配置环境
#### Node.js安装
文档中所有例子均使用vue-cli脚手架搭建作为演示，所需依赖Node。所以第一步我们先安装Node。
到Node官网（`http://nodejs.org/`)进行下载，根据不同操作系统不同类型下载。
* 下载Node完根据指示进行安装
* 当 安装完成后，我们打开CMD命令行，输入node -v查看node.js是否成功安装及版本号。输入npm -v查看npm是否自带成功安装及版本号。
#### 使用NPM安装Vue-Cli脚手架
因为npm在国内下载速度有时非常慢，所以接下来我们安装一下淘宝镜像（https://npm.taobao.org/）
在终端上输入
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
安装好淘宝镜像之后我们开始安装基于cli的vue.js脚架
（使用webpack前端模块化管理工具能够让我们快速构建和管理vue项目，官网http://webpack.github.io/）
接下来我们准备在D盘使用全局安装创建vue项目脚架
* 在终端打开D盘（D:）
* 输入cnpm install --global vue-cli 全局安装vue-cli
* 等待vue-cli下载完成后，我们创建一个基于webpack的新项目（名称为vue-app） 在终端输入vue init webpack vue-app
* 同时输入我们的项目名称，描述，邮箱，是否添加路由（我们这里用到路由所以默认添加），是否测试等等。
* 安装创建好新项目后，我们在终端进入我们的项目目录 cd vue-app进入到项目目录
* 进入目录后我们安装项目所依赖的环境，cnpm install
* 安装完依赖以后，我们在终端就可以运行我们的vue项目了，在终端输入npm run dev即可运行服务器
* 在浏览器打开http://localhost:8080 可以看到我们运行的项目。

 ---

## Vue.js目录结构
我们使用编辑器打开vue-app，可以看到我们的项目结构。
> * build           （最终发布的代码存放位置）
> * config          （配置目录，包括端口号等。我们初学可以使用默认的。）
> * node_modules    （npm 加载的项目依赖模块）
> * src             （这里是我们要开发的目录，基本上要做的事情都在这个目录里。）
> * static          （静态资源目录，如图片、字体等。）
> * .xxxx文件       （这些是一些配置文件，包括语法配置，git配置等。）
> * index.html      （首页入口文件，你可以添加一些 meta 信息或同统计代码等。）
> * package.json    （项目配置文件。）
> * README.md       （项目的说明文档，markdown 格式）

#### 修改vue文件
接下来我们修改一些vue-cli自带的不必要代码，让我们整个项目的思路变得更加清晰！
* 首先我们打开入口页index.html,可以看到我们index.html,只单单挂着一个`<div id="app"><div>`。
```javascript
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>vue-app</title>
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```
* 接着我们打开app.vue，将其改为以下代码,可以见到`<router-view></router-view>`，这便是我们vue路由的出口，它会将匹配到的组件将渲染在这里。
```javascript
<template>
  <div>
    <router-view></router-view>
  </div>
</template>
<script>
export default {
  name: 'app'
}
</script>
<style>
</style>
```
* 再次我们打开router下面的index.js也就是我们的路由文件了。可以看到路由默认加载Hello组件。（详细内容我们会在路由章节讲解）
```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    }
  ]
})
```
* 最后我们打开Hello.vue,并将其改为以下代码。`<template></template>`里面的内容就是我们的组件内容，也是真正渲染到页面的内容（详细内容我们会在组件章节讲解）。
```javascript
<template>
  <div>
    <h2>Hello Vue</h2>
  </div>
</template>
<script>
export default {
  data () {
    return {
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
* 现在我们打开浏览器去看看效果，你会发现页面只单单剩下`Hello Vue`了。

修改完vue-cli自带的不必要代码后，相信您已经有一个大概的思路了吧？如果您还是感到困惑也不要紧，相信学习完接下来的章节，您会对整个项目的逻辑变得更加清晰。

---

## VUE组件结构
这里只讲述vue的基本结构，详细内容会在组件章节中作详解。
组件（Component）是 Vue.js 最强大的功能之一。
组件可以扩展 HTML 元素，封装可重用的代码。
组件系统让我们可以用独立可复用的小组件来构建大型应用，几乎任意类型的应用的界面都可以抽象为一个组件树
#### 代码：
```javascript
<template></template>
<script type="text/ecmascript-6">
</script>
<style scoped>
</style>
```
#### 讲解：
* `<template></template>`是我们组件的内容，也是HTML放置区域。
* `<script type="text/ecmascript-6"></script>`相信大家都不陌生，就是js区域。type="text/ecmascript-6"声明支持ES6语法。
* `<style scoped></style>`是我们组件的样式区域。
* vue中最大的设计特点就是HTML/CSS/JS都放置在同一个组件里面，这更加方便我们后期的维护。
---

## VUE的基本语法
在上节我们讲到，vue默认挂载Hello组件。所以我们可以在Hello做相应的例子学习！


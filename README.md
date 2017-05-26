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
> * build
> * config
> * node_modules
> * src
> * static
> * .xxxx文件
> * index.html
> * package.json
> * README.md

# VUE 从快速入门到项目实战
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
* `<template></template>`是我们组件的内容，也是HTML放置区域（注意`<template></template>`中只允许一个根节点，否则会报错）。
* `<script type="text/ecmascript-6"></script>`相信大家都不陌生，就是js区域。type="text/ecmascript-6"声明支持ES6语法。
* `<style scoped></style>`是我们组件的样式区域。
* vue中最大的设计特点就是HTML/CSS/JS都放置在同一个组件里面，这更加方便我们后期的维护。
---

## VUE的基本语法
在上节我们讲到，vue默认挂载Hello组件。所以我们可以在Hello.vue中做相应的例子学习！
### 插值
> 文本
#### 代码：
```javascript
<template>
  <div>
    <h2>{{message}}</h2>
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: 'Hello Vue'
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* `<h2>{{message}}</h2>` 数据绑定最常见的形式就是使用 {{...}}（双大括号）。我们在h2中绑定了message变量参数
* export default是ES6的语法，均可用于导出常量、函数、文件、模块等。因为我们Hello组件需要动态匹配到路由中，在app`<router-view></router-view>`中显示。所以需要export default进行导出。
* data 作为一个函数通过return返回数据，我们可以在data中定义数据。这里我们定义了message值，再通过{{message}}绑定在组件中。

> HTML
#### 代码：
```javascript
<template>
  <div>
    <div v-html="message"></div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: '<h1>VUE 从入门到项目实战</h1>'
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* v-html 指令用于输出 html 代码，`v-html="message"`绑定的是html节点`<h1>VUE 从入门到项目实战</h1>`。

> 绑定属性（数据的双向绑定）
#### 代码：
```javascript
<template>
  <div>
    <p v-bind:class="{'Textcolor': on}">VUE 从入门到项目实战</p>
    <label>点击</label><input type="checkbox" v-model="on" value="点击">
  </div>
</template>
<script>
export default {
  data () {
    return {
      on: false
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Textcolor{color: red;}
</style>
```
#### 讲解：
* data函数中我们定义了on变量参数
* p标签中添加了`v-bind:class="{'Textcolor': on}"` 我们可以通过v-bind：class绑定Textcolor样式类。也可以写成 `:class="{'Textcolor': on}"`
* 双大括号{class，show}，第一个参数是我们的样式类，第二个参数为Boolean类型，当show等于true时添加class类。
* input双向数据绑定。v-model="on" 绑定了on参数，当input选中时，on的值为true，则添加Textcolor类。同时取消选中时，on的值为false，又会取消Textcolor类。

> 表达式

#### 代码：
```javascript
<template>
  <div>
    {{5+5}}<br>
    {{ ok ? 'YES' : 'NO' }}<br>
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id">VUE 从快速入门到项目实战</div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      ok: true,
      message: 'VUE',
      id : 1
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
vue支持javascript表达式
* {{5+5}}  //10
* {{ ok ? 'YES' : 'NO' }}  //三元表达式
* {{ message.split('').reverse().join('') }} //使用函数
* v-bind:id="'list-' + id"  //绑定id

### 条件 (v-show与v-if)
#### 代码：
```javascript
<template>
  <div>
    <p v-if="seen">VUE 从快速入门到项目实战</p>
  </div>
</template>
<script>
export default {
  data () {
    return {
      seen: true
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* v-if="seen" seen参数可以是Boolean类型，也可以为表达式。当参数为true时则显示，反则隐藏。
在2.1.0中还可以使用
```javascript
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

#### 代码：
```javascript
<template>
  <div>
    <p v-show="seen">VUE 从快速入门到项目实战</p>
  </div>
</template>
<script>
export default {
  data () {
    return {
      seen: false
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* `v-show`与`v-if`类似

#### `v-show`与`v-if`的区别
* v-if 是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
* v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
* 相比之下， v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
* 一般来说， v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则使用 v-if 较好。

### 循环（v-for）
#### 代码：
```javascript
<template>
  <div>
    <ol>
      <li v-for="todo in todos">
        {{ todo.text }}
      </li>
    </ol>
  </div>
</template>
<script>
export default {
  data () {
    return {
      todos: [
        { text: '学习 JavaScript' },
        { text: '学习 Vue' },
        { text: '整个牛项目' }
      ]
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* data中我们定义了todos数组对象
* 通过`v-for="todo in todos"`遍历数组对象
* 使用双大括号绑定遍历后的对象属性值`{{ todo.text }}`
* 这样就能成功的将数据循环渲染组件中了

### 数据的双向绑定

#### 代码：
```javascript
<template>
  <div>
    <p>{{message}}</p>
    <input v-model="message">
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: 'VUE 实战例子'
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解
* data中我们初始化message
* 将初始化值绑定到p标签中`{{message}}`
* 再通过`v-model`绑定到input输入框中，这样就能实时监听和改变message的值。

### 过滤器

#### 代码：
```javascript
<template>
  <div>
    {{ message | capitalize }}
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: 'vue'
    }
  },
  filters: {
    capitalize: (value) => {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```

#### 讲解：
* filters是VUE中的过滤器，我们可以在里面定义过滤函数。
* 我们在filters中定义capitalize过滤函数。同时在组件中通过管道"|"添加过滤函数`{{ message | capitalize }}`
* (value) => {}为ES6中的箭头函数，相当于function(value){}。

### 事件处理
#### 代码：
```javascript
<template>
  <div>
      <p>{{ message }}</p>
      <button v-on:click="reverseMessage">逆转消息</button>
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: 'VUE项目实战'
    }
  },
   methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* methods是VUE的事件，我们可以在methods里面定义事件处理函数。
* 在methods中我们定义了reverseMessage逆转函数，来实现点击逆转字符串消息。
* 通过v-on:click="reverseMessage"绑定点击事件。

> 事件修饰符

Vue.js 为 v-on 提供了事件修饰符来处理 DOM 事件细节，如：event.preventDefault() 或 event.stopPropagation()。
Vue.js通过由点(.)表示的指令后缀来调用修饰符。
```javascrpt
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- click 事件至少触发一次，2.1.4版本新增 -->
<a v-on:click.once="doThis"></a>
```
除此之外还有按键修饰符，详情请访问vue官网。

### 缩写
#### v-bind 缩写
```javascript
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```
#### v-on 缩写
```javascript
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

### 计算

#### 代码：
```javascript
<template>
  <div>
      <p>原始字符串: {{ message }}</p>
      <p>计算后反转字符串: {{ reversedMessage }}</p>
  </div>
</template>
<script>
export default {
  data () {
    return {
      message: 'VUE项目实战'
    }
  },
   computed: {
      // 计算属性的 getter
      reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```
#### 讲解：
* computed是VUE中的计算，我们可以在computed中定义计算公式。
* 有同学会说computed看起来好像没什么特殊的地方，computed能实现的methods方法也能实现啊。
* 两者的区别：computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。 


VUE的基本语法我们就暂时讲那么多，需要了解更多基本语法的同学请访问VUE官网`https://cn.vuejs.org`作进一步的学习。

---

## VUE组件（核心内容）

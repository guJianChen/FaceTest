## 1. $.ajax 的原理

    通过浏览器的内置对象XMLHttpRequest 向服务器发送异步请求，然后JavaScript操作dom实现页面的更新

- json 和 xml 的区别
  json 是由键值对的形式组成，键值对之间使用逗号隔开，键名必须加上双引号可以是数组或者对象
  xml 格式较为严格，后台需要设置 content-type:text/xml
  ajax 的缺点：

      1. Ajax有一个问题一直困扰着开发者，就是网页状态无法被添加到历史记录中，这意味着用户不能通过浏览器的“前进”和“后退”按钮前进或者退回到某个状态

## 2.常见的状态码

- 200 成功
- 202 服务器已经接收请求，但是尚未处理
- 400 请求格式错误
- 404 请求失败 （请求的资源没有访问到）
- 500 服务端错误

## 3.跨域请求

    跨域请求就是：在两个不同源的网站之间进行数据请求

- 3.1 如何解决跨域问题
  - 使用$.ajax 的 jsonp 进行跨域
  - 后端设置响应头，使用 cors 进行跨域请求
- 3.2 jsonp 跨域原理
  - 1 利用了 script 标签不受同源策略的限制，可以进行外部文件的访问，并把返回的文件当做 js 文件来执行
  - 2 前端声明一个全局函数，动态生成 script 标签，把函数名拼接在访问的外部文件地址和后面
  - 3 后端返回一个函数调用，把返回给前端的数据作为参数返回给前端

## $ajax 和 axios 的区别

`$ajax的优缺点：`

1.本身是针对于 mvc 编程，不符合 mvvm 前端的开发

2.基于原生 XHR 进行开发的话，XHR 本身的结构不清晰

3.JQuery 整个项目太大，单纯使用 ajax 却要引入 jquery 非常不合理

`axios的优缺点：`

1.从浏览器中创建出 XMLHTTPRequest 2.从 node.js 中发出 http 请求

3.支持 PromiseAPI

4.客服端支持防止 CSRF（伪脚本攻击） -提供了并发请求 API 接口

5.支持请求/响应拦截 6.取消请求 -自动装换 json 数据

`需要再去了解fetch`

## 4.rem 布局原理

rem 就是一个相对单位，相对于 HTML 根元素 的 font-size
布局原理：拿到设计图根据设计图设置 rem 的大小，然后通过媒体查询或者 js 动态获取屏幕的大小，动态设计 rem 的值

- 4.1 设计图为什么是 750px 1.高清，2.考虑到 2 倍屏，所以设计师给图一般都是 2 倍图或者 3 倍图，我们进行压缩
  rem 布局相对于流式布局：设计图的还原率更高

## 5. flex 弹性盒子布局

给一个盒子设置了:display:flex,这个盒子就拥有了主轴和交插轴的概念
justify-content：center （水平居中）
align-items：center（垂直居中）

## 6. 移动端的兼容问题

`
1.ios 中默认 button 有样式
-webkit- appearance:none;
border:0;

ios 中 click 有 300ms 的延迟响应：
使用 zepto 中的 tap 事件代替 click 事件

在 ios 和安卓中的 video 和 audio 元素无法自动播放
解决：就是当用户一触碰到屏幕就开始播放
$(html).one("touchstart",functiojn(){
auto.play()
})

`

## 如何防止浏览器缓存

浏览器会根据 url 的地址是不是一个，来判断是不是一个请求，如果是就走缓存，
如果不是就走重新请求，我们可以再地址后拼接上随机的字符串，防止浏览器走默认缓存

## 本地存储和 h5 存储的区别：

localStorage：大小 5m 左右，永久存储，可以在同一个网站的多个窗口共享
sessionStorage：大小 5m 左右，声明周期在页面关闭的时候就会销毁，不能在多个页面共享
cookie：大小为 4k 左右，声明周期在页面关闭的时候就会销毁，可以设置时间周期，一个网站的多个页面可以共享，请求时候会携带

# vue 面试题

### 1.什么是 MVVM？

MVVM 是 Model-View-ViewModel 的缩写。MVVM 是一种设计思想。Model 代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象
在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互的，Model 和 ViewModel 之间的交互是双向的，因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会反应到 View 上
ViewModel 通过双向数据绑定把 View 和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需要关注业务逻辑，不需要手动操作 DOM，不需要数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理

### 2.MVVM 和 MVC 区别？它和其他框架(jQuery)的区别是什么？哪些场景适合？

MVC 和 MVVM 其实区别并不大。都是一种设计思想。主要就是 MVC 中 Controller 演变成的 ViewModel。MVVM 主要解决了 MVC 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验
区别：vue 数据驱动，通过数据来显示图层而不是节点操作
场景：数据操作比较多的场景，更加便捷

### 3.vue 的优点是什么？

低耦合。视图(View)可以独立于 Model 变化和修改，一个 ViewModel 可以绑定到不同的"View"上，当 View 变化的时候 Model 可以不变，当 Model 变化的时候 View 也可以不变
可复用性。可以把一些视图逻辑放在一个 ViewModel 里面，让很多 View 复用这段视图逻辑。
独立开发。开发人员可以专注于业务逻辑和数据的开发(ViewModel)，设计人员可以专注于页面设计。
可测试。界面素来是比较难测试的，而现在测试可以针对 ViewModel 来写。

### 4.组件之间的传值？

① 父组件 -> 子组件
父组件给子组件绑定属性，子组件通过 props 属性来接收传递的数据
② 子组件 -> 父组件
方式：在父组件中声明一个接收数据的函数，父组件给子组件绑定事件，子组件通过$emit 触发事件，并且可在此时传递参数，父组件通过定义好的监听事件接收参数
③ 兄弟组件
创建一个新的 vue 实例，让各个兄弟组件共用一个事件机制，通过事件触发$emit(方法名，传递的数据)，在 mounted()钩子函数中，触发事件$on(方法名，callback(接收数据))，此时 callback 函数中的 this 已经发生了改变，可以使用箭头函数

### 5.路由之间的跳转

声明方式(标签跳转) 编程式(js 跳转)

### 6.vue.cli 怎样使用自定义的组件？有遇到过哪些问题吗？

第一步：在 components 目录新中新建你的组件文件(indexPage.vue)，script 一定要 export default{}
第二步：在需要用的页面(组件)中导入：import indexPage from '@/components/indexPage.vue'
第三步：注入到 vue 中的子组件的 components 属性上面，components: {indexPage}
第四步：在 template 视图 view 中使用，例如有 indexPage 命名，使用的时候则 index-page

### 7.vue 如何实现按需加载配合 webpack 配置

webpack 中提供了 require.ensure()来实现按需加载。以前引入路由是通过 import 这样的方式引入，改为 const 定义的方式进行引入
不进行页面按需加载引入方式：import home from '../../common.home.vue'
进行页面按需加载的引入方式：

```js
    const home = r => require.ensure([],() => r(require('../../common/home.vue'))
    const homt = function(){

    }


    var a = require('normal-dep');

    if ( module.hot ) {
        require.ensure(['b'], function(require) {
            var c = require('c');

            // Do something special...
        });
    }
```

### 8.vuex 是什么？怎么使用？哪种功能场景使用它？

vue 框架中状态管理。在 main.js 引入 store，注入。新建一个目录 store，....export。场景有：单页面应用中，组件之间的状态。音乐播放器、登录状态、加入购物车

### 9.vuex 有哪几种属性？

有五种，分别是 State、Getter、Mutation、Action、Module

### 10.vuex 的 State 特性？

A.Vuex 就是一个仓库，仓库里面放了很多对象。其中 state 就是数据源存放地，对应一般 Vue 对象里面的 data
B.state 里面存放的数据是响应式的，Vue 组件从 state 中读取数据，若是 store 中的数据发生改变，依赖这个数据的组件也会发生 更新
C.它通过 mapState 把全局的 state 和 getters 映射到当前组件的 computed 计算属性中

### 11.vuex 的 Getter 特性

A.getter 可以对 State 进行计算操作，它就是 Store 的计算属性
B.虽然在组件内也可以做计算属性，但是 getter 可以在多组件之间复用
C.如果一个状态只在一个组件内使用，是可以不用 geters

### 12.vuex 的 Mutation 特性

Action 类似于 mutation，不同在于：Action 提交的是 mutation，而不是直接变更状态；Action 可以包含任意异步操作

### 13.不用 vuex 带来什么问题？

可维护性下降，想修改数据要维护三个地方；
可读性下降，因为一个组件里的数据，根本就看不出来从哪来的
增加耦合，大量的上传派发，会让耦合大大增加，本来 Vue 用 Component 就是为了减少耦合，现在这么用，就违背了组件化的初衷。

### 14.v-show 和 v-if 指令的共同点和不同点

v-show 指令是通过修改元素的 display 的 CSS 属性让其显示或隐藏
v-if 指令是直接销毁和重建 DOM 达到让元素显示和隐藏的效果

### 15.如何让 CSS 只在当前组件中起作用

将当前组件的<style>修改为<style scoped>

### 16. `<keep-alive></keep-alive>`的作用是什么？

`<keep-alive></keep-alive>`包裹动态组件时，会缓存不活动的组件实例，主要用于保留组件状态或避免重新渲染。

### 17.vue 中引入组件的步骤？

（1）采用 ES6 的 import...from...语法或 Common.js 的 require()方法引入组件
（2）对组件进行注册，代码如下
（3）使用组件`<my-component></my-component>`

### 18.指令 v-el 的作用是什么？

提供一个在页面中已存在的 DOM 元素作为 vue 实例的挂载目标，可以是 css 选择器，也可以是一个 HTMLElement 实例

### 19.在 vue 中使用插件的步骤

采用 ES6 的 import...form...语法或 CommonJS 的 require()方法引入插件
使用全局方法 Vue.use(plugin)使用插件，可以传入一个选项对象 vue.use(MyPlugin,{someOption: true})

### 20.请列举出 3 个 Vue 中常用的声明周期钩子函数？

created：实例已经创建完成之后调用，在这一步，实例已经完成数据观测，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没有开始，$el 属性目前还不可见
mounted：el 被新创建的 vm.$el 替换，并且挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内
activated：keep-alive 组件激活时调用

### 21.active-class 是哪个组件的属性？

vue-router 模块的 router-link 组件

### 22.怎么定义 vue-router 的动态路由以及如何获取传过来的动态参数？

在 router 目录下的 index.js 文件中，对 path 属性加上/:id。使用 router 对象的 params.id

### 23.vue-router 有哪几种导航钩子？

有三种
第一种：全局导航钩子，router-beforeEach(to,from,next)，作用：跳转前进行判断拦截
第二种：组件内的钩子
第三种：单独路由独享组件

### 24.声明周期的八个阶段？

创建前/后：在 beforeCreate 阶段，vue 实例挂载元素 el 和数据对象 data 都为 undefined，还未初始化。在 create 阶段，vue 实例的数据对象 data 有了，el 还没有
载入前/后：在 beforeMount 阶段，vue 实例的$el 和 data 都初始化了，但还是挂载之前为虚拟的 DOM 节点，data.message 还未替换。在 mounted 阶段，vue 实例挂载完成，data.message 成功渲染
更新前/后：当 data 变化时，会触发 beforeUpdate 和 updated 方法
销毁前/后：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 DOM 的绑定，但是 DOM 结构依然存在

### 25.什么是 vue 生命周期？

vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载 DOM -> 渲染、更新 -> 渲染、卸载等一系列过程，我们称这是 vue 的声明周期

### 26.vue 声明周期的作用是什么？

它的生命周期有多个事件钩子，让我们控制整个 vue 实例的过程时更容易形成好的逻辑

### 27.vue 声明周期总共有几个阶段？

可以总共分为 8 个阶段：创建前/后、载入前/后、更新前/后、销毁前/后

### 28.第一次页面加载会触发哪几个钩子？

第一次页面加载时会触发 beforeCreate、create、beforeMount、mounted 这几个钩子

### 29.DOM 渲染在哪个周期中就已经完成？

DOM 渲染在 mounted 中就已经完成了

### 30.简单描述每个周期具体适合哪些场景？

beforeCreate：可以在加个 loading 事件，在加载实例时触发
created：初始化完成时的事件写在这里，如在这结束 loading 事件，异步请求也适宜在这里调用
mounted：挂载元素，获取 DOM 节点
updated：如果对数据统一处理，在这里写相应函数
beforeDestroy：可以做一个停止事件的确认框
nextTick：更新数据后立即操作 DOM

### 31.说出至少 4 中 vue 当中的指令和它的用法？

v-if：判断是否隐藏； v-for：数据循环； v-bind: class； 绑定一个属性； v-model：实现双向数据绑定

### 32.v-loader 是什么？使用它的用途有哪些？

解析：vue 文件的一个加载器。
用途：js 可以写 ES6、style 样式，可以 scss 或 less、template 可以加 jade 等

### 33.scss 是什么？在 vue.cli 中的安装使用步骤是？有哪几大特性？

css 的预编译
第一步：安装 css-loader、node-loader、sass-loader 等加载器模块
第二步：在 build 目录中找到 webpack.bace.config.js，在那个 extends 属性中加一个扩展.scss
第三步：在同一个文件，配置一个 module 属性
第四步：然后在组件的 style 标签上 lang 属性，例如：lang="scss"

### 34.为什么使用 key？

当有相同标签名的元素切换时，需要通过 key 特性设置唯一的值来标记让 vue 区分它们，否则 vue 为了效率只会替换相同标签内部的内容。

### 35.为什么避免 v-if 和 v-for 用在一起？

当 vue 处理指令时，v-for 比 v-if 具有更高的优先级，通过 v-if 移动到容器元素，不会再重复遍历列表中的每个值。取而代之的是，我们只检查它一次，且不会再 v-if 为否的时候运算 v-for

### 36.VNode 是什么？虚拟 DOM 是什么？

vue 在页面渲染的节点，及其子节点称为"虚拟节点(virtual Node)"，简写为"VNode"。"虚拟 DOM"是由 vue 组件树建立起来的整个 VNode 树的称呼。

### 37.vue-router 是什么？它有哪些组件？

vue 用来写路由的一个插件。router-link、router-view

### 38.路由导航钩子有哪些？它们有哪些参数？

导航钩子有：全局钩子和组件内独享的钩子。beforeRouterEnter、afterEnter、beforeRouterUpdate、beforeRouteLeave
参数有：有 to(去的那个路由)、from(离开的路由)、next(一定要在这个函数才能去到下一个路由，如果不用就拦截)最常用的就这几种

### 39.vue 的双向数据绑定原理是什么？

vue.js 是采用数据劫持结合发布者-订阅者模式，通过 Object.defineProperty()来劫持各个属性的 setter、getter，在数据变动时发布消息给订阅者，触发相应的监听回调

### 40.vue 的计算属性，什么情况下要用计算属性？

计算属性：computed
需要计算某个数据，这个数据依赖其他的数据，其他数据的变化，会引起它的变化

### 41.axios 的优点？

可以设置拦截请求和响应
自动转换 json 请求和响应
支持 promise 的 api

### vue 的本地代理配置

使用 nodejs 代理服务器来实现跨域请求不需要后台的配合，
步骤 1.在 config 的 index 文件夹的 dev 中配置 proxyTable{}

```js
proxyTable: {
    '/api':{
        target:"跨域请求的地址",
        // 是否开启代理服务进行跨域
        changeOrigin:true,
        pathRewrite:{
            '^/api':''//在请求的时候就直接写/api来代表target的地址即可。拼接上请求的路径和参数
        }
    }
}
```

步骤 2.直接使用 axios 请求需要跨域的地址即可

## 面试总结：

### 回答的不好的

    1.`H5的离线缓存`
    `h5离线缓存就是web应用允许我们在脱机的时候与互联网进行交互
    如何实现h5的离线缓存，在后缀名为manifest的文件来进行管理的，需要服务端的支持，不同的服务端支持的方式也是不同的

```js
    // 步骤：1.创建一个cache.manifest文件，并确保文件具有正确的内容： `
    CACHE MANIFEST
    #v1 - 2013-09-09
    CACHE: //在cache文件后就是配置的需要缓存的文件
    index.html
    favicon.ico
    css/main.css
    …
    NETWORK: \*
    //在NEXTWORK之后可以指定的是在线的白名单，就是列出不希望我们离线缓存的文件（通常是一些需要有互联网访问才有意义的文件），所以在这里我们通常使用快捷的方式*统配符来解决

    FALLBACK//只在线和离线的使用文件
    online.html offline.html


    // 步骤2.在服务器上设置内容的类型
    AddType text/cache-manifest.manifest
    // 步骤3.所有的HTMl文件都指向cache.manifest
    // 使用h5新增的manifest的属性
    <html manifast='/cache.manifest'>
    </html>
    // 完成这一步后，就完成了web离线缓存的所有步骤。由于浏览的文件内容都没有更改且存储在本地，因此现在网页的打开速度会更快（即使是在线状态也如此）。

    // (4)需要注意的问题：
    // ?网站的每一个html页面都必须设置html元素的manifest属性。一定要这样做；
    // ?在你的整个网站应用中，只能有一个cache.manifest文件（建议放在网站根目录下）；
    // ?部分浏览器（如IE8-）不支持HTML5离线缓存。
```

`离线缓存 通过 JS 动态控制更新`

```applicationCache 对象提供个了一些方法和事件，管理离线存储的交互过程。通过在 firefox8.0 的控制台中输入 window.applicationCache 可以看到这个对象的所有属性和事件方法。

```

```js
applicationCache.onchecking = function(){
   //检查manifest文件是否存在
}

applicationCache.ondownloading = function(){
//检查到有manifest或者manifest文件
   //已更新就执行下载操作
   //即使需要缓存的文件在请求时服务器已经返回过了
}
applicationCache.onnoupdate = function(){
//返回304表示没有更新，通知浏览器直接使用本地文件
}
applicationCache.onprogress = function(){
//下载的时候周期性的触发，可以通过它
   //获取已经下载的文件个数
}
applicationCache.oncached = function(){
//下载结束后触发，表示缓存成功
}
application.onupdateready = function(){//第二次载入，如果manifest被更新   //在下载结束时候触发   //不触发onchched   alert("本地缓存正在更新中。。。");if(confirm("是否重新载入已更新文件")){       applicationCache.swapCache();       location.reload();   }}
applicationCache.onobsolete = function(){
//未找到文件，返回404或者401时候触发
}

applicationCache.onerror = function(){
//其他和离线存储有关的错误
}
```

    2.`前端的优化`
    `
    减少http的请求：
    把小图片整合到一张精灵图上，使用字体图标，使用baes64格式进行图片的储存，使用懒加载
    把css和js脚本进行外链式
    在head中加载css
    把js脚本放在最后加载
    （js脚本的延迟加载：使用defer属性，或者async属性来延迟加载js脚本）
    
    3.`前端的安全的优化`
    `
    1.XSS  的跨站qq攻击
    解决：把<号进行转义，
    2. XSRF 的跨站请求伪造
    解决：比如一些支付的接口可以增加验证的流程如指纹、密码、短信实际开发中前端也就是配合后端做这些验证
    
    `
    4.`http协议以及和https的区别`
    `http传输是明文传输的，https是加密传输的
    http占用的是80端口而https占用的是443端口
    http是无状态的，https协议是由SSL和HTTP协议构建的可以进行加密传输、身份认证的网络协议，要比HTTP协议安全
    `

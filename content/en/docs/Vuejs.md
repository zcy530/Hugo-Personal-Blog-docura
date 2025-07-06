---
title: Vue js
slug: Vue-js
lastmod: 2025-07-01T00:00:00+00:00
---

[vue面试题整理(2022-持续更新中...)_老古懂的博客-CSDN博客_vue面试题](https://blog.csdn.net/qq_45659769/article/details/119564784)

[2020秋招前端面经知识点汇总(二) Vue部分 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/260150638)

[(173条消息) 2021年Vue最常见的面试题以及答案（面试必过）_前端探险家的博客-CSDN博客_vue面试题](https://blog.csdn.net/qq_44182284/article/details/111191455?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-111191455-blog-119564784.pc_relevant_multi_platform_whitelistv1_exp2&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

# 总结

## Basic

- 介绍 Vue
    
    是一套用于构建用户界面的渐进式JavaScript框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合
    
    解释渐进式：vue 允许你将一个网页分割成可复用的组件，每个组件都包含属于自己的 HTML、CSS、JAVASCRIPT 以用来渲染网页中相应的地方。对于 VUE 的使用可大可小，它都会有相应的方式来整合到你的项目中。所以说它是一个渐进式的框架。VUE 是响应式的（reactive）这是VUE 最独特的特性，也就是说当我们的数据变更时，VUE 会帮你更新所有网页中用到它的地方
    
- Vue 2.0 和 Vue3.0 的区别
    
    [vue2和vue3的区别有哪些 - web开发 - 亿速云 (yisu.com)](https://www.yisu.com/zixun/729240.html#:~:text=%E5%8C%BA%E5%88%AB%EF%BC%9A1%E3%80%81vue2%E7%9A%84%E5%8F%8C%E5%90%91%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9A%E5%88%A9%E7%94%A8%E4%BA%86ES5%E7%9A%84API%20Object.definePropert%20%28%29%EF%BC%8C%E8%80%8Cvue3%E4%B8%AD%E4%BD%BF%E7%94%A8%E4%BA%86es6%E7%9A%84API,Proxy%EF%BC%9B2%E3%80%81Vue3%E6%94%AF%E6%8C%81%E7%A2%8E%E7%89%87%EF%BC%8C%E8%80%8Cvue2%E4%B8%8D%E6%94%AF%E6%8C%81%EF%BC%9B3%E3%80%81%20Vue2%E4%BD%BF%E7%94%A8%E9%80%89%E9%A1%B9%E7%B1%BB%E5%9E%8BAPI%EF%BC%8C%E8%80%8CVue3%E4%BD%BF%E7%94%A8%E5%90%88%E6%88%90%E5%9E%8BAPI%EF%BC%9B4%E3%80%81%E5%BB%BA%E7%AB%8B%E6%95%B0%E6%8D%AE%EF%BC%8Cvue2%E6%8A%8A%E6%95%B0%E6%8D%AE%E6%94%BE%E5%85%A5data%E5%B1%9E%E6%80%A7%E4%B8%AD%EF%BC%8C%E8%80%8CVue3%E4%BD%BF%E7%94%A8setup%20%28%29%E6%96%B9%E6%B3%95%EF%BC%9B5%E3%80%81vue3%E6%9C%89Teleport%E7%BB%84%E4%BB%B6%EF%BC%8Cvue2%E6%B2%A1%E6%9C%89%E3%80%82)
    
    区别：1、vue2的双向数据绑定利用了ES5的API Object.definePropert()，而vue3中使用了es6的API Proxy；2、Vue3支持碎片，而vue2不支持；3、 Vue2使用选项类型API，而Vue3使用合成型API；4、建立数据，vue2把数据放入data属性中，而Vue3使用setup()方法；5、vue3有Teleport组件，vue2没有。
    
- Vuex 使用情景
    
    vuex 是一个专为 vue.js 应用程序开发的状态管理模式
    
    可以理解为把需要**多个组件共享的变量**全部存储在一个对象里面，把这个对象放在顶层的 vue 实例当中，让其他组件可以使用，可以想象成是一个单例对象
    
    **使用情景：**
    
    - 大型开发，多个界面间的共享问题
    - 比如用户的登录状态、拿到和保存 token、用户名称、头像、地理位置信息等等
    - 比如商品的收藏、购物车中的物品（在很多页面都有添加购物车的功能）
    - 这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的
    
    **简单使用：**
    
    创建一个 store 文件夹，首先在 index.js 里定义四个东西： state, getters, mutations, actions
    
- 介绍 Vuex
    
    Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用**集中式存储**，管理应用的所有组件的状态，Vuex 可以帮助我们管理共享状态，并附带了更多的概念和框架。这需要对短期和长期效益进行权衡。如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex
    
    Vuex 是集中管理项目公共数据的，有 state、mutations 、getters、actions、module 属性
    
    - state 属性用来存储公共管理的数据
    - mutations 属性定义改变state中数据的方法， 注意：不要在mutation中的方法中写异步方法ajax，那样数据就不可跟踪了
    - getters 属性可以认为是定义 store 的计算属性。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算
    - action 属性类似于 mutation，不同在于：Action 提交的是 mutation，而不是直接变更状态。Action 可以包含任意异步操作
    - moudle 属性是将 store 分割成模块。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块，从上至下进行同样方式的分割
    
    使用方法： 
    
    - state ：直接以对象方式添加属性
    - mutations ：通过`store.commit`调用
    - action：通过 `store.dispatch` 方法触发
    - getters：直接通过store.getters 调用
    - 加分回答 可以使用mapState、mapMutations、mapAction、mapGetters一次性获取每个属性下对应的多个方法。 VueX在大型项目中比较常用，非关系组件传递数据比较方便
    
- SPA 单页面应用程序
    
    单页Web应用（single page web application，SPA）： SPA 是一种特殊的 Web 应用，是加载单个 HTML 页面并在用户与应用程序交互时动态更新该页面的。它将所有的活动局限于一个 Web 页面中，仅在该 Web 页面初始化时加载相应的 HTML 、 JavaScript 、 CSS 。一旦页面加载完成， SPA 不会因为用户的操作而进行页面的重新加载或跳转，而是利用 JavaScript 动态的变换 HTML（采用的是 div 切换显示和隐藏），从而实现UI与用户的交互。在 SPA 应用中，应用加载之后就不会再有整页刷新。相反，展示逻辑预先加载，并有赖于内容Region（区域）中的视图切换来展示内容。
    
    要实现单页面应用，现在已经有很多现成的框架了，它们都是很全面的开发平台，为单页面应用开发提供了必需的页面模板、路径解析和处理、后台服务 api 访问、 DOM 操作等功能
    
    ![Untitled](Untitled.png)
    
    **1) 有良好的交互体验**
    
    能提升页面切换体验，用户在访问应用页面是不会频繁的去切换浏览页面，从而避免了页面的重新加载；
    
    **2) 前后端分离开发**
    
    单页Web应用可以和 RESTful 规约一起使用，通过 REST API 提供接口数据，并使用 Ajax 异步获取，这样有助于分离客户端和服务器端工作。更进一步，可以在客户端也可以分解为静态页面和页面交互两个部分；
    
    **3) 减轻服务器压力**
    
    服务器只用出数据就可以，不用管展示逻辑和页面合成，吞吐能力会提高几倍；
    
    **4) 共用一套后端程序代码**
    
    不用修改后端程序代码就可以同时用于 Web 界面、手机、平板等多种客户端
    
- vue-router 的动态路由传参
    
    [https://blog.csdn.net/ww_5211314/article/details/103426989](https://blog.csdn.net/ww_5211314/article/details/103426989)
    
    1. route点击列表页，显示详情页面，此时就需要我们传递列表唯一的标识，然后显示对应的内容。通常做法是以“参数=值”的形式传递参数，而动态路由将参数融入到路由的路径定义之内成为路径的一部分。在参数名称之前加“：”，然后将参数写在路由的path内，比如 path: '/detail/:id’
    
          然后在.vue文件中用$route.params.Id可以获取当前路由的参数
    
    1. query
    
    ```java
    this.$router.push({
        path:"/login",//这个path就是你在router/index.js里边配置的路径
        query:{
              userId:"10011"
        }
    })
    ```
    
    1. vue的router-link标签传参
- vue-router 导航钩子
    
    第一种是全局导航钩子（全局守卫）：router.beforeEach(to,from,next)，作用：跳转前进行判断拦截。
    第 二种：全局解析守卫router.beforeResolve,在导航被确认前，所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用。（2.5.0新增）。
    第三种：单独路由独享的守卫beforeEnter,在路由配置时定义，与全局守卫的方法是一样的。
    第四种：组件内的守卫。直接在路由组件内定义守卫
    
- route 和 router
    
    $route和$router的区别
    
    答：$route是“路由信息对象”，包括path，params，hash，query，fullPath，matched，name等路由信息参数。而$router是“路由实例”对象包括了路由的跳转方法，钩子函数等
    
- <router-link>属性和方法
    
    ![Untitled](Untitled%201.png)
    
- vue 的路由实现
    
    Vue的路由实现：hash模式 和 history模式
    
    - hash模式： 在浏览器中符号“#”，#以及#后面的字符称之为hash，用window.location.hash读取。特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面
    - history模式： history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，history采用HTML5的新特性；且提供了两个新方法：pushState()，replaceState()可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更。
- <keep-alive></keep-alive>
    
    **作用**：缓存组件，提升性能，避免重复加载一些不需要经常变动且内容较多的组件
    
    **使用方法**：使用 `<keep-alive>` 标签对需要缓存的组件进行包裹，默认情况下被 `<keep-alive>` 标签包裹的组件都会进行缓存，区分被包裹的组件是否缓存有两种方法，第一种是给keepalive 添加属性，组件名称指的是具体组件添加的 name，不是路由里面的 name。include 包含的组件(可以为字符串，数组，以及正则表达式,只有匹配的组件会被缓存)。exclude 排除的组件(以为字符串，数组，以及正则表达式,任何匹配的组件都不会被缓存)。第二种也是最常用的一种是，和路由配合使用：在路由中添加meta属性。 使用keepalive导致组件不重新加载，也就不会重新执行生命周期的函数，如果要解决这个问题，就需要两个属性进入时触发：activated 退出时触发：deactivated 
    
    **适用的场景**：首页展示固定数据的组件，比如banner九宫格；或者比如有一个列表和一个详情，那么用户就会经常执行打开详情=>返回列表=>打开详情…这样的话列表和详情都是一个频率很高的页面，那么就可以对列表组件使用进行缓存，这样用户每次返回列表的时候，都能从缓存中快速渲染，而不是重新渲染，这样就会减轻服务器压力，提高性能
    
- MVVM (Model View VIewmodel)
    
    MVVM 由 Model,View,ViewModel 三部分构成，Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象
    在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到 View 上
    ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理
    
- vue 生命周期
    
    定义：Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程
    
    Vue 的生命周期总共分为：创建前/后，载入前/后，更新前/后，销毁前/后
    
    - beforeCreate 实例完全被创建出来之前，vue 实例的挂载元素 $el 和数据对象 data 都为 undefined，还未初始化
    - created  数据对象 data 已存在，可以调用 methods 中的方法操作 data 中的数据，但 dom 未生成，$el 未存在 。
    - beforeMount  vue 实例的 $el 和 data 都已初始化，挂载之前为虚拟的 dom节点，模板已经在内存中编辑完成了，但是尚未把模板渲染到页面中
    - mounted  vue 实例挂载完成，data.message 成功渲染。内存中的模板，已经真实的挂载到了页面中，用户已经可以看到渲染好的页面了。当执行完 mounted 就表示，实例已经被完全创建好了，DOM 渲染在 mounted 中就已经完成了
    - beforeUpdate 当 data 变化时，会触发beforeUpdate方法 。data 数据尚未和最新的数据保持同步
    - updated 当 data 变化时，会触发 updated 方法。页面和 data 数据已经保持同步了
    - beforeDestory 组件销毁之前调用 ，实例仍然完全可用。
    - destoryed  组件销毁之后调用，对 data 的改变不会再触发周期函数，vue 实例已解除事件监听和 dom绑定，但 dom 结构依然存在
- 父子组件生命周期的执行顺序
    
    加载渲染过程：beforeCreate(父) —> created(父)—>beforeMount(父)—>beforeCreate(子)—>created(子)—>beforeMount(子)—>mounted(子)—>mounted(父)
    更新过程：beforeUpdate(父) —> beforeUpdate(子) —> update(子) —> update(父)
    父组件更新：beforeUpdate(父) —> updated（父）
    销毁过程：beforeDestory(父) —> beforeDestory(子) —> destoryed(子) —> destoryed(父)
    
- vue 钩子函数
    
    全局导航钩子、组件内钩子、单独路由独享组件
    
    ```jsx
    全局的路由钩子函数：beforeEach、afterEach
    
    单个的路由钩子函数：beforeEnter
    
    组件内的路由钩子函数：beforeRouteEnter、beforeRouteLeave、beforeRouteUpdate
    ```
    
    - `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
    - `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
    - `update`：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
    - `componentUpdated`：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
    - `unbind`：只调用一次，指令与元素解绑时调用。
    
    指令钩子函数会被传入以下参数：
    
    - `el`：指令所绑定的元素，可以用来直接操作 DOM 。
    - `binding`：一个对象，包含以下属性：
    - `name`：指令名，不包括 v- 前缀。
    - `value`：指令的绑定值，例如：v-my-directive=“1 + 1” 中，绑定值为 2。
    - `oldValue`：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
    - `expression`：字符串形式的指令表达式。例如 v-my-directive=“1 + 1” 中，表达式为 “1 + 1”。
    - `arg`：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 “foo”。
    - `modifiers`：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
    - `vnode`： Vue编译生成的虚拟节点。移步 VNode API 来了解更多详情。
    - `oldVnode`：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用
    
- 常用的 vue 命令
    - `v-once`：能执行一次性地插值，当数据改变时，插值处的内容不会更新
    - `v-show`：和v-if一样，区别是 if 是将代码注释掉，v-show是给一个display：none 的属性让它不显示。v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换使用 v-show 较好，如果在运行时条件不大可能改变则使用 v-if 较好
    - `v-for`：基于数据渲染一个列表，类似于JS中的遍历。其数据类型可以是 Array | Object | number | string。
    - `v-html`：双大括号会将数据解释为普通文本，而非HTML 代码。为了输出真正的 HTML，你需要使用 v-html 而且给一个标签加了v-html 里面包含的标签都会被覆盖。
    - `v-text`：给一个便签加了v-text 会覆盖标签内部原先的内容
    - `v-bind`：动态属性绑定，缩写:
    - `v-on`：动态事件绑定，缩写@
    - `v-model`：双向数据绑定，限制在`<input>`、`<select>`、`<textarea>`、`components`中使用
- v-if 和 v-show
    
    同：两者都是达到显示隐藏的功能异：
    
    `v-if`指令是直接销毁和重建DOM达到让元素显示和隐藏的效果
    
    `v-show`指令通过修改元素的display属性让其显示或者隐藏
    
- v-el 和 $mount
    
    v-el：提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例
    
    el的优先级是高于$mount的，因此以el挂载节点为准
    
- real dom 和 vitual dom
- vue diff 算法
    
    提到vue的diff算法就不得不提一个名词 虚拟dom(Virtual DOM) ,什么是虚拟dom,我的理解是使用**js 对象来描述 dom 节点**，是 js 和 html 的中间层，是一层对真实 DOM 的抽象。以前传统的开发直接使用js操作dom，现在使用 js 操作 js 对象(虚拟dom)，在合适的时机将虚拟dom转化为真实dom节点
    
    为什么需要虚拟dom,直接操作dom不是更方便吗？实际上真正的 DOM 元素是非常庞大的，里面有非常多的属性，当我们频繁的去做 DOM 更新，会产生一定的性能问题。而虚拟 dom 使用 js 对象来描述dom节点，所以它比创建一个 DOM 的代价要小很多
    
    虚拟 DOM的最终目标是将虚拟节点渲染到视图上。但是如果直接使用虚拟节点覆盖旧节点的话，会有很多不必要的DOM操作。例如，在一个dom元素非常多的页面你只改里其中的一个地方，这种情况下如果使用新的虚拟节点覆盖旧节点的话，造成了性能上的浪费，这个时候就需要比较计算新老虚拟节点的不同，差量的更新。所以这个时候vue-diff 就出现了。
    

## Advance

- vue 组件之间的传参
    1. 父组件与子组件传值：
    
          子组件通过props方法接受数据
    
          子组件传给父组件：$emit方法传递参数
    
    1. 非父子组件间的数据传递，兄弟组件传值：eventBus
    
           就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适。（虽然也有不少人推荐直接用VUEX，具体来说看需求咯。技术只是手段，目的达到才是王道。）
    
- 父子组件之间传参数
    
    1.父组件传给子组件：子组件通过props方法接受数据;
    
    2.子组件传给父组件：$emit方法传递参数
    
    3.非父子组件间的数据传递，兄弟组件传值借用eventBus，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。发送数据使用 $emi t方法，使用 $on 接收
    
- vue 和 react 的区别
    1. 监听数据变化的实现原理不同：Vue通过getter/setter以及数据劫持来实现监听数据的变化 React则是通过比较引用（diff算法）来实现，如果不优化可能导致大量不必要的VDOM的重新渲染
    2. 两者设计理念不同，Vue使用的是可变的数据，React则强调数据的不可变，Vue更加简单，React构建大型应用的时候更加鲁棒。
    3. 数据流向不同Vue2.0中组件与DOM可以通过v-model双向绑定，2.0中不再支持父子组件之间通过props双向绑定，不鼓励组件对props进行修改，会警告。 React提倡单向数据流，使用Redux进行数据流状态管理
    4. 组件间的通信方式不同 Vue 的组件通信由三种方式：父组件通过props向子组件传递数据或者回到，子组件通过事件想父组件传递消息，通过2.2.0中新增的provide/inject实现父组件向子组件注入数据，可以跨越多个层级。 React的组件通信有三种方式：父组件通过props可以向子组件传递数据或者回调，可以通过context进行跨层级的通信，这其实和provide/inject起到的作用差不多，React本身不支持自定义时间，React中子组件向父组件传递消息使用回调函数。
    5. 模板渲染方式不同 React 通过JSX渲染模板，Vue通过拓展的 HTML 语法进行渲染。 React是在组件的 js 代码中，通过原生js来实现模板中的常见语法，比如插值，条件，循环等等，更加纯粹原生，而Vue是在和组件js代码分离的单独的模板中通过指令来实现的。
    6. 渲染过程不同 Vue 可以更快计算出虚拟DOM的差异，因为渲染过程中，Vue会收集依赖，然后根据注册的组件渲染对应的DOM，不需要重新渲染每一个组件 React在应用的状态改变时，全部子组件都会重新渲染。
    7. 框架本质不同Vue本质是MVVM框架，由MVC发展而来； React是前端组件化框架，由后端组件化发展而来
    8. Vuex和Redux的区别Redux使用的是不可变数据，而Vuex的数据是可变的，因此，Redux每次都是用新state替换旧state，而Vuex是直接修改。Redux在检测数据变化的时候，是通过diff的方式比较差异的，而Vuex其实和Vue的原理一样，是通过getter/setter来比较的，这两点的区别，也是因为React和Vue的设计理念不同。React更偏向于构建稳定大型的应用，非常的科班化。相比之下，Vue更偏向于简单迅速的解决问题，更灵活，不那么严格遵循条条框框。
- Promise 的原理
    
    **Promise的作用**：Promise是异步微任务，解决了异步多层嵌套回调的问题，让代码的可读性更高，更容易维护 
    
    **Promise使用**：Promise 是 ES6 提供的一个构造函数，可以使用 Promise 构造函数 new 一个实例，Promise 构造函数接收一个函数作为参数，这个函数有两个参数，分别是两个函数 `resolve`和 `reject`，`resolve` 将 Promise 的状态由等待变为成功，将异步操作的结果作为参数传递过去；`reject` 则将状态由等待转变为失败，在异步操作失败时调用，将异步操作报出的错误作为参数传递过去。实例创建完成后，可以使用 `then` 方法分别指定成功或失败的回调函数，也可以使用 catch 捕获失败，then 和 catch 最终返回的也是一个 Promise，所以可以链式调用
    
    **Promise的特点**： 
    
    1. 对象的状态不受外界影响（Promise对象代表一个异步操作，有三种状态） - pending（执行中） - Resolved（成功，又称Fulfilled） - rejected（拒绝） 其中pending为初始状态，fulfilled和rejected为结束状态（结束状态表示promise的生命周期已结束）
    
    2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。 Promise对象的状态改变，只有两种可能（状态凝固了，就不会再变了，会一直保持这个结果）： - 从Pending变为Resolved - 从Pending变为Rejected 
    
    3. resolve 方法的参数是then中回调函数的参数，reject 方法中的参数是catch中的参数 
    
    4. then 方法和 catch方法 只要不报错，返回的都是一个fullfilled状态的promise 
    
    **Promise的其他方法**： 
    
    - Promise.resolve() :返回的Promise对象状态为fulfilled，并且将该value传递给对应的then方法 Promise.reject()：返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法
    - Promise.all()：返回一个新的promise对象，该promise对象在参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败
    - Promise.any()：接收一个Promise对象的集合，当其中的一个 promise 成功，就返回那个成功的promise的值
    - Promise.race()：当参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象
- vue 响应式原理
    1. init 阶段： Vue 的 data的属性都会被reactive化，也就是加上 setter/getter函数。其中这里的Dep就是一个观察者类，相当于发布订阅模式中的事件中心这个模块，每一个data的属性都会有一个dep对象。当getter调用的时候，去dep里注册函数。setter的时候，就是去通知执行刚刚注册的函数。
    2. mount 阶段：mount 阶段的时候，会创建一个Watcher类的对象。这个Watcher实际上是连接Vue组件与Dep的桥梁。每一个Watcher对应一个vue component。new watcher的时候会在watch中生成一个updateComponent函数，这个函数会调用render函数来重新渲染对应的component。当render一个vue组件的时候，如果这个组件用到了某个属性title，那么这个组件对应的watcher对象会被注册到这个属性title的dep对象中，这就是收集依赖，收集完属性所有的依赖组件之后，当这个属性title发生改变之后，就会找到dep中注册过的所有的watcher对象，通知他们执行updateComponent函数来更新对应的组件在组件更新的时候，render函数里，会访问他所依赖的data的getter函数。
    3. 更新阶段：当某个属性title发生改变的时候，就去调用Dep的notify函数,然后通知所有的Watcher调用updateComponent函数更新
    
    总结
    
    第一步：组件初始化的时候，先给每一个data属性都注册getter，setter，也就是 reactive 化。然后再 new 一个自己的 Watcher 对象，此时 watcher 会立即调用组件的 render 函数去生成虚拟DOM。在调用 render 的时候，就会需要用到 data 的属性值，此时会触发 getter 函数，将当前的 Watcher 函数注册进 dep 里。
    
    第二步：当 data 属性发生改变之后，就会遍历 dep 里所有的 watcher 对象，通知它们去重新渲染组件。
    
- vue 2.0 双向绑定原理
    
    Vue响应式指的是：组件的 data 发生变化，立刻触发试图的更新 
    
    **原理**： Vue 采用数据劫持结合**发布者-订阅者模式**的方式来实现数据的响应式，通过Object.defineProperty 来劫持数据的 setter，getter，在数据变动时发布消息给订阅者，触发相应监听回调，订阅者收到消息后进行相应的处理。 通过原生js提供的监听数据的API，当数据发生变化的时候，在回调函数中修改 dom 核心API：Object.defineProperty 
    
    **响应式原理**： 获取属性值会触发getter方法，设置属性值会触发setter方法，在setter方法中调用修改dom的方法 
    
    **Object.defineProperty API**：用来定义对象属性，当把一个普通 Javascript 对象传给 Vue 实例来作为它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化
    
    Object.defineProperty的缺点：
    
    - 一次性递归到底开销很大，如果数据很大，大量的递归导致调用栈溢出
    - 不能监听对象的新增属性和删除属性
    - 无法正确的监听数组的方法，当监听的下标对应的数据发生改变时
- vue 3.0 双向绑定原理
    
    **定义**：Vue3.0 是通过 Proxy 实现的数据双向绑定。Proxy是ES6中新增的一个特性，实现的过程是在目标对象之前设置了一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写
    
    **用法**： ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例
    
    `var proxy = new Proxy(target, handler)` 
    
    - target: 是用Proxy包装的被代理对象（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）
    - handler: 是一个对象，其声明了代理target 的一些操作，其属性是当执行一个操作时定义代理的行为的函数
    
    在Vue中，`Object.defineProperty`无法监控到数组下标的变化，导致直接通过数组的下标给数组设置值，不能实时响应。目前只针对以上方法做了 hack 处理，所以数组属性是检测不到的，有局限性 Object.defineProperty 只能劫持对象的属性,因此我们需要对每个对象的每个属性进行遍历。Vue里，是通过递归以及遍历data对象来实现对数据的监控的，如果属性值也是对象那么需要深度遍历,显然如果能劫持一个完整的对象，不管是对操作性还是性能都会有一个很大的提升。 Proxy的两个优点：可以劫持整个对象，并返回一个新对象，有13种劫持
    
- 简单实现数据响应 Object.defineProperty
    
    ```jsx
    var demo={
        name:'张三'
    }
    //Object.defineProperty(obj,prop,descriptor)
    //obj:目标对象，prop:需要新增，或者修改的属性名，descriptor:定义的特性
    Object.defineProperty(demo,'name',{
        set(value){
            console.log('重新设为：'+value)
            name=value
        },
    
        get(){
            return name
        }
    })
    
    demo.name='李四'
    console.log(demo.name)//李四
    ```
    
- computed 和 watch
    
    **计算属性 computed**
    
    1. 支持缓存，只有依赖数据发生改变，才会重新进行计算
    2. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化
    3. computed 属性值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值
    4. 如果一个属性是由其他属性计算而来的，这个属性依赖其他属性，是一个多对一或者一对一，一般用computed
    5. 如果computed属性属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法
    
    ```jsx
    //计算属性中的属性不需要在data中定义，而且必须有return
    data(){
        return{
            firstname:"张",
            lastname:"三"
        }
    }
    computehd(){
        fullname(){
            return this.firstname+this.lastname
        }
    }
    /*计算属性具有缓存，计算属性是基于它们的依赖进行缓存的，只有在它的相关依赖发生改变时才会重新求值。
    只要计算属性的依赖没有改变，那么调用它就会直接返回之前的缓存。 同时computed对于其中变量的依赖时多个
    的时候，只要其中一个发生了变化都会触发这个函数*/
    
    //应用场景：当一个变量的值受多个变量的值影响
    ```
    
    **侦听属性watch**
    
    1. 不支持缓存，数据变，直接会触发相应的操作；
    2. watch支持异步；
    3. 监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；
    4. 当一个属性发生变化时，需要执行对应的操作；一对多；
    5. 监听数据必须是data中声明过或者父组件传递过来的props中的数据，当数据变化时，触发其他操作，函数有两个参数，　immediate：组件加载立即触发回调函数执行，　deep: 深度监听，为了发现对象内部值的变化，复杂类型的数据时使用，例如数组中的对象内容的改变，注意监听数组的变动不需要这么做。注意：deep无法监听到数组的变动和对象的新增，参考vue数组变异,只有以响应式的方式触发才会被监听到
    
    ```jsx
    //监听器watch中的值需要在data中定义，且函数有参数，newval和oldval
    data: {
      firstName: '张',
      lastName: '三',
      fullName: '张三r'
    },
    watch: {
      firstName: function (oval，nval) {
        this.fullName = nval + ' ' + this.lastName
      },
      lastName: function (oval，nval) {
        this.fullName = this.firstName + ' ' + nval
      },
      immediate: true,// 代表在wacth里声明了firstName之后立即先去执行其函数方法
      deep: true //深度监听
    }
    //watch的依赖是单个的，它每次只可以对一个变量进行监控，并且区别于computed属性，监听器watch可以是异步的而computed则不行
    
    //应用场景：当一个变量的值影响着多个变量的值
    ```
    
    总结：
    
    computed特性
    
    1. 是计算值，不支持异步操作，单纯的返回一个值
    2. 应用: 就是简化tempalte里面{{}}计算和处理props或$emit的传值
    3. 具有缓存性，页面重新渲染值不变化；计算属性会立即返回之前的计算结果，而不必再次执行函数，只有依赖数据发生改变，才会重新进行计算
    
    watch特性
    
    1. 是观察的动作，支持异步操作，可以进行一系列异步操作，
    2. 应用: 监听props，$emit或本组件的值执行异步操作
    3. 无缓存性，页面重新渲染时值不变化也会执行
- 创建全局组件
- v-model的实现原理
    
    **v-model**
    
    就是vue的双向绑定指令，能将页面上空间输入的值同步更新到相关绑定的属性，也会在更新data绑定属性的时候，更新页面上输入控件的值
    
    v-model作为双向绑定指令也是vue两个核心功能之一，使用非常方便，提高前端开发效率，在view层，model层相互需要数据交互，即可使用v-model
    
    **实现原理**
    
    **总的来说绑定数据并且监听(input事件)数据改变然后再赋值给变量**
    
    v-model 主要实现了两个功能，view 层输入值影响 data 的属性值，data 属性值发生改变会更新view层数值变化
    
    1. input 输入值后更新data
    
    首先在页面初始化时，vue 编译器会编译 该html 模板文件，将页面上的dom元素遍历生成一个虚拟的dom树再递归虚拟dom的每一个节点，当匹配到的是一个元素而非纯文本，则继续遍历每个属性，如果遍历到v-model这个属性，则会为这个节点添加一个input书简，当监听从页面输入值的时候，来更新vue实例中data相对应的属性值
    
    1. data属性赋值后更新input值
    
    同样初始化vue实例的时候，会遍历 data 的每一个属性，并通过 defineProperty来监听每一个属性的get和set方法，从而一旦某个属性重新赋值，则能监听到变化来操作响应的页面控制
    
    总结：
    
    核心就是，一方面model层通过defineProperty来劫持每个属性，一旦检测到变化，通过相应的页面元素更新另一方面通过编译模板文件，为控件的v-model绑定input事件，从而页面输入能实时的更新相关data属性值
    
    **v-model 的实现**
    
    ```jsx
    <input placeholder="请输入电话" id="username" />
    <p id="uName">显示值</p>
    ```
    
    ```jsx
    let obj ={}
    Objec.defineProperty(obj,'username',{
        get:function(){
            console.log('取值')
        }
        set:function(val){
            console.log('设置值')
            document.getElementById('uName').innerText=val
        }
    })
    document.getElementById('username').addEventListener('keyup',function(){
        obj.username=event.target.value
    })
    ```
    
- 对闭包的理解
    
    得分点：变量背包、作用域链、局部变量不销毁、函数体外访问函数的内部变量、内存泄漏、内存溢出、形成块级作用域、柯里化、构造函数中定义特权方法、Vue中数据响应式Observer 
    
    **定义**：闭包，一个函数和词法环境的引用捆绑在一起，这样的组合就是闭包（closure）
    
    **场景**：一般就是一个函数 A，return 其内部的函数 B，被 return 出去的 B 函数能够在外部访问 A 函数内部的变量，这时候就形成了一个 B 函数的变量背包，A 函数执行结束后这个变量背包也不会被销毁，并且这个变量背包在 A 函数外部只能通过 B 函数访问
    
    **闭包形成的原理**：作用域链，当前作用域可以访问上级作用域中的变量
    
    **闭包解决的问题**：能够让函数作用域中的变量在函数执行结束之后不被销毁，同时也能在函数外部可以访问函数内部的局部变量
    
    **闭包带来的问题**：由于垃圾回收器不会将闭包中变量销毁，于是就造成了内存泄露，内存泄露积累多了就容易导致内存溢出。 加分回答 闭包的应用，能够模仿块级作用域，能够实现柯里化，在构造函数中定义特权方法、Vue中数据响应式Observer中使用闭包等
    
- 插槽 slot
    
    slot就是为了实现真正的灵活的单页组件，在组件外部灵活控制组件内部的内容一种形式或者是入口，就是将组件内所需要的内容以插槽（slot）的形式插入到公共组件中，以达到灵活控制。
    当组件渲染的时候，这个 元素将会被替换为“Your Profile”。插槽内可以包含任何模板代码，包括 HTML
    
- vue-router 实现懒加载
    
    vue-router 实现懒加载的方法有两种
    
    - ES6的 impot 方式
    
    ```html
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue'), 
    ```
    
    - VUE中的异步组件进行懒加载方式
    
    ```html
    component: resolve=>(require(['../views/About'],resolve))
    ```
    
- 前端性能优化手段
    
    得分点：图片压缩和文件压缩、节流防抖、HTTP缓存、本地缓存、Vue的keep-alive缓存、ssr服务器端渲染、懒加载、对dom查询进行缓存、将dom操作合并 
    
    标准回答：前端性能优化分为两类，一类是文件加载更快，另一类是文件渲染更快
    
    - **加载更快的方法**： 
    让传输的数据包更小（压缩文件/图片）：图片压缩和文件压缩 
    减少网络请求的次数：雪碧图/精灵图、节流防抖 
    减少渲染的次数：缓存（HTTP缓存、本地缓存、Vue的keep-alive缓存等）
    - **渲染更快的方法**： 
    提前渲染：ssr服务器端渲染 
    避免渲染阻塞：CSS放在HTML的head中 JS放在HTML的body底部 
    避免无用渲染：懒加载 
    减少渲染次数：对dom查询进行缓存、将dom操作合并、使用减少重排的标签
    
    加分回答：雪碧图的应用场景一般是项目中不常更换的一些固定图标组合在一起，比如logo、搜索图标、切换图标等。 电商项目中最常用到的懒加载，一般在查看商品展示的时候通常下拉加载更多，因为商品数据太多，一次性请求过来数据太大且渲染的时间太长。
    
- 常用的性能优化指标
    
    Speed Index（lighthouse，速度指数）TTFB（Network，第一个请求响应时间） - 页面加载时间 - 首次渲染 - 交互动作的反馈时间 - 帧率FPS（动画 ctrl+shift+p） - 异步请求完成时间 使用性能测量工具进行量化 - Chrome DevTools - 开发调试、性能评测 - Audit(Lighthouse) - Throttling 调整网络吞吐 - Performance 性能分析 - Network 网络加载分析 - Lighthouse - 网站整体质量评估 - 还可以提出优化建议 - WebPageTest - 测试多地点(球各地的用户访问你的网站的性能情况) - 全面性能报告（first view,repeat view,waterfall chart 等等） - WebPageTest 还可以进行本地安装，让你的应用在还没上线的时候就可以测试
    
    常用的性能测量API DNS 
    
    解析耗时: domnLookupEnd - domnLookupStart 
    
    TCP 连接耗时: connectEnd - connectStart SSL 
    
    安全连接耗时: connectEnd - secureConnectionStart 
    
    网络请求耗时 (TTFB): responseStart - requestStart
    
    数据传输耗时: responseEnd - responseStart 
    
    DOM 解析耗时: domInteractive - responseEnd 
    
    资源加载耗时: loadEventStart - domContentLoadedEventEnd 
    
    First Byte时间: responseStart - domnLookupStart 
    
    白屏时间: responseEnd - fetchStart 
    
    首次可交互时间: domInteractive - fetchStart 
    
    DOM Ready 时间: domContentLoadEventEnd - fetchStart 
    
    页面完全加载时间: loadEventStart - fetchStart 
    
    http 头部大小： transferSize - encodedBodySize 
    
    重定向次数：performance.navigation.redirectCount 
    
    重定向耗时: redirectEnd - redirectStart
    
- 如何获取 data 中某一个数据的初始值
    
    ```jsx
    data() {
        return {
          num: 10
      },
    mounted() {
        this.num = 1000
      },
    methods: {
        countNum() {
            // 可以通过this.$options.data().keyname来获取初始值
            // 计算出num增加了多少
            console.log(1000 - this.$options.data().num)
        }
      }
    ```
    

# 学习

# **Part1 Meet Vue**

## **1. 安装**

方式一：直接CDN引入 你可以选择引入开发环境版本还是生产环境版本

```
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

方式二：下载和引入（前期学习使用这个，后续学习CLI使用NPM）

[https://vuejs.org/js/vue.js](https://vuejs.org/js/vue.js)

[https://vuejs.org/js/vue.min.js](https://vuejs.org/js/vue.min.js)

方式三：NPM安装

后续通过webpack和CLI的使用，我们使用该方式。

## **2. hello world**

区分**声明式编程和命令式编程**

**声明式编程**的好处，界面和数据可以全部分离

**第一个程序**

在es6中用let定义变量，用const定义常量

1. 创建vue实例，传入参数是对象
2. 创建div元素
3. vue挂载div，vue帮忙管理div的内容

```html
<body>
    <div id="app">{{message}}</div>

    <script src="vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app", // 用于挂载要管理的元素
            data: {
                message: "你好啊,李银河!",
                name: "coderwhy",
            },
        });
    </script>
</body>
```

双向绑定展示

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217162709.png)

在console直接修改message的值，**vue列表的展示**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217162735.png)

用到了循环 v-for

```
<body>
    <div id="app">
        <ul>
            <li v-for="item in movies">{{item}}</li>
        </ul>
    </div>

    <script src="vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app", // 用于挂载要管理的元素
            data: {
                message: "hello",
                movies: ["starwalk", "soul", "dreamspace"],
            },
        });
    </script>
</body>
```

同样可以在console随意添加数据

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217164757.png)

## **3. Vue lifecycle**

vue 回调函数

生命周期函数也叫做钩子函数 hook 表示回调的意思

小小例子

```
<body>
    <script src="vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app",
            created: function fun() { //一般在created里面做网络请求
                console.log("created");
            },
            mounted: function fun() {
                console.log('mounted');
            }
            //这两个函数不是我调的，是vue源码在内部做的回调函数
        });
    </script>
</body>
```

# **Part2 Basic Vue**

在开始之前定义一个模板template

```
"Print to myvue": {
    "prefix": "myvue",
    "body": [
        "<div id=\"app\">",
        "</div>",
        "<script src='vue.js'></script>",
        "<script>",
        "  const app = new Vue({",
        "    el: '#app', ",
        "    data: {",
        "    }",
        "  })",
        "</script>",
    ],
    "description": "vue模板"
},
```

## **1. 插值操作**

Mustache语法就是双大括号

可以把data里的值取出来

```
<body>
    <div id="app">
        <h2>{{message}}</h2>
        <h2>{{message}}, 李银河!</h2>
        <h2>{{firstName + lastName}}</h2>
        <h2>{{firstName + ' ' + lastName}}</h2>
        <h2>{{firstName}} {{lastName}}</h2>
        <h2>{{counter * 2}}</h2>
    </div>

    <script src="vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app",
            data: {
                message: "你好啊",
                firstName: "kobe",
                lastName: "bryant",
                counter: 100,
            },
        });
    </script>
</body>
```

**插值操作的其他指令**

- v-once 属性只能改变一次
    
    ```
    <h2 v-once>{{message}}</h2>
    ```
    
- v-html 该指令后面往往会跟上一个string类型
    
    会将string的html解析出来并且进行渲染
    
    ```
     <div id="app">
      <h2>{{url}}</h2>
      <h2 v-html="url"></h2>
    </div>
    
    <script src="vue.js"></script>
    <script>
      const app = new Vue({
        el: '#app',
        data: {
          message: '你好啊',
          url: '<a href="http://www.baidu.com">百度一下</a>'
        }
      })
    </script>
    ```
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217193129.png)
    
- v-test 展示文本
    
    用起来不太灵活
    
    ```
    <h2 v-text="message"></h2>
    ```
    
- v-pre 原封不动的显示出来，而不做任何解析
    
    ```
    <div id="app">
      <h2>{{message}}</h2>
      <h2 v-pre>{{message}}</h2>
    </div>
    ```
    
- v-cloak 我们浏览器可能会直接显然出未编译的Mustache标签
    
    ```
    <div id="app" v-cloak>
      <h2>{{message}}</h2>
    </div>
    ```
    

## **2. 绑定属性 v-bind**

不光是动态插值，某些属性希望动态绑定

比如a元素的herf属性，img元素的src属性

```
<div id="app">
    <img v-bind:src="imgURL" alt="" />
    <a v-bind:href="aHref">百度一下</a>

    <!--语法糖的写法-->
    <img :src="imgURL" alt="" />
    <a :href="aHref">百度一下</a>
</div>

<script src="vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            message: "你好啊",
            imgURL:
            "https://img11.360buyimg.com/mobilecms/s350x250_jfs/t1/20559/1/1424/73138/5c125595E3cbaa3c8/74fc2f84e53a9c23.jpg!q90!cc_350x250.webp",
            aHref: "http://www.baidu.com",
        },
    });
</script>
```

## **3. 计算属性**

把多个数据进行结合或者变化之后再展示

方法一：methods 里面定义的方法也是可以在双大括号里面使用的

方法二：使用计算属性 computed

尽可能按照属性的方法给函数取名字，使用的时候不需要加小括号

这样写其实也是一个语法糖 里面有setter和getter 这个是getter

```
<div id="app">
    <h2>{{getFullName()}}</h2>
    <!-- ！！计算属性不用加括号 -->
    <h2>{{fullName}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            firstName: 'Lebron',
            lastName: 'James'
        },
        computed: {   // computed: 计算属性()
            fullName: function () {
                return this.firstName + ' ' + this.lastName
            }
        },
        methods: {
            getFullName() {
                return this.firstName + ' ' + this.lastName
            }
        }
    })
</script>
```

## **4. 事件监听 v-on**

## **5. 条件和循环 v-show**

## **6. 表单绑定 v-model**

实现表单元素和数据的双向绑定

比如，当我们在输入框输入内容时，因为input中的v-model绑定了message，所以会实时将输入的内容传递给message，message实时发生改变

```
 <div id="app">
  <input type="text" v-model="message">
  {{message}}
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>
```

## **7. ES6语法补充**

### **let/var**

我们可以将let看成更完美的var

var没有块级作用域，在代码块里定义的东西，在变量外也可以访问

块级作用域引起的问题

```
<button>按钮1</button>
<button>按钮2</button>
<button>按钮3</button>
<button>按钮4</button>
<button>按钮5</button>

<script>
    var btns = document.getElementsByTagName('button');
    for (var i = 0; i < btns.length; i++) {
        btns[i].addEventListener('click', function () {
            console.log('第' + i + '个按钮被点击');
            // 点击了第1个，打印却是第5个，点击其他按钮也是打印第5个
            // 打印的i是在一个函数里面，在点击之前，这个i已经被改掉了，进行了5次循环
        })
    }
</script>
```

在es5中，我们解决的方法是建立一个函数作用域，形成闭包。在js里面只有函数有作用域，而if和for都没有块级作用域

```
var btns = document.getElementsByTagName('button');
for (var i = 0; i < btns.length; i++) {
    (function (num) { // 0
        btns[i].addEventListener('click', function () {
            console.log('第' + num + '个按钮被点击');
        })
    })(i)
}
```

在es6中加入了let，if和for都有块级作用域

```
// es6写法
const btns = document.getElementsByTagName('button')
for (let i = 0; i < btns.length; i++) {
    btns[i].addEventListener('click', function () {
        console.log('第' + i + '个按钮被点击');
    })
}
```

### **const**

使用const修饰的标识符为常量，不可以再次赋值

在ES6开发时优先使用const，只有需要改变某一个标识符时才使用let

1. 不能修改
    
    ```
     const a=20;
     a=30;// 错误:不可以修改
    ```
    
2. 必须赋值
    
    ```
    const name; // 错误:const修饰的标识符必须赋值
    ```
    
3. 指针不能改，内部属性可以改
    
    ```
    const obj = {
        name: 'why',
        age: 18,
        height: 1.88
    }
    // obj = {}
    console.log(obj);
    
    obj.name = 'kobe';
    obj.age = 40;
    obj.height = 1.87;
    
    console.log(obj);
    ```
    

### **javascript高阶函数**

fliiter

map

### **换行字符串**

用波浪号的按键敲出的引号

```
const str = `abc`

template: `
  <div>
    <h2></h2>
  <div<`
```

可以换行的字符串

# **Part3 Vue组件化开发**

提供了一种抽象，开发出一个个独立的可复用的小组件来构造应用，任何应用都会被抽象一颗**组件树**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211219170400.png)

## **1. 组件基础**

创建组件构造器对象 → 注册组件 → 使用组件

```
1. const cpnC = Vue.extend()
2. Vue.component("my-cpn", cpnC);
3. <my-cpn></my-cpn>
```

举例

```
  <body>
    <div id="app">
      <!-- 第一种展示 -->
      <my-cpn></my-cpn>
      <my-cpn></my-cpn>
      <my-cpn></my-cpn>
      <!-- 第二种展示 -->
      <div>
        <my-cpn></my-cpn>
      </div>
    </div>

    <!-- 第三种展示 -->
    <my-cpn></my-cpn>

    <script src="vue.js"></script>

    <script>
      // 1. 创建组件构造器对象
      const cpnC = Vue.extend({
        template: `
          <div>
            <h2>我是标题</h2>
            <h2>我是内容，哈哈哈哈</h2>
          </div>
          `,
      });

      // 2.注册组件
      Vue.component("my-cpn", cpnC);

      const app = new Vue({
        el: "#app",
        data: {},
      });
    </script>
  </body>
```

**注册全局组件的语法糖**：省略extend

```
Vue.component("cpn1", {
    template: `
        <div>
          <h2>我是标题1</h2>
          <h2>我是内容</h2>
        </div>
        `,
});
```

**注册局部组件的语法糖**

写在vue对象参数里面

```
const app = new Vue({
        el: "#app",
        data: {
          message: "你好",
        },
        components: {
          cpn2: {
            template: `
                <div>
                  <h2>我是标题2</h2>
                  <h2>我是内容</h2>
                </div>
                `,
          },
        },
      });
```

**组件模板分离的写法**

[Untitled](Untitled%20714b50250a564e6aa9059143b7a91d81.csv)

1.script标签

2.template标签

```
<div id="app">
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
</div>

<!-- 1.script标签，类型必须是text/x-template -->
<script type="text/x-template" id="cpn">
    <div>
        <h2>我是标题1</h2>
        <h2>我是内容</h2>
    </div>
</script>

<!-- 2.template标签 -->
<template id="cpn">
    <div>
        <h2>我是标题1</h2>
        <h2>我是内容</h2>
    </div>
</template>

<script src="vue.js"></script>

<script>
    //注册一个全局组件
    Vue.component("cpn", {
        template: "#cpn",
    });

    const app = new Vue({
        el: "#app",
        data: {
        },
    });
</script>
```

## **2. 组件高级**

## **3. 组件声明周期**

## **4. ES6模块化实现**

export/import关键字

在script里面加上 `type = ”module“`表示按照模块化开发

```
<script src="./aaa.js" type="module"></script>
<script src="./bbb.js" type="module"></script>
```

每一个模块都是一个自己的空间，不能用其他模块的东西，如果想访问别的模块的东西，就export/import

导出

```
// aaa.js 文件

//第一种方法，先把三个变量定义好再一起导出
let name = "小明";
let age = 18;
function sum(num1, num2) {
  return num1 + num2;
}

export { name, flag, sum };

//第二种方法，定义的时候就导出
export let name = "小明";
export let age = 18;
export function sum(num1, num2) {
  return num1 + num2;
}
export class person {
    run() {
        console.log("running");
    }
}

//
```

导入

```
// mmm.js文件想使用aaa.js文件中的flag和sum

// import
import { flag, sum } from "./aaa.js";

if (flag) {
  console.log("小明是天才");
}

//统一导入
import * as aaa from './aaa.js'
console.log(aaa.name);
```

# **Part4 Webpack**

前端模块化，并帮我们处理模块间的依赖关系

webpack模块化打包，为了可以正常运行，必须依赖node环境

## **1. 安装**

先检查自己的node环境

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211219193806.png)

全局安装webpack

```
npm install webpack@3.6.0 -g
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211219213153.png)

局部安装webpack

```
npm install webpack@3.6.0 --save-dev
```

一般项目有两个文件夹，src和dist，src是开发的源代码，dist是发布给服务器的打包代码

## **2. 简单使用**

把src文件夹里的两个js文件用webpack打包，在dist文件里生成bundle.js文件

```
webpack ./src/main.js ./dist/bundle.js
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211219213452.png)

只需在index.js里引用bundle.js就可以了

```
<script src="./dist/bundle.js"></script>
```

## **3. 配置vue ⭐️**

从现在开始的后续项目中，我们会使用vuejs进行开发，而且以特殊的文件来组织vue的组件

我们首先需要对其有依赖，先进行安装

```
npm install vue --save
```

```
import Vue from "vue";

new Vue({
  el: "#app",
  data: {
    message: 'hello webpack'
  }
})
```

SPA：单页面复应用 simple page web application

一般项目里只有一个html代码，多个页面是通过路由跳转的

# **Part5 Vue CLI**

开发大型项目需要考虑项目结构，必然要使用vue cli，自动生成目录结构和各种配置

command line interface 命令行界面，俗称脚手架

vue-cli可以快速搭建vue开发环境以及webpack相应配置

使用前提：**1.node和npm 2. webpack**

## **安装 vue脚手架**

```
npm install -g @vue/cli
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217195257.png)

## **vue-cli 3 特点**

vue-cli 3 基于webpack 4，设计原则是零配置

提供了vue ui命令，提供了可视化配置

新增了public文件夹

## **vue-cli 3 创建项目**

在vscode进入文件夹，用集成终端terminal打开文件夹

```
> vue create projectname
```

选择手动 manual

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217201955.png)

选择项目需要的东西

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217202901.png)

放在独立的配置文件还是 package.json

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217203013.png)

再选择一些其他配置之后，回车开始创建项目，创建成功

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217203441.png)

## **vue-cli 3 项目结构**

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217204021.png)

node_modules：保存的node包

public：相当于 vue-cli 2 的static

src：源代码

.browserSlistrc：浏览器相关配置

.gitignore：忽略文件，不提交到服务器的文件，很少改

babel.config.js：配置babel的东西

package.json：项目配置

package.lock.json：中间文件，安装的真实版本

postcss.config.js：css转化文件

## **vue-cli 3 项目运行**

打包用build

```
vue-cli service build
```

跑项目用serve

```
npm run serve
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211217204817.png)

访问localhost:8080

xgxt项目运行

```
npm install
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211218135442.png)

```
npm run build
```

![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211218135743.png)

```
npm run serve
```

# **Part6 vue-router**

前端路由

# **Part7 vuex**

vuex 是一个专为 vue.js 应用程序开发的状态管理模式

可以理解为把需要**多个组件共享的变量**全部存储在一个对象里面，把这个对象放在顶层的 vue 实例当中，让其他组件可以使用，可以想象成是一个单例对象

## 7.1 情景

- 大型开发，多个界面间的共享问题
- 比如用户的登录状态、拿到和保存 token、用户名称、头像、地理位置信息等等
- 比如商品的收藏、购物车中的物品（在很多页面都有添加购物车的功能）
- 这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的

## 7.2 简单使用 - 购物车

创建一个 store 文件夹，首先在 index.js 里定义四个东西： state, getters, mutations, actions

![Untitled](Untitled%202.png)

- state 存放变量
    
    ![Untitled](Untitled%203.png)
    
- getters 可以理解为 state 的一个计算属性，这样组件里面就可以通过 getters 来**访问到这个数据**
    
    ![Untitled](Untitled%204.png)
    
    定义好 getters 之后，就可以这样在组件里访问 items
    
    ![Untitled](Untitled%205.png)
    
    ![Untitled](Untitled%206.png)
    
- mutations 是用来**设置 state** 的
    
    ![Untitled](Untitled%207.png)
    
- mutation-type 用来管理我们可能会操作数据的方法的名字
    
    ![Untitled](Untitled%208.png)
    

# **Part8 axios**

ajax
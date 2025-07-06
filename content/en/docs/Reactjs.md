---
title: React js
slug: React-js
lastmod: 2025-07-01T00:00:00+00:00
---

[https://github.com/adrianhajdin/portfolio_website](https://github.com/adrianhajdin/portfolio_website)

[【前端工程师面试宝典】学习说明_互联网校招面试真题面经汇总_牛客网 (nowcoder.com)](https://www.nowcoder.com/issue/tutorial?tutorialId=96&uuid=1678a0fd35cd4db486af18589e34e4d4)

### 面试常考题目总结

- react 生命周期
    
    React 组件的生命周期有三个不同的阶段：
    
    1. 初始渲染阶段：*这是组件即将开始其生命之旅并进入 DOM 的阶段。
    2. 更新阶段：*一旦组件被添加到 DOM，它只有在 prop 或状态发生变化时才可能更新和重新渲染。这些只发生在这个阶段。
    3. 卸载阶段：*这是组件生命周期的最后阶段，组件被销毁并从 DOM 中删除
    
    ***componentWillMount***() – 在渲染之前执行，在客户端和服务器端都会执行
    
    ***componentDidMount***() – 仅在第一次渲染后在客户端执行。
    
    ***componentWillReceiveProps*****()** – 当从父类接收到 props 并且在调用另一个渲染器之前调用。
    
    ***shouldComponentUpdate*****()** – 根据特定条件返回 true 或 false。如果你希望更新组件，请返回**true** 否则返回 **false**。默认情况下，它返回 false。
    
    ***componentWillUpdate*****()** – 在 DOM 中进行渲染之前调用。
    
    ***componentDidUpdate*****()** – 在渲染发生后立即调用。
    
    ***componentWillUnmount*****()** – 从 DOM 卸载组件后调用。用于清理内存空间。
    
- react 的优缺点
    
    React的一些主要优点是：
    
    1. 采用组件化模式，声明式编码，提高开发效率和组件复用率
    2. 使用虚拟 dom 和优秀的 diffing 算法，尽量减少与真实 dom 的交互
    3. 使用范围广，可以开发 web 应用，也可以用 react navie 进行移动端开发，还可以用 react 360 进行 VR 开发
    4. 由于 JSX，代码的可读性很好
    5. 使用 React，编写UI测试用例变得非常容易
    
    React的限制如下：
    
    1. React 只是一个 JS 库，而不是一个完整的框架
    2. 它的库非常庞大，需要时间来理解
    3. 新手程序员可能很难理解
    4. 编码变得复杂，因为它使用内联模板和 JSX
- react 和 vue 的对比
- real dom 和 vitual dom
    
    **什么是 dom？**
    
    DOM是用一颗逻辑树来表示一个文档，树的每个分支的终点都是一个节点，可以用特定的方式（编写JS、CSS、HTML）来改变这个树的结构，从而改变文档结构、样式或内容
    
    **什么是虚拟DOM？**
    虚拟DOM就是一个JS对象，通过对象的方式来表示DOM结构，通过事务处理机制，**将多次DOM修改的结果一次性更新到页面上**，减少DOM操作的次数，从而有效的减少页面渲染次数，减少修改DOM重绘重排的时间，提高渲染性能
    
    React在内存中维护一个跟真实DOM一样的虚拟DOM树，再改动完组件后，会再生成一个新的虚拟DOM，React会将新的虚拟DOM和原来的虚拟DOM进行对比，找出两个DOM树的不同的地方（diff），然后在真实DOM上更新diff，提高渲染速度
    
    ![Untitled](Untitled.png)
    
- 类式组件 和 函数式组件
    - 类组件有生命周期，函数组件没有
    - 类组件需要继承 Class，函数组件不需要
    - 类组件可以获取实例化的 this，并且基于 this 做各种操作，函数组件不行
    - 类组件内部可以定义并维护 state， 函数组件为无状态组件（可以通过hooks实现）
    - 函数式组件配合 hooks 使用
    
- 类式组件中的 this 的指向问题
    
    ```tsx
    class App extends React.Component {
      handleClick() {
        console.log(this);// undefined 
      }
      render() {
        return <div onClick={this.handleClick} >点我</div>;
      }
    }
    ```
    
    在 react中，事件处理函数中的 this 很容易丢失，我们有如下4种解决方案
    
    1. 箭头函数
    2. 构造函数中的 `bind`
    3. 事件绑定时的 `bind`
    4. 事件绑定时的匿名函数+箭头函数
    
    [(181条消息) 一文详解React事件中this指向，面试必备_爱笑的眼睛11的博客-CSDN博客_react 事件this](https://blog.csdn.net/u013176440/article/details/122675897?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-122675897-blog-124859641.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-122675897-blog-124859641.pc_relevant_multi_platform_whitelistv3&utm_relevant_index=1)
    
- 受控组件 和 非受控组件
    
    ![Untitled](Untitled%201.png)
    
- React redux
    
    **什么是 Redux**
    
    专门针对 react 所设计的状态管理工具，顶层套一个 provider，底层的组件都可以使用顶层的数据
    
    ![Untitled](Untitled%202.png)
    
    **数据如何通过 Redux 流动？**
    
    1. 首先，用户（通过View）发出 Action，发出方式就用到了 dispatch 方法。\
    2. 然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action，Reducer 会返回新的 State
    3. State 一旦有变化，Store 就会调用监听函数，来更新 View
    
    **Redux 遵循的三个原则是什么？**
    
    1. 单一事实来源：整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序
    2. 状态是只读的：改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示
    3. 使用纯函数进行更改：为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数
    
    **你对“单一事实来源”有什么理解？**
    
    Redux 使用 “Store” 将程序的整个状态存储在同一个地方。因此所有组件的状态都存储在 Store 中，并且它们从 Store 本身接收更新。单一状态树可以更容易地跟踪随时间的变化，并调试或检查程序。
    
    **Redux 由以下组件组成**
    
    1. **Action** – 这是一个用来描述发生了什么事情的对象，是把数据从应用传到store的载体，它是store数据的唯一来源，一般来说，我们可以通过 store.dispatch() 将 action 传递给 store
    2. **Reducer** – 这是一个确定状态将如何变化的地方，本质就是一个函数，它用来响应发送过来的actions，然后经过处理，把state发送给store
    3. **Store** – Store就是把action与reducer联系到一起的对象，整个程序的状态/对象树保存在Store中。
    4. **View** – 只显示 Store 提供的数据
    
    ![Untitled](Untitled%203.png)
    
- Redux middleware
    
    [(189条消息) Redux中间件原理详解_daysRoc的博客-CSDN博客_redux中间件的原理](https://blog.csdn.net/Donspeng/article/details/83032832)
    
    作用就是改造dispatch函数，当你应用了中间件，在触发一个action操作的时候，action操作就会经过先经过中间件，最终再形成dispatch(action)
    
    常见的中间件：
    
    - Redux-actions帮助我们简化了action代码和reducer代码
    - redux-logger 记录所有action及其发送前后的state的日志，我们可以了解到代码实际运行时到底发生了什么
    - redux-thunk：处理异步action
    
    常规使用：createStore + applyMiddleWare，定义 myMiddleware中间件，放在applyMiddleware 方法之中，传入createStore方法，就完成了store.dispatch()的功能增强。即可以在reducer中进行一些异步的操作
    
    ```jsx
    import { applyMiddleware, createStore } from 'redux';
    import thunk from 'redux-thunk';
    import createLogger from 'redux-logger';
    
    const logger = createLogger();
    
    const store = createStore(
      reducers, 
      applyMiddleware(thunk, logger) //会按顺序执行
    );
    ```
    
    ![Untitled](Untitled%204.png)
    
    下面是createStore + applyMiddleWare的源码
    
    ```jsx
    const store = createStore(reducer, preloadedState, enchancer);
    
    // 如果没有中间件，正常触发一个action；
    // 如果有中间件的时候 creatStore内部的执行逻辑是这样的
    // enchancer 就是你应用的中间件，调用applyMiddleware得到的组合中间件
    
    function applyMiddleware(...middlewares) {
      return createStore => (...args) => {
      
        // 该创建的store还是要创建的,只传入了两个参数，没有中间件，得到的是正常的store
        const store = createStore(...args)
        let dispatch = () => {
          throw new Error(
            `Dispatching while constructing your middleware is not allowed. ` +
              `Other middleware would not be applied to this dispatch.`
          )
        }
        // 把getState、dispatch传给中间件
        const middlewareAPI = {
          getState: store.getState,
          dispatch: (...args) => dispatch(...args)
        }
        // 下面方法返回来了一个函数数组，中间件被剥离到
        // next => {}
        const chain = middlewares.map(middleware => middleware(middlewareAPI))
        // 再执行下面的，中间件就被剥离到
        // action => {}
        dispatch = compose(...chain)(store.dispatch)
    
        return {
          ...store,
          dispatch
        }
      }
    }
    
    // 下面得到的结果是 
    // 假设中间件为 a b
    // a(b(store.dispatch))
    return enchancer(createStore)(reducer, preloadedState)；
    
    // 结合上面thunk的源码
    （{ dispatch, getState }) => next => action => {
        if (typeof action === 'function') {
            return action(dispatch, getState);
        }
        return next(action);
      };
    ```
    
    ![Untitled](Untitled%205.png)
    
- React hook
    
    React Hooks 是从 React 16.8 版本推出的新特性，目的是解决 React 的状态共享以及组件生命周期管理混乱的问题。React Hooks 的出现标志着，React 不会再存在无状态组件的情况，React 将只有类组件和函数组件的概念
    
    hooks 为函数组件提供了状态，也支持在函数组件中进行数据获取、订阅事件解绑事件等等
    
    - useState：通过 useState 为组件提供状态。useState 的参数是 state 的初始值，他只有在组件第一次渲染的时候会生效，他的返回值是一个数组，第一个是 state，第二个是设置state的函数。
    
    ```tsx
    const [count, setCount] = useState(0);
    ```
    
    - useEffect：通常在useEffect中进行ajax请求，事件的绑定与解绑，设置定时器与清除等等
    
    ```tsx
    // useEffect第一个参数是一个回调函数，在里面进行业务逻辑代码的书写
      // 第二个参数是依赖项数组，如果数组中的依赖发生变化，那么该副作用就会重新执行，
      // 如果不设置第二个参数，那么当该组件每渲染一次，副作用就会执行一次
      useEffect(() => {
        console.log("useEffect副作用执行");
        //用setTimeout模拟ajax请求
        setTimeout(() => {
          setList(result);
        }, 3000);
      }, [list]);
    ```
    
    - useCallback：用于缓存函数，第一个参数为要缓存的函数，第二个参数为依赖项数组，如果依赖发生了变化，那么就会生成一个新的函数；否则当组件重新渲染时，不会重新定义这个函数，而是会取缓存。
    - useMemo：用于缓存函数的返回值，第一个参数为要缓存的函数（注意实际被缓存的是函数被执行过后的值），第二个参数为依赖项数组，如果依赖发生了变化，那么就会重新执行这个函数，得到新的返回值；否则当组件重新渲染时，不会重新执行这个函数，而是直接取被缓存的该函数的返回值。
- React router
    1. 什么是React 路由？
        
        React router是一个构建在 React 之上的强大的路由库，它有助于向应用程序添加新的屏幕和流。这使 URL 与网页上显示的数据保持同步。它负责维护标准化的结构和行为，并用于开发单页 Web 应用。 React 路由有一个简单的API
        
        ```
        <switch>
            <route exact="" path="’/’" component="{Home}/">
            <route path="’/posts/:id’" component="{Newpost}/">
            <route path="’/posts’" component="{Post}/">
        </route></route></route></switch>
        ```
        
    2. 为什么需要 React 中的路由？
        
        Router 用于定义多个路由，当用户定义特定的 URL 时，如果此 URL 与 Router 内定义的任何 “路由” 的路径匹配，则用户将重定向到该特定路由。所以基本上我们需要在自己的应用中添加一个 Router 库，允许创建多个路由，每个路由都会向我们提供一个独特的视图
        
    3. 为什么React Router v4中使用 switch 关键字 ？
        
        虽然<div>用于封装 Router 中的多个路由，当你想要仅显示要在多个定义的路线中呈现的单个路线时，可以使用 “switch” 关键字。使用时，<switch>标记会按顺序将已定义的 URL 与已定义的路由进行匹配。找到第一个匹配项后，它将渲染指定的路径。从而绕过其它路线。
        
    4. 列出 React Router 的优点
        
        4.1 就像 React 基于组件一样，在 React Router v4 中，API 是 'All About Components'。可以将 Router 可视化为单个根组件（），其中我们将特定的子路由（）包起来。
        
        4.2 无需手动设置历史值：在 React Router v4 中，我们要做的就是将路由包装在 组件中。
        
        4.3 包是分开的：共有三个包，分别用于 Web、Native 和 Core。这使我们应用更加紧凑。基于类似的编码风格很容易进行切换
        
- React router v6 的新特性
    
    有哪些新hooks，如何传递路由参数？
    
    [react-router v6新特性 - 简书 (jianshu.com)](https://www.jianshu.com/p/15614a18a86e)
    
    现在一般都是用的 React router v6
    
    1. <Switch>重命名为<Routes>
    
    ```tsx
    /* v5 */
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/user/:id" render={(routeProps) => <User id={routeProps.match.params.id} />} />
    </Switch>
    /* V6 */
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="user/:id" element={<User id={id} />} />
    </Routes>
    ```
    
    1. <Route>的新特性变更:
        
        1.废弃exact
        2.component/render被element替代
        3.routeProps可以在element中直接获取
        4.简化的路径匹配，仅支持动态:id样式参数和*通配符，不再支持RegExp
        
    2. 嵌套路由
        
        1.支持相对路径
        2.<Route> 标签支持嵌套，可以在一个文件内配置嵌套路由，便于统一管理路由
        3.结合新API Outlet实现嵌套路由
        
    
    ```tsx
    import { HashRouter as Router, Routes, Route } from 'react-router-dom'
    import Home from '@/pages/demo/Home'
    import Foo from '@/pages/demo/Foo'
    import Bar from '@/pages/demo/Bar'
    import BarDetail from '@/pages/demo/BarDetail'
    import '@/assets/style/App.css'
    function App() {
     return (
       <Router>
         <Routes>
           <Route path="/" element={<Home />} />
           <Route path="foo" element={<Foo />} />
           {/* 嵌套路由场景：需要在Bar（父路由的组件）声明Outlet组件，用于渲染子路由 */}
           <Route path="bar" element={<Bar />}>
             <Route path=":id" element={<BarDetail />} />
           </Route>
         </Routes>
       </Router>
     )
    }
    export default App
    ```
    
    1. 新API：Outlet
    
    注意：嵌套路由场景，需要在父路由的组件（Bar）使用Outlet组件，用于渲染子路由，类似于vue的router-view
    
    ```tsx
    import { Outlet } from 'react-router-dom'
    function Bar() {
      return (
        <div>
          <div>Bar</div>
          {/* 有嵌套路由的场景需要使用 */}
          <Outlet />
        </div>
      )
    }
    export default Bar
    ```
    
    1. 嵌套路由可配置化：useRoutes代替react-router-config
    
    同理，配置化使用嵌套路由，Outlet 也是必要的
    
    ```tsx
    import { useRoutes } from 'react-router-dom'
    import Home from '@/pages/demo/Home'
    import Foo from '@/pages/demo/Foo'
    import Bar from '@/pages/demo/Bar'
    import BarDetail from '@/pages/demo/BarDetail'
    import '@/assets/style/App.css'
    function App() {
      let element = useRoutes([
        {
          path: '/',
          element: <Home />
        },
        {
          path: 'foo',
          element: <Foo />
        },
        {
          path: 'bar',
          element: <Bar />,
          children: [
            {
              path: ':id',
              element: <BarDetail />
            }
          ]
        }
      ])
      return element
    }
    export default App
    ```
    
    **注意：**入口文件需要添加Router包裹App组件，否则会报错
    （可以理解为，useRoutes返回的相当于Routes标签下的内容）
    
    `import React from 'react'
    import ReactDOM from 'react-dom'
    import { HashRouter as Router } from 'react-router-dom'
    import App from '@/App'
    import '@/assets/style/index.css'
    ReactDOM.render(
      <React.StrictMode>
        <Router>
          <App />
        </Router>
      </React.StrictMode>,
      document.getElementById('root')
    )`
    
    1. 用useNavigate代替useHistory
    
    ```tsx
    /* v5 */
    const history = useHistory()
    history.push('/home')
    history.replace('/home')
    history.goBack()
    history.goForward()
    history.go(2)
    /* V6 */
    const navigate = useNavigate()
    navigate('/home')
    navigate('/home', {replace: true})
    navigate(-1)
    navigate(1)
    navigate(2)
    ```
    
- React router 中两种路由模式的区别？
- React 16 有哪些新特性
- location 和 history 的使用
    
    在 react 组件的 componentDidMount 方法中打印一下 this.props，在浏览器控制台中查看输出如下，其中页面的 url 信息全都包含在 match 字段中
    
    ```jsx
    localhost:3000/app/knowledgeManagement/modify
    /STY20171011124209535/3/1507701970070/0/?s=1&f=7
    ```
    
    ![Untitled](Untitled%206.png)
    
    ![Untitled](Untitled%207.png)
    
    - **match：**包含了具体的 url 信息，在 params 字段中可以获取到各个路由参数的值
    - **history：**包含了组件可以使用的各种路由系统的方法，常用的有 push 和 replace，两者都是跳转页面，但是 replace 不会引起页面的刷新，仅仅是改变 url
    - **location：**相当于 URL 的对象形式表示，通过 search 字段可以获取到 url 中的 query 信息，所以location.search 是获取 url 参数的方法
    这里 state 的含义与 HTML5 history.pushState API 中的 state 对象一样。每个 URL 都会对应一个 state 对象，你可以在对象里存储数据，但这个数据却不会出现在 URL 中。实际上，数据被存在了 sessionStorage 中
    
- diff 算法
    
    diff算法探讨的就是虚拟DOM树发生变化后，生成DOM树更新补丁的方式、它通过对比新旧两颗虚拟DOM树的变更差异，将更新补丁作用于真实DOM，以最小的成本完成试图更新
    
- JSX 语法
    
    JSX 是 JavaScript XML 的简写。是 React 使用的一种文件，它利用 JavaScript 的表现力和类似 HTML 的模板语法。这使得 HTML 文件非常容易理解。此文件能使应用非常可靠，并能够提高其性能
    
    浏览器只能处理 JavaScript 对象，而不能读取常规 JavaScript 对象中的 JSX。所以为了使浏览器能够读取 JSX，首先，需要用像 Babel 这样的 JSX 转换器将 JSX 文件转换为 JavaScript 对象，然后再将其传给浏览器。
    
- **学习资源**
    
    Youtube Traversy Media
    
    Udemy [**Brad Traversy](https://www.udemy.com/user/brad-traversy/)**  **MERN eCommerce From Scratch**
    
    Udemy [**Brad Traversy](https://www.udemy.com/user/brad-traversy/)  [MERN Stack Front To Back: Full Stack React, Redux & Node.js](https://www.bilibili.com/video/BV1Av411s74b?spm_id_from=333.337.search-card.all.click)**
    
    Udemy [**John Smilga](https://www.udemy.com/user/janis-smilga-3/)    MERN Stack Course 2022 - MongoDB, Express, React and NodeJS**
    

### **React 介绍**

**用于构建用户界面的JavaScript库**

### **React Basic**

- 1 Create React App
    
    以前：下载 create-react-app
    
    ```
    npm install -g create-react-app
    create-react-app myapp
    
    cd myapp
    npm start
    ```
    
    现在：直接 npx create-react-app
    
    npx是直接安装这个包所需的文件，并且立即执行，然后从磁盘上删除，不用占用内存
    
    ```
    npx create-react-app myapp
    
    cd myapp
    npm start
    ```
    
    运行结果：[http://localhost:3000/](http://localhost:3000/)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220716233445.png)
    
    (optional) run ceate-app online
    
    [https://codesandbox.io/s/new](https://codesandbox.io/s/new)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220716182102.png)
    
- 2 项目结构
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220716233011.png)
    
    - **package.json**
        
        这个文件管理项目的依赖，相当于maven里的pom.xml文件，但是它里面还有一些命名。总之，跟Vue是一样的
        
        build脚本：创建一个最优化的低内存版本，用于打包托管服务器
        
        test脚本：确保一个文件里的代码做了期望的事情
        
    - **index.html**
        
        manifest.json 指定了开始页面 index.html，一切的开始都从这里开始，所以这个是代码执行的源头。其中的<div id="root"></div>是项目的总容器，我们把这个 div 称为根 DOM 节点，在此 div 下的所有内容都由 React DOM 来管理
        
        ```
          <body>
            <noscript>You need to enable JavaScript to run this app.</noscript>
            <div id="root"></div>
          </body>
        ```
        
    - **index.js**
        
        src 文件存放的是项目的核心内容，也是我们主要的工作区域
        
        index.js 是和 index.html 文件关联的唯一接口，属于项目入口的文件，所有的起点都在这里，统一做一些初始化工作，例如加载各种依赖、加载状态管理库等等
        
        ```
        import React from 'react';
        import ReactDOM from 'react-dom/client';
        import './index.css';
        import App from './App';
        import reportWebVitals from './reportWebVitals';
        
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(
          <React.StrictMode>
            <App />
          </React.StrictMode>
        );
        
        // If you want to start measuring performance in your app, pass a function
        // to log results (for example: reportWebVitals(console.log))
        // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
        reportWebVitals();
        ```
        
    - **App.js**
        
        react 基本上是用function来return html
        
        ```
        import logo from './logo.svg';
        import './App.css';
        
        function App() {
          return (
            <div className="App">
              <header className="App-header">
                <img src={logo} className="App-logo" alt="logo" />
                <p>
                  Edit <code>src/App.js</code> and save to reload.
                </p>
                <a
                  className="App-link"
                  href="https://reactjs.org"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  Learn React
                </a>
              </header>
            </div>
          );
        }
        
        export default App;
        ```
        
    
    可维护的 React 程序之项目结构梳理：
    
    [https://zhuanlan.zhihu.com/p/39799393](https://zhuanlan.zhihu.com/p/39799393)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220716234326.png)
    
    Class vs Hook
    
    Hook：编写组件的一个新方法
    
    Class：是传统的常用的方法，更多人在用
    
    学习路线 class -> hook
    
- 4 JSX 语法规则
    1. 文件名可以是 jsx 也可以是 js，不影响
    2. return 里面必须是闭合的，要有一个根元素
    3. 组件名称必须大写 `<App />`，不能用 `<app />`
    4. js 中想写 html 用圆括号，html 中想写 js 用花括号
    5. 类名要用 `<div className = ""> </div>`
    6. 如果要直接在标签里写 css，要用驼峰命名法，不能用横杠
        
        ```python
        <h3 style={{marginBottom:'30px',}}>Input Your Information</h3>
        <div style={{backgroundColor:'skyblue'}}> </div>
        ```
        
    7. 注释用 `{/* */}`
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723172811.png)
        
- 5 JSX Mapping Arrays
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717231126.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717231639.png)
    
    **keys to mapping:**
    
    可以确定一个唯一的id
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220718001035.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220718000940.png)
    
    **NOTE:**
    
    react 中的列表循环有且只有 map 可以使用，不能用 forEach 和 for
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723173458.png)
    
    可以简写成一行
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723173904.png)
    

### React 组件

- 1 函数组件和类组件
    
    组件化开发：function 组件和 class 组件
    
    ### **Class Component (1.4 - 1.6)**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717212118.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717212036.png)
    
    ### **Function Component (1.7 - 1.10)**
    
    - 函数式组件没有生命周期
    - 函数式组件没有 this
    - 函数式组件没有 state 状态
    - 配合 hooks 使用
    
    函数式组件写法一：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717221612.png)
    
    写法二：使用箭头函数
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723205804.png)
    
- 2 类组件中方法的 this 指向
- 2 组件之间通讯的三种方式
    
    父子组件之间的调用
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723220451.png)
    
    ### **Father to Son**
    
    父子组件之间的传参（父传子）
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723220640.png)
    
    ### **Son to Father**
    
    父子组件之间的传参（子传父）
    
    注意：无论是react还是vue，所谓子传父，真实在干活的都是父组件
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723220930.png)
    
    如果想要**在子组件里面修改变量**：
    
    1. 在父组件里面定义 state hook 和 `setNum` 的函数
    2. 在传递给子组件的 props 里面加入 `setNum = { setNum }`
    3. 子组件可以用 `porps.setNum( 789 )` 来调用
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723222054.png)
    
    ### **Grandfather to Son**
    
    就是跨级组件传值的意思，一般使用上下文空间 context
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723222439.png)
    
    1. 创建上下文空间：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723222933.png)
    
    1. 用 `<NumContext.Provider>` 和 `<NumContext.Consumer>` 分别包裹爷孙组件
    2. 不管是使用还是读取，如果传参是两个以上，都用花括号
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723223143.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723223228.png)
    
    1. 可以用 useContext 这个 hook，来简化代码
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723223720.png)
    
- 3 受控组件和不受控组件
    
    受控组件和不受控组件只存在于表单元素，所谓的受控组件就是表单元素的value需要通过state来定义
    
    input 里面要有绑定的 value 和对应的 onchange 函数
    
    ![Untitled](Untitled%208.png)
    
    不受控组件意味着表单元素的value无法通过state获取， 只能使用 ref useRef
    
    ![Untitled](Untitled%209.png)
    
- 4 Props 的使用
- 2 React State 和 setState
    
    只有 class component 有state
    
    ### **Use of State**
    
    **背景**：当所有的东西都是 hardcoded，意味着代码里面没有动态的东西，而我们需要动态呈现
    
    **作用**：local state，也可以简称 state，可以让我们在 html 中直接使用和利用 JavaScript 变量，每当这些变量发生变化时，react 会重新渲染我们看到的这个 html
    
    **位置**：写在构造器 constructor 里面。我们可以实际访问和生成 state 的方式是通过constructor()，constructor() 方法是一个对 class component 都可用的方法，super() 对我们 react 组件代码的作用并不重要，调用 super() 只是调用任何其他 extend 的类的底层构造方法
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717221444.png)
    
    ### **Set State**
    
    **作用**：每当这些变量发生变化时，React 会 rerendering 我们的 html 页面
    
    **注意**：你的 component 当 state 是一个完全不同的 object 在内存中时，才会重新渲染
    
    下面理解一下react里面的对象、指针问题
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717223342.png)
    
    所以下面这种方法没有作用
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717224015.png)
    
    ⭐️ 采用 setState() 的方法才有用
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717223811.png)
    
    **Callback：**
    
    二次 callback的作用是，希望 console.log(this.state) 可以显示更新后的值，所以第二个 () => {} 写的这个函数就是回调，一旦代码完成了，就执行这个回调，这将在 state 完全更新后运行
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717230154.png)
    
    **NOTE：**
    
    setState 的调用是一个非同步(non synchronous)的调用，这是一个异步调用 (asynchronous)
    
    **THREE WAYS To setState():**
    
    按钮二和按钮三都是独立定义了 onClick 函数，但是会有 "this" undefine 的问题
    
    - 按钮二是通过 `.bind(this)` 来解决的
    - 按钮三是通过箭头函数来规避了这个问题，但是后面要加上括号
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723181431.png)
    
    如果想要**函数传参**的话：
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723204549.png)
    
    ### **Shallow Merge**
    
    当你传递一个对象给它时，它将寻找存在于当前 state object 的任何 key，然后把它更新为新的 key，其他的 key 保持不变。所以 shallow merge 的意思就是它只更新被传递给它的 key and value，其他的东西都会以同样的方式保留
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220717224927.png)
    
- 7 React Hooks
    
    定义：hook 就是钩子，生命周期函数，只能用在函数组件的最顶层
    
    ### **useState hook**
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723212028.png)
    
    log出来可以发现 `useState()` 定义的是一个数组，前一个数是变量，后一个是函数
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723211258.png)
    
    于是可以把定义的变量拆解为数组  `[ verb, setVerb ]`
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723211019.png)
    
    ### **useEffect hook**
    
    可以模拟 mounted updated beforeDestory (数据请求 检测数据更新 垃圾回收) 三个生命周期
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723212101.png)
    
    - 模拟 mounted
        
        当页面第一次加载完成时运行，一般用来写 ajax
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723212624.png)
        
    - 模拟 updated
        
        检测哪个数据更新了，第一个参数是 function，第二个参数是想要检测的变量们的数组
        
        如果所有的变量都想检测，可以直接删掉数组不填
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723212542.png)
        
    - 模拟 beforeDestory
        
        一般在这个阶段处理脏数据或者垃圾回收
        
        ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723220011.png)
        
    
    ### **useContext hook**
    
    用于跨域组件的传值
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723223808.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20220723223831.png)
    
- 8 虚拟 DOM 和 diff 算法

### React Hooks

### React Redux

- 1 Intro
    
    **简介**
    
    专门针对 react 所设计的状态管理工具，可以理解为把需要多个组件共享的变量全部存储在一个对象里面。顶层套一个 provider，底层的组件都可以使用顶层的数据
    
    ```python
    npm i redux react-redux
    ```
    
     
    
    **数据如何通过 Redux 流动？**
    
    1. 首先，用户（通过View）发出 Action，发出方式就用到了 dispatch 方法
    2. 然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action，Reducer 会返回新的 State
    3. State 一旦有变化，Store 就会调用监听函数，来更新 View
    
    ![Untitled](Untitled%2010.png)
    
    **Redux 遵循的三个原则是什么？**
    
    1. 单一事实来源：Redux 使用 “Store” 将程序的整个状态存储在同一个地方。因此所有组件的状态都存储在 Store 中，并且它们从 Store 本身接收更新。单一状态树可以更容易地跟踪随时间的变化，并调试或检查程序。
    2. 状态是只读的：改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示
    3. 使用纯函数进行更改：为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数
    
    **使用情景：**
    
    - 大型开发，多个界面间的共享问题
    - 比如用户的登录状态、拿到和保存 token、用户名称、头像、地理位置信息等等
    - 比如商品的收藏、购物车中的物品（在很多页面都有添加购物车的功能）
    - 这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的
    
    **简单使用**
    
    需要在项目里新建文件夹 store，里面有 
    
    - 左：index.js (仓库的入口文件)
    - 右：reduce.js (创建初始状态，并导出一个函数)
    
    ![Untitled](Untitled%2011.png)
    
    修改组件
    
    - 修改 src/index.js 添加 **provider**
    - 修改 app componant，添加 **connect**，定义状态映射（将 reducer 中的 state 映射成 props，让开发者可以在组件中使用 props.num 去调用 state 中的 num），传入参数props
    
    ![Untitled](Untitled%2012.png)
    
- 2 Redux 使用的简单 demo
    
    ![Untitled](Untitled%2013.png)
    
    创建 action 文件夹(因为在真实开发中可能会发送很多个 action)
    
    写一个简单 action 构建函数
    
    ![Untitled](Untitled%2014.png)
    
    创建 reducers 文件夹，写一个简单 reducer
    
    ![Untitled](Untitled%2015.png)
    
    创建 store 文件夹，构建 store
    
    ![Untitled](Untitled%2016.png)
    
    在home使用上面的 store
    
    ![Untitled](Untitled%2017.png)
    
    效果：
    
    ![Untitled](Untitled%2018.png)
    
- 2 Redux 四大组件
    
    **Redux 由以下组件组成**
    
    1. **Action**
        - 这是一个用来描述发生了什么事情的 JavaScript 对象，是把数据从应用传到 store 的载体，它是 store 数据的唯一来源，只是描述了有事情要发生，并没有描述如何去更新
        - 我们可以通过 store.dispatch() 将 action 传递给 store
        - Action 是个动作对象，对象内部必须要有 type 和 data 属性，type 通常是字符串，表示动作执行的类型，data 表示跟本次动作执行相关的数据。我们在项目中更喜欢用 action creator 函数
        
        ```java
        // 1. action
        {
            type: 'string',
            info: {...},
            isLoading: true
        }
        
        // 2. action creator function
        function addAction(params)
        {
            // 返回一个 action 对象
            return {
                type: 'string',
                info: {...},
                isLoading: true
            }
        }
        
        ```
        
    2. **Reducer**
        - 这是一个确定状态将如何变化的地方，本质就是一个函数，它用来响应和处理发送过来的 old state + actions，然后经过处理，把 new state 发送给 store，reducer 是真正做事的人
            - Reducer 函数接受两个参数：old state，action
        - 在 Reducer 函数中，一定要 return 返回值，就是 new state 的，这样 store 才能接收到
        
        ```java
        const initState = {...};
        rootReducer = (state = initState, action) => {... return {...}};
        ```
        
    3. **Store**
        
        Store 就是把 action 与 reducer 联系到一起的对象，整个程序的状态/对象树保存在Store 中，主要职责：
        
        - 维持应用的 state
        - 提供 getState() 获取 state
        - 提供 dispatch() 发送 action
        - 通过 subscribe() 来注册监听
        - 通过 subscribe() 返回值来注销监听
        
        ```java
        import {createStore} from "redux";
        const store = createStore(reducer);
        ```
        
    4. **View**
        
        通过 getstate() 来显示 Store 提供的数据
        
    
    ![Untitled](Untitled%2010.png)
    
- 3 mapState vs mapDispatch
    
    **mapState**：状态映射，将 reducer 中的 state 映射成 props，让开发者可以在组件中使用 props.num 去调用 state 中的 num
    
    **mapDispatch**：事件派发映射，将 reducer 中的事件映射成 props，让开发者可以在组件中使用 props.add() 去实现 num 的累加
    
    ![Untitled](Untitled%2019.png)
    
    注意：左图的reduce.js文件里面，比起 if 判断，一般还是常用 switch
    

### React Router

- 0 SPA 单页面应用程序简介
    
    单页面应用程序 single page application，整个应用只有一个完整的 html 页面，但有多个组件，点击页面的链接不会刷新页面，只会做页面的局部更新，数据都需要通过 ajax 请求获取，并在前端异步展现
    
- 1 安装使用 react-router-dom
    
    react-router-dom 是 react 的一个插件库，目前最新的是 v6 版本
    
    ```tsx
    npm install react-router-dom@6
    yarn add react-router-dom@6 
    ```
    
- 2 路由配置 History Hash
    
    react-router-dom 中有两种模式：
    
    - **History 模式**：BrowserRouter，使用 h5 的 history.pushState API 来实现
    - **Hash 模式**：HashRouter，使用 URL 的哈希值来实现，url 里面会带有井号 #，直接打包就可以放到线上
    
    **History 模式**
    
    ```jsx
    import { BrowserRouter, Routes, Route, Link } from "react-router-dom"
    import Home from './pages/home' 
    import About from './pages/about' 
    
    function App() {
        return(
            <BrowserRouter>
                {/* 点击跳转 */}
                <Link to='/'>home</Link>
                <Link to='/about'>about</Link>
                {/* 路由出口位置 */}
                <Routes>
                    <Route path='/' element={<Home />} />
                    <Route path='/' element={<Home />} />
                </Routes>
            </BrowserRouter>
        )
    }
    
    export default App; 
    ```
    
    **HashRouter 模式**
    
    ```jsx
    import { HashRouter, Routes, Route, Link } from "react-router-dom"
    import Home from './pages/home' 
    import About from './pages/about' 
    
    function App() {
        return(
            <HashRouter>
                {/* 点击跳转 */}
                <Link to='/'>home</Link>
                <Link to='/about'>about</Link>
                {/* 路由出口位置 */}
                <Routes>
                    <Route path='/' element={<Home />} />
                    <Route path='/about' element={<About />} />
                </Routes>
            </HashRouter>
        )
    }
    
    export default App; 
    ```
    
- 3 核心组件介绍 Link Routes Route
    
    **Link**
    
    **作用**：用于指定导航链接，完成路由跳转
    
    **语法说明：**组件通过 to 属性指定路由地址，最终会渲染为 a 链接元素
    
    ```java
    <Link to='/'>home</Link>
    ```
    
    **Routes**
    
    **作用：**提供一个路由出口，满足条件的路由组件会渲染到组件内部
    
    ```java
    <Routes>
        <Route/>
        <Route/>
    </Routes>
    ```
    
    **Route**
    
    **作用：**用于指定导航链接，完成路由匹配
    
    **语法说明：**path 属性指定匹配的路径地址，element 属性指定要渲染的组件
    
    ```java
    <Route path='/' element={<Home />} />
    ```
    
- 4 事件跳转 useNavigate
    
    作用：通过 js 编程的方式进行路由跳转，比如从登录页面跳到关于页
    
    ```jsx
    import { useNavigate } from 'react-router-dom'
    
    function Login () {
    
        const navigate = useNavigate()
        
      const goAbout = () => {
            navigate('/about')
        }
        
        return (
            <div>
                login
                <button onClick={goAbout}> jump to about page</button>
            </div>
        )
    }
    ```
    
    注意：如果在跳转时不想加历史记录，就是点左上角返回的时候不会再回去，可以添加额外参数 replace:true
    
    ```jsx
    navigate('/about',{replace: true})
    ```
    
- 5 跳转携带参数 useSearchParams useParams
    
    **useSearchParams**
    
    params是一个对象，对象里面有一个 get 的方法，用来获取对应的参数，把参数的名称作为 get 方法是参数传过来
    
    ```jsx
    // 传参 Login.js
    navigate('/about?id=1001&&name=mike')
    
    // 取参 About.js
    import { useSearchParams } from 'react-router-dom'
    
    let [params] = useSearchParams()
    let id = params.get('id')
    let name = params.get('name')
    ```
    
    **useParams**
    
    ```jsx
    // 先在 App.js 配置占位路由
    <Route path='/about/:id' element={<About />} />
    
    // 传参 Login.js
    navigate('/about/1001')
    
    // 取参 About.js
    let params = useParams()
    let id = params.id
    ```
    

1. 发起签到的时候报错
2. 人脸识别签到，没有传照片退出的时候，要显示签到失败
3. 学生签到之后要查看到记录
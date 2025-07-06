---
title: MERN E-Commerce
slug: MERN-E-Commerce
lastmod: 2025-07-01T00:00:00+00:00
---

### 项目简介

- 简历
    
    项目介绍：采用 MERN 技术架构 (react全家桶 + nodejs + MongeDB数据库 + Express框架)，包括 Redux 的状态管理方案和 React Router 6 路由管理方案，使用 mongoose 来连接 MongoDB 数据库，实现了产品的完整增删查改操作，分页浏览和模糊搜索，用户的登录注册和信息管理，使用 JWT 身份验证和授权，验证电子邮件，加入购物车和下订单等功能，并把项目部署在 Heroku 上
    
- Udemy 介绍
    
    There are a lot of "eCommerce" courses out there, but most use some kind of prebuilt plugin or platform. In this course, we will build a completely customized eCommerce / shopping cart application from scratch with the MERN stack with the following functionality...
    
    现在有很多 "电子商务 "课程，但大多数都使用某种预制的插件或平台。在本课程中，我们将使用MERN堆栈从头开始建立一个完全定制的电子商务/购物车应用程序，具有以下功能…
    
    Full featured shopping cart 
    
    Product reviews and ratings
    
    Top products carousel top3 产品轮播图
    
    Product pagination 产品分页
    
    Product search feature 产品搜索功能
    
    User profile with orders 带订单的用户资料
    
    Admin product management admin 产品管理
    
    Admin user management admin 用户管理
    
    Admin Order details page admin 订单详情页
    
    Mark orders as delivered option 标记订单为已交付选项 
    
    Checkout process (shipping, payment method, etc) 
    
    结账流程（运输、支付方式等）
    
    PayPal / credit card integration 贝宝/信用卡整合
    
    Custom database seeder script 自定义数据库播种机脚本
    
    This is not a documentation-type course. This is a jump in and get your hands dirty course where by the end, you have an actual real-world project to use and put on your portfolio. You will learn the following by completing this course..
    
    这不是一个文档类型的课程。这是一个跳入并弄脏你的手的课程，到最后，你有一个实际的真实世界的项目来使用并放在你的投资组合上。通过完成本课程，你将学到以下内容。
    
    React with Functional Components & Hooks
    
    React router
    
    React-Bootstrap UI library
    
    How to structure components
    
    Component level state & props
    
    Managing global state with Redux (Actions & Reducers)
    
    Using Redux state in components (useDispatch & useSelector)
    
    Creating an extensive back end with Express
    
    Working with a MongoDB database and the Mongoose ODM
    
    JWT authentication (JSON web tokens)
    
    Creating custom authentication middleware
    
    Custom error handler
    
    Integrating the PayPal API
    
    Environment variables
    
    Project deployment
    
    Much more!
    
    您将会学到什么
    
    Build a custom eCommerce platform with React, Redux, Node, Express & MongoDB 
    
    用React、Redux、Node、Express和MongoDB建立一个定制的电子商务平台
    
    An actual real-world project built in a linear and progressive manner 
    
    以线性和渐进的方式构建一个实际的真实世界项目
    
    Full featured shopping cart with PayPal & credit/debit payments
    
    具有PayPal和信用卡/借记卡支付功能的全功能购物车
    
    Admin area to manage customers, products & orders
    
    管理区可以管理客户、产品和订单
    
    Product rating & review system
    
    产品评级和评论系统
    
    Product search, carousel, pagination & more
    
    产品搜索、旋转木马、分页等功能
    
- 用通俗的语言介绍这个项目
    
    这是一个功能比较齐全的购物网站，首页会展示一些商品，每张商品卡片上有详细信息，顶部有搜索框进行模糊搜索。点开之后是商品详情页，可以查看详细信息，对其进行评论，或者选择数量，加入购物车。这里涉及到用户登录注册的问题，因此我实现了用户的认证和授权 Authentication 和 Authorization。加入之后呢，会跳转到购物车页面里，购物车中可以也进行产品的修改和删除，左侧会显示总的数量和总的价格。接下来的支付功能，我实现了微信支付和支付宝支付的接口。除此之外有一个对应的 admin 管理系统，可以对所以产品和用户进行增删改。除此之外还有一些小的功能，比如模糊搜索商品，显示top3的商品。大概就是这样
    
- 项目亮点
    1. 复杂度高，完成度高，全栈开发，功能完善，项目文件结构很清晰
    2. 对业务组件进行了抽象，比如 Messenger、Loder、搜索栏组件，抽离了一些开箱即用的组件
    3. 在项目技术选型上选取了比较流行的 mern 技术栈
    4. 对前端的性能优化有一定的实践，包括图片懒加载、资源预加载
    5. 部署在了云平台上面
    
    ![Untitled](Untitled.png)
    
- 项目难点
    1. 复杂度高，工作量大，全栈开发，很多功能的实现
    2. 对这种复杂的项目的结构的掌握，经常就是改了这个忘记改那个，比如给 redux 里的 action 加了参数，又忘了给 homeScreen 里面加上参数 
    3. 用户认证和授权
    4. Redux 的使用，概念抽象，步骤复杂，但我总结了一下
    5. 支付的 api
    6. 部署

### 项目细节

- MERN 技术栈
    
    MERN(MongoDB、Express、React、Node.js)技术栈是专门针 对 SPA 和 NoSQL 热潮而发展起来的早期开源技术栈之一。MERN 技 术栈中的 React 是 一个用来构建用户界面的 JavaScript 库。MongoDB 是一个流行的数据 存储 NoSQL 数据库。Node.js 是一个服务器端 JavaScript 运行环境，而 Express 是一个构建于 Node.js 之上的 Web 服务器
    
    1. 前端和后端开发之间进行自由切换的能力。mern 技术栈它全部使用的是同一个语言，无论在后端还是前端，都使用 JavaScript，所以只需熟悉一种语言，便可在客户端和服务器之间轻松切换，就可以高效开发一个完整的web应用，我们可以将JavaScript用于客户端和服务器端代码，甚至可以用它来编写MongoDB的数据库脚本
    2. 具有效率和生产率上的优势。所有这四种技术均基于框架中的Javascript和JSON(JavaScript Object Notation，对象表示法)数据，进而节省了消耗在潜在JSON编码上的时间。由于均栈里各种工具都可以在本地使用底层的JSON数据，因此Node + Express.js + MongoDB数据库的结合，为基于JSON的Web服务提供了出色的实现效果
    3. 鉴于其事件驱动的架构和无阻塞的I/O特点，Node.js在此成为了一种非常快速和灵活的Web服务器
    4. MERN栈提供了大量可供人们免费使用的 npm 软件包。即便它们无法完全满足您的需求，您也可以通过对其 fork，来制作出属于自己的 npm 软件包
- Express
    
    [Express detail](https://www.notion.so/Express-detail-6998fb67b6614fec9e6e500e6c190bff?pvs=21)
    
    [(190条消息) 一些基于nodejs的服务端框架对比。express、koa、egg、nest、midway_Nicker2013的博客-CSDN博客_egg express koa](https://blog.csdn.net/Nicker_/article/details/110881857)
    
    [express](https://so.csdn.net/so/search?q=express&spm=1001.2101.3001.7020)、koa、egg、nest、midway都是常见的nodejs开源框架。其关系，基本如下：
    
    ```jsx
    Midway.js ---|> Egg.js ---|> Koa.js,
                   Nest.js ---|> Express.js
    ```
    
    而koa实际上是 express 团队用新理念重写的，从[架构](https://so.csdn.net/so/search?q=%E6%9E%B6%E6%9E%84&spm=1001.2101.3001.7020)上讲，更加先进一些
    
    midway.js和egg.js背后都是阿里的团队，其架构基于koa
    
    nest.js背后是国外的Trilon团队，其架构基于express
    
    Express 是一个保持最小规模的灵活的 [Node](https://so.csdn.net/so/search?q=Node&spm=1001.2101.3001.7020).js Web 应用程序开发框架，为 Web 和移动应用程序提供强大的功能
    
    koa 是由 Express 原班人马打造的，致力于成为一个更小、更富有表现力、更健壮的 Web 框架。使用 koa 编写 web 应用，通过组合不同的 generator，可以免除重复繁琐的回调函数嵌套，并极大地提升错误处理的效率。koa 不在内核方法中绑定任何中间件，它仅仅提供了一个轻量优雅的函数库，使得编写 Web 应用变得得心应手
    
    nest 是一个封装了node的有规范的框架，什么是有规范？意思是必须按照它制定的一套规则来写代码，否则程序就会无法运行。上手成本稍高一点，但是后期维护与扩展会很方便，nest属于前端ts大趋势下深度使用注解特性并提供各种增强开发体验的框架，它提供了一套完整的解决方案，包含了认证、数据库、路由、http状态码、安全、配置、请求等开箱即用的技术
    
- MongoDB & Mongoose
    
    [https://blog.csdn.net/weixin_38601104/article/details/88367741](https://blog.csdn.net/weixin_38601104/article/details/88367741)
    
    [https://blog.csdn.net/qq_38721111/article/details/111074981](https://blog.csdn.net/qq_38721111/article/details/111074981)
    
    **Mongoose**
    
    它也是针对 mongoDB 操作的一个对象模型库，封装了 mongoDB 对文档的一些增删改查等常用方法，让 nodejs 操作 mongoDB 数据库变得更加容易
    
    **MongoDB** **主要特征：**
    
    - **NoSql数据库**：与一些关系型数据库相比，它更显得轻巧、灵活，缺点是不支持事务。非常适合在数据规模很大、事务性不强的场合下使用
    在 sql 中，我们的数据层级是：数据库（db）-> 表（table）-> 记录（record）-> 字段。在 mongodb 中，数据的层级是：数据库 -> 集合（collection）-> 文档（document）-> 字段，这四个概念可以对应得上
    - **面向文档存储的数据库**：操作起来比较简单和容易。将数据存储为一个文档，数据结构由键值对组成。这个文档就是 bson 格式，bson 是 json 的超集，比如 json 中没法储存二进制类型，而 bson 拓展了类型，提供了二进制支持
    - MongoDB 允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可
    - **分布式文件存储**：在高负载的情况下，添加更多的节点，可以保证服务器性能，保证海量数据存储的同时，具有良好的查询性能
    - **分片技术**：MongoDB 使用分片技术对数据进行扩展，MongoDB能自动分片、自动转移分片里面的数据块，去掉了关系型数据库的关系型特性，数据之间没有关系。让每一个服务器里面存储的数据都是一样大小。这样就非常容易扩展
    - **内嵌数据库**：表与表之间没有联系，好处就是查关联数据的时候比较方便，坏处就是数据可能不统一，不像 sql 中一样，可以设定外键，可以进行表连接
    
    **和其他 nosql 数据库的对比：**
    
    hbase 、redis 、mongodb 虽然都属于 nosql 的大范畴。但它们关注的领域是不一样的。hbase 是存海量数据的，redis 用来做缓存，而 mongodb 则试图取代一些使用 mysql 的场景
    
- MongoDB 的操作
    
    [MongoDB 索引 | 菜鸟教程 (runoob.com)](https://www.runoob.com/mongodb/mongodb-indexing.html)
    
    ```jsx
    显示所有数据库
    show databases
    
    创建数据库 
    use Products
    
    查看数据库 
    db
    
    显示所有集合 
    show collections
    
    创建集合 插入文档数据
    1. 插入文档数据时创建 
    db.Name.insert(doc)
    2. 直接创建 
    db.createCollection('新建集合名')
    
    插入文档数据 
    db.Name.insert(doc) 
    db.users.insert({name:'jack',age:18})
    
    查看所有数据 
    db.users.find() 
    
    查看name是jack的数据 
    db.users.find({name:'jack'})
    
    修改数据 
    db.users.update({name:'jack'},{$set:{age:28}})
    
    删除文档数据 
    db.users.remove({name:'jack'})
    
    删除集合 
    db.users.drop()
    
    删除数据库 
    db.dropDatabase()
    ```
    
    索引
    
    ```jsx
    1、查看集合索引
    db.col.getIndexes()
    
    2、查看集合索引大小
    db.col.totalIndexSize()
    
    3、删除集合所有索引
    db.col.dropIndexes()
    
    4、删除集合指定索引
    db.col.dropIndex("索引名称")
    
    5、创建索引
    db.col.createIndex({"title":1,"description":-1})
    ```
    
- Mongoose 的操作
    1. 导出
    2. 创建 schema：
        
        Schema 是 mongoose 里会用到的一种数据模式，是对 ducument 结构的定义，每个 schema 会映射到 mongodb 中的一个 collection，它不具备操作数据库的能力，仅仅只是定义数据库模型
        
    3. 创建 model：
        
        model是由schema生成的模型，可以对数据库的操作
        
    4. 进行增删查改的操作
    
    ```jsx
    1. const mongoose = require("mongoose");导入mongoose模块
    
    2. 连接数据库 // 注意url地址最后面的地址是数据库的名称
        const url = "mongodb://127.0.0.1:27017/bk1824";
    
            mongoose.connect(url,(err)=>{
                    if(err){
                        console.log("链接失败")
                    }else{
                        console.log("链接成功")
                    }
            })
    
    2. 创建文档结构schema
            const UserSchema = new db.Schema({ 
                username: String,
                password: String,
                nick: String,
                headerimg: String,
            })
    
    3. 创建 model
    const userModel = new db.model('user', UserSchema, 'user')  
    
    5.添加数据
            const { username, password, nick } = req.body // 接收参数
            let user = new UserModel({
                username,
                password,
                nick,
                headerimg,
            })
            
    6. 将增加的数据存入数据库的表中
        user.save() // 保存数据到db
    
    7. 删除数据
            User.remove({username:"zhao1234"})
    
    8. 改数据
            User.update({username:"1111"},{$set:{username:"zhao"}})
    
    9.. 查数据
            const { username, password } = req.body
            let data = await UserModel.find({username,password})
    ```
    
- Redux 的实现
    
    可以理解为把需要多个组件共享的变量全部存储在一个对象里面，把这个对象放在顶层的 react 实例当中，让其他组件可以使用
    
    **使用情景：**
    
    - 大型开发，多个界面间的共享问题
    - 比如用户的登录状态、拿到和保存 token、用户名称、头像、地理位置信息等等
    - 比如商品的收藏、购物车中的物品（在很多页面都有添加购物车的功能）
    - 这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的
    
    **实现方法：**
    
    顶层套一个 provider，底层的组件都可以使用顶层的数据
    
    1. 首先，用户（通过View）发出 Action，发出方式就用到了 dispatch 方法。
    2. 然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action，Reducer 会返回新的 State
    3. State 一旦有变化，Store 就会调用监听函数，来更新 View
    
    Product reducer
    
    ![Untitled](Untitled%201.png)
    
    Product Actions
    
    ![Untitled](Untitled%202.png)
    
    User Reducer
    
    ![Untitled](Untitled%203.png)
    
    User Actions
    
    ![Untitled](Untitled%204.png)
    
- 中间件 middleware 的使用
    
    中间件就是处理 HTTP 请求的函数。它最大的特点就是，一个中间件处理完，再传递给下一个中间件
    
    每个中间件可以从 App 实例里接收三个参数，依次为 request 对象（HTTP 请求）、response 对象（HTTP 回应），next() 回调函数（下一个中间件）。每个中间件都可以对 HTTP 请求（request 对象）进行加工，并且决定是否调用 next() 方法，将 request 对象再传给下一个中间件
    
    **anthMiddleware.js**
    
    1. 从 header 里面的 authorization 头里面的信息拿到 token
    2. 通过 jwt.decode(token,secret)，来解析 token，解析出来的信息打印出来就是下面的 json，于是就可以拿到 id
        
        ```jsx
        {
            id: '5f6bf78dqi0w',
            iat: 1600978514,
            exp: 1600978514
        }
        ```
        
    3. 通过 id 查找用户，返回除了密码以外的信息
- location 和 history 的使用
    
    在 react 组件的 componentDidMount 方法中打印一下 this.props，在浏览器控制台中查看输出如下，其中页面的 url 信息全都包含在 match 字段中
    
    ```jsx
    localhost:3000/app/knowledgeManagement/modify
    /STY20171011124209535/3/1507701970070/0/?s=1&f=7
    ```
    
    ![Untitled](Untitled%205.png)
    
    ![Untitled](Untitled%206.png)
    
    - **match：**包含了具体的 url 信息，在 params 字段中可以获取到各个路由参数的值
    - **history：**包含了组件可以使用的各种路由系统的方法，常用的有 push 和 replace，两者都是跳转页面，但是 replace 不会引起页面的刷新，仅仅是改变 url
    - **location：**相当于 URL 的对象形式表示，通过 search 字段可以获取到 url 中的 query 信息，所以location.search 是获取 url 参数的方法
    这里 state 的含义与 HTML5 history.pushState API 中的 state 对象一样。每个 URL 都会对应一个 state 对象，你可以在对象里存储数据，但这个数据却不会出现在 URL 中。实际上，数据被存在了 sessionStorage 中
    
- 身份认证的实现
    
    分成两个方面吧，一个是身份认证，一个是授权，Authentication 和 Authorization
    
    **认证**(Authentication)，我们接受电子邮件和密码，在数据库中对其进行认证，证明是这个用户本人。**授权**(Authorization)，是让这个用户有权限访问某些信息，或者使用受到保护的 API 的权限，这个通过发送 Json Web Token来做到这一点
    
    **普通用户认证：**
    
    (1) 为了密码的安全，我使用了 bcrypt 这个包，注册的时候通过 bcrypt.hash 把密码保存在数据库里，在登录的时候用 bcrypt.compare 的方法来比较输入的这个文本字符串和数据库中加密过的密码是不是一样的
    
    (2) 登录的时候，会使用 authUser 这个接口，在这个接口里面，如果匹配成功了，返回 userInfo，存储在 redux 的 store 里面，是一个全局的状态 (将 userInfo 存进 localstorage 里面去)
    
    (3) 前端的处理就是在登录页面，把 userInfo 注册在 useEffect 这个 hook 里面随时检测更新，如果收到有返回的用户信息了，就跳转到首页
    
    **授权：**
    
    (1) 后端，在登录的时候，引入了 jsonwebtoken 的库，下载Openssl，下载后生成私钥。使用 jwt.sign 的方法通过一些用户信息和私钥生成一个 token(RS256 加密算法)，那这个 token 放在哪个位置呢，就是用户身份认证成功之后返回的 user 信息里的那个 json 文件里。于是在用户成功登录之后，我们就可以在保存在 redux 里面的 userInfo 这个对象里面得到了 token
    
    (2) 前端，在需要调用一些受到保护的 api 的时候，前端会使用 getState() 的方法从 redux 里面拿到这个 token，然后封装在 header 的 Authorization 头部，再对这个接口发起 http 请求
    
    ![Untitled](Untitled%207.png)
    
    **Admin 权限的认证：**
    
    添加了一个 authAdmin 的中间件，就是判断一下
    
    ![Untitled](Untitled%208.png)
    
    在 userRoutes.js 里面注册这个 api 的时候，执行函数前面要加上 protect 和 admin 两个中间件，admin 放在 protect 中间件后面，就表示首先登录，再验证是否有 admin 的权限，只有都满足，才能调用这个 api
    
    ![Untitled](Untitled%209.png)
    
- 支付宝 api
    
    [(225条消息) Node.js接入支付宝（蚂蚁金服）支付_nj物是人非的博客-CSDN博客](https://blog.csdn.net/njweiyukun/article/details/79478455?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-79478455-blog-113250029.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-17-79478455-blog-113250029.pc_relevant_default&utm_relevant_index=18)
    
    [NodeJS 支付宝网站支付 Demo 开发 - 掘金 (juejin.cn)](https://juejin.cn/post/6844903984478552078)
    
    前端页面 -> 向服务端发送订单信息 -> 服务端确认信息，向客户端发送确认信息 -> 客户端确认信息向服务端发送订单请求 -> 服务端验证订单请求信息 -> 服务端像支付宝发送订单生成 -> 支付宝向服务端返回订单数据 -> 服务端向客户端发送支付宝的表单信息 -> 客户端跳转到支付宝支付页面 -> 客户端支付成功 -> 支付宝让客户端同步跳转到服务端指定的页面 -> 支付宝异步通知服务端订单支付结果 -> 服务端接收异步通知做相应的业务处理
    
    ![Untitled](Untitled%2010.png)
    
- 前端的性能优化
    
    ![Untitled](Untitled.png)
    
- 商品模糊搜索的实现
    
    正则表达式是使用几个简单的字符串来描述和匹配一系列符合某个句法规则的字符串
    
    MongoDB 使用 $regex 操作符来设置匹配字符串的正则表达式，比如搜索 iph 就可以搜到 iphone，搜 ar 就可以搜到 airpords，设置 $option = “$i”，就可以不区分大小写
    
    ![Untitled](Untitled%2011.png)
    
- TOP3 的实现
    
    Product.find({}).sort({rating:-1}).limit(3)
    
- Admin 后台管理怎么实现
- 部署在 horuku 上面具体实现
    
    *Heroku* 是一个支持多种编程语言的云平台
    
    > 为什么要用云平台？
    > 
    > 
    > ——云平台不用租域名不用租服务器不用备案不用自己手动配置各种软件，而且是免费的。
    > 
    
    > 云平台有什么缺点？
    > 
    > 
    > 缺点就是流量限制一般比较严，性能相对较差。但是就我自己的实际使用经验来看，一般的小站或者个人博客放在云平台上是完全够用的。并且云平台会提供无缝扩展的服务，如果需要更高性能或者更多流量可以花钱扩展。还有一点就是云平台的域名是二级域名，如果您想使用自己的域名的话，可以通过alias别名设置。
    > 
    
    > 为什么要用国外的云平台？
    > 
    > 
    > 国内的云平台我个人总结有两大缺点：1、文档不完善，2、限制较多
    > 
    > 文档不完善就导致了新手很难入门，往往会遇到各种各样的问题难以解决。国外的云平台文档非常完善，并且有很多示例，只要你懂一些基本的英文就可以轻松搞定。限制较多主要体现在开发者认证以及开发环境这两方面。新浪云和百度云都需要申请开发者认证，我自己是很讨厌这种方式的。开发环境限制就是版本旧，自由度低。
    > 
    
    > 为什么要用heroku？
    > 
    > 
    > 国外的云平台，我自己也试用过几个。因为国外的云平台文档大多很完善，所以不存在使用障碍，选择的标准就变成了适不适合自己。因为我使用的是express框架，所以对比之下发现heroku对JavaScript的支持更好，并且官方就有部署JavaScript的示例，所以选择了heroku。实际应用中发现确实很不错
    > 
    
    > 步骤？
    > 
    > 1. npm run build → 生成一个build包
    > 2. 下载 Heroku CLI，通过 heruko login 进行登录
    > 3. 创建一个新项目 heroku create projname，这时候就会生成一个以 [https://projname.herukoapp.com](https://projname.herukoapp.com) 的网址，点开是新项目的欢迎页面
    > 4. 创建 Procfile 文件：Heroku 需要一个 Procfile 才能知道如何运行应用程序，Procfile 是一个“进程文件”，用于告诉 Heroku 运行哪个命令来管理给定的进程，比如告诉 Heroku 如何在 Web 上启动服务器进行监听，没有 Procfile，Heroku 就不能让服务器在线
    > 5. 使用 git add commit push，添加和提交文件
    > 6. 在 Heroku 网站的 setting 里配置 .env 文件的参数，包括数据库、jwt_secret，端口号等等
    - 我在部署中就遇到了打不开网站的情况，错误日志如下，经排查发现代码中打开端口的时候写死了6789，所以导致报错，heroku推荐用$port的方式绑定端口，而不是写死某一个端口
    - heroku buildpacks:set heroku/python #显示指定用python来构建打包，这个非常重要，没有这句会报以下错误
    
    ![Untitled](Untitled%2012.png)
    

### 支付的实现

- 教程
    
    [https://www.bilibili.com/video/BV1ZT4y1c7iL?p=3&spm_id_from=pageDriver&vd_source=a314bfb0589f50a82d60a44b2d833d8a](https://www.bilibili.com/video/BV1ZT4y1c7iL?p=3&spm_id_from=pageDriver&vd_source=a314bfb0589f50a82d60a44b2d833d8a)
    
- 前期准备，账号申请
    
    **微信公众账号：**必须有企业认证过的公众账号，个人是不能申请微信支付的
    
    **微信商户平台：**需要一个商户平台账号，也是要企业主体的，当我们申请完之后微信官方会给我们发一封邮件，包含了账号信息
    
    ![Untitled](Untitled%2013.png)
    
    **支付宝商户平台：**需要一个支付宝商户平台账号
    
    **备案过的域名：**已经在工信部备案通过的域名
    
    **服务器：**需要一个具有外网 ip 的服务器，用来部署项目
    
- 服务器配置
    
    
- 微信 API 的官方文档研究
    
    **这里用到的是 native 支付方式：**
    
    就是二维码 
    
    ![Untitled](Untitled%2014.png)
    
    **使用的是统一下单 API 流程：**
    
    1. 后台系统根据用户选购的商品生成订单
    2. 用户确认支付后调用微信支付的**统一下单API**生成预支付
    3. 微信支付系统收到请求后，如果成功会返回 code_url 就是二维码的链接，当我们拿到这个 code_url 只需要把这个二维码生成，在页面上展示就可以
    4. 用户扫描二维码付款
    
    ![Untitled](Untitled%2015.png)
    
    ![Untitled](Untitled%2016.png)
    
    **统一下单 api 请求参数介绍：**
    
    其中比较复杂的是签名的生成算法和随机数生成算法
    
    ![Untitled](Untitled%2017.png)
    
    把这些信息拼接成一个 xml 字符串
    
    ![Untitled](Untitled%2018.png)
    
    **统一下单 API 的返回信息：**
    
    ![Untitled](Untitled%2019.png)
    
    ![Untitled](Untitled%2020.png)
    
    **下面是一些错误信息的描述：**
    
    ![Untitled](Untitled%2021.png)
    
    **下面介绍签名算法：分为两步**
    
    第一步，把所有参数按照顺序拼接成 URL 的格式
    
    第二步，在拼接好的字符串后面，拼接商户密钥（微信商户平台的密钥设置得到），用MD5的方法加密
    
    ![Untitled](Untitled%2022.png)
    
    ![Untitled](Untitled%2023.png)
    
- 微信 API 对接实战
    
    **对接接口，拼接xml**
    
    ![Untitled](Untitled%2024.png)
    
    使用qs模块做字符串拼接
    
    ![Untitled](Untitled%2025.png)
    
    通过axios调用接口
    
    ![Untitled](Untitled%2026.png)
    
    **支付接口的实现：**
    
    使用 mongoose 创建 order 的 schema
    
    ![Untitled](Untitled%2027.png)
    
    **实现接口：**
    
    成功之后可以生成一个二维码
    
    ![Untitled](Untitled%2028.png)
    
    现在的效果：
    
    ![Untitled](Untitled%2029.png)
    
    处理 code_url 生成二维码，使用 qrcode 的包
    
    ![Untitled](Untitled%2030.png)
    
    1. 微信开发服务器验证
    2. 微信登录授权获取 openid
    3. 微信 jsapi 签名认证
    4. 微信支付接口签名
    5. 公众账号调用支付 api
- 支付宝 API 对接
    
    ![Untitled](Untitled%2031.png)
    
    ![Untitled](Untitled%2032.png)
    
    ![Untitled](Untitled%2033.png)
    
    开发工具生成私钥和公钥
    
    ![Untitled](Untitled%2034.png)
    
    配置 sdk
    
    ![Untitled](Untitled%2035.png)
    
    ![Untitled](Untitled%2036.png)
    
    ![Untitled](Untitled%2037.png)
    
    ![Untitled](Untitled%2038.png)
    
    ![Untitled](Untitled%2039.png)
    
    ![Untitled](Untitled%2040.png)
    
    1. 支付宝证书生成
    2. 支付宝服务器端 sdk 对接
        1. 页面效果实现

### 1️⃣ 搭建前端页面

- 1. 新建 React 项目
    
    create react app
    
    ![Untitled](Untitled%2041.png)
    
    regular function & arrow function
    
    ![Untitled](Untitled%2042.png)
    
    ![Untitled](Untitled%2043.png)
    

### 2️⃣ 从Epress框架获取数据

- 1. 后端简单接口，跑起来
    
    下载 express 框架
    
    ```jsx
    npm install express --save
    ```
    
    创建 backend 文件夹，创建 server.js 文件，然后写一点简单的代码尝试
    
    ![Untitled](Untitled%2044.png)
    
    运行下面的命令，可以把这个程序在 5000 端口跑起来
    
    ```jsx
    npm backend/server.js
    ```
    
    打开 [localhost:5000](http://localhost:5000) 看到已经跑起来了
    
    ![Untitled](Untitled%2045.png)
    
    引入 product datas，再写两个接口
    
    ![Untitled](Untitled%2046.png)
    
    ![Untitled](Untitled%2047.png)
    
    ![Untitled](Untitled%2048.png)
    
- 2. 前端获取产品的数据 (useState useEffect axios)
    1. **配置环境**
    
    import axios, a http library
    
    ```jsx
    npm install axios
    ```
    
    配置 proxy
    
    ![Untitled](Untitled%2049.png)
    
    1. **连接 home screen**
    
    引入 product state
    
    ![Untitled](Untitled%2050.png)
    
    useEffect 的作用是想在这个 component load 的时候执行这个 arrow function
    
    ![Untitled](Untitled%2051.png)
    
    1. **连接 product detail screen**
    
    ![Untitled](Untitled%2052.png)
    
    如何把 product 的信息显示出来呢
    
    ![Untitled](Untitled%2053.png)
    
- 3. 配置 Nodemon Concurrently
    
    import both
    
    ```jsx
    npm install -D nodemon concurrently
    ```
    
    ![Untitled](Untitled%2054.png)
    
    **Nodemon** is a tool that we can use to constantly watch our server so that we dont have to resetting it.  就是说他会自动监听到你后端的变化，所以当你有任何的改动代码时，不用重新启动后端
    
    ![Untitled](Untitled%2055.png)
    
    **Concurrently** 可以同时把前端和后端跑起来，不用分开跑
    
    ![Untitled](Untitled%2056.png)
    
    所以现在只需要运行 `npm run dev` 命令就可以
    
- 4. 配置 .env 文件
    
    To put any API key or stuff like that, any secert token, database strings, database password, and any secerts you want to put in here
    
    要把端口号，任何 API 密钥，或者任何 secret token，数据库字符串，数据库密码，开发模式，以及任何你想放在这里的 secret 放进去
    
    在**根目录(不是backend也不是frontend)**新建 `.env` 文件
    
    ![Untitled](Untitled%2057.png)
    
    在 `server.js` 中使用定义的环境变量 import dotenv
    
    ![Untitled](Untitled%2058.png)
    
    ![Untitled](Untitled%2059.png)
    
- 6. ES module in Node.js
    
    修改模块导入部分
    
    common js : const express = require(’express’)
    
    ES : impor … from …
    
    ![Untitled](Untitled%2060.png)
    
    修改模块导出部分
    
    common js : module.export = products
    
    ES: export defalut products
    
    ![Untitled](Untitled%2061.png)
    
    ![Untitled](Untitled%2062.png)
    

### 3️⃣ 配置 Mongo DB

- 1. Mongodb 官网配置，下载 Compass
    
    **进入官网并登录账号**
    
     [https://www.mongodb.com/](https://www.mongodb.com/) 
    
    ![Untitled](Untitled%2063.png)
    
    ![Untitled](Untitled%2064.png)
    
    **设置 security informations**
    
    包括 database access 和 network access
    
    ![Untitled](Untitled%2065.png)
    
    ![Untitled](Untitled%2066.png)
    
    **下载 compass**
    
    compass 是桌面的 gui 软件，可以用来连接database和管理数据
    
    ![Untitled](Untitled%2067.png)
    
    **添加表和数据**
    
    点击collections → add my own data
    
    ![Untitled](Untitled%2068.png)
    
    **把数据连接到本地的 compass**
    
    ![Untitled](Untitled%2069.png)
    
    复制这个connection string
    
    ![Untitled](Untitled%2070.png)
    
    粘贴到 compass，然后把密码填写成自己的密码，test改成自己的数据库名
    
    ![Untitled](Untitled%2071.png)
    
    连接成功
    
    ![Untitled](Untitled%2072.png)
    
    **连接 mongo db 到项目里**
    
    点击第二个 connect your application
    
    ![Untitled](Untitled%2073.png)
    
    同样是复制这个connection string
    
    ![Untitled](Untitled%2074.png)
    
    然后 copy 进 .env file
    
    ![Untitled](Untitled%2075.png)
    
- 2. 用 mongoose ****连接 Mongo DB
    
    **下载 mongoose**
    
    Mongoose 是一个让我们可以通过 Node 来操作 MongoDB 数据库的一个模块
    Mongoose 是一个对象文档模型（ODM）库，它是对 Node 原生的 MongoDB 模块进行了进一步的优化封装。大多数情况下，他被用来把结构化的模式应用到一个 MongoDB 集合，并提供了验证和类型装换等好处，基于MongoDB驱动，通过关系型数据库的思想来实现非关系型数据库
    
    ![Untitled](Untitled%2076.png)
    
    ```jsx
    npm install mongoose
    ```
    
    **写配置文件**
    
    在后端文件夹新建 config 文件夹，新建 db.js 文件
    
    使用 `mongoose.connect(MONGO_URL)` 的方法来连接
    
    ![Untitled](Untitled%2077.png)
    
    然后在 server 引入
    
    ![Untitled](Untitled%2078.png)
    
- 3. 用 mongoose 创建 ****Schema 和 modal
    
    通过 `Schema` 创建 `Model`
    
    Model 代表的是数据库中的集合，通过 Model 才能对数据库进行操作
    
    首先在 backend 目录下创建 **model** 文件夹，里面装的是三个数据表的schema，是通过 `moogose.Schema({})` 的方法创建的，然后用 `mongoose.modal(name, schema)` 的方法创建 modal
    
    **userModel**
    
    ![Untitled](Untitled%2079.png)
    
    ![Untitled](Untitled%2080.png)
    
    ```jsx
    import mongoose from 'mongoose';
    
    const userSchema = new mongoose.Schema(
      {
        name: { type: String, required: true },
        email: { type: String, required: true, unique: true },
        password: { type: String, required: true },
        isAdmin: { type: Boolean, default: false, required: true },
        isSeller: { type: Boolean, default: false, required: true },
        seller: {
          name: String,
          logo: String,
          description: String,
          rating: { type: Number, default: 0, required: true },
          numReviews: { type: Number, default: 0, required: true },
        },
      },
      {
        timestamps: true,
      }
    );
    const User = mongoose.model('User', userSchema);
    export default User;
    ```
    
    **peoductModel**
    
    ```jsx
    import mongoose from 'mongoose';
    const reviewSchema = new mongoose.Schema(
      {
        name: { type: String, required: true },
        comment: { type: String, required: true },
        rating: { type: Number, required: true },
      },
      {
        timestamps: true,
      }
    );
    const productSchema = new mongoose.Schema(
      {
        name: { type: String, required: true, unique: true },
        seller: { type: mongoose.Schema.Types.ObjectID, ref: 'User' },
        image: { type: String, required: true },
        brand: { type: String, required: true },
        category: { type: String, required: true },
        description: { type: String, required: true },
        price: { type: Number, required: true },
        countInStock: { type: Number, required: true },
        rating: { type: Number, required: true },
        numReviews: { type: Number, required: true },
        reviews: [reviewSchema],
      },
      {
        timestamps: true,
      }
    );
    const Product = mongoose.model('Product', productSchema);
    
    export default Product;
    ```
    
    **orderModel** 
    
    ```jsx
    import mongoose from 'mongoose';
    
    const orderSchema = new mongoose.Schema(
      {
        orderItems: [
          {
            name: { type: String, required: true },
            qty: { type: Number, required: true },
            image: { type: String, required: true },
            price: { type: Number, required: true },
            product: {
              type: mongoose.Schema.Types.ObjectId,
              ref: 'Product',
              required: true,
            },
          },
        ],
        shippingAddress: {
          fullName: { type: String, required: true },
          address: { type: String, required: true },
          city: { type: String, required: true },
          postalCode: { type: String, required: true },
          country: { type: String, required: true },
          lat: Number,
          lng: Number,
        },
        paymentMethod: { type: String, required: true },
        paymentResult: {
          id: String,
          status: String,
          update_time: String,
          email_address: String,
        },
        itemsPrice: { type: Number, required: true },
        shippingPrice: { type: Number, required: true },
        taxPrice: { type: Number, required: true },
        totalPrice: { type: Number, required: true },
        user: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
        seller: { type: mongoose.Schema.Types.ObjectID, ref: 'User' },
        isPaid: { type: Boolean, default: false },
        paidAt: { type: Date },
        isDelivered: { type: Boolean, default: false },
        deliveredAt: { type: Date },
      },
      {
        timestamps: true,
      }
    );
    const Order = mongoose.model('Order', orderSchema);
    export default Order;
    ```
    
- 4. 伪造一些简单的数据  bcryptjs
    
    关于用户的密码使用 bcryptjs
    
    ```jsx
    npm i bcryptjs
    ```
    
    下面是伪造好的一些数据：
    
    ![Untitled](Untitled%2081.png)
    
    ![Untitled](Untitled%2082.png)
    
- 5. 数据 Seeder 批量导入脚本
    
    把 json 里的数据导入到数据库里面去
    
    ![Untitled](Untitled%2083.png)
    
    ![Untitled](Untitled%2084.png)
    
    定义另一个 destroy 所有数据的方法 && 如何定义命令行的快捷指令：
    
    ![Untitled](Untitled%2085.png)
    
    刷新之后，可以看到数据库本来是空的，现在已经导入了
    
    ![Untitled](Untitled%2086.png)
    
- 6. 后端新建 route 文件，封装 server.js 中的 api
    
    首先在后端文件夹里，新建  route 文件夹，存放 api
    
    把 server.js 里的 api 复制过去
    
    ![Untitled](Untitled%2087.png)
    
    把app.get 改成 route.get
    
    ![Untitled](Untitled%2088.png)
    
    然后，在 server.js 里面，把跟/api/products 相关的api，跟 productRoutes 这个 route 关联起来
    
    ![Untitled](Untitled%2089.png)
    
    所以 `app.get('/api/products/',()=>{})` 相当于 
    
    `app.use('/api/products', productRoutes )` +  productRoutes 文件夹中的   `route.get('/',()=>{})`
    
- 7. 从 MongoDB 中获得数据
    
    关于 express-async-handler，用来错误处理：
    
    ![Untitled](Untitled%2090.png)
    
    用 asyncHandler包裹函数
    
    - getAllProduct api
        
        ![Untitled](Untitled%2091.png)
        
    - getProductById api
        
        ![Untitled](Untitled%2092.png)
        
    
    ⭐所以在 mongodb里面获取数据是用 `.find`  或者 `.findById`
    
- 8. 创建 Error Handler 的 node 中间件
    
    server.js 里面 app.use 表示使用中间件
    
    ![Untitled](Untitled%2093.png)
    
    效果
    
    ![Untitled](Untitled%2094.png)
    
    为了让代码看起来简约，我们新建 middleware 文件夹，把这个错误处理的 middleware 放在文件夹里
    
    ![Untitled](Untitled%2095.png)
    
    然后在 serverjs 里面引入
    
    ![Untitled](Untitled%2096.png)
    
    ![Untitled](Untitled%2097.png)
    

### 4️⃣ 引入 Redux 状态管理

- 1. Redux 介绍
    
    state 的属性有两种，一种是组件 level，一个是全局 level ，redux 是针对于整个应用的全局性的 state 管理。 比如在我们项目中的 product 这个 state，我们在项目中会在不同的组件当中都用到这个 state，可能是更新、添加、删除这样，你希望 product 是对所有的组件都 available 的。另一个例子是经过身份验证的 user，当我们登录之后，购物车物品，订单之类的都需要对这个 user 的 state 进行操作
    
    ![Untitled](Untitled%2098.png)
    
    改变 state 的方式是通过 reducer 或 reduce 或函数，基本上，除了 Actions，它只是一些函数，它们负责操作并将 state 传递给组件。现在，Action 只是代表改变这个 state 的意图的对象。我们也有 action creator，他们是将 dispatch 或 fire off 这些 action 的函数
    
    举个例子，我们可能有一个名为 Get Products 的 action creator function 。在这个 action creator 中，我们向后端发出一个功能请求，使用 Axios 或 Fetch API 或其他方式获取数据。然后我们得到这些数据，然后我们 dispatch  一个 action 到 reducer，并附加一个 payload。该 payload 将包含获取的数据
    
    现在在 reducer 中，我们可以将 payload 数据分配给 state，我们可以将其传递给任何需要它的组件。好的，所以我们可以有多个组件要求得到同一块 state。所以， 把 state 想成是盘旋在你的应用程序上的一朵云。当我们需要发生一些事情时，比如说我们想点击一个按钮，从服务器上获取一些数据，然后显示出来，我们必须创建一个 action 或一个  action creator，将一个特定的动作 dispatch 给 reducer，然后 reducer 将其传递给组件
    
    同样，我知道这听起来可能超级混乱。我在理论上解释redux和看图说话时总是遇到困难，但当我们开始跳入代码并看到它的实际工作时，大多数人真的倾向于掌握它
    
    **之前系统学的时候的一些笔记：**
    
    **简介**
    
    专门针对 react 所设计的状态管理工具，顶层套一个 provider，底层的组件都可以使用顶层的数据
    
    ![Untitled](Untitled%2099.png)
    
    ```python
    npm i redux react-redux
    ```
    
    **简单使用**
    
    需要在项目里新建文件夹 store，里面有 
    
    - 左：index.js (仓库的入口文件)
    - 右：reduce.js (创建初始状态，并导出一个函数)
    
    ![Untitled](Untitled%20100.png)
    
    修改组件
    
    - 修改 src/index.js 添加 **provider**
    - 修改 app componant，添加 **connect**，定义状态映射（将 reducer 中的 state 映射成 props，让开发者可以在组件中使用 props.num 去调用 state 中的 num），传入参数props
    
    ![Untitled](Untitled%20101.png)
    
    ## 2.2 mapState vs mapDispatch
    
    **mapState**：状态映射，将 reducer 中的 state 映射成 props，让开发者可以在组件中使用 props.num 去调用 state 中的 num
    
    **mapDispatch**：事件派发映射，将 reducer 中的事件映射成 props，让开发者可以在组件中使用 props.add() 去实现 num 的累加
    
    ![Untitled](Untitled%20102.png)
    
    注意：左图的reduce.js文件里面，比起 if 判断，一般还是常用 switch
    
- 2. 在 src 目录下新建文件 store.js，createStore
    
    在 frontend 文件夹下安装 redux 以及相关的中间件和插件
    
    ```sql
    npm i redux react-redux redux-thunk redux-devtools-extension
    ```
    
    ![Untitled](Untitled%20103.png)
    
    在 src 目录下新建文件 store.js ，这里是我们连接 reducers 和一些 middleware 的地方
    
    ![Untitled](Untitled%20104.png)
    
    在 src 的 index 目录下 引入 provider 和 store，用 provider 标签包裹 App 标签
    
    ![Untitled](Untitled%20105.png)
    
    PS：之前包裹 app 的是这个
    
    ![Untitled](Untitled%20106.png)
    
- 3. 创建 Product list 的 Reduce & Action
    
    **创建 Reducers**
    
    在 frontend 的 src 目录创建 reducers 文件夹
    
    基本上我们应用程序的每个资源都会有一个 reduce，比如产品。所以在 reducers 文件夹里创建一个 `productReducers.js` 文件，然后在这个文件里，创建 `productListReducer`
    
    创建 Reducer 是一个箭头函数，传入的参数是 state 和 action
    
    ![Untitled](Untitled%20107.png)
    
    在 store 中引入 productList，放到 combineReducers 里面去
    
    ![Untitled](Untitled%20108.png)
    
    现在已经可以在浏览器插件里看到 state 了，虽然它还是空的
    
    ![Untitled](Untitled%20109.png)
    
    **创建 Actions**
    
    在 frontend 的 src 目录创建 actions 文件夹，在 actions 文件夹里创建一个 `productActions.js` 文件，然后在这个文件里，创建 `ListProducts`
    
    ![Untitled](Untitled%20110.png)
    
    PS: 现在这个 ListProducts action 要做的事情和我们之前在 HomeScreen 组件的使用效果中做的差不多 👇 We're going to do it through this action and we're going to dispatch actions to the reducer.
    
    ![Untitled](Untitled%20111.png)
    
- 4. 在 HomeScreen 里引入 Product list 的 Redux
    1. 把之前的 local state 的 product 删掉，因为我们不需要再把 product 设置为我们的 loacal state 或我们的 component level state，我们需要从 Redux 中把它带进来
    2. 把 axios 删掉，因为已经交给 action 去处理了
    3. 引入 hooks **useDispatch**，会被用来 dispatch or call in action
        
        PS：在过去，我们会使用一个叫做 Connect 的高阶方法，我们把 state 映射到 props 上，现在这种 useDispatch 方法更加简单
        
    4. 引入 hooks **useSelector**，用来选择部分需要的 state，我们将想要 product list 中的部分状态
    
    ![Untitled](Untitled%20112.png)
    
    修改 homePage 的页面，设置 loading/error/正常 三种状态的显示
    
    ![Untitled](Untitled%20113.png)
    
- 5. 在主页添加 Loading 和 Message 组件
    
    刚刚在 homePage 的页面，设置 loading/error/正常 三种状态的显示，现在来细化 loading/error 的显示
    
    在 component 中创建 Loader.js
    
    ![Untitled](Untitled%20114.png)
    
    在 component 中创建 Message.js
    
    ![Untitled](Untitled%20115.png)
    
    修改 homeScreen 中的组件
    
    ![Untitled](Untitled%20116.png)
    
- 6. 创建 Product detail 的 Reduce & Action (对应3)
   并在 productScreen 里引入 Product dtail 的 Redux (对应4)
    
    **可作为以后创建其他 redux state 的 general 流程**
    
    1. 在 constant 文件里面添加相应的 action.type
        
        ![Untitled](Untitled%20117.png)
        
    2. 在 Reducers 文件夹 的 productReducers 里面创建新的 productDetailsReducer
        
        ![Untitled](Untitled%20118.png)
        
    3. 进入 store 文件，在 combineReducers 里面引入这个新建的 productDetailsReducer
        
        ![Untitled](Untitled%20119.png)
        
    4. 在 action 文件夹中的 productActions.js 中，新建 listProductDetails 这个 action creator function
        
        ![Untitled](Untitled%20120.png)
        
    5. 进入 productScreen，跟上面的(3)和(4)做一样的操作
        
        ![Untitled](Untitled%20121.png)
        
        ![Untitled](Untitled%20122.png)
        

### 5️⃣ 添加购物车

- 1. 选择添加到购物车 item 数量，实现 add 按钮事件
    
    实现效果
    
    ![Untitled](Untitled%20123.png)
    
    实现选择 qty 的下拉菜单，如果 product 的 countInStock 数据还大于 0，则显示这个选择 qty 的下拉框，并且把 countInStock 的数量 map 为多个 option
    
    ![Untitled](Untitled%20124.png)
    
    实现这个 button 的 onclick 函数
    
    ![Untitled](Untitled%20125.png)
    
- 2. 添加到购物车的 reducer & action
    
    跟之前的步骤一样
    
    1. 创建 cartConstant.js 文件
        
        ![Untitled](Untitled%20126.png)
        
    2. 创建 cartReducers.js 文件夹，添加 add_to_cart reducer
        
        ![Untitled](Untitled%20127.png)
        
    3. 在 store.js 里面注册这个 reducer
        
        ![Untitled](Untitled%20128.png)
        
    4. 在 actions 文件夹里创建 cartActions.js，新建 addToCart Action，在 action 的 payload 里面返回查找到的商品对象，并且保存在 localStorage 中
        
        ![Untitled](Untitled%20129.png)
        
    5. 在 store.js 里面引入 cartItem 的 localStorage
        
        ![Untitled](Untitled%20130.png)
        
    6. 在 CartScreen view 里面实现添加到购物车的功能，放在下一节讲
- 3. 添加到购物车的 screen function
    
    引入需要的hook，useEffect 是我们要实际 dispatch 添加到购物车的地方
    
    ![Untitled](Untitled%20131.png)
    
    在 view 中实现添加购物车的功能
    
    match 可以从 url 中找到 id，location.search 可以从 url 中提取出问号后面的参数，这里提取出来的是 ?qty=1 这个字符串
    
    ![Untitled](Untitled%20132.png)
    
    现在的效果是，可以在 state 中看见 cartItem 的增加了
    
    ![Untitled](Untitled%20133.png)
    
- 4. 写购物车的前端界面 CartScreen
    
    在 App.js 当中引入这个路由
    
    ![Untitled](Untitled%20134.png)
    
    效果
    
    ![Untitled](Untitled%20135.png)
    
    ```html
    <Row>
      <Col md={8}>
        <h1>Shopping Cart</h1>
        {cartItems.length === 0 ? (
          <Message>
            Your cart is empty <Link to='/'>Go Back</Link>
          </Message>
        ) : (
          <ListGroup variant='flush'>
            {cartItems.map((item) => (
              <ListGroup.Item key={item.product}>
                <Row>
                  <Col md={2}>
                    <Image src={item.image} alt={item.name} fluid rounded />
                  </Col>
                  <Col md={3}>
                    <Link to={`/product/${item.product}`}>{item.name}</Link>
                  </Col>
                  <Col md={2}>${item.price}</Col>
                  <Col md={2}>
                    <Form.Control
                      as='select'
                      value={item.qty}
                      onChange={(e) =>
                        dispatch(
                          addToCart(item.product, Number(e.target.value))
                        )
                      }
                    >
                      {[...Array(item.countInStock).keys()].map((x) => (
                        <option key={x + 1} value={x + 1}>
                          {x + 1}
                        </option>
                      ))}
                    </Form.Control>
                  </Col>
                  <Col md={2}>
                    <Button
                      type='button'
                      variant='light'
                      onClick={() => removeFromCartHandler(item.product)}
                    >
                      <i className='fas fa-trash'></i>
                    </Button>
                  </Col>
                </Row>
              </ListGroup.Item>
            ))}
          </ListGroup>
        )}
      </Col>
    
      <Col md={4}>
        <Card>
          <ListGroup variant='flush'>
            <ListGroup.Item>
              <h2>
                Subtotal ({cartItems.reduce((acc, item) => acc + item.qty, 0)})
                items
              </h2>
              $
              {cartItems
                .reduce((acc, item) => acc + item.qty * item.price, 0)
                .toFixed(2)}
            </ListGroup.Item>
            <ListGroup.Item>
              <Button
                type='button'
                className='btn-block'
                disabled={cartItems.length === 0}
                onClick={checkoutHandler}
              >
                Proceed To Checkout
              </Button>
            </ListGroup.Item>
          </ListGroup>
        </Card>
      </Col>
    </Row>
    ```
    
- 5. 从购物车删除的 reducer & action & screen function
    1. 添加 remove constant
    2. 添加 cartReducer 的另一个 case
        
        ![Untitled](Untitled%20136.png)
        
    3. 添加 action
        
        ![Untitled](Untitled%20137.png)
        
    4. 在 cartScreen 里实现功能，实现这个 removeFromCartHandler
        
        ![Untitled](Untitled%20138.png)
        

### 6️⃣ 后端身份认证

- 0. Prepare：把后端 route 封装成 Controller
    
    新建 controllers 文件夹，新建 productController.js
    
    以前的 productRoutes 文件，都是把具体函数的实现写在 router.get()里面
    
    ![Untitled](Untitled%2091.png)
    
    现在直接用 router.route(’url’).get(controler) 来封装起来
    
    ![Untitled](Untitled%20139.png)
    
    在 controller 内部，只需要把以前写在 router 里面的函数复制过去
    
    ![Untitled](Untitled%20140.png)
    
- 1. 新建 authUser 的 Route 和 Controller (r+u=接口)
    
    (1)在 server.js 中添加 userRoutes
    
    ![Untitled](Untitled%20141.png)
    
    (2)新建 userRoutes.js，接到 authUser 这个 Controller
    
    ![Untitled](Untitled%20142.png)
    
    (3)新建 userController.js，创建 authUser 这个 Controller，处理 request
    
    ![Untitled](Untitled%20143.png)
    
    为了我们能在 body 中接收 json 数据，需要在 server.js 里面添加一个中间件
    
    ![Untitled](Untitled%20144.png)
    
    效果：
    
    ![Untitled](Untitled%20145.png)
    
    上面只是测试一下接口能不能跑通，下面开始正式匹配账号和密码，并且返回用户信息：
    
    (1)在 userModel 里面添加 bcrypt match 的方法：
    
    因为数据库里面的密码是加密的，所以我们需要通过 bcrypt.compare 的方法来比较输入的这个文本字符串和数据库中加密过的密码是不是一样的
    
    ![Untitled](Untitled%20146.png)
    
    ![Untitled](Untitled%20147.png)
    
    (2)修改 userController 里的方法，判断身份验证是否成功：
    
    ![Untitled](Untitled%20148.png)
    
    (3)现在的效果：验证 email 和 passward 成功之后，会返回 user 的信息
    
    ![Untitled](Untitled%20149.png)
    
- 2. Authentication 和 Authorization 的区别
    
    **认证和授权是两件不同的事情**
    
    之前，我们已经实现了**认证**(Authentication)，我们接受电子邮件和密码，在数据库中对其进行认证，证明是这个用户本人
    
    现在，**授权**(Authorization)是让该用户有权限访问某些部分，或者 API 中的某些受保护 routes，我们通过发送 Json Web令牌来做到这一点
    
    当登录时，它将创建一个Json Web 令牌，并将其与一个密钥 sign。这样服务器就可以知道它是否被篡改了，然后这个 token 就会被送回给客户，可以把它存储在客户端，可以把它存储在浏览器中。当我们必须访问任何受保护的 routes 时，我们可以在 header 中发送该令牌
    
    **token** **有三个不同的部分**
    
    - header，包括令牌的类型，这将是JWT，然后是用来签名的算法。
    - payload 数据是实际内容,通常我们会发送一个 user ID 或 session ID 来识别用户，我们会把它放在 payload 中。你要确保不要把安全数据，如密码诸如此类的数据放在里面，所以通常我们只发送一个用户ID。这样，服务器就可以收到它，我们就可以做一个数据库调用，或者我们可以得到那个用户
    - signature 签名是用来验证沿途是否有任何改变，它验证了发件人是他们所说的那个人
    
    可以在这个网站解析 token，**jwt.io**
    
    ![Untitled](Untitled%20150.png)
    
    **方法：在 header 里面添加 Authentication**
    
    如果我们现在跳回到 Postman上，当我们 post 这个 login route时，它就会**认证**我们的身份(Authentication)。但我们只得到一些基本的用户数据，我们并没有得到一个我们可以用来发送到受保护 route 的 token
    
    ![Untitled](Untitled%20151.png)
    
    所以在下一个视频中，我们将使它能够发送一个令牌回来
    
    这样做的方法是，一旦我们得到它，就说明，这个 route 是受保护的，我们将创建我们自己的 middleware，我们将创建我们自己的中间件来保护路由，但如果这是受保护的，我们将不得不在 header 中发送授权值，我们将放置令牌，like this
    
    ![Untitled](Untitled%20152.png)
    
    当我们到达我们的前端时，我们将采取令牌，我们将把它存储在客户端，然后我们会用 Axios 发送。当然如果你愿意，你也可以使用Fetch
    
- 3. 在身份认证成功之后，生成并返回 JWT json web token
    
    安装 jsonwebtoken
    
    ```jsx
    npm i jsonwebtoken
    ```
    
    新建 utils 文件夹，在里面写 generateToken 的方法：
    
    ![Untitled](Untitled%20153.png)
    
    在 userController 引入这个生成 token 的函数，然后在用户身份认证成功之后返回的 user 信息里，用这个函数生成一个 token：
    
    ![Untitled](Untitled%20154.png)
    
    ![Untitled](Untitled%20155.png)
    
    效果：身份认证成功之后，我们得到了 token
    
    ![Untitled](Untitled%20156.png)
    
    可以看到 token 里隐藏的信息，exp 是过期时间，exp 的值是个时间戳：
    
    ![Untitled](Untitled%20157.png)
    
- 4. 新建 middleware 匹配并解析 token 信息
    
    **下面创建一个需要授权才能访问的受保护的 route：**
    
    新建一个 access 属性为 private (怎么才能实现它的私有属性呢，后面需要通过一个 protect 的中间件来实现) 的 getUserProfile 的 controller，只有当身份认证成功之后才能访问这个接口：
    
    (测试版本)
    
    ![Untitled](Untitled%20158.png)
    
    (完善版本)
    
    ![Untitled](Untitled%20159.png)
    
    在 userRoute 里添加这个 /profile，对接 getUserProfile 这个 controller，每次添加了新的 controller 之后都要记得在这里注册呀！
    
    ![Untitled](Untitled%20160.png)
    
    **下面开始实现 protect 中间件：**
    
    在 middleware 文件夹下面，新建 anthMiddleware.js 文件
    
    1. 从 header 里面的 authorization 头里面的信息拿到 token
    2. 通过 jwt.decode(token,secret)，来解析 token，解析出来的信息打印出来就是下面的 json，于是就可以拿到 id
        
        ```jsx
        {
            id: '5f6bf78dqi0w',
            iat: 1600978514,
            exp: 1600978514
        }
        ```
        
    3. 通过 id 查找用户，返回除了密码以外的信息
    4. 没有 token 的情况处理
    
    ![Untitled](Untitled%20161.png)
    
    然后，在 profile 这个 route 的参数里面，加上 protect 这个中间件，这样只要我们触发了这个 route，protect 中间件就会运行
    
    ![Untitled](Untitled%20162.png)
    
    效果：
    
    ![Untitled](Untitled%20163.png)
    
    **TIPS：**
    
    把 /login 生成的 token 保留在 postman 里面，这样在调用 /profile 的时候就不用一直 copy了
    
    ![Untitled](Untitled%20164.png)
    
    当我们运行完 /login 之后，可以发现 postman 的 env 文件里保留了这个 token
    
    ![Untitled](Untitled%20165.png)
    
    在这个地方设置好 {{TOKEN}}
    
    ![Untitled](Untitled%20166.png)
    
- 5. 新建 userRegister 的 Route 和 Controller
    
    新建 registerUser 的 Controller，作用是解析 request body 里面传进来的 user 对象，然后通过 User.create() 在数据库创建一个新的用户信息
    
    ![Untitled](Untitled%20167.png)
    
    ![Untitled](Untitled%20168.png)
    
    一定要记得在 userRoutes 里注册 registerUser 这个 controller(第一个) 
    
    ![Untitled](Untitled%20169.png)
    
    为了密码的安全，在 useModel 里面预处理密码加密：
    
    ![Untitled](Untitled%20170.png)
    
    然后就可以看到数据库里的密码是经过 hash 加密过的：
    
    ![Untitled](Untitled%20171.png)
    

### 7️⃣ 前端身份认证

- 1. 用户登录的 reducer & action
    
    (1) 新建 userConstant
    
    ![Untitled](Untitled%20172.png)
    
    (2) 新建 userLoginReducers
    
    ![Untitled](Untitled%20173.png)
    
    (3) 在 store.js 里面注册这个 reducer
    
    ![Untitled](Untitled%20174.png)
    
    (4) 在 useAction.js 文件里面新建 login 的 action creator，如果匹配成功了，要将 userInfo 存进 localstorage 里面去
    
    ![Untitled](Untitled%20175.png)
    
    ![Untitled](Untitled%20176.png)
    
    (5) 在 store.js 里面引入 cartItem 的 localStorage
    
    ![Untitled](Untitled%20177.png)
    
- 2. 用户登录的 screen function
    
    t在 screen 文件夹里面新建 loginScreen.js，然后在 app.js 里面添加 loginScreen 的路由
    
    ![Untitled](Untitled%20178.png)
    
    在 component 文件夹里新建 formContainer.js
    
    ![Untitled](Untitled%20179.png)
    
    **loginScreen.js：**
    
    > 路由重定向的部分没有看懂，为什么登录成功之后就直接跳转到主页了呢？还有组件的参数 location, history 也没有看懂
    > 
    
    好像看懂了，location.search 是获取 url 参数的方法，在 react 组件的 componentDidMount 方法中打印一下 this.props，在浏览器控制台中查看输出如下，其中页面的 url 信息全都包含在 match 字段中
    
    ```jsx
    localhost:3000/app/knowledgeManagement/modify
    /STY20171011124209535/3/1507701970070/0/?s=1&f=7
    ```
    
    ![Untitled](Untitled%205.png)
    
    ![Untitled](Untitled%206.png)
    
    - match：包含了具体的 url 信息，在 params 字段中可以获取到各个路由参数的值
    - history：包含了组件可以使用的各种路由系统的方法，常用的有 push 和 replace，两者都是跳转页面，但是 replace 不会引起页面的刷新，仅仅是改变 url
    - location：相当于 URL 的对象形式表示，通过 search 字段可以获取到 url 中的 query 信息（这里 state 的含义与 HTML5 history.pushState API 中的 state 对象一样。每个 URL 都会对应一个 state 对象，你可以在对象里存储数据，但这个数据却不会出现在 URL 中。实际上，数据被存在了 sessionStorage 中）
    
    所以，如果 url 里面没有携带 query 参数的话，redirect 的值就是 ‘/’，这样在 useEffect 里面，只要登录成功拿到 userInfo 了，就可以跳转到 ‘/’ 也就是 homeScreen.js 组件页面
    
    ![Untitled](Untitled%20180.png)
    
    ![Untitled](Untitled%20181.png)
    
    ![Untitled](Untitled%20182.png)
    
    在 userActions 里面实现 logout 这个 action
    
    ![Untitled](Untitled%20183.png)
    
- 3. 用户注册的 reducer & action & screen function
    
    (1) 在 userConstant.js 里面添加常数
    
    ![Untitled](Untitled%20184.png)
    
    (2) 在 userReducers.js 文件里添加 userRegisterReducer
    
    ![Untitled](Untitled%20185.png)
    
    (3) 在 store.js 里面注册这个 reducer
    
    ![Untitled](Untitled%20186.png)
    
    (4) 在 usrActions.js 里面创建 register 这个 action creator 函数
    
    ![Untitled](Untitled%20187.png)
    
    ![Untitled](Untitled%20188.png)
    
    (5) 新建 registerScreen.js
    
    ![Untitled](Untitled%20189.png)
    
    ![Untitled](Untitled%20190.png)
    
    ![Untitled](Untitled%20191.png)
    
    ![Untitled](Untitled%20192.png)
    
    ![Untitled](Untitled%20193.png)
    
    (6) 在 App.js 里面注册 registerScreen
    
    ![Untitled](Untitled%20194.png)
    
    效果
    
    ![Untitled](Untitled%20195.png)
    
- 3. 导航栏登录显示头像， 退出登录
    
    效果：
    
    ![Untitled](Untitled%20196.png)
    
    在 component 文件夹中找到 header.js，引入 redux 的 userInfo 这个全局状态
    
    ![Untitled](Untitled%20197.png)
    
    增加判断条件，如果有 userInfo，则显示名字和下拉菜单，如果没有，则还是 sign in 按钮
    
    ![Untitled](Untitled%20198.png)
    
- 5. 更新用户信息

### 8️⃣ 支付 API

### 9️⃣ Admin 系统的用户管理

- 1. Get User 的 route 和 controller
    
    在 userController.js 里面新建 getUsers，返回所有的用户
    
    ![Untitled](Untitled%20199.png)
    
    userRoute.js 里面添加 getUsers 的 controller，这个方法也是受保护的，所以也要加上 protect 这个中间件
    
    ![Untitled](Untitled%20200.png)
    
- 2. 验证 Admin 权限的 middleware
    
    在 authMiddleware.js 里面添加 admin 中间件
    
    ![Untitled](Untitled%208.png)
    
    在 userRoutes.js 里面引入 admin 中间件，放在 protect 中间件后面，表示首先登录，再验证是否有 admin 的权限，只有都满足，才能调用这个 api
    
    ![Untitled](Untitled%209.png)
    
- 3. User List 的 reducer & action & screen function
    
    (1) 在 userConstant.js 里面加入 user list 
    
    ![Untitled](Untitled%20201.png)
    
    (2) 在 userReducers.js 里面新增 userListReducer
    
    ![Untitled](Untitled%20202.png)
    
    (3) 在 store.js 里面引入这个 userListReducer
    
    ![Untitled](Untitled%20203.png)
    
    (4) 在 userActions.js 里面新增 listUsers 这个 action creator function
    
    这里的 204 行的代码没有看懂是什么意思
    
    ![Untitled](Untitled%20204.png)
    
    ![Untitled](Untitled%20205.png)
    
    (5) 创建 userListScreen.js
    
    效果
    
    ![Untitled](Untitled%20206.png)
    
    ![Untitled](Untitled%20207.png)
    
    表格的 html
    
    ![Untitled](Untitled%20208.png)
    
    ![Untitled](Untitled%20209.png)
    
    ![Untitled](Untitled%20210.png)
    
    (6) 在 App.js 里面引入这个 userListScreen
    
    ![Untitled](Untitled%20211.png)
    
    (7) 设置进入这个 userListScreen 的入口，在 header 的下拉菜单里面，增加了“用户管理”、“商品管理”、“订单管理”三个 drop down menu
    
    ![Untitled](Untitled%20212.png)
    
- 4. Access security

### 1️⃣0️⃣ Admin 系统的商品管理

### 1️⃣1️⃣ 发表产品的评论

- 1. 发表评论的 route 和 controller
- 2. 发表评论前端实现
    
    效果图：
    
    ![Untitled](Untitled%20213.png)
    

### 1️⃣2️⃣ 模糊搜索栏、产品分页、显示top10

- 1. 模糊搜索
    
    在 App.js 里面加入这个 route
    
    ![Untitled](Untitled%20214.png)
    
    新建 searchBox.js 这个 component
    
    ![Untitled](Untitled%20215.png)
    
    ![Untitled](Untitled%20216.png)
    
    在 header 里面引入 searchBox
    
    ![Untitled](Untitled%20217.png)
    
    修改 productAction.js 里面的 listProducts
    
    ![Untitled](Untitled%20218.png)
    
    所以在使用 listProducts 的地方就是 HomeScreen 也要有所改动
    
    ![Untitled](Untitled%20219.png)
    
    修改 productController 里面的 getProducts 函数，使用了正则表达式
    
    ![Untitled](Untitled%2011.png)
    
- 2. HomeScreen 的分页展示
- 3. AdminScreen 的分页展示
- 4. 轮播图显示最火的 top3 产品
    
    Product.find({}).sort({rating:-1}).limit(3)
    
    ![Untitled](Untitled%20220.png)
    
    mongoDB sort 的底层实现
    
    ```jsx
    db.testdoc.find({"a":2222}).sort({"_id":-1}).limit(10)
    ```
    
    当数据量少时，会使用`{"_a":1}`索引，并进行内存排序，当数据量大时，会使用`{"_id":1}`
    索引，这个时候`find`里的a并没有用到索引，所以最终是会扫描所有文档，速度非常慢 
    
- 5. page tile

### 1️⃣3️⃣ 部署在 Heroku

- 1. npm run build 生成 build 文件夹
    
    ![Untitled](Untitled%20221.png)
    
    npm run build → 生成一个build包
    
    进入后端的server.js 配置
    
    ![Untitled](Untitled%20222.png)
    
    然后跑 npm start，启动backend
    
- 2. Deploy on Heruko
    
    **Heroku CLI 方法总览：**
    
    ![Untitled](Untitled%20223.png)
    
    登录：
    
    ![Untitled](Untitled%20224.png)
    
    下载 heruko CLI
    
    ![Untitled](Untitled%20225.png)
    
    在命令行输入 `heruko login` 的命令，弹出登录网页，点击登录
    
    ![Untitled](Untitled%20226.png)
    
    `heroku create proshopapp`
    
    ![Untitled](Untitled%20227.png)
    
    可以点开这个网址
    
    ![Untitled](Untitled%20228.png)
    
    可以看到新项目的欢迎页面
    
    ![Untitled](Untitled%20229.png)
    
    在项目里新建Procfile 文件
    
    ![Untitled](Untitled%20230.png)
    
    ![Untitled](Untitled%20231.png)
    
    用git工具提交
    
    ![Untitled](Untitled%20232.png)
    
    在setting里配置 .env 文件的参数
    
    ![Untitled](Untitled%20233.png)
    
    ![Untitled](Untitled%20234.png)
    
    部署成功！！
    
    ![Untitled](Untitled%20235.png)
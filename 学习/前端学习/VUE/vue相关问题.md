作者：李纯一

链接：https://www.zhihu.com/question/62372823/answer/2635307142

来源：知乎

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

  

**1.Vue****中****key****值作用**

高逼格答案： 提升[vue](https://www.zhihu.com/search?q=vue&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)渲染性能

- 1.vue在渲染的时候,会 先把 新DOM 与 旧DOM 进行对比， 如果dom结构一致，则vue会复用旧的dom。 （此时可能造成数据渲染异常）
- 2.使用key可以给dom添加一个 唯一标识符，让vue强制更新dom

**2.vue****组件传值**

父传子

- 1.子组件props定义变量
- 2.父组件在使用子组件时通过行内属性给props变量传值
- 特点：单向数据流

子传父

- 1.子组件：$emit触发父的事件
- 2.父在使用组件用@自定义事件名=父的方法 (子把值带出来)
- 特点：事件监听

非父子组件

- [vuex](https://www.zhihu.com/search?q=vuex&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)

**3.==****【必问】****==vue****生命周期总共分为几个阶段？**

核心： 四个阶段8个勾子

Vue 实例从创建到销毁的过程，就是生命周期。也就是从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程，我们称这是 Vue 的生命周期。

**1****）beforeCreate**

在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

**2****）created**

在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)， 属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。

**3****）beforeMount**

在挂载开始之前被调用：相关的 render 函数首次被调用。

**4****）mounted**

el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。

**5****）beforeUpdate**

数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。

**6****）updated**

由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

**7****）activated**

keep-alive 组件激活时调用。该钩子在服务器端渲染期间不被调用。

**8****）deactivated**

keep-alive 组件停用时调用。该钩子在服务器端渲染期间不被调用。

**9****）beforeDestroy**

实例销毁之前调用。在这一步，实例仍然完全可用。该钩子在服务器端渲染期间不被调用。

**10****）destroyed**

Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

**11****）errorCaptured（2.5.0+ 新增）**

当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。

**4.==****【必问】****==****第一次加载页面会触发哪几个****钩子函数****？**

- 四个钩子
    
    - beforeCreate,
    - created,
    - beforeMount,
    - mounted 这几个钩子函数

**5.****【必问】****Vue****的路由实现模式：****hash****模式和****history****模式**

1.路径不同

hash有#, history没有#

2.工作模式不同

hash : 修改当前页面hash,不需要服务器额外配置

history: 会给服务器发送请求，需要服务器配置

- 1.hash模式：在浏览器中符号“#”，#以及#后面的字符称之为[hash](https://www.zhihu.com/search?q=hash&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)，用 window.location.hash 读取。特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
- 2.history模式：history采用HTML5的新特性；且提供了两个新方法： pushState()， replaceState()可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更

**6.****【必问】请说出路由配置项常用的属性及作用**

- 路由配置参数：
    
    - path : 跳转路径
    - component : 路径相对于的组件
    - name:命名路由
    - children:子路由的配置参数(路由嵌套)
    - props:路由解耦
    - redirect : 重定向路由

  

**7.****【必问】说一下你在****vue****中踩过的坑**

- 1操作data中的数据，发现没有响应式
    
    - 原因： 数组中有很多方法，有的会改变数组（例如pop push）,有的不会改变数组（例如slice, filter）
    - 解决方案：通过Vue.set(对象，属性，值)这种方式就可以达到，对象新添加的属性是响应式的
- 2.在created操作dom的时候，是报错的，获取不到dom，这个时候实例vue实例没有挂载
    
    - 解决方案：Vue.nextTick([回调函数](https://www.zhihu.com/search?q=%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)进行获取
- 3.其他的可以自由发挥，只要不是太低级就可以（比如，单词写错，代码位置写错，这种就是低级问题。其他的都可以说，千万别说这两个)

  

**【加分】****Vue** **的** **nextTick** **的原理是什么****?**

- 1为什么需要 nextTick
    
    - Vue 是异步修改 DOM 的并且不鼓励开发者直接接触 DOM，但有时候业务需要必须对数据更改--刷新后的 DOM 做相应的处理，这时候就可以使用 Vue.nextTick(callback)这个 api 了。
- 2.知识储备（可以不说，但是自己要知道，以防不测）
    
    - [事件循环](https://www.zhihu.com/search?q=%E4%BA%8B%E4%BB%B6%E5%BE%AA%E7%8E%AF&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)中宏任务和微任务这两个概念
    - 常见的宏任务有 script, setTimeout, setInterval, setImmediate（一种执行更加频繁的定时器）
    - 常见的微任务有 ,Promise.then(), async
- 3.最终答案：
    
    - nextTick 的原理是 vue 通过异步队列控制 DOM 更新
    - nextTick底层是[promise](https://www.zhihu.com/search?q=promise&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)，所以是微任务。这个一定要知道
    - （官方语言) ： nextTick 回调函数先后执行的方式。如果大家看过这部分的源码，会发现其中做了很多 isNative()的判断，因为这里还存在兼容性优雅降级的问题。可见 Vue 开发团队的深思熟虑，对性能的良苦用心。
- 4.小科普：其实vue在版本更新的时候。 时而将nextTick封装成宏任务，时而将nextTick封装成微任务。 不过目前[vue2](https://www.zhihu.com/search?q=vue2&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2635307142%7D)最新的版本，nextTick底层是微任务
    
    - 课外阅读nextTick源码：[https://juejin.cn/post/6875492931726376974](https://link.zhihu.com/?target=https%3A//juejin.cn/post/6875492931726376974)

**【加分】****v-slot****插槽与作用域插槽**

- 1.插槽作用：父组件 传递 html结构 给 子组件
- 2.具名插槽作用：父组件 传递 多个html结构 给 子组件
- 3.作用域插槽作用：父组件 给 子组件 传递插槽 时，可以使用子组件内部的数据

**【加分】****vue****路由****作用与原理**

- 路由作用： 实现单页面应用
- 原理：监听location的hash值

**【加分】** **自定义指令****的方法有哪些****?****它有哪些钩子函数****?****还有哪些钩子函数参数****?**

- 全局定义指令：在vue对象的directive方法里面有两个参数，一个是指令名称，另外一个是函数。组件内定义指令：directives
- 钩子函数：bind(绑定事件触发)、inserted(节点插入的时候触发)、update(组件内相关更新)
- 钩子函数参数：el、binding
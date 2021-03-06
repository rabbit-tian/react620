1. 优雅的修改共享状态

   - *所有对数据的操作必须通过 dispatch 函数*
   - 它接受一个参数 `action`，这个 `action`是一个普通的 JavaScript 对象，里面必须包含一个 `type` 字段来声明你到底想干什么
   - `dispatch` 在 `swtich` 里面会识别这个 `type` 字段，能够识别出来的操作才会执行对 `appState` 的修改。

   ```js
   let appState = {
     title: {
       text: 'React.js',
       color: 'red',
     },
     content: {
       text: 'React.js 内容',
       color: 'blue'
     }
   }
   
   
   function dispatch(action){
     switch(action.type){
       case "UPDATE_TITLE_TEXT":
         appState.title.text = action.text
         break
       case "UPDATE_TITLE_COLOR":
         appState.title.color = action.color
         break
       default:
         break
     }
   }
   
   
   
   function renderApp(appState) {
     renderTitle(appState.title)
     renderContent(appState.content)
   }
   
   function renderTitle(title) {
     const titleDOM = document.getElementById('title')
     titleDOM.innerHTML = title.text
     titleDOM.style.color = title.color
   }
   
   function renderContent(content) {
     const contentDOM = document.getElementById('content')
     contentDOM.innerHTML = content.text
     contentDOM.style.color = content.color
   }
   
   renderApp(appState) // 渲染到页面上
   
   dispatch({ type: 'UPDATE_TITLE_TEXT', text: 'reject-redux' }) // 修改标题文本
   dispatch({ type: 'UPDATE_TITLE_COLOR', color: 'red' }) // 修改标题颜色
   renderApp(appState) // 把新的数据渲染到页面上
   ```

2. 抽离 store 和 事件监听

   - 现在我们有了一个比较通用的 `createStore`，它可以产生一种我们新定义的数据类型 `store`，通过 `store.getState` 我们获取共享状态，而且我们约定只能通过 `store.dispatch` 修改共享状态。`store` 也允许我们通过 `store.subscribe` 监听数据数据状态被修改了，并且进行后续的例如重新渲染页面的操作。

3. 纯函数 （pure function）

   - 一个函数的返回结果只依赖于它的参数

   - 并且在执行过程里面没有副作用

   - 除了修改外部的变量，一个函数在执行过程中还有很多方式产生*外部可观察的变化*，比如说调用 DOM API 修改页面，或者你发送了 Ajax 请求，还有调用 `window.reload`刷新浏览器，甚至是 `console.log` 往控制台打印数据也是副作用

     ```js
     // 纯函数：现在 foo 的返回结果只依赖于它的参数 x 和 b，foo(1, 2) 永远是 3。今天是 3，明天也是 3，在服务器跑是 3，在客户端跑也 3，不管你外部发生了什么变化，foo(1, 2) 永远是 3。只要 foo 代码不改变，你传入的参数是确定的，那么 foo(1, 2) 的值永远是可预料的。
     const a = 1
     const foo = (x, b) => x + b
     foo(1, 2) // => 3
     ```



## react-redux

#### react-redux的进化过程

1. react中的 状态管理：状态提升，将状态放在 相关联的 所有组件的公共父组件中
   - 缺点：一层层传递，对于结构复杂的大项目来说，很是繁琐

2. context的出现：将共享组件放在父组件的 context 上，这个父组件下的所有组件都可以从context中直接获取数据，而不需要传递数据

   - 缺点：所有组件都可能修改context中状态，导致程序运行的不可预料性

3. 将context和store结合起来，store里面的数据 只能通过dispatch 来修改，解决了context的问题

   — 问题： 大量重复代码，对 context依赖性过强

   - 创建store
   - store.getState(): 获取数据
   - store.dispatch(): 修改数据
   - store.subscribe(): 监听数据

4. connect 和 mapStateToProps

   - 高阶组件，减少重复代码，包装的新组件和原来组件通过props传递信息
   - Dumb 组件：减少依赖，只依赖传进来的props和自己的state，不依赖外界任何数据
   - 高阶组件connect和 context 打交道，把里面数据取出来通过 `props` 传给 Dumb 组件
     - `connect` 函数接受一个组件 `WrappedComponent` 作为参数，把这个组件包含在一个新的组件 `Connect` 里面，`Connect` 会去 context 里面取出 store。现在要把 store 里面的数据取出来通过 `props` 传给 `WrappedComponent`。

5. mapDispatchToProps

   - 一个参数来告诉它我们的组件需要如何触发 `dispatch`

6. Provider

   - `Provider` 做的事情也很简单，它就是一个容器组件，会把嵌套的内容原封不动作为自己的子组件渲染出来。它还会把外界传给它的 `props.store` 放到 context，这样子组件 `connect` 的时候都可以获取到。




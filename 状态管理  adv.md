1. dva：基于 redux 和 redux-saga，的数据流方案，内置了react-router和fetch，是一个轻量级的应用框架

2. dva数据流向：

   - 数据的改变发生通常是通过用户交互行为或者浏览器行为（如路由跳转等）触发的，当此类行为会改变数据的时候可以通过 `dispatch` 发起一个 action，
   - 如果是同步行为会直接通过 `Reducers` 改变 `State`，
   - 如果是异步行为（副作用）会先触发 `Effects` 然后流向 `Reducers` 最终改变 `State`，所以

3. 快速安装

   - npm install dva-cli -g
   - dva new dva-quickStart
   - 进入文件 ，npm start

4. 定义路由

   - 第一路由组件 比如 ConterPage.js

   - 在router.js 中引入，然后使用

     ```	js
     <Route path="/counter" exact component={CounterPage}/>
     ```

   - 去掉路由路径上的 `#`号： 切换 history 为 browserHistory

     - BrowserRouter 和 HashRouter 的原理区别
       - HashRouter：锚点技术
       - BrowserRouter/historyRouter: 用js控制浏览器的地址变化 
     - 单页面应用：在一个页面里面跳转，通过js控制里面内容

5. 编写 UI component

6. 定义 model： 管理数据

7. 使用diapatch 派发一个 action

8. model中的 reducer的编写

9. model中的  异步处理  effects 

10. Saga 中  select的方法： 取到state的值

11. action 或 dispatch 的两个常见问题

    - reducers和effects里面的函数不能重名
    - yield put的异步执行： 直接再写个 yield put

12. 路由跳转的两种方式

    - 父子关系传递：拿到父组件传来的   `history`，然后 ` history.push('./')`

    - 其他关系：使用高阶组件包裹一下，withRouter包裹一下子组件，不用传history

    - 从`dva/router`中解构出 `link`进行跳转  `<link to="/">go home</link>`

    - 使用上下文跳转  

      ```js
      Counter.contextTypes = {
        router: PropTypes.object
      }
      <button onClick={context.router.history.push('/')}>go home(context)</button>
      ```

    -  routerRedux

      ```js
      <button onClick={() => dispatch(routerRedux.push('/'))}>go home(routerRedux)</button>
      ```

    - Effect 中写`routerRedux`跳转:

      ```js
      import { routerRedux } from 'dva/router'
      yield put(routerRedux.push('/'))
      ```

    

13.   subscriptions 订阅 

    - 监听数据变化，触发事件

14. 发送ajax请求

15. 

16. 

    

    

      

      

      












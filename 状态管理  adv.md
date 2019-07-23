1. dva：基于 redux 和 redux-saga，的数据流方案，内置了react-router和fetch，是一个轻量级的应用框架
2. dva数据流向：
   - 数据的改变发生通常是通过用户交互行为或者浏览器行为（如路由跳转等）触发的，当此类行为会改变数据的时候可以通过 `dispatch` 发起一个 action，
   - 如果是同步行为会直接通过 `Reducers` 改变 `State`，
   - 如果是异步行为（副作用）会先触发 `Effects` 然后流向 `Reducers` 最终改变 `State`，所以
3. 


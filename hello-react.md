1. #### 启动 react 项目

   ```js
   // 1. 全局安装  create-react-app 环境
   npm install -g create-reatc-app
   
   // 2. 构建一个 名为hello-react 的react项目工程
   create-react-app hello-react
   
   // 3. 进入 hello-react 项目
   cd hello-react
   
   // 4. 启动项目
   npm start
   ```

2. #### jsx语法

   ```js
   class Header extends Component {
     // 定义函数
     renderWord (text1,text2) {
       const isRight = true
       return isRight ? text1 : text2
     }
     
     render () {
       const isClick = true;
       const goodWord = <div>good</div>;
       const badWord = <div>bad</div>;
       return (
         <div>
           <h1>nice to meet you {1+2}</h1>
           <h2>{(function () {return 'figthing'})()}</h2>
           <h3>{
             isClick?
             <p className="head">我很美丽</p>
             :<p className="main">我很漂亮</p>
           }</h3>
           <h4>{
             isClick? goodWord : badWord
           }</h4>
           <h5>{
             this.renderWord('田','甜')
           }</h5>
         </div>
       )
     }
   }
   ```

3. #### **组件的组合、嵌套和组件树**

   - ##### 自定义的组件都必须要用大写字母开头，普通的 HTML 标签都用小写字母开头。

     ```js
     
     // 标题组件
     class Title extends Component {
       render () {
         return (
           <h1>我是大标题哦</h1>
         )
       }
     }
     
     // 头部组件
     class Header extends Component {
       render () {
         return (
           <div>
             <Title/>
             <h1>我是Header</h1>
           </div>
         )
       }
     }
     
     // 主体
     class Main extends Component {
       render () {
         return (
           <div>
             <h1>我是main</h1>
           </div>
         )
       }
     }
     
     // 底部
     class Footer extends Component {
       render() {
         return (
           <div>
             <h1>我是Footer</h1>
           </div>
         )
       }
     }
     
     // index组件
     
     class Index extends Component {
       render () {
         return (
           <div>
             <Header></Header>
             <Main></Main>
             <Footer></Footer>
           </div>
         )
       }
     }
     
     ReactDOM.render(<Index />, document.getElementById('root'));
     ```

4. #### 事件监听

   - 给需要监听事件的元素加上属性类似于 `onClick`、`onKeyDown` 这样的属性,这些事件属性名都必须要用驼峰命名法
   - event：事件监听函数会被自动传入一个 `event` 对象,  e.target
   - this:  `this` 是 `null` 或者 `undefined`，
     - 因为 React.js 调用你所传给它的方法的时候，并不是通过对象方法的方式调用（`this.handleClickOnTitle`），而是直接通过函数调用 （`handleClickOnTitle`），所以事件监听函数内并不能通过 `this` 获取到实例。
     - 如果你想在事件函数当中使用当前的实例，你需要手动地将实例方法 `bind` 到当前实例上再传入给 React.js。
     - `bind` 会把实例方法绑定到当前实例上，然后我们再把绑定后的函数传给 React.js 的 `onClick` 事件监听

5. #### **组件的 state 和 setState**

   - setState 接受对象参数
   
   - setState 接受函数参数
   
   - setState 合并，在使用 React.js 的时候，并不需要担心多次进行 `setState` 会带来性能问题。
   
6. 配置组件的 props

   - *在使用一个组件的时候，可以把参数放在标签的属性当中，所有的属性都会作为 props 对象的键值*：

     ```js
     <LikeButton liked="已赞" unliked="赞"></LikeButton>
     ```

   - 组件内部是通过 `this.props` 的方式获取到组件的参数的，

     ```js
     const liked = this.props.cancel || "取消"
     ```

   - 可以把一个对象传给点赞组件作为参数

     ```js
      <LikeButton wodrings={{ unlikedText: "已赞", likedText: "赞" }} ></LikeButton>
     ```

   - 把一个h函数传给点赞组件作为参数

     ```js
     <LikeButton onClick={() => { console.log('click has been'); }}></LikeButton>
     
     // 调用
       handleClick(){
         // 传入对象作为参数
         this.setState({
           isLike:!this.state.isLike
         })
         // 执行传入的函数
         if (this.props.onClick) {
           this.props.onClick()
         }
       }
     ```

7. #### 默认配置 defaultProps

   - `defaultProps` 作为点赞按钮组件的类属性，里面是对 `props` 中各个属性的默认配置。这样我们就不需要判断配置属性是否传进来了：如果没有传进来，会直接使用 `defaultProps` 中的默认属性。

     ```js
       // 默认配置
       static defaultProps = {
         wodrings: {
           unlikedText: "取消",
           likedText: "点赞"
         }
       }
     ```

   - ##### props 不可变，但这并不意味着由 `props` 决定的显示形态不能被修改。组件的使用者可以*主动地通过重新渲染的方式*把新的 `props` 传入组件当中，这样这个组件中由 `props` 决定的显示形态也会得到相应的改变。

8. ##### State  VS   props

   - `state` 的主要作用是用于组件保存、控制、修改*自己*的可变状态。`state` 在组件内部初始化，可以被组件自身修改，而外部不能访问也不能修改。你可以认为 `state` 是一个局部的、只能被组件自身控制的数据源。`state` 中状态可以通过 `this.setState`方法进行更新，`setState` 会导致组件的重新渲染。

   - `props` 的主要作用是让使用该组件的父组件可以传入参数来配置该组件。它是外部传进来的配置参数，组件内部无法控制也无法修改。除非外部组件主动传入新的 `props`，否则组件的 `props` 永远保持不变。

   - #### 它们的职责其实非常明晰分明：*state 是让组件控制自己的状态，props 是让外部对组件自己进行配置*。

9. 渲染列表数据

   - key: 对于用表达式套数组罗列到页面上的元素，都要为每个元素加上 key 属性，这个 key 必须是每个元素唯一的标识, 高效节省性能
   - 在实际项目当中，如果你的数据顺序可能发生变化，标准做法是最好是后台数据返回的 `id` 作为列表元素的 `key`。

10. 小栗子---评论功能

   - 项目分析，组件划分
   - 在 React.js 当中必须要用 `setState` 才能更新组件的内容
   - 状态提升：当某个状态被多个组件*依赖*或者*影响*的时候，就把该状态提升到这些组件的最近公共父组件中去管理，用 `props` 传递*数据或者函数*来管理这种*依赖*或着*影响*的行为。

11. 生命周期

    - 挂载阶段的生命周期函数：
      - ComponentDidMount ： ajax，定时器启动
      - ComponentWillUnmount
    - 更新阶段的生命周期函数
      - shouldComponentUpdate(nextProps, nextState) ：
      - componentDidUpdate() : 组件重新渲染并且把更改变更到真实的 DOM 以后调用

12. ref 和react.js 中 dom 的操作

13. props.children 和 容器类组件

    - 相当于 vue 里面的插槽

    ```js
    class Card extends Component {
      render() {
        return (
          <div className='card'>
            <div className='card-content'>
              {this.props.children}
            </div>
          </div>
        )
      }
    }
    
    class Ref extends Component {
      render () {
        return (
          <div>
            <Card>
              <h2>哈哈哈</h2>
              <input/>
            </Card>
          </div>
        )
      }
    }
    ```

14. dangerourslySetHTML 和 style 属性

    - dangerourslySetHTML:  出于安全考虑的原因（XSS 攻击），在 React.js 当中所有的表达式插入的内容都会被自动转义，就相当于 jQuery 里面的 `text(…)` 函数一样，任何的 HTML 格式都会被转义掉，

      ```js
      class dangerously extends Component {
        state = {
          content: "<h1>我是html</h1>"
        }
        render() {
          return (
            <div dangerouslySetInnerHTML={{ __html: this.state.content}}/>
          )
        }
      }
      ```

    - Style:

      - 驼峰命名,  键值对

      ```js
      <div style={{color: "red",fontSize: "10px"}}>我要加style </div>
      ```

15. react命名及顺序的规范写法

    - 命名：组件的私有方法都用 `_` 开头，所有事件监听的方法都用 `handle` 开头。把事件监听方法传给组件的时候，属性名用 `on` 开头，
    - 组件的内容编写顺序：
      - static 开头的类属性，如 `defaultProps`、`propTypes`。
      - 构造函数，`constructor`。
      - getter/setter（还不了解的同学可以暂时忽略）。
      - 组件生命周期。
      - `_` 开头的私有方法。
      - 事件监听方法，`handle*`。
      - `render*`开头的方法，有时候 `render()` 方法里面的内容会分开到不同函数里面进行，这些函数都以 `render*` 开头。
      - `render()` 方法。

16. 高阶组件

    - 为了组件之间的代码复用

    - 组件可能有着某些相同的逻辑，把这些逻辑抽离出来，放到高阶组件中进行复用

    - 高阶组件内部的包装组件和被包装组件之间通过 props 传递数据

      ```js
      //  wrapWithLoadData 组件
      // 作用：newComponent组件根据第二个参数name，获取到存储的数据，并且更新到自己的 data 中，渲染的时候将 state.data 通过 props.data 传给 WrappedComponent。
      
      import React, { Component } from 'react'
      export default (WrapWithLoadData,name) => {
        	class newComponent extends Component {
            constructor () {
              super()
              this.state = { data: null }
            } 
            componentDidMount () {
              let data = localStorage.getItem(name);
              this.setState({data})
            }
            render(){
              return (
                <WrapWithLoadData data={this.state.data}/>
              )
            }
          }
          return newComponent
      }
      
      
      // 我们在  src/wrapWithLoadData.js  中使用这个高阶函数
      
      import wrapWithLoadData from './wrapWithLoadData'
      class InputWithUsername extends Component {
        render() {
          return (
          	<div>
            	<input value={this.props.state}/>
            </div>
          )
        }
      }
      
      InputWithUsername = wrapWithLoadData(InputWithUsername,'username')
      
      export default InputWithUsername
      
      ```

##### 










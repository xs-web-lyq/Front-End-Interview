- [React](#react)
  - [什么是 React](#什么是-react)
  - [react生命周期(><16.3)](#react生命周期163)
  - [react中发起网络请求应该在哪个生命周期中进行？为什么？](#react中发起网络请求应该在哪个生命周期中进行为什么)
  - [state 和 props 触发更新的生命周期分别？](#state-和-props-触发更新的生命周期分别)
  - [虚拟dom、更新原理](#虚拟dom更新原理)
  - [虚拟DOM是怎么对比的、diff原理](#虚拟dom是怎么对比的diff原理)
  - [什么是jsx、渲染原理](#什么是jsx渲染原理)
  - [props和state](#props和state)
  - [props为什么是只读的](#props为什么是只读的)
  - [react中怎么检验props？验证props的目的是什么](#react中怎么检验props验证props的目的是什么)
  - [react单向数据流是什么](#react单向数据流是什么)
  - [react组件之间的通信](#react组件之间的通信)
  - [setstate是同步还是异步、setstate之后的流程、setState和replaceState的区别](#setstate是同步还是异步setstate之后的流程setstate和replacestate的区别)
  - [如何理解hooks、为什么要用hooks，解决了哪些问题](#如何理解hooks为什么要用hooks解决了哪些问题)
  - [hooks使用限制是什么?](#hooks使用限制是什么)
  - [React Hooks 和生命周期的关系？](#react-hooks-和生命周期的关系)
  - [useEffect 与 useLayoutEffect 的区别](#useeffect-与-uselayouteffect-的区别)
  - [fiber架构的理解](#fiber架构的理解)
  - [react性能优化的手段，避免不必要的render](#react性能优化的手段避免不必要的render)
  - [react组件中怎么做事件代理？它的原理是什么？SyntheticEvent层（合成事件层)](#react组件中怎么做事件代理它的原理是什么syntheticevent层合成事件层)
  - [如何解决react层级嵌套过深的问题](#如何解决react层级嵌套过深的问题)
  - [react框架是mvvm框架还是mvc框架](#react框架是mvvm框架还是mvc框架)
  - [React.Component 和 React.PureComponent 的区别](#reactcomponent-和-reactpurecomponent-的区别)
  - [类组件与函数组件有什么异同？](#类组件与函数组件有什么异同)
  - [有受控组件和不受控组件的理解](#有受控组件和不受控组件的理解)
  - [有状态组件和无状态组件的理解、使用场景](#有状态组件和无状态组件的理解使用场景)
  - [对React中Fragment的理解，它的使用场景是什么？](#对react中fragment的理解它的使用场景是什么)
  - [对React的插槽(Portals)的理解，如何使用，有哪些使用场景](#对react的插槽portals的理解如何使用有哪些使用场景)
  - [React声明组件有哪几种方法，有什么不同？](#react声明组件有哪几种方法有什么不同)
  - [react高阶组件、纯组件、和普通组件有什么区别，适用什么场景](#react高阶组件纯组件和普通组件有什么区别适用什么场景)
  - [refs、react中可以在render访问refs吗?](#refsreact中可以在render访问refs吗)
  - [react路由的实现原理](#react路由的实现原理)
  - [如何配置 React-Router 实现路由切换](#如何配置-react-router-实现路由切换)
  - [React中遍历的方法有哪些？](#react中遍历的方法有哪些)
  - [Vue 和 React 数据驱动的区别](#vue-和-react-数据驱动的区别)
  - [react与vue的区别、为什么选择react、优点](#react与vue的区别为什么选择react优点)
  - [dispatch](#dispatch)

# React

```txt
知识点参考链接

https://www.nowcoder.com/discuss/629644?type=all&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_all_nctrack&gio_id=6F75134E4ACC8F86EF18014BC2C6C0D9-1646828193985

https://www.nowcoder.com/discuss/854671?type=post&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_post_nctrack&gio_id=6F75134E4ACC8F86EF18014BC2C6C0D9-1646828462902

https://juejin.cn/post/6941546135827775525
https://juejin.cn/post/6940942549305524238
```

```txt
值得借鉴的面经

https://www.nowcoder.com/discuss/123161?type=post&order=jing&pos=&page=2&ncTraceId=&channel=-1&source_id=search_post_nctrack&subType=2&gio_id=6F75134E4ACC8F86EF18014BC2C6C0D9-1646830844478

https://blog.csdn.net/qq_32534855/article/details/**107484533**
```

## 什么是 React

React是一个简单的javascript UI库，用于构建高效、快速的用户界面。它是一个轻量级库，因此很受欢迎。它遵循组件设计模式、声明式编程范式和函数式编程概念，以使前端应用程序更高效。它使用虚拟DOM来有效地操作DOM。它遵循从高阶组件到低阶组件的单向数据流

## react生命周期(><16.3)

- react < 16.3
  (挂载生命周期)
    `constructor(props)`: 初始化props和state
    `componentWillMount()`: Dom被渲染之前触发，在此方法中触发setstate方法，在组件初次渲染之前修改组件的state。如果组件渲染渲染完毕后调用，setstate方法就会启动新的生命周期。
    `render()`: 渲染，只要父组件 render 被调用，其所有子组件的 render 都会被调用
    `componentDidMount()`: 组件渲染完毕后触发，在此阶段中可以获取DOM，调用setState方会触发重新渲染
    `componentWillUnMount()`: 组件被卸载之前触发，可以在这里清除后台的一些进程，清除timer，取消网络请求等
  (更新生命周期)
    当组件的state发生变化或者父组件接收到新的属性的变化，会触发一系列的饿更新生命周期
    `componentWillReceiveProps(nextProps)`: 仅当新的属性被传递给了组件后才会调用。这也是唯一可以调用 setState 方法的地方。
    `shouldComponentUpdate(nextProps, nextState)`:这个生命周期函数是用来提升速度的，它是在重新渲染组件开始前触发的，默认返回 true，可以比较 this.props 和 nextProps ，this.state 和 nextState 值是否变化，来确认返回 true 或者 false。当返回 false 时，组件的更新过程停止，后续的 render、componentDidUpdate 也不会被调用。在进行新旧对比的时候，是浅对比， 也就是说如果比较的数据时引用数据类型，只要数据的引用的地址没变，即使内容变了，也会被判定为true。主要是针对一下两个场景的优化：setState 函数在任何情况下都会导致组件重新渲染吗（会）？如果没有调用 setState，props 值也没有变化，是不是组件就不会重新渲染（父组件重新渲染时，不管传入的 props 有没有变化，都会引起子组件的重新渲染）？
    `componentWillUpdate(nextProps, nextState)`: 组件更新之前触发
    `componentDidUpdate(prevProps, prevState)`: 更新操作发生后，调用render之后触发。

- react >= 16.3
  (挂载生命周期)
  `constructor(props)`
  `getDerivedStateFromProps(props, state)`：static getDerivedStateFromProps(props, state)，这是个静态方法，所以不能在这个函数里使用 this，它应返回一个对象来更新 state，如果返回 null 则不更新任何内容。
  `render()`
  `componentDidMount()`
  `componentWillUnMount()`
  (更新生命周期)
  当组件的 props 改变了，或组件内部调用了 setState/forceUpdate，会触发更新重新渲染。
  `getDerivedStateFromProps(props, state)`
  `shouldComponentUpdate(nextProps, nextState)`
  `render`
  `getSnapshotBeforeUpdate(prevProps, prevState)`:参数表示更新之前的props和state，最近一次渲染输出（提交到 DOM 节点）之前调用，它使得组件能在发生更改之前从 DOM 中捕获一些信息（例如，滚动位置）。此生命周期方法的任何返回值将作为参数传递给 componentDidUpdate()。在最终确定的render执行之前执行，也就是能保证其获取到的元素状态与didUpdate中获取到的元素状态相同。
  `componentDidUpdate()`

getDerivedStateFromProps代码讲解：
 getDerivedStateFromProps接收到新的 props 或者调用了 setState 和 forceUpdate 时被调用。如当接收到新的属性想修改 state ，就可以使用。

  ```html
    // 当 props.counter 变化时，赋值给 state 
  class App extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        counter: 0
      }
    }
    static getDerivedStateFromProps(props, state) {
      if (props.counter !== state.counter) {
        return {
          counter: props.counter
        }
      }
      return null
    }

    handleClick = () => {
      this.setState({
        counter: this.state.counter + 1
      })
    }
    render() {
      return (
        <div>
          <h1 onClick={this.handleClick}>Hello, world!{this.state.counter}</h1>
        </div>
      )
    }
  }
  ```

但是这里有个问题，如果想要通过点击实现 state.counter 的增加，但这时会发现值不会发生任何变化，一直保持 props 传进来的值。这是由于在 React 16.4^ 的版本中 setState 和 forceUpdate 也会触发这个生命周期，所以当组件内部 state 变化后，就会重新走这个方法，同时会把 state 值赋值为 props 的值。因此需要多加一个字段来记录之前的 props 值，这样就会解决上述问题。

```html
  // 这里只列出需要变化的地方
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      // 增加一个 preCounter 来记录之前的 props 传来的值
      preCounter: 0,
      counter: 0
    }
  }
  static getDerivedStateFromProps(props, state) {
    // 跟 state.preCounter 进行比较
    if (props.counter !== state.preCounter) {
      return {
        counter: props.counter,
        preCounter: props.counter
      }
    }
    return null
  }
  handleClick = () => {
    this.setState({
      counter: this.state.counter + 1
    })
  }
  render() {
    return (
      <div>
        <h1 onClick={this.handleClick}>Hello, world!{this.state.counter}</h1>
      </div>
    )
  }
}
```

getDerivedStateFromProps代码讲解：
最终确定的render执行之前执行，也就是能保证其获取到的元素状态与didUpdate中获取到的元素状态相同

```html
class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 我们是否在 list 中添加新的 items ？
    // 捕获滚动​​位置以便我们稍后调整滚动位置。
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 如果我们 snapshot 有值，说明我们刚刚添加了新的 items，
    // 调整滚动位置使得这些新 items 不会将旧的 items 推出视图。
    //（这里的 snapshot 是 getSnapshotBeforeUpdate 的返回值）
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}

```

## react中发起网络请求应该在哪个生命周期中进行？为什么？

- 对于异步请求，最好放在componentDidMount中；同步的状态改变，可以放在componentWillMount中，一般用的比较少

## state 和 props 触发更新的生命周期分别？

区别：更新props和state触发的生命周期相同
但是 getDerivedStateFromProps shouldComponentUpdate、getSnapshotBeforeUpdate这几个周期中
如果是更新state，参数prevState会有值，nextProps是一个空对象；
如果是更新props，参数nextProps会有值，prevState是一个空对象。

## 虚拟dom、更新原理

- 为什么需要虚拟dom
  我们知道在前端性能优化中，有一个很重要的一项就是尽可能少的操作 DOM，不仅仅是 DOM 操作相对较慢，更是因为频繁的 DOM 操作会造成浏览器的回流或者重绘，这些都会对我们的性能造成影响。
- 虚拟dom是什么
  虚拟dom是页面中真实的dom元素的js表示形式，每当DOM发生更改时，浏览器都需要重新计算CSS、进行布局并重新绘制web页面，使用VirtualDOM有效地重建DOM。
- 虚拟dom更新原理
  每当有更新发生时，Reconciler（协调器）会做如下工作：
    1.调用函数组件、或class组件的render方法，将返回的JSX转化为虚拟DOM（整个DOM副本保存为虚拟DOM）
    2.将虚拟DOM和上次更新时的虚拟DOM对比
    3.通过对比找出本次更新中变化的虚拟DOM
    4。通知Renderer（渲染器）将变化的虚拟DOM渲染到页面上

## 虚拟DOM是怎么对比的、diff原理

## 什么是jsx、渲染原理

JSX，是一个 JavaScript 的语法扩展，JSX 可以生成 React “元素”，在JSX中，结合了javascript和HTML，并生成了可以在DOM中呈现的react元素。JSX在编译时会被Babel编译为React.createElement方法。

## props和state

（1）props
props是一个从外部传进组件的参数，主要作为就是从父组件向子组件传递数据，它具有可读性和不变性，只能通过外部组件主动传入新的props来重新渲染子组件，否则子组件的props以及展现形式不会改变。
（2）state
state的主要作用是用于组件保存、控制以及修改自己的状态，它只能在constructor中初始化，它算是组件的私有属性，不可通过外部访问和修改，只能通过组件内部的this.setState来修改，修改state属性会导致组件的重新渲染。
（3）区别
props 是传递给组件的（类似于函数的形参），而state 是在组件内被组件自己管理的（类似于在一个函数内声明的变量）。
props 是不可修改的，所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。
state 是在组件中创建的，一般在 constructor中初始化 state。state 是多变的、可以修改，每次setState都异步更新的。

## props为什么是只读的

this.props是组件之间沟通的一个接口，原则上来讲，它只能从父组件流向子组件。React具有浓重的函数式编程的思想。提到函数式编程就要提一个概念：纯函数。它有几个特点：

- 给定相同的输入，总是返回相同的输出。
- 过程没有副作用。
- 不依赖外部状态。
this.props就是汲取了纯函数的思想。props的不可以变性就保证的相同的输入，页面显示的内容是一样的，并且不会产生副作用

## react中怎么检验props？验证props的目的是什么

react为我们提供了PropsTypes以供验证使用，当传入的props传入的数据无效，数据类型不符合时，就会在控制台发出警告信息。避免随着应用越来复杂而出现的问题，并且可以让程序变得易读。
如果项目汇中使用了TypeScript，那么就可以不用PropTypes来校验，而使用TypeScript定义接口来校验props。

```html
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

## react单向数据流是什么

单向数据流是指数据的流向只能由父组件通过props将数据传递给子组件，不能由子组件向父组件传递数据，要想实现数据的双向绑定，只能由子组件接收父组件props传过来的方法去改变父组件的数据，而不是直接将子组件的数据传递给父组件。

## react组件之间的通信

- 父组件向子组件通信
  父级通过props向子组件传递需要的信息

  ```html
  const Child = props => {
    return <p>{props.name}</p>
  }
  const Parent = () => {
    return <Child name='react'></Child>
  }
  ```

- 子组件向父组件通信
  通过props加回调函数的方式

  ```html
  const Child = props => {
    const test = (params) => {
      props.deal(msg)
    }
    return (
    <button onclick={test('你好)}></button>)
  }

  const Parent = () => {
    const deal = (msg) => {
      console.log(msg)
    }
    render(){
      return <Child deal={this.deal.bind(this)}></Child>
    }
  }
  ```

- 跨级组件通信
  
  父组件向子组件的子组件通信，以及向更深层的子组件通信
  （1）props层层传递，但是如果父级的结构较深，那么需要一层曾的去传递，增加了复杂度，并且，这些props并不是中间组件需要的
  （2）context，相当是一个大容器，可以把要通信的内容放在这个容器中，不管嵌套多深，都可使用。对于跨域多层的全局数据可以使用context实现

 ```html
 const BatContext = createContext();
 // 父组件
 class Parent extends Component {
   render() {
     const {color} = this.state
     return (
      <BatContext.Provider value={color}>
        <Child></Child>
      </BatContext.Provide>
     )
   }
 }
 // 子组件
 const Child = () => {
   return (
   <GrandChild />)
 }
// 子组件的子组件
class GrandChild extends Component {
  render(){
    return (
      <BatContext.Consumer>
        {color => <h1 style={{"color": color}}>我是彩色的</h1>}
      </BatContext.Consumer>
    )
  }
 }
 ```

- 非嵌套关系的组件通信
  没有任何包含关系的组件，包括兄弟组件以及不在同一父级中的非兄弟组件
 （1）发布订阅者
 （2）全局状态管理器，dva,redux等
 （3）如果是兄弟组件通信，可以找到两个兄弟节点的共同父级节点，结合父子间通信方式进行通信

## setstate是同步还是异步、setstate之后的流程、setState和replaceState的区别

- 参考链接：<https://zhuanlan.zhihu.com/p/65627731>
（1）同步or异步
如果所有的setstate是同步的, 那么就意味着每执行一次setstate时，都会重新的执行虚拟dom diff更新以及DOM渲染流程，效率极低；
如果是异步，可以把一个同步代码中的多次setstate合并成一次组件的更新。当我们在设置setState后，立即通过this.state是获取最新状态是获取不到的。如果要获取最新的状态可以在setState回调中获取.
所以setState 并不是单纯同步/异步的，它的表现会因调用场景的不同而不同。默认情况下，我们认为他是异步的。
（2）setstate之后的流程
  - 首先，调用了setState 入口函数，根据入参的不同，将其分发到不同的功能函数中去；
  - enqueueSetState 方法将新的 state 放进组件的状态队列里，并调用 enqueueUpdate 来处理将要更新的实例对象；
  
    ```html
    ReactComponent.prototype.setState = function (partialState, callback) {
    this.updater.enqueueSetState(this, partialState);
    if (callback) {
      this.updater.enqueueCallback(this, callback, 'setState');
    }
    };

    
    ```

    ```html
    enqueueSetState: function (publicInstance, partialState) {
    // 根据 this 拿到对应的组件实例
    var internalInstance = getInternalInstanceReadyForUpdate(publicInstance, 'setState');
    // 这个 queue 对应的就是一个组件实例的 state 数组
    var queue = internalInstance._pendingStateQueue || (internalInstance._pendingStateQueue = []);
    queue.push(partialState);
    //  enqueueUpdate 用来处理当前的组件实例
    enqueueUpdate(internalInstance);
    }
    ```

    ```html
    function enqueueUpdate(component) {
      // 注意这一句是问题的关键，isBatchingUpdates标识着当前是否处于批量创建/更新组件的阶段,如果没有处于批量创建/更新组件的阶段，则处理update state事务
      if (!batchingStrategy.isBatchingUpdates) {
        // 若当前没有处于批量创建/更新组件的阶段，则立即更新组件
        batchingStrategy.batchedUpdates(enqueueUpdate, component);
        return;
      }
      // 如果正处于批量创建/更新组件的过程，将当前的组件放在dirtyComponents数组中
      dirtyComponents.push(component);
    }
    ```

  代码中，通过isBatchingUpdates 来判断setState 是先存进 state 队列还是直接更新，如果值为 true 则执行异步操作，为 false 则直接更新。
  当前如果正处于创建/更新组件的过程，就不会立刻去更新组件，而是先把当前的组件放在dirtyComponent里，所以不是每一次的setState都会更新组件。
  这段代码就解释了我们常常听说的：setState是一个异步的过程，它会集齐一批需要更新的组件然后一起更新。

  那么，batchingStrategy是什么呢？

  ```html
  var ReactDefaultBatchingStrategy = {
    // 用于标记当前是否出于批量更新
    isBatchingUpdates: false,
    // 当调用这个方法时，正式开始批量更新
    batchedUpdates: function (callback, a, b, c, d, e) {
      var alreadyBatchingUpdates = ReactDefaultBatchingStrategy.isBatchingUpdates;

      ReactDefaultBatchingStrategy.isBatchingUpdates = true;

      // 如果当前事务正在更新过程在中，则调用callback，既enqueueUpdate
      if (alreadyBatchingUpdates) {
        return callback(a, b, c, d, e);
      } else {
      // 否则执行更新事务
        return transaction.perform(callback, null, a, b, c, d, e);
      }
    }
  };
  ```

  注意两点： 1、如果当前事务正在更新过程中，则使用enqueueUpdate将当前组件放在dirtyComponent里。 2、如果当前不在更新过程的话，则执行更新事务。
（3）setState和replaceState的区别

  ```html
    setState(object nextState[, function callback])
    // 将要设置的新状态（该状态会和当前的state合并）、回调函数（在setstate设置成功，并且组件重新渲染后调用）
    replaceState(object nextState[, function callback])
    // 将要设置的新状态（该状态会替换当前的state）、回调函数（在replaceState设置成功，且组件重新渲染后调用）
  ```
  
 总结：setstate修改其中的部分状态，只是覆盖，不会减少原来的状态；replaceState 是完全替换原来的状态，相当于赋值，将原来的 state 替换为另一个对象，如果新状态属性减少，那么 state 中就没有这个状态了。

## 如何理解hooks、为什么要用hooks，解决了哪些问题

- 官方：Hook 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。
- 解决了哪些问题?
  >
  >(1)在组件之间复用状态逻辑很难:过去常见的解决方案是高阶组件、render props 及状态管理框架
  > React 没有提供将可复用性行为“附加”到组件的途径（例如，把组件连接到 store）。如果你使用过 React 一段时间，你也许会熟悉一些解决此类问题的方案，比如 render props 和 高阶组件。但是这类方案需要重新组织你的组件结构，这可能会很麻烦，使你的代码难以理解。如果你在 React DevTools 中观察过 React 应用，你会发现由 providers，consumers，高阶组件，render props 等其他抽象层组成的组件会形成“嵌套地狱”。尽管我们可以在 DevTools 过滤掉它们，但这说明了一个更深层次的问题：React 需要为共享状态逻辑提供更好的原生途径。
  >你可以使用 Hook 从组件中提取状态逻辑，使得这些逻辑可以单独测试并复用。Hook 使你在无需修改组件结构的情况下复用状态逻辑。 这使得在组件间或社区内共享 Hook 变得更便捷
  >(2)复杂组件变得难以理解:生命周期函数与业务逻辑耦合太深，导致关联部分难以拆分。
    >我们经常维护一些组件，组件起初很简单，但是逐渐会被状态逻辑和副作用充斥。每个生命周期常常包含一些不相关的逻辑。例如，组件常常在 componentDidMount 和 componentDidUpdate 中获取数据。但是，同一个 componentDidMount 中可能也包含很多其它的逻辑，如设置事件监听，而之后需在 componentWillUnmount 中清除。相互关联且需要对照修改的代码被进行了拆分，而完全不相关的代码却在同一个方法中组合在一起。如此很容易产生 bug，并且导致逻辑不一致。
    >在多数情况下，不可能将组件拆分为更小的粒度，因为状态逻辑无处不在。这也给测试带来了一定挑战。同时，这也是很多人将 React 与状态管理库结合使用的原因之一。但是，这往往会引入了很多抽象概念，需要你在不同的文件之间来回切换，使得复用变得更加困难。
    >为了解决这个问题，Hook 将组件中相互关联的部分拆分成更小的函数（比如设置订阅或请求数据），而并非强制按照生命周期划分。你还可以使用 reducer 来管理组件的内部状态，使其更加可预测。
  >(3)难以理解的 class:常见的有 this 的问题，但在 React 团队中还有类难以优化的问题，希望在编译优化层面做出一些改进.
    >除了代码复用和代码管理会遇到困难外，我们还发现 class 是学习 React 的一大屏障。你必须去理解 JavaScript 中 this 的工作方式，这与其他语言存在巨大差异。还不能忘记绑定事件处理器。没有稳定的语法提案，这些代码非常冗余。大家可以很好地理解 props，state 和自顶向下的数据流，但对 class 却一筹莫展。即便在有经验的 React 开发者之间，对于函数组件与 class 组件的差异也存在分歧，甚至还要区分两种组件的使用场景。

    总的来说：
    实际上就是类组件在多年的应用实践中，发现了很多无法避免问题而又难以解决，而相对类组件，函数组件又太过于简陋，比如，类组件可以访问生命周期方法，函数组件不能；类组件中可以定义并维护 state（状态），而函数组件不可以；类组件中可以获取到实例化后的 this，并基于这个 this 做各种各样的事情，而函数组件不可以；
    但是，函数式编程方式在JS中确实比 Class 的面向对象方式更加友好直观，那么只要能够将函数的组件能力补齐，也就解决了上面的问题，而如果直接修改函数组件的能力，势必会造成更大的成本，最好的方式就是开放对应接口进行调用，非侵入式引入组件能力，也就是我们现在看到的 Hooks 了；

## hooks使用限制是什么?

  (1)不可以在循环、条件或者嵌套函数中调用hook
  (2)在react函数组件中调用hook

 why?
 为了解决以上是那个问题，所以hooks是基于函数组件设计的，所以只支持函数组件。
 React需要利用调用顺序来正确更新相应的状态，以及调用相应的钩子函数。一旦在循环或条件分支语句中调用Hook，就容易导致调用顺序的不一致性，导致错误。

## React Hooks 和生命周期的关系？

- 函数组件 的本质是函数，没有 state 的概念的，因此不存在生命周期一说，仅仅是一个 render 函数而已。
- 引入Hooks之后的函数组件，让组件在不使用 class 的情况下拥有 state，也就有了生命周期的概念，所谓的生命周期其实就是 useState、 useEffect() 和 useLayoutEffect()
- 总结：Hooks 组件（使用了Hooks的函数组件）有生命周期，而函数组件（未使用Hooks的函数组件）是没有生命周期的。
  
  具体的class组件与hooks组件生命周期的对应关系：
  (1): constructor -->> useState(0), useState 来初始化 state
  (2): shouldComponentUpdate -->> React.memo 包裹一个组件来对它的 props 进行浅比较，其中，React.memo 等效于 PureComponent，它只浅比较 props。这里也可以使用 useMemo 优化每一个节点。
  (3): componentDidMount, componentDidUpdate -->> useEffect
  (4): render：这是函数组件体本身
  (5): componentWillUnmount：相当于 useEffect里面返回的 cleanup 函数
  (6): componentDidCatch and getDerivedStateFromError：目前还没有这些方法的 Hook 等价写法

  ```html
  // componentDidMount
  useEffect(() => {
  // 需要在componentDidMount执行内容
  }, [])

  // componentDidMount,仅在 count 更改时更新
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count])

  // componentDidMount/componentWillUnmount
  useEffect(()=>{
  // 需要在 componentDidMount 执行的内容
  return function cleanup() {
    // 需要在 componentWillUnmount 执行的内容      
  }
  }, [])

  ```

## useEffect 与 useLayoutEffect 的区别

同：useEffect 与 useLayoutEffect 两者都是用于处理副作用；使用方式也完全相同
不同：useEffect在React渲染过程中是被异步调用的，用于绝大多数场景
     useLayoutEffect会在所有的DOM变更之后同步调用，需要避免在 useLayoutEffect 做计算量较大的耗时任务从而造成阻塞。

## fiber架构的理解

>主流浏览器的刷新频率是60HZ，每（1000ms / 60Hz）16.6ms浏览器刷新一次。
>我们知道，JS可以操作DOM，GUI渲染线程与JS线程是互斥的。所以JS脚本执行和浏览器布局、绘制不能同时执行。
>在每16.6ms时间内，需要完成如下工作：

```txt
JS脚本执行 -----  样式布局 ----- 样式绘制
```

>当JS执行时间过长，超出了16.6ms，这次刷新就没有时间执行样式布局和样式绘制了。从而会导致页面掉帧，导致用户感觉到卡顿。
>如何给用户制造很快的“假象”，解决一个任务长期霸占着资源的问题？
>答案是：通过Fiber 架构，让这个执行过程变成可被中断。“适时”地让出 CPU 执行权。
>具体的：fiber架构的在浏览器每一帧的时间中，预留一些时间给JS线程，React利用这部分时间更新组件（在源码中，预留的初始时间是5ms）。
>当预留的时间不够用时，React将线程控制权交还给浏览器使其有时间渲染UI，React则等待下一帧时间到来继续被中断的工作。

## react性能优化的手段，避免不必要的render

- 避免不必要的render，可以使用shouldComponentUpdate和PureComponent来减少因父组件更新而触发子组件的其中，purecomponent只做浅层的比较。
- React.memo来实现，缓存组件的渲染，避免不必要的更新
- 使用usememo或者usecallback缓存变量或者函数
- 使用suspense(react16.6新增组件)或者lazy进行组件的懒加载，suspense可以在组件请求数据时展示一个pending状态。请求成功后渲染数据。
- 在显示列表或表格时始终使用 Keys，这会让 React 的更新速度更快

```html
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
 
function MyComponent() {
  return (
    <div>
      // 组件加载阶段，显示一个loading...
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

## react组件中怎么做事件代理？它的原理是什么？SyntheticEvent层（合成事件层)

```html
https://juejin.cn/post/6844903502729183239
```

```html
<div onClick={this.handleClick.bind(this)}>点我</div>
```

- React并不是将click事件绑定到了div的真实DOM上，而是在document处监听了所有的事件，当事件发生并且冒泡到document处的时候，React将事件内容封装并交由真正的处理函数运行。这样的方式不仅仅减少了内存的消耗，还能在组件挂在销毁时统一订阅和移除事件。

- 除此之外，冒泡到document上的事件也不是原生的浏览器事件，而是由react自己实现的合成事件（SyntheticEvent）。因此如果不想要是事件冒泡的话应该调用event.preventDefault()方法，而不是调用event.stopProppagation()方法。

- 在React底层，主要对合成事件做了：事件委派和自动绑定。
事件委派： React会把所有的事件绑定到结构的最外层，使用统一的事件监听器，这个事件监听器上维持了一个映射来保存所有组件内部事件监听和处理函数。
自动绑定： React组件中，每个方法的上下文都会指向该组件的实例，即自动绑定this为当前组件。

- 为什么要有这个？
  如果DOM上绑定了过多的事件处理函数，整个页面响应以及内存占用可能都会受到影响。React为了避免这类DOM事件滥用，同时屏蔽底层不同浏览器之间的事件系统差异，实现了一个中间层——SyntheticEvent。

## 如何解决react层级嵌套过深的问题

- 使用context API,提供了一种组件之间的状态共享，而不必通过显式组件树逐层传递props
- 使用一些状态管理库，redux, dva等。

## react框架是mvvm框架还是mvc框架

- MVVM --->>>  model层(模型层，主要负责处理业务数据)；view层(视图层，主要负责视图显示)；VM(ViewModel, V与M之间的桥梁，负责监听M或者V的修改);典型的特征：数据双向绑定，
  也就是当M层数据进行修改时，VM层会监测到变化，并且通知V层进行相应的修改，反之修改V层则会通知M层数据进行修改，以此也实现了视图与模型层的相互绑定。(vue)
- MVC --->>> M(model 数据模型层 ) V（view 视图层 ） C（controller 控制层 ）
  主要实现通过控制层监听model的变化，数据变化后通过controller 控制层 来实现view层的渲染。(react)

```txt
React是一个单向数据流的库，状态驱动视图。
State --> View --> New State --> New View
```

## React.Component 和 React.PureComponent 的区别

- pureComponent是纯组件，就是基于浅比较的方式，给每一个组件设置shouldComponentUpdate（如果自己设置了，以自己的为主），在里面把状态和属性都做对比，如果两者基于浅比较都没有发生任何的更改，则不再重新渲染组件
- 浅比较含义，就是只比较第一级，对于基本数据类型，只比较值；对于引用数据类型值，直接比较地址是否相同，不管里面内容变不变，只要地址一样，我们就认为没变。浅比较会忽略属性和或状态突变情况，其实也就是数据引用指针没有变化，而数据发生改变的时候render是不会执行的。如果需要重新渲染时，对于引用类型数据赋值的时候，我们尽可能把之前值拿过来克隆一份，赋给它新的地址就好。
- 优点：当组件更新时，优化React程序，省去虚拟DOM的生成和对比过程，减少render函数执行的次数，从而提高组件的性能。
- 注意：PureComponent不能乱用，只有那些状态和属性不经常的更新的组件我们用来做优化，对于经常更新的，这样处理后反而浪费性能，因为每一次浅比较也是要消耗时间的

## 类组件与函数组件有什么异同？

- 相同点
  组件是react可以复用的最小代码片段，最终返回在页面上渲染的react元素，无论是函数组件，还是类组件，在最终的呈现方式上是完全一致的。
  甚至可以将一个类组件改写成函数组件，或者把函数组件改写成一个类组件；
  从使用者的角度而言，很难从使用体验上区分两者，而且在现代浏览器中，闭包和类的性能只在极端场景下才会有明显的差别。
  
- 不同点
  (1)类组件是基于面向对象编程的，主要有继承、生命周期等概念；函数组件是函数式编程，主打的是没有副作用，引用透明，immutable等特点
  (2)之前，使用场景上，如果存在需要使用生命周期的组件，那么主推类组件；设计模式上，如果需要使用继承，那么主推类组件。
     但现在由于 React Hooks 的推出，生命周期概念的淡出，函数组件可以完全取代类组件。其次继承并不是组件最佳的设计模式，官方更推崇“组合优于继承”的设计概念，所以类组件在这方面的优势也在淡出。
  (3)性能优化上，类组件主要依靠 shouldComponentUpdate 阻断渲染来提升性能，而函数组件依靠 React.memo 缓存渲染结果来提升性能。
  (4)从上手程度而言，类组件更容易上手，从未来趋势上看，由于React Hooks 的推出，函数组件成了社区未来主推的方案。
  (5)从未来发展来看，由于生命周期带来的复杂度，并不易于优化；而函数组件本身轻量简单，更能适应 React 的未来发展。

## 有受控组件和不受控组件的理解

- 受控组件
官方定义：在 HTML 中，表单元素（如`<input>`、 `<textarea>` 和 `<select>`）通常自己维护 state，并根据用户输入进行更新。而在 React 中，可变状态（mutable state）通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新。

受控组件更新state的流程：

- 可以通过初始state中设置表单的默认值
- 每当表单的值发生变化时，调用onChange事件处理器
- 事件处理器通过事件对象e拿到改变后的状态，并更新组件的state
- 一旦通过setState方法更新state，就会触发视图的重新渲染，完成表单组件的更新

```html
class NameFrom extends React.Component {
  constroctor(props){
    super(props);
    this.state = {
      value: ''
    }
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    handleChange(e) {
      this.setSate({
        value: e.target.value
      })
    }
    handleSubmit(event) {
    alert('提交的名字: ' + this.state.value);
    event.preventDefault();
  }

  render(){
    return(){
      <form onSubmit={this.handleSubmit}>
        <label>
          名字：
          <input type='text' value={this.state.value} onChange={this.handleChange}>
        </label>
      </form>
    }
  }
  }
}
```
  
- 非受控组件
  官方定义：表单数据的处理都由DOM节点处理，要编写一个非受控组件，而不是为每个状态更新都编写数据处理函数，你可以 使用 ref 来从 DOM 节点中获取表单数据。

```html
class NameFrom extends React.Component {
  constroctor(props){
    super(props);
    this.input = React.createRef();
    this.handleSubmit = this.handleSubmit.bind(this);

    handleSubmit(event) {
      alert('A name was submitted: ' + this.input.current.value);
      event.preventDefault();
    }


  render(){
    return(){
      <form onSubmit={this.handleSubmit}>
        <label>
          名字：
          <input type='text' ref={this.input}>
        </label>
      </form>
    }
  }
  }
}

```

总结：当有多个输入框，或者多个这种组件时，如果使用受控组件，需要编写多个事件处理函数，使得代码非常臃肿。

## 有状态组件和无状态组件的理解、使用场景

- 有状态组件
特点：是类组件、有继承、可以使用react的生命周期、可以使用this、内部可以使用state,维护自身状态的变化，可以根据外部组件传入的props和state进行渲染。
（当一个类组件不需要管理自身状态时，也可称为无状态组件。）
- 无状态组件
特点：是类组件或者函数组件、没有this(使用箭头函数事件无需绑定)、组件内部不维护state，只根据外部组件传入的props进行渲染组件，当props改变s时，组件重新渲染。
优点：组件不需要被实例化，无生命周期，提升性能。 输出（渲染）只取决于输入（属性），无副作用； 简化代码、专注于 render； 视图和数据的解耦分离
缺点：无法使用 ref；无生命周期方法；无法控制组件的重渲染，因为无法使用shouldComponentUpdate 方法，当组件接受到新的属性时则会重渲染；

使用场景：当一个组件不需要管理自身状态时，也就是无状态组件，应该优先设计为函数组件。比如自定义的 `<Button />`、 `<Input />` 等组件。

## 对React中Fragment的理解，它的使用场景是什么？

- 在React中，组件返回的元素只能有一个根元素。为了不添加多余的DOM节点，我们可以使用Fragment标签来包裹所有的元素，Fragment标签不会渲染出任何元素。

```txt
官方解释：React 中的一个常见模式是一个组件返回多个元素。Fragments 允许你将子列表分组，而无需向 DOM 添加额外节点
```

```html
import React, {Component, Fragment} from 'react'
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  )
  // 也可以写成以下形式
  render() {
    return (
      <>
        <ChildA />
        <ChildB />
        <ChildC />
      </>
    );
  }
}
```

## 对React的插槽(Portals)的理解，如何使用，有哪些使用场景

官方定义：提供了一种将子节点渲染到存在于父组件以外的DOM节点的优秀方案。
Portals 是React 16提供的官方解决方案，使得组件可以脱离父组件层级挂载在DOM树的任何位置。通俗来讲，就是我们 render 一个组件，但这个组件的 DOM 结构并不在本组件内。
有些元素需要被挂载在更高层级的位置。
最典型的应用场景：当父组件具有overflow: hidden或者z-index的样式设置时，组件有可能被其他元素遮挡，这时就可以考虑要不要使用Portal使组件的挂载脱离父组件。例如：对话框，模态窗，悬浮卡以及提示框。

```txt
ReactDOM.createProtal(child, container)
// 参数child是任何可以渲染的React子元素，例如一个元素，字符串，或者fragment；container是一个dom元素
```

```html
render() {
  // 挂载了一个新的div，并且把子元素渲染其中
  return (
    <div>
      {this.props.children}
    </div>
  )
}

render() {
  // 并没有创建新的div，只是把子元素渲染到domNode中
  // domNode 是一个可以在任何位置的有效 DOM 节点。
  return ReactDOM.createPortal(
    this.props.children,
    domNode
  )
}
```

## React声明组件有哪几种方法，有什么不同？

- 函数式定义无状态组件:创建纯展示组件，这种组件只负责根据传入的props来展示,不涉及到state状态的操作,组件不会被实例化，整体渲染性能得到提升，不能访问this对象，不能访问生命周期的方法
- ES5原生方式React.createClass定义组件:React.createClass会自绑定函数方法，导致不必要的性能开销。
- ES6形式的extends React.Component定义组件:目前极为推荐的创建有状态组件的方式，最终会取代React.createClass形式；相对于 React.createClass可以更好实现代码复用。
(1)React.createClass

```html
import React from 'react';
const Contact = React.createClass({
  // (1)定义属性类型：通过proTypes对象和getDefaultProps()方法来设置和获取props, 有关组件props的属性类型及组件默认的属性会作为组件实例的属性来配置
  propTypes: {
    name: React.PropTypes.string
  }
  getDefaultProps() {
    return {
      name: ''
    };
  },
  // (2)通过getInitialState()方法返回一个包含初始值的对象
  getInitialState(){
    return {
      isEditing: false
    }
  }
  // (3)this能够正确的绑定
  handleClick() {
    console.log(this);  // React Component instance
  },
  render(){
    return (
      <div onClick={this.handleClick}></div>
    )
  }
})
export default Contacts;
```

(2)React.Component

```html
import React from 'react';
class Contact extends React.Component {
  // (1)定义属性类型：通过设置两个属性propTypes和defaultProps，是作为组件类的属性，不是组件实例的属性，也就是所谓的类的静态属性来配置的
  static propTypes = {
    name: React.PropTypes.string
  }
  static defaultProps = {
    name: ''
  }
  constructor(props){
    super(props);
    // (2)在constructor里通过this.state设置初始状态
    this.state = {
      isEditing: false
    }
  }
   // (3)属性并不会自动绑定到 React 类的实例上,需要开发者手动绑定，否则this不能获取当前组件实例对象。
  handleClick(){
        console.log(this); // null
    }
    handleFocus(){  // manually bind this
        console.log(this); // React Component Instance
    }
    handleBlur: ()=>{  // use arrow function
        console.log(this); // React Component Instance
    }
  render(){
    return (
      <div onClick={this.handleClick} onFocus={this.handleFocus.bind(this)} onBlur={this.handleBlur}></div>
    )
  }
}
```

## react高阶组件、纯组件、和普通组件有什么区别，适用什么场景

```html
<
```
  
## refs、react中可以在render访问refs吗?

- react中refs的作用是什么? 用于访问在 render 方法中创建的 React 元素或 DOM 节点
  
- 使用场景？
  (1) 管理焦点，文本选择或者媒体播放
  (2) 触发强制动画
  (3) 集成第三方 DOM 库
  
- react中可以在render访问refs吗？为什么？
  不可以，render 阶段 DOM 还没有生成，无法获取 DOM

- 怎么用ref
  (1) React.createRef()，创建实例对象，绑定到dom节点（React16的方法）

  ```html
    class Co extends React.Component {
      constructor(props) {
        super(props)
        this.myref = React.creatRef()
      }
      render() {
        return <div ref = {this.myRef}></div>
      }
    }
  ```

  (2)函数回调 Refs：你会传递一个函数。这个函数中接受 React 组件实例或 HTML DOM 元素作为参数，以使它们能在其他地方被存储和访问。

  ```html
    function CustomTextInput(props) {
  // 这里必须声明 textInput，这样 ref 回调才可以引用它
      let textInput = null;
      function handleClick() {
        textInput.focus();
      }
      return (
        <div>
          <input
            type="text"
            ref={(input) => { textInput = input; }} />
          <input
            type="button"
            value="Focus the text input"
            onClick={handleClick}
          />
        </div>
      );  
    }
  ```

## react路由的实现原理

- 基于hash的路由：通过监听hashchange事件，感知 hash 的变化
  (1):改变 hash 可以直接通过 location.hash=xxx
- 基于H5 history路由：
  (1):改变 url 可以通过 history.pushState 和 resplaceState 等，会将URL压入堆栈，同时能够应用 history.go() 等 API
  (2):监听 url 的变化可以通过自定义事件触发实现

## 如何配置 React-Router 实现路由切换

- 使用`<Route>` 组件
  路由匹配是通过比较 `<Route>` 的 path 属性和当前地址的 pathname 来实现的。当一个 `<Route>` 匹配成功时，它将渲染其内容，当它不匹配时就会渲染 null。没有路径的 `<Route>`将始终被匹配
  
  ```html
    // when location = { pathname: '/about' }
  <Route path='/about' component={About}/> // renders <About/>
  <Route path='/contact' component={Contact}/> // renders null
  <Route component={Always}/> // renders <Always/>
  ```

- 结合使用 `<Switch>` 组件和 `<Route>` 组件
  `<Switch>` 不是分组 `<Route>` 所必须的，但他通常很有用。 一个 `<Switch>` 会遍历其所有的子 `<Route>`元素，并仅渲染与当前地址匹配的第一个元素。
  不加`<Switch>`，当 URL 的 path 为 “/login” 时，`<Route path="/" />`和`<Route path="/login" />` 都会被匹配，因此页面会展示 Home 和 Login 两个组件。这时就需要借助 `<Switch>`来做到只显示一个匹配组件：
  
   ```html
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route path="/contact" component={Contact} />
    </Switch>

  ```

- 使用 `<Link>`、 `<NavLink>`、`<Redirect>` 组件

  ```html
    <Link to="/">Home</Link>  // 应用程序中创建链接
   // <a href='/'>Home</a>
   <NavLink to="/react" activeClassName="hurray">
    React
   </NavLink>

   <Redirect from='/users/:id' to='/users/profile/:id'/> 
   // 当请求 /users/:id 被重定向去 '/users/profile/:id'
   <Redirect to='/users/profile/:id'/> 
   // 当路由没有被匹配到的时候，则通过Redirect进行跳转
   // this.props.match.params.id 取得url中的动态路由id部分的值
  ```

## React中遍历的方法有哪些？

- map, forEach, for...of
- for...in, Object.entries(obj).map

## Vue 和 React 数据驱动的区别

在数据绑定上来说，vue的特色是双向数据绑定，而在react中是单向数据绑定。

vue中实现数据绑定靠的是数据劫持（Object.defineProperty()）+发布-订阅模式

vue中实现双向绑定

```html
<input v-model="msg" />
```

react中实现双向绑定

```html
<input value={this.state.msg} onChange={() => this.handleInputChange()} />
```

## react与vue的区别、为什么选择react、优点

相同点

## dispatch

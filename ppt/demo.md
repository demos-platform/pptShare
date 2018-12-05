title: React16.X 各个版本的特性
speaker: 牧云云
url: https://github.com/ksky521/nodeppt
transition: zoomin
files: /js/demo.js,/css/demo.css,/js/zoom.js
highlightStyle: monokai_sublime
theme: moon
date: 2018年11月29日

[slide style="background-image:url('https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg')"]
# React16.X 各个版本的特性
----

<small>by 牧云云</small>

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

> Before you're going to hate it, then you're going to love it.{:&.zoomIn}

![](http://i2.hdslb.com/bfs/archive/d8b21651319c885d730a04e7853ad752869a3ff2.jpg){:&.zoomIn}

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]
## <span class="red">React 16 里新加了哪些特性呢?<span class="yellow">
----

![](http://with.muyunyun.cn/18be54d827e9dde7d9e29d029e329334.jpg){:&.zoomIn}

* <span class="blue">Concurrent Render {:&.zoomIn}</span>
* <span class="blue">render</span>
* <span class="blue">Portals</span>
* <span class="blue">Error Boundaries</span>
* <span class="blue">Service Side Render</span>
* <span class="blue">Custom Attribute</span>
* <span class="blue">Context</span>
* <span class="blue">new lifecycles</span>
* <span class="blue">React.memo</span>
* <span class="blue">Hooks</span>

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]
# Concurrent Render
----

![](http://with.muyunyun.cn/1daa3d783a4a7ed7f742882a08a3aa09.jpg){:&.zoomIn}

* <span class="red">Time Slicing 对应解决左侧的问题 {:&.zoomIn}</span>
* <span class="red">Suspense 对应解决了右侧的问题</span>
* <span class="red">Fiber 架构是上述两者的基石</span>

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## Time Slicing

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 现阶段

![](http://with.muyunyun.cn/39db8e34ec1ce048695c3bde132a739e.jpg) {:&.zoomIn}

* <span class="blue">一次性潜水到底 {:&.zoomIn}</span>
* <span class="blue">中途遇到优先级更高的事件无法调整相应的顺序</span>

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## Fiber 架构如何解决(浅显理解)?

![](http://with.muyunyun.cn/02a6b5ac36b12b3c676157ef3985fe4a.jpg) {:&.zoomIn}

* <span class="blue">现在变为可以每次潜 10 米，分 3 个 chunk 进行 {:&.zoomIn}</span>
* <span class="blue">chunk 和 chunk 之间通过链表连接</span>
* <span class="blue">chunk 间插入优先级更高的任务, 先前的任务被抛弃</span>
* <span class="green">requestIdleCallback(): 借力此 api, 浏览器能在空闲的时间处理低优先级的事</span>
* <span class="red">开启 Async Render 后，获取异步数据的方法应放到 render 后面的生命周期钩子里(phase 2 阶段)进行, 因为 render 前面的生命周期钩子(phase 1阶段)会被执行多次</span>
* <span class="red">并没有缩短原先组件的渲染时间(甚至还加长了)，但用户却能感觉操作变流畅了</span>

![](https://image-static.segmentfault.com/104/345/1043453063-5a9cd751cba93_articlex) {:&.zoomIn}

[note]
> We've built a generic way to ensure that high-priority updates like user input don't get blocked by rendering low-priority updates.
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Suspense(16.6)

* code splitting(16.6, 已上线): 文件懒加载。在此之前的实现方式是 [react-loadable](https://github.com/jamiebuilds/react-loadable) {:&.zoomIn}
* 并发模式(16.8, 2019 年 Q2 季度);
* data fetching(16.9 版本, 2019 年中): 数据动态呈现;

[note]
```js
import React, { lazy, Suspense } from 'react'
const OtherComponent = lazy(() => import('./OtherComponent'))

function MyComponent() {
  return (
    <Suspense fallback={<div>loading...</div>}>
      <OtherComponent />
    </Suspense>
  )
}
```

一种简单的预加载思路

```js
const OtherComponentPromise = import('./OtherComponent');
const OtherComponent = React.lazy(() => OtherComponentPromise);
```

> [preload](https://medium.com/@pomber/lazy-loading-and-preloading-components-in-react-16-6-804de091c82d)
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Portals

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 实现一个 Modal 组件
----
<iframe data-src="https://codepen.io/gaearon/pen/yzMaBd" src="about:blank;"></iframe>

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 冒泡到父节点的兄弟节点?
----
<iframe data-src="https://codepen.io/gaearon/pen/jGBWpE" src="about:blank;"></iframe>

[note]
如果组件返回是 Portal 对象，则将该组件的父组件的上的事件 copy 到该组件上。其实并不是真的冒泡到了父节点的兄弟节点上。
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Error Boundaries

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## componentDidCatch(error, errorInfo)
----
<iframe data-src="https://codepen.io/gaearon/pen/wqvxGa?editors=0010" src="about:blank;"></iframe>

[note]
`componentDidCatch(error, errorInfo)`, 它能将子组件生命周期里所抛出的错误捕获, 防止页面全局崩溃。

componentDidCatch 并不会捕获以下几种错误

* 事件机制抛出的错误(事件里的错误并不会影响渲染)
* Error Boundaries 自身抛出的错误
* 异步产生的错误
* 服务端渲染
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# 服务端渲染

[note]
在 React 16 版本中引入了 `React.hydrate()`, 它的作用主要是将相关的事件`注水`进 `html` 页面中, 同时会比较前端生成的 `html` 和服务端传到前端的 `html` 的文本内容的差异, 如果两者不一致将前端产生的文本内容替换服务端生成的(忽略属性)。
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# 自定义属性

[note]
在 React 16 版本中, 支持自定义属性(推荐 `data-xxx`), 因而 React 可以少维护一份 attribute 白名单, 这也是 React 16 体积减少的一个重要因素。
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## react 16 中 render 新增的返回类型

* React elements {:&.zoomIn}
* <span class="yellow">Arrays and fragments</span>
* <span class="yellow">Portals</span>
* <span class="yellow">String and numbers</span>
* <span class="yellow">Booleans or null</span>

[note]
```js
const renderArray = () => [
  <div key="A">A</div>
  <div key="B">B</div>
]
```

> render() 支持返回数组的特性类似 [Fragments](https://reactjs.org/docs/fragments.html)(16.2), 使用 Fragments 可以不用写 key。
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Context(16.3、16.6)

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 冗余的传递

```js
<Page riderId={riderId} />
// ... which renders ...
<RiderDetail riderId={riderId} />
// ... which renders ...
<RiderLevel riderId={riderId} />
// ... which renders ...
<Avatar riderId={riderId} />
```

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 之前可以怎么解决呢

```js
function Page(props) {
  const avatar = <Avatar riderId={props.riderId} />
  return <RiderDetail avatar={avatar} />
}

<Page riderId={riderId} />
// ... which renders ...
<RiderDetail avatar={avatar} />
// ... which renders ...
<RiderLevel avatar={avatar} />
// ... which renders ...
{ props.avatar }
```

* 官方推荐这种 {:&.zoomIn}

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## context

```js
const RiderContext = React.createContext(1) // 这里为默认值

function Page(props) {
  const riderId = props.riderId
  return (
    <RiderContext.Provider value={riderId}>
      <RiderDetail />
    </RiderContext.Provider>
  )
}

function RiderDetail() {
  return <RiderLevel />
}

class RiderLevel extends React.Component {
  static contextType = RiderContext
  render() {
    return <Avatar avatar={this.context} />;
  }
}
```

[note]
[proposal-static-class-features](https://github.com/tc39/proposal-static-class-features)
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# new life cycle

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

![](https://user-images.githubusercontent.com/12389235/41266906-b6a6e75a-6e2b-11e8-8266-9597b2d57f11.png)

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 移除的 3 个钩子以及为什么要移除？

* `componentWillMount()` {:&.zoomIn}
* `componentWillReceiveProps(nextProps)`
* `componentWillUpdate()`

[note]
```js
componentWillReceiveProps(nextProps) {
  if (nextProps.riderId !== this.props.riderId) {
    fetchData()
  }
}
```

```js
getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.riderId !== prevState.riderId) {
    return {
      riderId: nextProps.riderId
    }
  }
  // 返回 null 则表示 state 不用作更新
  return null
}
```
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 新加入的 2 个钩子

* `getDerivedStateFromProps(nextProps, prevState)`: 更加语义化, 用来替代 `componentWillMount()` 和 `componentWillReceiveProps(nextProps)` {:&.zoomIn}
* `getSnapshotBeforeUpdate(prevProps, prevState)`: 可以将该钩子返回的结果传入 componentDidUpdate 的第三个参数中, 从而达到 dom 数据统一。用来替代 componentWillUpdate()

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# React.memo(16.6)

* `React.memo` 是一个高阶组件, 它使无状态组件拥有有状态组价中的 `shouldComponentUpdate()` 以及 `PureComponent` 的能力 {:&.zoomIn}

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

```js
const MyComponent = React.memo(function MyComponent(props) {
  ...
})
```

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Hooks(16.7)

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 什么是 Hooks

在 React 16.7 之前，React 有两种形式的组件，有状态组件(类)和无状态组件(函数)。Hooks 的意义就是赋能先前的无状态组件，让之变为有状态。{:&.zoomIn}

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## useState
----

```js
function App() {
  const [count, setCount] = useState(0)

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  )
}
```
[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## useEffect(fn)

在每次 render 后都会执行这个钩子。可以将它当成是 `componentDidMount`、`componentDidUpdate`、`componentWillUnmount` 的合集。它的优点因此有{:&.zoomIn}

1. 可以避免在 `componentDidMount、componentDidUpdate` 书写重复的代码 {:&.zoomIn};
2. 可以将关联逻辑写进一个 `useEffect`;(在以前得写进不同生命周期里);

[note]
在上述提到的生命周期钩子之外，其它的钩子是否在 hooks 也有对应的方案或者舍弃了其它生命周期钩子, 后续进行观望。
[/note]

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

## 聊聊 React 的未来

![](http://with.muyunyun.cn/fd1dd7ca2ba34bebef2d489c63befa25.jpg) {:&.zoomIn}

[slide style="background-image:url('/img/bg1.png')" data-transition="cards"]

# Q & A

## Thanks

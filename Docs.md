> Doc link: https://reactjs.org/docs/getting-started.html

# Installation

## Getting Started

how to learn React?

- by doing: Tutorial
- step by step: Main Concept 

I choose the second.



## Add React to a Website

### 1. embed React into HTML

you can use react as a `jquery` library to your existing HTML page

### 2. add `jsx` to a project

if you want to use `jsx` grammar,use `babel` to convert.

a `jsx` grammar like this:

 ```js
class LikeButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = { liked: false };
  }

  render() {
    if (this.state.liked) {
      return 'You liked this.';
    }
    // a jsx grammer like this:
    return (
      <button onClick={() => this.setState({ liked: true }) }>
        Like
      </button>
    );
    // plain js
    /*return React.createElement(
        'button',
        { onClick: function onClick() {
            return _this2.setState({ liked: true });
          } },
        'Like'
     );
     */
  }
}
 ```

## Create a New React App

very simple,just run:

```visual basic
npx create-react-app my-app
cd my-app
npm start
```

# Main concepts

## 1. Hello World

```js
// <div id="root"></div>
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

I find this doc is very nice and considerate !

## 2. Introducing `JSX`

- `JSX`语法实际上是在创建对象，产生的对象称为`React elements`;

- 对这些`React elements`进行渲染，构建出`DOM`

```js
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
// => 等于如下写法：
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);

// => 创建出的对象（React elements）如下形式：
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

## 3. Rendering Elements

> An element describes what you want to see on the screen.

原则：尽可能少的操作`DOM`

如下面react官网的例子就是很好的说明：

```js
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));}

setInterval(tick, 1000);
```

> Even though we create an element describing the whole UI tree on every tick, only the text node whose contents have changed gets updated by React DOM



![DOM inspector showing granular updates](assets/granular-dom-updates.gif)

## 4. Components and Props

> Conceptually, `components` are like JavaScript functions. They accept arbitrary inputs (called “`props`”) and return `React elements` describing what should appear on the screen.

- Component的两种写法：

  ```js
  // Function Components
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  
  // => 等价于下面写法
  
  // Class Components
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```

- 渲染Component的机制

  官网例子：

  ```js
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  
  const element = <Welcome name="Sara" />;
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
  ```

  分析component的渲染到页面上的过程：

  1. we call `ReactDOM.render()` the `<Welcome name="Sara" />` element.

  2. React calls the `Welcome` component with `{name: 'Sara'}` as the ***props***.

  3. Our `Welcome` component returns a `Hello, Sara` element as the result

  4. React DOM efficiently updates the DOM to match `Hello, Sara`.

- Components可以组合使用

  `Components`可以组合使用，也可以将常用部分提取出来作为`components`

> tips : **Props are Read-Only**

## 5. State and Lifecycle

- 何谓`state`

  > A component needs `state` when some data associated with it changes over time. For example, a `Checkbox` component might need `isChecked` in its state,

  - 组件内部涉及的数据会根据时间条件变化

  - 随着数据的变化，要相应的更新`DOM`

  - 此时：需要使用`state`去接收这些不断变化的数据，然后通过`setState`更新`DOM`

  

- 何谓`Lifecycle methods ` 

  > `Lifecycle methods` are custom functionality that gets executed during the different phases of a component. There are methods available when the component gets created and inserted into the DOM (`mounting`), when the component updates, and when the component gets `unmounted` or removed from the DOM

  - 组件的生命周期即组件从被创建、渲染插入DOM，从DOM中移除所经历的阶段

  - 每个阶段都有对应的函数，你可以去做相应的操作，比如下面demo中，`componentDidMount`函数在组件被渲染进DOM时调用，`componentWillUnmount`函数在组件从`DOM`中移除时调用

  

- `state` VS `props`

  > The most important difference between `state` and `props` is that `props` are passed from a parent component, but `state` is managed by the component itself. A component cannot change its `props`, but it can change its `state`.

  - `props`是由外部传入组件的，组件不能改变`props`
  - `state`是在组件内部进行管理的，组件可以改变 `state`

  

- 何谓`单向数据流`

  父组件可以向子组件传值，反之不行。比如下面DEMO中：父组件`Clock`将自己`state`中存的`date`的值传给了子组件`FormattedDate`

官网DEMO：

```js
// 子组件
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
 
   // 生命周期函数
  componentDidMount() {  
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <FormattedDate date={this.state.date} />
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

## 6. Handling Events

`Html`中处理添加事件：

```js
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

`React`中：

```js
function ActionLink() {
  function handleClick(e) { 
      e.preventDefault();  
      console.log('The link was clicked.');  
  }
  return (
    <a href="#" onClick={handleClick}> Click me </a>
  );
}
```

## 7. Conditional Rendering

- 根据不同条件，渲染不同的组件

- 如果组件的返回值为null，则不渲染该组件

```js
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);

```
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

## 8. Lists and Keys

`React`中渲染列表，简单粗暴：

```js
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

That it is! cool!

注意遍历时要给`element`加`key`属性，否则控制台会报警告。

## 9. Forms

> An input form element whose value is controlled by React in this way is called a “***controlled component***”

```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

`input`,`textarea`,`select`都是以上述的方式被`React`控制的：`value={this.state,value} onChange={this.handleChange}`

## 10. Lifting  State Up

将多个组件共享的数据提升至 离这些组件最近的共同父组件中进行管理。

> There should be a single “source of truth” for any data that changes in a React application. Usually, the state is first added to the component that needs it for rendering. Then, if other components also need it, you can ***lift it up*** to their closest common ancestor. Instead of trying to sync the state between different components, you should rely on the [top-down data flow](https://reactjs.org/docs/state-and-lifecycle.html#the-data-flows-down).

官网[demo](https://codepen.io/gaearon/pen/WZpxpz?editors=0010)是个非常好的例子：

![Monitoring State in React DevTools](assets/react-devtools-state.gif)

## 11. Composition vs Inheritance

> Remember that components may accept arbitrary props, including primitive values, React elements, or functions.

`React`的组件的`composition`和`props`组合起来用，而不是用继承，如下demo：

```js
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}
```

## 12. Thinking In React

React change the way that Web apps should be build.

`UI` -> `Web apps` 四步：

1. Break The UI Into A Component Hierarchy 

   将UI结构拆解成组件结构

2. Build A Static Version in React

   > It’s best to decouple these processes because building a static version requires a lot of typing and no thinking, and adding interactivity requires a lot of thinking and not a lot of typing. 

   这个阶段用不到`state`

3. Identify The Minimal (but complete) Representation Of UI State

   找到`state`,即交互中哪些数据会改变

4. Identify Where Your State Should Live

   将`state`放到合适的组件中维护

5. Add Inverse Data Flow

   如果有反向数据流，即子组件影响父组件内的状态，传回调函数给子组件去影响父组件的值

# Advance Guides

## Accessibility

- 如何只用键盘就即可使用网页全部功能
- 网页如何服务残障人士

## Code-Splitting

Why split code?

> Code-splitting your app can help you “lazy-load” just the things that are currently needed by the user, which can dramatically improve the performance of your app.

## Context

数据用props在组件之间传递，当组件层次较深，会显得冗余，用`context`：

> Context provides a way to pass data through the component tree without having to pass props down manually at every level.

```js
const MyContext = React.createContext(defaultValue);
<MyContext.Provider value={/* some value */}>
```

## Error Boundaries

React是如何优雅地处理错误的。React 16中引入`error boundary`

```react
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

## Forwarding Refs

> Ref forwarding is a technique for automatically passing a [ref](https://reactjs.org/docs/refs-and-the-dom.html) through a component to one of its children. This is typically not necessary for most components in the application. However, it can be useful for some kinds of components, especially in reusable ***component libraries***

写组件库时会用到，ref可以拿到组件所渲染的DOM

## Fragments

> Fragments let you group a list of children without adding extra nodes to the DOM

用来包裹一些特殊DOM节点（html结构中的，tr td、ul li...），因为这些节点不能用div来包裹

```react
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```

## Higher-Order Components

> Concretely, **a higher-order component is a function that takes a component and returns a new component.**

```react
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

当两个`compent`中重复代码较多时，可用高阶组件，将公共部分提取，提高代码的复用

## Integrating with other libraries

现在就可以把react用到项目上去：

```js
$('#container').html('<button id="btn">Say Hello</button>');
$('#btn').click(function() {
  alert('Hello!');
});
```

```react
function Button() {
  return <button id="btn">Say Hello</button>;
}

ReactDOM.render(
  <Button />,
  document.getElementById('container'),
  function() {
    $('#btn').click(function() {
      alert('Hello!');
    });
  }
);
```

## `JSX` In Depth

`JSX`语法的详细介绍，放在项目里用来替代渲染模板也不错哦。

## Optimizing Performance


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


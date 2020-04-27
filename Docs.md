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


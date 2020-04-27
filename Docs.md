> Doc link: https://reactjs.org/docs/getting-started.html

# Installation

## Gettting Started

how to learn React?

- by doing：Tutorial
- step by step: Main Concept 

I choose the second.



## Add React to a Website

### 1. embed React into html

you can use react as a `jquery` libray to your exsiting HTML page

### 2. add `jsx` to a project

if you want to use `jsx` grammer,use `babel` to convert.

a `jsx` grammer like this:

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




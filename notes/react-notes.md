# React

- modular, reusable components
- uses JSX to combine HTML with the full power of JavaScript
- allows us to easily create SPA
- virtual DOM - better performance, better user experience

## Environment

- react + react-dom
- webpack: bundling tool which combines and minifies JavaScript files and other static resources
- babel: a set of tools which mainly used to convert ES6 to backwards compatible versions of JS but can also convert JSX to JS
- create-react-app

## JSX

- syntax extension to JavaScript
- JSX can look a lot like HTML but is really a JavaScript expression which represents function calls - babel is responsible for this compilation
- JSX includes html tags (lowercase tags), JavaScript expressions (indicated with {}), and React components (capitalized tags)

## Components

- primary unit of code reuse in React

There are 4 ways to create components

1. createClass

```javascript
const HelloWorld = React.createClass({
  render: function () {
    return <h1>Hello World</h1>;
  },
});
```

2. ES Classes

```javascript
class HelloWorld extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h1>Hello World</h1>;
  }
}
```

3. Function

```javascript
function HelloWorld(props) {
  return <h1>Hello World</h1>;
}
```

4. Arrow Function

```javascript
const HelloWorld = (props) => <h1>Hello World</h1>;
```

### When and Why are Functions Preferred?

- simpler syntax, react assumes return statement returns that of the render function
- recommended over class components when possible
  - avoids the need for extending React.Component, class based structures like the constructor and (for arrow functions) the quirks of the 'this' keyword
  - less transpiled code, more efficient performance
  - signal to noise ratio (cleaner and less code)
  - easy to test

### Container Components

- contain little or no markup
- mainly concerned with application logic
- typically stateful

### Presentation Components

- nearly all markup
- receives data and actions via props from container components
- typically not stateful

* we refer to these components as container/presentation but you may also hear smart/dumb, stateful/stateless, controller view/view

### PropTypes

1. Can I use TypeScript with React? [Yes!](https://create-react-app.dev/docs/adding-typescript/)
2. Can I leverage typechecking with react alone? [Yes!](https://reactjs.org/docs/typechecking-with-proptypes.html)

## Data in React

### Props

- look like HTML attributes, allow you to pass data down to child components
- immutable - if you want to change props, you need to pass down a function provided by the parent

### State

- holds mutable state
- do not set state directly

#### State In Class Components

```javascript
class Example extends Component {
  constructor(props) {
    super(props);
    this.state = { name: "" };
  }
  onChange(event) {
    this.setState({ name: event.target.value });
  }
  render() {
    return <input onChange={this.onChange} value={this.state.name} />;
  }
}
```

```javascript
class Example extends Component {
  state = { name: "" };
  onChange(event) {
    this.setState({ name: event.target.value });
  }
  render() {
    return <input onChange={this.onChange} value={this.state.name} />;
  }
}
```

#### State In Function Components

```javascript
const Example = () => {
  const [name, setName] = useState("");

  onChange(event) {
    setName(event.target.value);
  }

    return <input onChange={this.onChange} value={name} />;
}
```

#### Class Component Lifecycle

- react components have three lifecycle phases
  1. Mounting - when an instance of a component is being created and inserted into the DOM
  2. Updating - when an update is caused by changes to props or state
  3. Unmounting - when a component is being removed from the DOM
- when changing state in a class component, there are methods associated with these lifecycle phases that you can configure
  1. componentDidMount
  2. componentDidUpdate
  3. componentWillUnmount

#### Hooks in Function Components

- lifecycle methods are only available in class based components
- react has a handful of hooks, and you can create your own custom hooks
- useState is used to handle local state
  - takes a param of initial value
  - returns the state and a function used to set the state
- useEffect is used to handle side effects
  - runs after each render
  - takes two params: first is the callback which occurs, and the second is the dependency array
    - the execution of your callback is determined by the values specified in your dependency array
    - when a state or prop in your dependency array changes, your callback is executed
  - useEffect combines the functionality of the lifecycle methods provided in class based components

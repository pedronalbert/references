# React
<!-- TOC -->

- [React](#react)
  - [Component](#component)
    - [Functional](#functional)
    - [Stateful](#stateful)
    - [State](#state)
    - [LifeCycle Methods](#lifecycle-methods)
    - [Proptypes](#proptypes)
    - [Error Handling](#error-handling)
    - [Refs](#refs)
      - [Forwarding](#forwarding)
    - [Portal](#portal)
  - [JSX](#jsx)
    - [Binding](#binding)
      - [Property](#property)
    - [List](#list)
    - [Event Handling](#event-handling)
      - [Caveats](#caveats)
    - [Children](#children)
    - [Fragment](#fragment)
      - [Short Syntax](#short-syntax)
  - [High Order Components](#high-order-components)
    - [Proxy Pass](#proxy-pass)
    - [Inheritance Inversion](#inheritance-inversion)

<!-- /TOC -->
## Component
### Functional
```js
const MyComponent = props => (<div>
  ...
</div>);
```

### Stateful
```js
class MyComponent extends Component {
  constructor(props) {
    super(props);

    this.state = {
      //...
    }
  }

  render() {
    return (<div>
      ...
    </div>)
  }
}
```

### State
```js
this.setState({
  // ...
});

this.setState((state, props) => ({
  //...
}));
```

### LifeCycle Methods
```js
componentWillMount()
componentDidMount()
componentWillReceiveProps(nextProps)
shouldComponentUpdate(nextProps, nextState)
componentWillUpdate(nextProps, nextState)
componentDidUpdate(prevProps, prevState)
componentWillUnmount()
```

### Proptypes
```js
.array
.bool
.func
.number
.object
.string
.symbol
.node
.element
.instanceOf()
.oneOf(types: Any[])
.oneOfType(types: PropType[])
.arrayOf(type: PropType)
.objectOf(type: PropType)
.shape({
  key: PropType
})

.isRequired
```

### Error Handling
```js
componentDidCatch(error, info)
```

### Refs
```js
constructor(props) {
  super(props);

  this.myInput = React.createRef();
}

focusInput() {
  this.myInput.current.focus();
}

render()  {
  return <input ref={this.myInput} />
}
```

#### Forwarding
[Docs](https://reactjs.org/docs/forwarding-refs.html)
```js
const MyButton = React.forwardRef((props, ref) => (
  <button ref="ref">
    {props.children}
  </button>
));

class MyComponent extends Component {
  constructor(props) {
    super(props);

    this.buttonRef = React.createRef();
  }

  render() {
    return <div>
      <MyButton ref={this.buttonRef} />
    </div>
  }
}
```

### Portal
```js
render() {
  return React.createPortal(
    <Component />,
    domNode
  );
}
```

## JSX

### Binding
```js
<div>{bar}</div>
```

#### Property
```js
<MyComponent foo={bar}>
```

### List
```js
{users.map(user => <UserProfile
  user={user}
  key={user.id}
/>)}
```

### Event Handling
[SyntheticEvent Docs](https://reactjs.org/docs/events.html)
```js
const eventHandler = (e: SyntheticEvent) => {
  //...
};

<button onClick={eventHandler} />
<button onClick={eventHandler.bind(this, user)} />
<button onClick={(e) => eventHandler.bind(this, e)} />
```

#### Caveats
> When you define a eventHandler on class component you have to bind the handers
```js
class MyComponent extends Component {
  constructor(props) {
    super(props);

    this.handleClick = this.handleClick.bind(this);
  }
}
```

### Children
```js
<div>
  {props.children}
</div>
```

### Fragment
```js
import { Fragment } from 'react';

<Fragment>
  <Component1 />
  <Component2 />
</Fragment>
```

#### Short Syntax
```js
<>
  <Component1 />
  <Component2 />
</>
```


## High Order Components
### Proxy Pass
```js
const ppHOC = (WrapperdComponent) => {
  return class PP extends Component {
    // ...
  }
}
```

### Inheritance Inversion
```js
function iiHOC(WrappedComponent) {
  return class Enhancer extends WrappedComponent {
      render() {
        super.render();
      }
  }
}
```

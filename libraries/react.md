# React
<!-- TOC -->autoauto- [React](#react)auto  - [Component](#component)auto    - [Functional](#functional)auto    - [Stateful](#stateful)auto    - [State](#state)auto    - [LifeCycle Methods](#lifecycle-methods)auto    - [Proptypes](#proptypes)auto    - [Error Handling](#error-handling)auto    - [Refs](#refs)auto      - [Forwarding](#forwarding)auto    - [Portal](#portal)auto    - [Hooks](#hooks)auto      - [UseState](#usestate)auto      - [UseEffect](#useeffect)auto  - [JSX](#jsx)auto    - [Binding](#binding)auto      - [Property](#property)auto    - [List](#list)auto    - [Event Handling](#event-handling)auto      - [Caveats](#caveats)auto    - [Children](#children)auto    - [Fragment](#fragment)auto      - [Short Syntax](#short-syntax)auto  - [High Order Components](#high-order-components)auto    - [Proxy Pass](#proxy-pass)auto    - [Inheritance Inversion](#inheritance-inversion)autoauto<!-- /TOC -->
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

### Hooks

#### UseState
```js
const Component = () => {
  const [name, setName] = useState('default name');
}
```

#### UseEffect

El Hook useEffect nos permite ejecutar código cuando se monta, desmonta o actualiza nuestro componente, el primer argumento es la funcion y el segundo argumento es un array donde se hará el watch que hara que la función se reejecute


```js
const Component = () => {
  useEffect(() => {
    //...
  }, [name]);
};
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

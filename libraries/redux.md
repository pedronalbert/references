# Redux
## Actions
```js
const myAction(params) => ({
  type: ACTION_TYPE,
  payload: {
    /// ...params
  },
  error: true,
  meta: {
    // ...metadata
  }
})
```

### Async
> With redux-thunk
```js
const fetchUsers = ids => {
  return (dispatch) => {
    // ... dispatch actions and wait for promises
  };
};
```

## Reducer
[TypeToReducer Utility](https://github.com/tomatau/type-to-reducer)

```js
const myReducer = (state = initialState, action) => {
  switch(action.type) {
    // ...
  }

  return state;
}
```

### Combining
```js
import { combineReducers } from 'redux';

const reducer = combineReducers({
  reducerOne,
  reducer2: reducerTwo,
});
```

## Store
```js
import { createStore } from 'redux';
import reducers from './reducers';

const store = createStore(reducers, initialState?);
```

## Middleware
```js
const myMiddleware = store => next => action => {
  console.log('Dispatching', action);
  const result = next(action);

  return resul;
}

// store
import { createStore, applyMiddlware } from 'redux';

const store = createStore(
  reducers,
  applyMiddleware(myMiddleware, ...),
);
```

## React-Redux
```js
import { connect } from 'react-redux';

const mapStateToProps = (state, ownProps) => {
  return {
    // ...
  };
};

const mapDispatchToProps = (dispatch, ownProps) => {
  return {
    onClick() {
      dispatch(action(params));
    },
  };
};

const MyComponent = connect(
  mapStateToProps,
  mapDispatchToProps,
)(MyComponent);
```
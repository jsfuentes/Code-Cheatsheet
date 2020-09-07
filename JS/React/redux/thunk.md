# Thunk

The Redux core (ie, `createStore`) is completely synchronous. When you call `store.dispatch()`, the store runs the root reducer, saves the return value, runs the subscriber callbacks, and returns, with no pause. By default, any asynchronicity has to happen outside of the store.

But, what if you want to have async logic interact with the store by dispatching or checking the current store state? That's where [Redux middleware](https://redux.js.org/advanced/middleware) come in. They extend the store, and allow you to:

- Execute extra logic when any action is dispatched (such as logging the action and state)
- Pause, modify, delay, replace, or halt dispatched actions
- Write extra code that has access to `dispatch` and `getState`
- Teach `dispatch` how to accept other values besides plain action objects, such as functions and promises, by intercepting them and dispatching real action objects instead

#### Why Use Thunks?[#](https://redux-toolkit.js.org/tutorials/advanced-tutorial#why-use-thunks)

You might be wondering what the point of all this is. There's a few reasons to use thunks:

- Thunks allow us to write reusable logic that interacts with *a* Redux store, but without needing to reference a specific store instance.
- Thunks enable us to move more complex logic outside of our components
- From a component's point of view, it doesn't care whether it's dispatching a plain action or kicking off some async logic - it just calls `dispatch(doSomething())` and moves on.
- Thunks can return values like promises, allowing logic inside the component to wait for something else to finish.

For further explanations, see [these articles explaining thunks in the `redux-thunk` documentation](https://github.com/reduxjs/redux-thunk#why-do-i-need-this).

## Usage

The thunk middleware will see the function, prevent it from actually reaching the "real" store, and call our function and pass in `dispatch` and `getState` as arguments. So, a "thunk function" looks like this:

```js
function exampleThunkFunction(dispatch, getState) {
  // do something useful with dispatching or the store state here
}

// normally an error, but okay if the thunk middleware is added
store.dispatch(exampleThunkFunction)
```


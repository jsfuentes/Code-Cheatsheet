# Thunk

[Do I need async middleware? ](http://stackoverflow.com/questions/35411423/how-to-dispatch-a-redux-action-with-a-timeout/35415559#35415559)

Just defining a function that takes the dispatch works fine most of the time

```javascript
let nextNotificationId = 0
export function showNotificationWithTimeout(dispatch, text) {
  const id = nextNotificationId++
  dispatch(showNotification(id, text))

  setTimeout(() => {
    dispatch(hideNotification(id))
  }, 5000)
}

// component.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged in.')

// otherComponent.js
showNotificationWithTimeout(this.props.dispatch, 'You just logged out.')    
```

More advanced async control flows like multi-step onboarding or retrying failed requests might need [Redux Saga](https://github.com/yelouafi/redux-saga) or [Redux Loop](https://github.com/raisemarketplace/redux-loop). 

## Overview

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

 **If Redux Thunk middleware is enabled, any time you attempt to dispatch a function instead of an action object, the middleware will call that function with `dispatch` method itself as the first argument** and `getState` as the second.

 So, a "thunk function" looks like this:

```js
export const fetchIssues = (
  org: string,
  repo: string,
  page?: number
): AppThunk => async dispatch => {
  try {
    dispatch(getIssuesStart())
    const issues = await getIssues(org, repo, page)
    dispatch(getIssuesSuccess(issues))
  } catch (err) {
    dispatch(getIssuesFailure(err.toString()))
  }
}
```

### Basics

```jsx
function exampleThunkFunction(dispatch, getState) {
  // do something useful with dispatching or the store state here
}

// normally an error, but okay if the thunk middleware is added
store.dispatch(exampleThunkFunction)

//Using like regular action creator
function exampleThunk() {
  return function exampleThunkFunction(dispatch, getState) {
    // do something useful with dispatching or the store state here
  }
}

// normally an error, but okay if the thunk middleware is added
store.dispatch(exampleThunk())
```


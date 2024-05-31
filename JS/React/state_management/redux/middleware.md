# Middleware

Intercept actions and does more logic/async/random code then dispatchs more actions or forwards to reducer or next middleware



### OG

Can be thought of as editing the dispatch(next) of store by chaining them 

```js
import { createStore, combineReducers, applyMiddleware } from 'redux'

const logger = store => next => action => {
  console.log('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  return result
}

const store = createStore(
  todoApp,
  applyMiddleware(logger)
)
```

Apparently will hold the bulk of your applications logic


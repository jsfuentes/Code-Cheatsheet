# Redux Toolkit

```
yarn add react-redux @reduxjs/toolkit
```

includes the Redux core, as well as other key packages like(Redux Thunk and Reselect)  and helper functions

## Helper Functions

- A [`configureStore()` function](https://redux-toolkit.js.org/api/configureStore) with simplified configuration options. It can automatically combine your slice reducers, adds whatever Redux middleware you supply, includes `redux-thunk` by default, and enables use of the Redux DevTools Extension.

```jsx
const store = configureStore({
  reducer: counter
})
```

- A [`createSlice()` function](https://redux-toolkit.js.org/api/createSlice) that accepts a set of reducer functions, a slice name, and an initial state value, and automatically generates a slice reducer with corresponding action creators and action types. Default(unknown action type) returns current. 
  - Mutations of state will auto create a new object on change as needed

```jsx
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: 0,
  reducers: {
    increment: (state) => state + 1,
    decrement: (state) => state - 1,
    //called when dispatch type counter/addTodo
    addTodo(state, action) {
      const { id, text } = action.payload;
      state.push({ id, text, completed: false });
      //allowed to mutuate because function wrapped with produce from Immer library
    },
  },
});

export const { increment, decrement, addTodo } = todosSlice.actions;

export default todosSlice.reducer;
```

- The [`createSelector` utility](https://redux-toolkit.js.org/api/createSelector) from the [Reselect](https://github.com/reduxjs/reselect) library, re-exported for ease of use.

```js
import React from 'react'
import { useSelector } from 'react-redux'

export const CounterComponent = () => {
  const counter = useSelector(state => state.counter)
  return <div>{counter}</div>
}
```

#### Old Helpers but unneeded b/c create Slic

- A [`createReducer()` utility](https://redux-toolkit.js.org/api/createReducer) that lets you supply a lookup table of action types to case reducer functions, rather than writing switch statements. In addition, it automatically uses the [`immer` library](https://github.com/mweststrate/immer) to let you write simpler immutable updates with normal mutative code, like `state.todos[3].completed = true`.

```jsx
//OLD
function counter(state = 0, action) {
  switch (action.type) {
    case increment.type:
      return state + 1
    case decrement.type:
      return state - 1
    default:
      return state
  }
}

//NEW
const increment = createAction('INCREMENT')
const decrement = createAction('DECREMENT')

const counter = createReducer(0, {
  [increment.type]: state => state + 1,
  [decrement.type]: state => state - 1
})
```

- A [`createAction()` utility](https://redux-toolkit.js.org/api/createAction) that returns an action creator function for the given action type string. The function itself has `toString()` defined, so that it can be used in place of the type constant.

```jsx
const increment = createAction('INCREMENT')
const decrement = createAction('DECREMENT')

//With payload generation helper, must return object with payload
export const addTodo = createAction('ADD_TODO', text => {
  return {
    payload: { id: nextTodoId++, text }
  }
})

const counter = createReducer(0, {
  [increment]: state => state + 1,
  [decrement]: state => state - 1
})

const store = configureStore({
  reducer: counter
})

document.getElementById('increment').addEventListener('click', () => {
  store.dispatch(increment())
})
```

- However, we can take advantage of `createAsyncThunk` to clean up the above code, and to create those three actions automatically:

  ```javascript
  const usersSlice = createSlice({
    name: 'users',
    initialState: { entities: [], loading: 'idle' },
    reducers: {
      // standard reducer logic, with auto-generated action types per reducer
    },
    extraReducers: {
      // Add reducers for additional action types here, and handle loading state as needed
      [fetchUserById.fulfilled]: (state, action) => {
      // Add user to the state array
        state.entities.push(action.payload)
    }
    }
  })
  
  const getUsers = createAsyncThunk("users/getUsers", () => {
    return fetch("/api/users/")
      .then(response => {
        if (!response.ok) throw Error(response.statusText);
        return response.json();
      })
      .then(json => json);
  });
  ```
  
  What `createAsyncThunk` does here, is to **automatically create an action creator for each Promise state**. For example if we name our async thunk "users/getUsers", it generates:
  
  - **pending**: "users/getUsers/pending"
  - **rejected**: "users/getUsers/rejected"
  - **fulfilled**: "users/getUsers/fulfilled"
# Setup

### New Project

```
npx create-react-app my-app --template redux
```

### Existing Project

```bash
yarn add react-redux @reduxjs/toolkit
yarn add -D redux-devtools
```

`@reduxjs/toolkit` => includes the Redux core, as well as other key packages like(Redux Thunk and Reselect) and

### 1) Add Store

*Using latest configureStore with basic middleware instead of older createStore*

index.js

```jsx
import { configureStore } from "@reduxjs/toolkit";
import React, { Suspense } from "react";
import ReactDOM from "react-dom";

import rootReducer from "./redux/rootReducer.js";
import App from "./App.js"

const store = configureStore({
  reducer: rootReducer,
});

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

###2) Create Slice

featureSlice.js

```jsx
import { createSlice } from '@reduxjs/toolkit'

const todosSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    //called on dispatch of type todos/addTodo
    addTodo(state, action) {
      const { id, text } = action.payload
      state.push({ id, text, completed: false })
    }, 
    toggleTodo(state, action) {
      const todo = state.find(todo => todo.id === action.payload)
      if (todo) {
        todo.completed = !todo.completed
      }
    }
  }
})

export const { addTodo, toggleTodo } = todosSlice.actions

export default todosSlice.reducer

//async dispatch
export const login = ({ username, password }) => async dispatch => {
  try {
    // const res = await api.post('/api/auth/login/', { username, password })
    dispatch(loginSuccess({username}));
  } catch (e) {
    return console.error(e.message);
  }
}
```

### 3) Create root reducer

```jsx
import { combineReducers } from '@reduxjs/toolkit'

import todosReducer from './todos'
import visibilityFilterReducer from './visibilityFilter'

export default combineReducers({
  todos: todosReducer,
  visibilityFilter: visibilityFilterReducer
})
```

### 4) Use in App

```jsx
import {useDispatch, useSelector} from 'react-redux';
import {login, logout} from './store/user'

function App() {
  const dispatch = useDispatch()
  const { user } = useSelector(state => state.user)

      return(<div>
        Hi, {user.username}!
        <button onClick={() => dispatch(logout())}>Logout</button>
      </div>
    )

}
```


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

`@reduxjs/toolkit` => includes the Redux core with some sweet sugar, as well as other key packages like(Redux Thunk and Reselect)

###1) Create Slice

redux/todos.js

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

### 2) Create root reducer

redux/rootReducer.js

```jsx
import { combineReducers } from '@reduxjs/toolkit'

import todosReducer from './todos'
import visibilityFilterReducer from './visibilityFilter'

export default combineReducers({
  todos: todosReducer,
  visibilityFilter: visibilityFilterReducer
})
```

### 3) Add Store

index.js

```jsx
import { configureStore } from "@reduxjs/toolkit";
import { Provider } from "react-redux";
import React from "react";
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

### 4) Use in App

```jsx
import React from "react";
import { useDispatch, useSelector } from "react-redux";

import { addTodo, toggleTodo } from "./redux/todos";

export default function App() {
  const dispatch = useDispatch();
  const todos = useSelector((state) => state.todos);

  return (
    <div className="App">
      <h1> Todo List </h1>
      {todos.map((t) => (
        <div key={t.id}>
          {t.text} {t.completed ? "X" : "O"}
          <button onClick={() => dispatch(toggleTodo(t.id))}>Toggle</button>
        </div>
      ))}
      <button
        onClick={() =>
          dispatch(
            addTodo({ id: Math.floor(Math.random() * 1000), text: "Lalalal" })
          )
        }
      >
        Hit Me
      </button>
    </div>
  );
}
```


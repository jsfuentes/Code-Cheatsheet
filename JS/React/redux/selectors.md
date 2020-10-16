## Selectors

### useSelector()

```jsx
import { useDispatch, useSelector } from "react-redux";

const userStatus = useSelector((state) => ({state.userStatus.audioDeviceId, }));
const dispatch = useDispatch();
```

When action is dispatched, a `===` reference comparison of prev ft return and current will trigger resulting in rerender if different

Use multiple useSelectors(they will be batched)

*Dont return an object, will always rerender*, reselect or similar lib can help here

2nd arg is the equality function to be used

```javascript
import { shallowEqual, useSelector } from 'react-redux'

// later, doesn't seem to work with [] and [] ??
const selectedData = useSelector(selectorReturningObject, shallowEqual)
```

## CreateSelector()

[`createSelector` utility](https://redux-toolkit.js.org/api/createSelector) from the [Reselect](https://github.com/reduxjs/reselect) library, re-exported for ease of use.

```jsx
import React from "react";
import { useDispatch, useSelector } from "react-redux";
import { createSelector } from "reselect";

//fine to define here if only one instance of App
const selectNumOfDoneTodos = createSelector(
  (state) => state.todos,
  (todos) => todos.filter((todo) => todo.completed).length
);

export default function Done() {
  const num = useSelector(selectNumOfDoneTodos);
  return <div> DID {num} </div>;
}

```

If selector is used in multiple component instances and depends on the props, must make unique selector instance per component instance (see [here](https://github.com/reduxjs/reselect#accessing-react-props-in-selectors))

- Solution is to useMemo to create the Selector

```jsx
import React, { useMemo } from 'react'
import { useSelector } from 'react-redux'
import { createSelector } from 'reselect'

const makeNumOfTodosWithIsDoneSelector = () =>
  createSelector(
    state => state.todos,
    (_, isDone) => isDone,
    (todos, isDone) => todos.filter(todo => todo.isDone === isDone).length
  )

export const TodoCounterForIsDoneValue = ({ isDone }) => {
  const selectNumOfTodosWithIsDone = useMemo(
    makeNumOfTodosWithIsDoneSelector,
    []
  )

  const numOfTodosWithIsDoneValue = useSelector(state =>
    selectNumOfTodosWithIsDone(state, isDone)
  )

  return <div>{numOfTodosWithIsDoneValue}</div>
}

export const App = () => {
  return (
    <>
      <span>Number of done todos:</span>
      <TodoCounterForIsDoneValue isDone={true} />
      <span>Number of unfinished todos:</span>
      <TodoCounterForIsDoneValue isDone={false} />
    </>
  )
}
```


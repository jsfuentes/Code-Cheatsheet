# Hooks

#### Motivation

- Allow you to use state and effects in functions not classes
- Reuse state logic
- Have one block of effects for one purpose with clean up and everything
- Allows easier reuse of stateful logic often done with patterns like [higher-order components](https://reactjs.org/docs/higher-order-components.html) and [render props](https://reactjs.org/docs/render-props.html).

#### Basics

- Only call Hooks **at the top level**. Don’t call Hooks inside loops, conditions, or nested functions.
- Only call Hooks **from React function components**.

## State

```js
function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Updating *replace*s its value instead of setState which *merges*

## Effects

For data fetching, subscriptions, or manually changing the DOM because they can affect other components and can’t be done during rendering.

`useEffect` Hook runs after every render and offers clean up so === to  `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

```js
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### Conditional Effect

```js
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

Pass an empty array(`[]`) if you only want the effect on mount and unmount

#### Clean up

Add as return 

```js
  useEffect(() => {
    // ...
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

## Custom Hooks

```js
function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  });
  
  return width;
}
```

```js
function MyResponsiveComponent() {
  const width = useWindowWidth(); // Our custom Hook
  return (
    <p>Window width is {width}</p>
  );
}
```

### Other

```js
const value = useContext(MyContext);
```

Still need MyContext.Provider above

- [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer)

- [`useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback)

  - ```react
    function MeasureExample() {
      const [height, setHeight] = useState(0);
    
      const measuredRef = useCallback(node => {
        if (node !== null) {
          setHeight(node.getBoundingClientRect().height);
        }
      }, []);
    
      return (
        <>
          <h1 ref={measuredRef}>Hello, world</h1>
          <h2>The above header is {Math.round(height)}px tall</h2>
        </>
      );
    }
    ```

    Unlike useRef, notifies us on change of ref

- [`useMemo`](https://reactjs.org/docs/hooks-reference.html#usememo)

- [`useRef`](https://reactjs.org/docs/hooks-reference.html#useref)

  - ```react
    function TextInputWithFocusButton() {
      const inputEl = useRef(null);
      const onButtonClick = () => {
        // `current` points to the mounted text input element
        inputEl.current.focus();
      };
      return (
        <>
          <input ref={inputEl} type="text" />
          <button onClick={onButtonClick}>Focus the input</button>
        </>
      );
    }
    ```

    Can also be equivalent to instance variables in class components. Mutating the `.current` property won’t cause a re-render.

    Updating a ref is a side effect so it should be done only inside an `useEffect` (or `useLayoutEffect`) or inside an event handler.

- [`useImperativeHandle`](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)

- [`useLayoutEffect`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)

- [`useDebugValue`](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)
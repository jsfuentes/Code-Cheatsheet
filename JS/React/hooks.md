# Hooks

#### Motivation

- Allow you to use state and effects in functions not classes
- Reuse state logic
- Have one block of effects for one purpose with clean up and everything
- Allows easier reuse of stateful logic often done with patterns like [higher-order components](https://reactjs.org/docs/higher-order-components.html) and [render props](https://reactjs.org/docs/render-props.html).

#### Basics

- Only call Hooks **at the top level**. Don’t call Hooks inside loops, conditions, or nested functions.
- Only call Hooks **from React function components**.
- Functions/useCallbacks must be above their use in dependency arrays or else they *DONT ACTUALLY CAUSE A RERENDER*(cuz hoisting)

## All Hooks

- useState => See state.md

- useEffect => See effect.md

- useContext

  - Still need MyContext.Provider above

  ```jsx
  const value = useContext(MyContext);
  ```

- [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer)

  - If one element of your state relies on the value of another element of your state, then it's almost always best to use `useReducer`

- [`useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback)

  Not actually cheaper than defining function by itself. But makes the reference the same for React's equality check if you use the ft in **another hook or as a prop** to avoid reruns

  - ```jsx
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

  - ```jsx
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
    ```

  - Your app must still work perfectly well (maybe a bit slow though) if `useMemo` calls your callback on every render.

  - Introduces overhead, but for expensive pure computations

- [`useRef`](https://reactjs.org/docs/hooks-reference.html#useref)

  - ```jsx
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

- useTransition

  New in v18

  ```react
  const [isPending, startTransition] = useTransition();
  
  setInputValue(input);
  startTransition(() => {
    setSearchQuery(input);
  });
  ```

  For large UI transitions to mark them as interruptable so typing and stuff doesnt freeze it

- [`useImperativeHandle`](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)

- [`useLayoutEffect`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)

- [`useDebugValue`](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)

## Custom Hooks

##### useWindowWidth

```jsx
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

```jsx
function MyResponsiveComponent() {
  const width = useWindowWidth(); // Our custom Hook
  return (
    <p>Window width is {width}</p>
  );
}
```

##### useDebounce

```jsx
import { useEffect, useState } from "react";

function useDebounce(value, delay = 500) {
  const [debouncedVal, setDebouncedVal] = useState(value);

  useEffect(() => {
    const timeoutID = setTimeout(() => setDebouncedVal(value), delay);
    return () => clearTimeout(timeoutID);
  }, [value, delay]);

  return debouncedVal;
}

export default useDebounce;
```

##### useRandomId

```js
export function useRandomId() {
  const randomId = useMemo(() => {
    return "_" + Math.random().toString(36).slice(2, 9);
  }, []);

  return randomId;
}
```


# State and Lifecycle

Encapulsate changes in the compoonent

- Local **State** is dict like props, but **private** and fully controlled by component and not setup by React
- Can pass state down to child through props
- The **order** of updates is always respected.

## useState

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

`setCount(prevState => return ....)`

### Advanced

```react
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

#### [Optimizations](https://reactjs.org/docs/hooks-reference.html#bailing-out-of-a-state-update)

If you update a State Hook to the same value as the current state, React will bail out without rendering the children or firing effects. (React uses the [`Object.is` comparison algorithm](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description).)

Note that React may still need to render that specific component again before bailing out. That shouldn’t be a concern because React won’t unnecessarily go “deeper” into the tree. If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.


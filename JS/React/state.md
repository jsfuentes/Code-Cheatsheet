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
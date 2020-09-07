# [Optimization](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab)

So you have a working app and want to decrease unneccessary renders and loads

- Look at using more granular contexts, Redux with selectors, or a custom hook that accesses local storage
- React.lazy load with Suspense

## React.memo

If a parent component changes state/rerenders, all of its child also rerender unless you use React.memo. The DOM might not change though.

Use React.memo when **given the same props, component returns same output** and reasonably expensive/used with same props. No internal state?

Like shouldComponentUpdate of old, `React.memo` shallowly compare its props before deciding to rerender:

```jsx
const Button = React.memo((props) => {
  // your component
});
```

`React.memo` is equivalent to `PureComponent`, but it only compares props. (2nd arg can be custom compare ft, that skips rerender if returns true)

Can [optimize individual children with `useMemo`](https://reactjs.org/docs/hooks-faq.html#how-to-memoize-calculations).

```jsx
// Only re-rendered if `a` changes:
const child1 = useMemo(() => <Child1 a={a} />, [a]);

return (<>{child1}</>);
```

*React only takes React.memo as a hint, must be allowed to rerender*
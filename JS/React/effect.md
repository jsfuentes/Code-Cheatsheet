## useEffect

For data fetching, subscriptions, or manually changing the DOM because they can affect other components and can’t be done during rendering.

`useEffect` Hook runs after every render and offers clean up so === to  `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
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

## 
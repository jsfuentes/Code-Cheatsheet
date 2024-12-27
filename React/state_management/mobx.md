# Mobx

- declarative, reactive programming
- different paradigm then redux/zustand

### Diff from Zustand/Redux

- Instead of selectors, just wrap functional component in observers if it relies on state

- Need to pass store down yourself either just directly or useContext

// store.js

```ts
import { makeAutoObservable } from "mobx";

class CounterStore {
    value = 0;

    constructor() {
        makeAutoObservable(this);
    }

    increment() {
        this.value++;
    }
}

export const counterStore = new CounterStore();

```

// CounterComponent.js

```ts
import React from "react";
import { observer } from "mobx-react-lite";
import { counterStore } from "./store";

const Counter = observer(() => (
    <div>
        <p>Count: {counterStore.value}</p>
        <button onClick={() => counterStore.increment()}>Increment</button>
    </div>
));

export default Counter;
```

### Advanced

- **`autorun`**: Automatically tracks any observable accessed within its function and re-executes when they change.
- **`reaction`**: Tracks a specific observable and runs side-effects when it changes.
- **`when`**: Executes a function when a specific condition becomes true.

```ts
reaction(
    () => store.user.name, // Observe changes to user's name
    (name) => console.log(`User's name is now ${name}`) // Side effect
);
```


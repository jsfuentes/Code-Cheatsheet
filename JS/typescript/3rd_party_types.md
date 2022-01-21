# 3rd Party Types

## React 

#### React Props

Prop types:

```js
MyComponent.propTypes = {
  error: PropTypes.instanceOf(Error),
  children: PropTypes.node,
  status: PropTypes.oneOf(['inactive', 'inProgress', 'success', 'failed'])
  value: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Error)
  ]),
}
```

TypeScript:

```ts
interface Props {
  error: Error
  children: React.ReactNode
  status: 'inactive' | 'inProgress' | 'success' | 'failed'
  value: string | number | Error
}
```

#### React Keys

```tsx
import React, { useState, useEffect, KeyboardEvent } from "react";

interface Props {
	onKeyDown: (e: KeyboardEvent) => void;
}
        <textarea
          onKeyDown={onKeyDown}
          style={{ resize: "none" }}
        />
```

#### React useRef

```ts
//f should be from useCallback to avoid reruns
export function useClickOutside(ref: React.MutableRefObject<HTMLElement>, f: () => any, isActive: boolean) {
  useEffect(() => {
    function stopExit(e: MouseEvent) {
      e.stopPropagation();
    }

    if (isActive) {
      //https://stackoverflow.com/questions/33657212/javascript-click-anywhere-in-body-except-the-one-element-inside-it/33657471
      let elRef = ref.current;
      elRef.addEventListener("mousedown", stopExit);
      document.body.addEventListener("mousedown", f);
      return () => {
        elRef.removeEventListener("mousedown", stopExit);
        document.body.removeEventListener("mousedown", f);
      };
    }
  }, [ref, f, isActive]);
}
```


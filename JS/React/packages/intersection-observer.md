# [Intersection Observer](https://github.com/thebuilder/react-intersection-observer)

```bash
yarn add react-intersection-observer
```

## Usage

```tsx
import React from 'react';
import { useInView } from 'react-intersection-observer';

const Component = () => {
  const { ref, inView, entry } = useInView({
    /* Optional options */
    threshold: 0,
  });

  return (
    <div ref={ref}>
      <h2>{`Header inside viewport ${inView}.`}</h2>
    </div>
  );
}
```


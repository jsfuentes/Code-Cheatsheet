# hooks

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




# Errors in React

**As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.**

## [Error Boundary](https://reactjs.org/docs/error-boundaries.html) 

**Components that catch Javascript Errors** from child components, log those and display a fallback UI instead of crashing.

defines one or both of `static getDerivedStateFromError()` or `componentDidCatch()` 

Does not catch:

- Event handlers - react wont crash here so you should handle
- Asynchronous code (e.g. `setTimeout` or `requestAnimationFrame` callbacks)
- Server side rendering
- Errors thrown in the error boundary itself (rather than its children)

### Usage

ErrorBoundary

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```



```jsx
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```


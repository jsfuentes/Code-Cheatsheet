# Children

Grid.js

```js
function Grid(props) {
    return <div>{props.children}</div>;
}
```

Usage

```jsx
<Grid>
  <Row />
  <Row />
  <Row />
</Grid>
```

#### Extra

Children can be anything, any type so use helpers

```jsx
<Fetch url="api.myself.com">
  {(result) => <p>{result}</p>}
</Fetch>
```

#### To Change Children

```jsx
renderChildren() {
  return React.Children.map(this.props.children, child => {
    return React.cloneElement(child, {
      name: this.props.name
    })
  })
}
```

#### Helpers

**React.Children.map**

Better than `this.props.children.map` b/c if ft would map would be undefined

```jsx
class IgnoreFirstChild extends React.Component {
  render() {
    const children = this.props.children
    return (
      <div>
        {React.Children.map(children, (child, i) => {
          // Ignore the first child
          if (i < 1) return
          return child
        })}
      </div>
    )
  }
}
```

**React.Children.count**

If you just passed a raw string, would count length of string oops

```jsx
class ChildrenCounter extends React.Component {
  render() {
    return <p>React.Children.count(this.props.children)</p>
  }
}
```

**React.Children.toArray** 

```jsx
class Sort extends React.Component {
  render() {
    const children = React.Children.toArray(this.props.children)
    // Sort and render the children
    return <p>{children.sort().join(' ')}</p>
  }
}
```


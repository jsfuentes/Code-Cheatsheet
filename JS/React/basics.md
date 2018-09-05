# Basics

`npm install -g create-react-app`

`create-react-app my-app`

### Simplest Example

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

react-scripts creates the root html page

## Thinking about React

- Data flows down from parent to child

- Passing props for specialization is equivalent of composition/inheritance, 

- can even pass other components in props and choose what to do with it

Given design:

1) Break UI into component hierarchy

2) Build Static version in react(no state, state for interactivity)

3) Identify The Minimal (but complete) Representation Of UI State(calculate computed terms on render and remember if its passed in props then its the parent's job to change)

4) Identify where state should live

5) Add Inverse Data Flow, pass update fts to lower components
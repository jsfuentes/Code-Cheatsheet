#  Router

#### Setup

React doesn't come with changing component rendered based on url out of the box, so need `react-router-dom`

`npm install react-router-dom`

```js
import { BrowserRouter, Route, Link } from 'react-router-dom';
```

## Routers

- If multiple paths regex match, will render multiple components (basically this is conditional rendering based on path)

- Use switch to only render one

- Need BrowserRouter outer component

### Switch

`<Switch>`  groups Route components, and will choose the first to match if any

```jsx
return (<BrowserRouter>
  <Switch>
    <Route exact path="/" component={Home} />
    <Route path="/about" component={About} />
    <Route path="/contact" component={Contact} />
    {/* when none of the above match, <NoMatch> will be rendered */}
    <Route component={NoMatch} />
  </Switch>
</BrowserRouter>);
```

- exact doesnt do regex matching, but exact matching
- strict means the ending / mattersss 

#### 3 Render Options

```react
<BrowserRouter>
  <Route path="/home" component={Home} />
  <Route path="/about" render{ () =>  <About {...props} extra={someVariable} /> } />
  <Route children={() => <div> Always Renders </div>} /> 
</BrowserRouter>
```

### Access History and Match in props

- These objs are passed down from Router to children comp

```js
	history: {length: 8, action: "POP", location: {…}, createHref: ƒ, push: ƒ, …}
  location: {pathname: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", search: "", hash: "", state: undefined, key: "pmanoj"}
  match: {path: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", url: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", isExact: true, params: {…}}
  staticContext: undefined
```

To access these router objs from anywhere, use higher order component

```js
import { withRouter } from 'react-router-dom';

export default withRouter(SomeComponent);
```

### URL Path

App.js

```jsx
<Route path="/:handle" component={Editor} />
```

Editor.js

```jsx
const { handle } = props.match.params;
```

### Query Parameters

```jsx
import queryString from 'query-string'
//....
componentDidMount() {
  const values = queryString.parse(this.props.location.search); // "?filter=top&origin=im"
  console.log(values.filter) // "top"
  console.log(values.origin) // "im"
}
```

## Link

```react
<Link to="/">HOME</Link>
//build upon prev url
<Link to="{match.url+"/email"}"> Email </Link>
```

Navlinks add style when active, classes, and on actived event

### Redirect

```react
<Redirect to='/error'/>

//Inside switches
<Redirect path="/home" to "/" />
```

### Advanced

`Prompt` will alert when you navigate away from page like for form
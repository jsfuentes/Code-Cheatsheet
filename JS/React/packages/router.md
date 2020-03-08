#  React Router

#### Setup

React doesn't come with changing component rendered based on url out of the box, so need `react-router-dom`

`npm install react-router-dom`

```js
import { BrowserRouter, Route, Link, Redirect } from 'react-router-dom';
```

*Use HashRouter for within filesystems(electron)*

### Routers

- Need BrowserRouter outer component
- Will render **any number of regex matches** of child Routes
  - Basically conditional rendering based on path

#### Switch

`<Switch>`  groups Route components, and will **choose the first to match** if any

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

### Navigation

#### Link

```react
<Link to="/">HOME</Link>
//build upon prev url
<Link to="{match.url+"/email"}"> Email </Link>
```

**Navlinks** add style when active, classes, and on actived event

#### Redirect

1) Return Redirect Object

```react
<Redirect to='/error'/>

//Inside switches
<Redirect path="/home" to "/" />
```

2) 

```js
const history = useHistory();

history.push("/");
```

3)   HTML5 way

```javascript
window.location.href = "www.example.com";
window.location.replace("www.example.com"); //replaces current page in history
```

## Accessing Router Info

Default passed to Route child, but can also access from anywher with 

1) Hooks which are more effective b/c less renders?

```javascript
import { useParams, useLocation, useHistory, useRouteMatch } from 'react-router-dom';
  
const params = useParams();
const location = useLocation(); //query string at search
const history = useHistory();
const match = useRouteMatch();
```

2) Higher Order Components

```js
import { withRouter } from 'react-router-dom';

export default withRouter(SomeComponent);
```

#### Info Example

```js
history: {length: 8, action: "POP", location: {…}, 	createHref: ƒ, push: ƒ, …}

location: {pathname: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", search: "", hash: "", state: undefined, key: "pmanoj"}

match: {path: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", url: "/getting-some-closure-with-javascript-closures-3f3aa88ecf8c", isExact: true, params: {…}}

staticContext: undefined
```

#### Query Parameters

```jsx
import queryString from 'query-string'

//.......(props) {
const vals = queryString.parse(props.location.search); 
// "?filter=top&origin=im"
console.log(vals.filter); // "top"
console.log(vals.origin); // "im"
```

## Advanced

#### URL Path

App.js

```jsx
<Route path="/:handle" component={Editor} />
```

Editor.js

```jsx
const { handle } = props.match.params;
```

#### Other

`Prompt` will alert when you navigate away from page like for form
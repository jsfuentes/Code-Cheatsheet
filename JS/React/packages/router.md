#  Router

React doesn't come with changing component rendered based on url out of the box, so need `react-router-dom`

`npm install react-router-dom`

```js
import { BrowserRouter, Route, Link } from 'react-router-dom';
```

## Routers

If the path regex matches, will render that component

**If multiple paths match, will render multiple components**(basically this is conditional rendering based on path)

Need BrowserRouter outer component to creat history and allow other router components to work

#### 3 Render Options

- `render={props => <About {...props} extra={someVariable} />}` for inline declaration
- `component={Home}` for premade component

```react
<BrowserRouter>
	<div>
    	<Route path="/home" component={Home} />
        <Route path="/about" render{ () =>  <div> About </div> } />
            <Route children={() => <div> Always Rendered </div>} /> 
    </div>
</BrowserRouter>
```

### Switch

`<Switch>`  groups Route components, and will choose the first to match if any

```js
<Switch>
	<Route exact path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
  {/* when none of the above match, <NoMatch> will be rendered */}
  <Route component={NoMatch} />
</Switch>
```

### Access History and Match in props

- Passes down from Router object to components these objs:

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

### attrs path

```react
<Route exact path="/" component={Home} />
<Route strict path="/about/" ...
```

- exact doesnt do regex matching, but exact matching
- strict means the ending / mattersss 

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

`Prompt` will alert when you navigate away from page like for form, 
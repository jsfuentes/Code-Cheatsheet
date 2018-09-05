# Router

React doesn't come with changing component rendered based on url out of the box, so need `react-router-dom`

`npm install react-router-dom`

import { BrowserRouter, Route, Link } from react-router-dom

## Routers

- Component that allows other router components to work 
- `children` always renders the child
- regex match from path to url i.e within url path found somewhere 
- Will render multiple paths if they match, unless in a `<Switch>`  which will only render one and offers default

```react
<BrowserRouter>
	<div>
    	<Route path="/home" component={Home} />
        <Route path="/about" render{ () =>  <div> About </div> } />
            <Route children={() => <div> Always Rendered </div>} /> 
    </div>
</BrowserRouter>
```

### Passes some props down

- match is objc with path(select by route), url(actual), isExact bool, params obj 
  - /users/:id is path, /users/abc would be url with {id: 'abc'} in params

### attrs path

```react
 <Route exact path="/" component={Home} />
<Route strict path="/about/" ...
```

- exact doesnt do regex matching, but exact matching
- strict means the ending / mattersss 

## LInk

```react
<Link to="/">HOME</Link>
//build upon prev url
<Link to="{match.url+"/email"}"> Email </Link>
```

Navlinks add style when active, classes, and on actived event

### Redirect

```react
<Redirect to '/error'/>
//Inside switches
<Redirect path="/home" to "/" />
```

### Advanced

`Prompt` will alert when you navigate away from page like for form, 
#  React Router v6

#### Setup

React doesn't come with changing component rendered based on url out of the box, so need `react-router-dom`

`npm install react-router-dom`

```js
import { BrowserRouter, Route, Routes } from "react-router-dom";
```

*Use HashRouter for within filesystems(electron)*

### Routers

- Need BrowserRouter outer component
- Will render **any number of regex matches** of child Routes
  - Basically conditional rendering based on path

#### Routes

`<Routes>` groups Route components, and will choose the most specific route so /event/login matches /event/login over /event/:id

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<MyRedirect url="/login" />} />
    <Route path="/login" element={<Login />} />
    <Route path="/" element={<UserRoute requiredOrganizer />}>
      <Route path="/create-event" element={<CreateEvent />} />
      <Route
        path="/dashboard/*"
        element={<DashboardRouter />}
      />
    </Route>
	</Routes>)
```

### Navigation

#### Link

```jsx
<Link to="/">HOME</Link>
//build upon prev url
<Link to="{match.url+"/email"}"> Email </Link>
```

**[Navlinks](https://reactrouter.com/web/api/NavLink)** add style when active, classes, and on actived event

```react
<ul>
  <li>
    <NavLink
      to="messages"
      style={({ isActive }) =>
  isActive ? activeStyle : undefined
            }
      >
      Messages
    </NavLink>
  </li>
  <li>
    <NavLink
      to="tasks"
      className={({ isActive }) =>
  isActive ? activeClassName : undefined
                }
      >
      Tasks
    </NavLink>
  </li>
</ul>
```

#### Redirect

1) 

```js
import { useNavigate } from "react-router-dom";

function Dashboard() {
  let navigate = useNavigate(); 
  //usage somewhere 
  navigate(`/invoices`)
```

3)   HTML5 way

```javascript
window.location.href = "www.example.com";
window.location.replace("www.example.com"); //replaces current page in history
```

## Accessing Router Info

### Route with parameter

```jsx
<Route path="/e/:event_id/*" element={<EventRouter />} />
```

Access Data

```js
import {
  useLocation,
  useParams,
} from "react-router-dom";

//Access /:event_id 
const params = useParams<{ event_id: string }>();

//Access query string ?prompt=Whats%20up?
const location = useLocation();
const params = new URLSearchParams(location.search);
const prompt = params.get("prompt") || undefined; //Whats up?
```

## Advanced

#### URL Path

### Redirect to Route

```jsx
<Route
  path="*"
  element={<Navigate to={`/e/${event_id}`} replace={true} />}
/>
```

### Redirect to External Route

MyRedirect.tsx

```react
const debug = require("debug")("app:MyRedirect");

interface MyRedirectProps {
  url: string;
}

export default function MyRedirect(props: MyRedirectProps) {
  window.location.href = props.url;
  return null;
}
```

Usage

```jsx
<Route
  path="/careers"
  element={
  <MyRedirect url="https://clayboard.com" />
  }
/>
```

# React-Toastify

```
npm install react-toastify
```

## Setup

1) Import style

2) Either toast.configure() once or throw in ToastContainer to App, both recieve the same props

```jsx
import { ToastContainer, toast } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

//toast.configure()

 function App() {
   notify = () => toast("Wow so easy !");

   return (
     <div>
       <button onClick={this.notify}>Notify !</button>
       <ToastContainer />
     </div>
   );
 }
```

## Usage

toast.configure/ToastContainer

```js
toast('🦄 Wow so easy!', {
position: "top-right"
autoClose: 5000
hideProgressBar: false
closeOnClick: true
pauseOnHover: true
draggable: true
});
```

Just call toast and it pops up overriding any defaults from configure

```jsx
toast("YOLO", { autoClose: 15000 });
toast("7 Kingdoms", { autoClose: 7000 });
```

With component

```jsx
import React from 'react';
import { ToastContainer, toast } from "react-toastify";

const Msg = ({ closeToast }) => (
  <div>
    Lorem ipsum dolor
    <button>Retry</button>
    <button onClick={closeToast}>Close</button>
  </div>
)

const App = () => (
  
  <div>
    <button onClick={() => toast(<Msg />)}>Hello 😀</button>
    <ToastContainer />
  </div>
);
```
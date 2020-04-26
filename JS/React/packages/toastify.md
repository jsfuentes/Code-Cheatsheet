# React-Toastify

```
yarn add react-toastify
```

## Setup

```jsx
import React, { Component } from 'react';
import { toast } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

// Call it once in your app root
toast.configure();

function App() {
  const notify = () => toast("Wow so easy !");

  return <button onClick={notify}>Notify !</button>;
}
```

toast.configure adds ToastContainer to App

## Configurations

Can do at the toast.configure level or override it when calling toast

toast.configure/ToastContainer

```js
toast('🦄 Wow so easy!', {
  position: "top-right",
  autoClose: 5000, //false to disable
  hideProgressBar: false,
  closeOnClick: true,
  pauseOnHover: true,
  pauseOnFocusLoss: false,
  draggable: true
});
toast("YOLO", { autoClose: 15000 });
```

- Position:  **top-right, top-center, top-left, bottom-right, bottom-center, bottom-left**

Toast component

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

## Customize

```js
toast.configure({
  bodyClassName: "ml-3 text-green-500 text-lg relative z-max",
  progressClassName: "h-full opacity-100 bg-green-200 z-auto",
  toastClassName:
    "rounded-xl bg-green-100 flex items-center justify-center min-h-0", //disable default min height
  closeButton: <X color="green" className="w-4 h-4 z-max" />,
  position: toast.POSITION.BOTTOM_CENTER,
  autoClose: 5000, //false to disable
  closeOnClick: true,
  pauseOnHover: false,
  pauseOnFocusLoss: false
});
```

If you configure in individual, then you lose access to the outer container and `className` becomes `toastClassName`

### Controlled Progress Bar Example

```js
import React, { Component } from 'react';
import { toast } from 'react-toastify';
import axios from 'axios';

class Example extends Component {
  upload = () => {
    // we need to keep a reference of the toastId to be able to update it
    let toastId = null;

    axios.request({
      method: "post", 
      url: "/foobar", 
      data: myData, 
      onUploadProgress: p => {
        const progress = p.loaded / p.total;

        // check if we already displayed a toast
        if(toastId === null){
          toastId = toast('Upload in Progress', {
            progress: progress
          });
        } else {
          toast.update(toastId, {
            progress: progress
          })
        }
      }
    }).then (data => {
      // Upload is done! 
      // The remaining progress bar will be filled up
      // The toast will be closed when the transition end
      toast.done(toast.id)
    })
  }

  render(){
    return (
      <div>
      <button onClick={this.upload}>Upload something</button>
</div>
);
}
}
```


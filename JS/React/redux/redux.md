# Redux

Minimal 3rd party State management lib

- Stores is **singleton** that holds all app data

- Actions are events that trigger change state, objects with a type field usually written as `"domain/eventName"` with single `payload`
- Reducers are pure functional defs of how app changes on events, you have m

Allows you to not pass stateHandlers and data down through children, by allowing global accessiblity

Just like React dont mutate store, make new obj so redux trigger updates

## Function List

- [createStore(reducer, [preloadedState\], [enhancer])](https://redux.js.org/api/createstore)
- [combineReducers(reducers)](https://redux.js.org/api/combinereducers)
- [applyMiddleware(...middlewares)](https://redux.js.org/api/applymiddleware)
- [bindActionCreators(actionCreators, dispatch)](https://redux.js.org/api/bindactioncreators)
- [compose(...functions)](https://redux.js.org/api/compose)

`import {createStore, combineReducers} from 'redux';`

[Store](https://redux.js.org/api/store)

- [getState()](https://redux.js.org/api/store#getState)
- [dispatch(action)](https://redux.js.org/api/store#dispatchaction)
- [subscribe(listener)](https://redux.js.org/api/store#subscribelistener)
- [replaceReducer(nextReducer)](https://redux.js.org/api/store#replacereducernextreducer)

## Store

- The Single Store, only way to change its state is by dispatching actions

- Can subscribe to its changes

```jsx
var store = createStore(reducer);
//opt 2nd param initial state, opt 3rd param middlewar
store.getState();
store.dispatch(addItem('carrot')); //send out action 
const unsub = store.subscribe( () => {
    //happens everytime an action is dispatched
});
unsub(); //stop ft from happening
```

## ACTIONS

```jsx
const ADD_ITEM = "ADD_ITEM";

var action = {
    type: ADD_ITEM,
    item: "apple"
}

//action creators
const addItem = item => {
    return {
        type: ADD_ITEM,
        item: item
    }
}
```

## Reducers

```jsx
//initial state is [] and define below
const reducer = (prevState = [], action) => {
    switch (action.type) {
        case "ADD_ITEM":
            return [...prevState, action.item];
        case "DELETE_ITEM":
            return [...prevState.slice(0, action.index), ...prevState.slice(action.index+1)];
        default:
            return prevState;
    }
}
```

## Advanced Reducers

Splitting it up instead of one ft, often for single value in an action

```jsx
var initialState = {
    items: [],
    filter: "none",
    discount: 0
};

const items = (state = [], action) => {
    switch (action.type) {
        case "ADD_ITEM": return [...state, action.item]
        //etc
    }
}

const filter = ;//etc
const reducer = (state = initState, action) => {
    return {
        items: items(state.items, action),
        filter: filter(state.filter, action),
        discount: discount(state.discount, action)
    }
}
//OR
var reducer = combineReducers( { items, filter, discount });
```


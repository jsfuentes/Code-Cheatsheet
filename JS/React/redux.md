# Redux

3rd party State management lib

- Stores is singleton that holds all app data

- Actions are events that trigger change state
- Reducers are pure functional defs of how app changes on events

Allows you to not pass stateHandlers and data down through children, by allowing global accessiblity

Just like React dont mutate store, make new obj so redux trigger updates

## Installation

`npm install redux`

`import {createStore, combineReducers} from 'redux';`

## ACTIONS

```react
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

```react
//initial state is [] and define below
const reducer = (prevState = [], action) => {
    switch (aciton.type) {
        case "ADD_ITEM":
            return [...prevState, action.item];
        case "DELETE_ITEM":
            return [...prevState.slice(0, action.index), ...prevState.slice(action.index+1)];
        default:
            return prevState;
    }
}
```

 ## Store

Single Store 

```react
var store = createStore(reducer);
//opt 2nd param initial state, opt 3rd param middleware

store.getState();
store.dispatch(addItem('carrot')); //send out action 
const unsub = store.subscribe( () => {
    //happens everytime an action is dispatched
});
unsub(); //stop ft from happening
```

## Advanced Reducers

Splitting it up instead of one ft, often for single value in an action

```react
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
const reducer = (state = initStaet, action) => {
    return {
        items: items(state.items, action),
        filter: filter(state.filter, action),
        discount: discount(state.discount, action)
    }
}
//OR
var reducer = combineReducers( { items, filter, discount });
```


# Redux

See redux for base redux(global state management)

React component's state and action dispatching methods/event handles is now passed in as props by redux

So redux changes passed in as props, trigger rerender 

### INstallation

`npm install redux`

`npm install react-redux`

## Components Types

### Container Components

Wrapper handle state management/redux and dispatchs presentational comps can do 

### Presentational Components

Present their props just as normal react components and use their prop callbacks

*Forms can keep track of their own state so UI can sync*

## Basics

### Provider

Provide your store to all your React components

```react
import { Provider } from 'react-redux';

<Provider store={store}>
	<App />
</Provider>
```

### Connect

Connect store state to component props

```react
import { connect } from 'react-redux';

//how will the props be available
const mapStateToProps = state => {
    return {
        items: state.items
    };
};

//how will dispatchs map to redux actions
const mapDispatchToProps = dispatch => {
    return {
        onAdd: (name, price) => {
            dispatch(addItem(name, price));
        },
        onDelete: id => {
            dispatch(deleteItem(id));
        }
    };
};

// to be used as <ItemsListContainer />
const ItemsListContainer = connect(mapStateToProps, mapDispatchToProps)( 
	Itemslist //what component to attach redux state to
);
```


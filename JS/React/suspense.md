# Suspense

defer rendering part of app until some condition is met

2 Uses:

- code splitting: the condition is the download of a chunk of your app when the user wants to access to it,
- data fetching: the condition is the download of data.

```js
import React, { Suspense } from 'react';
import PokemonList from './PokemonList';
import Loading from './Loading';

function App(props) {
	return (
		<Suspense fallback={<Loading />}>
			<PokemonList />
		</Suspense>
	);
}
```

React adds 100ms delay before rendering fallback

## Lazy Components

As of 10/10/19, this is the only use case:

`React.lazy`takes a function that will execute the dynamic import. It returns a component that will run this function during its first rendering.

```jsx
import React, { Suspense } from 'react';
import Loading from './Loading';

// we declare PokemonList variable, which is a lazy component
const PokemonList = React.lazy(() => import('./List/PokemonList'));
const StarWarsList = React.lazy(() => import('./List/StarWarsList'));

function App(props) {
	return (
		<Suspense fallback={<Loading />}>
			{/* We use PokemonList like any imported component */}
			{props.route === 'pokemon' && <PokemonList />}
			{props.route === 'starwars' && <StarWarsList />}
		</Suspense>
	);
}
```

*Webpack must be configured to handle dynamic imports, it is in most boilerplates including CRA and Next*

## Future 

Data fetching...
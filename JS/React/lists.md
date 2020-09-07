# Lists

- Can just render an array of jsx 
- But you should have a **key**  that is  *permanent* and *unique*(in the array) which identifies which items have changed/added/removed

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
                                                        ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);

//OR

  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />

      )}
    </ul>
  );
```

Keys arent passed to components

```jsx
const content = posts.map((post) =>
  <Post
    key={post.id} //Post props.key wont work
    id={post.id} //Post props.id will work
    title={post.title} />
);
```

You should add a key to each child **as well as each element inside children **.[Stackoverflow on issue](https://stackoverflow.com/questions/28329382/understanding-unique-keys-for-array-children-in-react-js).
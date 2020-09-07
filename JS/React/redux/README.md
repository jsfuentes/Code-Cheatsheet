# Redux

## Three Principles

1) **The [global state](https://redux.js.org/glossary#state) of your application is stored in an object tree within a single [store](https://redux.js.org/glossary#store).**

2) **The only way to change the state is to emit an [action](https://redux.js.org/glossary#action), an object describing what happened.**

3) **To specify how the state tree is transformed by actions, you write pure [reducers](https://redux.js.org/glossary#reducer).** (pure means no random or async)

### Why Redux in a World with React Context?

- You have large amounts of application state that are needed in many places in the app
- The app state is updated frequently over time
- The logic to update that state may be complex
- The app has a medium or large-sized codebase, and might be worked on by many people
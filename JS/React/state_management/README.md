# How to manage state in React

## Recommended: [Zustand](https://github.com/pmndrs/zustand)

- Simplest implementation of redux like state machine
  - Has useSelector, async functions, and more out of box

- Won't rerender actions/functions 
- 1.16KB, tiny

## UseContext

- all `useContext` children rerender on state change
- two file code and need to wrap app with provide

## React Redux Toolkit

- A lot of boilerplate even with toolkit, CreateSlice, export actions, combine Reducers.

## [Jotai](https://jotai.org/)

- Simplest global atom, like a better useContext with optimized rendering
- setAtom is what you get for defining actions

## Other

- Xstate, Proper state machine architecture for really complex state management
- MobX
- Recoil
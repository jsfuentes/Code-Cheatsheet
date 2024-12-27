# Zustand

```npm
npm install immer
npm install zustand
```

- Much less boilerplate than React Redux with same benefits over useContext
  - Selectively updates components, easy slices

## Basics

- like useSelector, updates based on strict equality

```tsx
import { create } from 'zustand'

const useStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))

function BearCounter() {
  const bears = useStore((state) => state.bears)
    const increasePopulation = useStore((state) => state.increasePopulation)
  return <h1>{bears} around here...</h1>
}
```

## Slices Pattern With Immer

- Immer makes nested updates easier

  - IE, Since `set(() => ({bears: {a: 0}))` is shallowly merged, it would override other parts of {bears} so you would need `set((state) => ({bears: {...state.bears, a: 0}}))`

  - Immer makes it `set((state) => state.bears.a = 0)

store/userSlice.ts

```tsx
import { StateCreator } from 'zustand';

import { User } from '@/API';
import type { AllSlices } from './index';

export interface UserSlice {
  user: User;
  setUser: (user: User) => void;
}

export const createUserSlice: StateCreator<AllSlices, [['zustand/immer', never]], [], UserSlice> = (
  set
) => ({
  user: null,
  setUser: (user: User) =>
    set((state) => {
      state.user = user;
    }),
});
```

store/index.ts

```tsx
import { create } from 'zustand';
import { immer } from 'zustand/middleware/immer';

import { createUserSlice, UserSlice } from './userSlice';

//To add type & UserSlice with the newSlice
export type AllSlices = UserSlice;

export const useAppStore = create<AllSlices>()(
  immer((...args) => ({
    ...createUserSlice(...args),
  }))
);
```

### Advanced

Slices

```tsx
export const createFishSlice = (set) => ({
  fishes: 0,
  addFish: () => set((state) => ({ fishes: state.fishes + 1 })),
})

export const createBearSlice = (set) => ({
  bears: 0,
  addBear: () => set((state) => ({ bears: state.bears + 1 })),
  eatFish: () => set((state) => ({ fishes: state.fishes - 1 })),
})

import { create } from 'zustand'

export const useBoundStore = create((...a) => ({
  ...createBearSlice(...a),
  ...createFishSlice(...a),
}))
```

Nonhook update

```tsx
const useDogStore = create(() => ({ paw: true, snout: true, fur: true }))

// Getting non-reactive fresh state
const paw = useDogStore.getState().paw
// Listening to all changes, fires synchronously on every change
const unsub1 = useDogStore.subscribe(console.log)
// Updating state, will trigger listeners
useDogStore.setState({ paw: false })
// Unsubscribe listeners
unsub1()
```

Persist Middleware

```ts
import { create } from 'zustand'
import { persist, createJSONStorage } from 'zustand/middleware'

const useFishStore = create(
  persist(
    (set, get) => ({
      fishes: 0,
      addAFish: () => set({ fishes: get().fishes + 1 }),
    }),
    {
      name: 'food-storage', // name of the item in the storage (must be unique)
      storage: createJSONStorage(() => sessionStorage), // (optional) by default, 'localStorage' is used
    },
  ),
)
```

- Could [autogenerate](https://docs.pmnd.rs/zustand/guides/auto-generating-selectors) selectors to turn `const bears = useBearStore((state) => state.bears)` into the *much?* better `const bears = useBearStore.use.bears()`

- [Third Party Libs](https://docs.pmnd.rs/zustand/integrations/third-party-libraries)

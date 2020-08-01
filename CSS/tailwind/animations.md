# Animation

| Cls            | Effect                              |
| -------------- | ----------------------------------- |
| animate-spin   | Spin                                |
| animate-ping   | solid then grow and fade completely |
| animate-pulse  | fade to slightly clear then back    |
| animate-bounce | up and down and hang time           |

### Transition

On any change in property listed, will animate into it

Only need to add duration for most basic effect i.e

```jsx
<div className="duration-150 hover:[someproperty/transformation]" />
```

- Transition-property: props that transition
- Transition-duration: time it takes, s or ms
- Transition-timing-function: bezier curve 
- Transition delay: time until starts (good for hover if someone just moves past it)
- Transition: shorthand for 4

| Transition    | Cls                                                          |
| ------------- | ------------------------------------------------------------ |
| transition    | transition-property: background-color, border-color, color, fill, stroke, opacity, box-shadow, transform; |
| duration-150  | transition-duration: 150ms;                                  |
| ease-in       | transition-timing-function: cubic-bezier(0.4, 0, 1, 1);      |
| delay-150     | transition-delay: 150ms;                                     |
| Scale-110     | --transform-scale-x: 1.1; --transform-scale-y: 1.1;          |
| rotate-180    | --transform-rotate: 180deg;                                  |
| translate-x-1 | --transform-translate-x: 0.25rem;                            |
|               |                                                              |

Look at transform origin

*Cant transition to width auto*

## Transforms

Seem to need to put `transform` class to make it work

##### Example

```html
<button class="transition duration-500 ease-in-out bg-blue-500 hover:bg-red-500 transform hover:-translate-y-1 hover:scale-110">
  Hover me
</button>
```


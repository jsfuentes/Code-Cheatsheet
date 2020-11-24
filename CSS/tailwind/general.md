## General

| Cls             | Prop              |
| --------------- | ----------------- |
| .bg-blue-500    |                   |
| .font-medium    | font-weight: 500; |
| .cursor-pointer | cursor: pointer;  |
|                 |                   |

##### Font Weight

font-hairline | font-thin | font-light | font-normal | font-medium | font-semibold | font-bold | font-extrabold | font-black

#### Text

Text-xs|text-sm|text-base|text-lg|text-2xl | text-3xl | text-4xl

.75rem | .875 | 1 | 1.125 | 1.25 | 1.5 | 1.875 | 2.25

| Cls                   | Prop                       |
| --------------------- | -------------------------- |
| .text-xl              | font-size: 1.25rem;        |
| .text-2xl //goes to 6 | font-size: 1.5rem;         |
| .text-gray-700        | color: gray-700            |
| .uppercase            | text-transform: uppercase; |

#### Border

| Cls                   | Prop                        |
| --------------------- | --------------------------- |
| .border-[solid\|none] | border-style: [solid\|none] |
| .border-4             |                             |
| .border-gray-600      |                             |
| .rounded-sm           | border-radius: .125rem;     |
| .rounded              | border-radius: 0.25rem;     |
| .rounded-full         | border-radius: 9999px;      |
|                       |                             |

###### Shadow

| Cls    | Prop                                                         |
| ------ | ------------------------------------------------------------ |
| shadow | box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06); |

## Active Styles

Just prepend any class with `hover:` or `focus:`

### Container

Container sets the max-width to the different sizing breakpoints

```jsx
<div class="container mx-auto">
  <!-- ... -->
</div>
```

## 
# Tailwind

Put CSS inline as utility classes

Can put it right in HTML or use custom classes

```html
<div className="text-4xl block font-bold pb-2">
  Hello to React
</div>
```

```css
.btn-blue {
	@apply bg-blue-500 text-gray-700;
}
```

## Size and Spacing

Same for margins except m

| Class          | Properties       |
| -------------- | ---------------- |
| .p-0           | padding: 0;      |
| .p-2           | padding: .5rem;  |
| .py-4          | Y-axis: 1rem     |
| .px-6          | X-axis: 1.5rem   |
| .pb-8          | bottom: 2rem     |
| .pl-10         | Left: 2.5rem     |
| .pr-12         | Right: 3rem;     |
| .pt-16         | Top: 4rem;       |
| .w-0           | width:0;         |
| .min-w-0       |                  |
| .max-w-xs      |                  |
| .h-full        | height: 100%;    |
| .h-screen      | height: 100vh;   |
| .w-1/2         | width: 50%; //   |
| .w-4/5         | width: 80%;      |
| //2,3,4,5,6,12 | all fractions of |

#### Media Queries

```
sm:inline
md:
lg:
```

100% is default

## Positioning

#### Flex

##### Cross-Axis

.items-stretch  | .items-start  | .items-center  | .items-end  | .items-baseline  |

##### Main-Axis

Justify-start | justify-center | justify-end | justify-between | justify-around

```html
<div className="flex flex-col justify-center items-center mt-4 lg:mt-36 mb-20 lg:mb-28">
  <div> Tails </div>
  <div> Sonic </div>
</div>
```

#### Position

.static | .fixed | .absolute | .relative | .sticky

```html
<div class="absolute top-0 right-0 bg-gray-800">
  
</div>
```

## Other

| Cls             | Prop                    |
| --------------- | ----------------------- |
| .bg-blue-500    |                         |
| .font-bold      | font-weight: 700;       |
| .cursor-pointer | cursor: pointer;        |
| .rounded-sm     | border-radius: .125rem; |

#### Text

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
| .rounded-full         | border-radius: 9999px;      |



## Active Styles

Just prepend any class with `hover:` or `focus:`

### Container

Container sets the max-width to the different sizing breakpoints

```jsx
<div class="container mx-auto">
  <!-- ... -->
</div>
```

## Parts

```css
@tailwind base; /* Preflight will be injected here */


@tailwind components;
@tailwind utilities;
```

Preflight is opinionated and makes things like lists, h1, h2, etc unstyled by default

## Installation

Can use `npx tailwind build styles.css -o output.css`, but builtin cli doesn't include watch ability need postcss

```bash
npm install tailwindcss --save-dev
npx tailwind init tailwind.config.js --full
npm install postcss-cli autoprefixer --save-dev
```

postcss.config.js

```js
const tailwindcss = require("tailwindcss");

module.exports = {
  plugins: [tailwindcss("./tailwind.config.js"), require("autoprefixer")]
};
```

Autoprefixer is not required, but automatically tracks caniuse.com and properly prefixes(or unprefixes) css props

Tailwind replaces @tailwind directives with css

index.css

```css
@tailwind base;/* Preflight will be injected here */
//Put all classes here
@tailwind components;
@tailwind utilities;
```

Preflight is opinionated and makes things like lists, h1, h2, etc unstyled by default

package.json

```json
"scripts": {
  "build:css": "postcss src/css/index.css -o src/index.css",
  "watch:css": "postcss src/css/index.css -o src/index.css -w",
  "start": "npm run watch:css & react-scripts start",
  "build": "npm run build:css && react-scripts build",
}
```

#### 
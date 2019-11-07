# Tailwind

Gives you utilities instead of components

Already need to understand CSS

Mobile is the default

### Installation

```bash
npm install tailwindcss
npm install postcss-cli

tailwind build src/style.css -o dist/style.css
po
watch:style": "postcss src/styles/index.css -o src/styles/tailwind.css -w #add postcss.config.js with tailwind plugin
```

postcss.config.js

```js
const tailwindcss = require("tailwindcss");
module.exports = {
  plugins: [tailwindcss("./tailwind.config.js"), require("autoprefixer")]
};
```

Can do a `tailwind init` that will give you the ability to edit many things

Can put it right in HTML or use custom classes

```js
.btn {
	@apply font-bold py-2 px-4 rounded;
}

.btn-blue {
	@apply bg-blue-500 text-white;
}
```

# Sizing

Same for margins except m

| Class          | Properties       |
| -------------- | ---------------- |
| .p-0           | padding: 0;      |
| .p-4           | padding: 1rem;   |
| .py-4          | Y-axis           |
| .px-4          | X-axis           |
| .pb-4          | bottom           |
| .pl-0          | Left             |
| .pr-2          | Right            |
| .pt-4          | Top              |
| .w-0           | width:0;         |
| .min-w-0       |                  |
| .max-w-xs      |                  |
| .h-full        | height: 100%;    |
| .h-screen      | height: 100vh;   |
| .w-1/2         | width: 50%; //   |
| .w-4/5         | width: 80%;      |
| //2,3,4,5,6,12 | all fractions of |

#### Flex

```html
<div className="flex flex-col justify-center items-center -mt-4 lg:mt-36 mb-20 lg:mb-28">
  <div>
    Tails
  </div>
  <div>
    Sonic
  </div>
</div>
```

#### Media Queries

```
sm:inline
md:
lg:
```

100% is default

## Position

.static | .fixed | .absolute | .relative | .sticky

```html
<div class="absolute top-0 right-0 bg-gray-800">
  
</div>
```

## Active Styles

Just prepend any class with `hover:` or `focus:`

## Other

| Cls                   | Prop                   |
| --------------------- | ---------------------- |
| .rounded-full         | border-radius: 9999px; |
| .font-bold            | font-weight: 700;      |
| .text-xl              | font-size: 1.25rem;    |
| .text-2xl //goes to 6 | font-size: 1.5rem;     |
| .cursor-pointer       | cursor: pointer;       |

## Parts

```css
@tailwind base; /* Preflight will be injected here */

@tailwind components;

@tailwind utilities;
```

Preflight is opinotated and makes things like lists, h1, h2, etc unstyled by default
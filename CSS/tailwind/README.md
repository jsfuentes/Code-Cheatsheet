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

## Parts

```css
@tailwind base; /* Preflight will be injected here */


@tailwind components;
@tailwind utilities;
```

Preflight is opinionated and makes things like lists, h1, h2, etc unstyled by default

## Customize

- Edit theme.colors if you want to replace the colors and theme.extend.colors if you want to just add a color
- Can use `p-[4px]` to use custom explicit values 

```ts
module.exports = {
  content: ['./App.{js,jsx,ts,tsx}', './src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {
      colors: {
        primary: '#D4FF9A',
      },
      spacing: {
        '8xl': '96rem',
        '9xl': '128rem',
      },
      borderRadius: {
        '4xl': '2rem',
      }
    },
  },
  plugins: [],
};

```


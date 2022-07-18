# CSS

Next.js has built-in support for [styled-jsx](https://github.com/vercel/styled-jsx)(CSS in JS lib)

Can also import .css and .scss files

## Tailwind

https://github.com/vercel/next.js/tree/canary/examples/with-tailwindcss

```bash
yarn add tailwindcss postcss-preset-env postcss-flexbugs-fixes
npx tailwind init tailwind.config.js --full
```

postcss.config.js

```jsx
module.exports = {
  plugins: [
    'tailwindcss',
    'postcss-flexbugs-fixes',
    [
      'postcss-preset-env',
      {
        autoprefixer: {
          flexbox: 'no-2009'
        },
        stage: 3,
        features: {
          'custom-properties': false
        }
      }
    ]
  ]
}
```

tailwind.config.js

```jsx
module.exports = {
  purge: [
    './components/**/*.{js,ts,jsx,tsx}', 	
    './pages/**/*.{js,ts,jsx,tsx}'
  ],
  //...
}
```

styles/index.css

```css
@tailwind base;
@tailwind components;

@tailwind utilities;
```


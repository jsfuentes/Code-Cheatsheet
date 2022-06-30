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
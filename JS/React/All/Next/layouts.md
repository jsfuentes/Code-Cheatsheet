# [Layouts](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates)

Root layout required

App/layout.tsx

```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        <main>{children}</main>
      </body>
    </html>
  )
}
```

## Nested layout

Put `layout.tsx` in folder and it will apply to everything in the folder

app/dashboard/layout.tsx

```tsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}: {
  children: React.ReactNode
}) {
  return (
    <section>
      <nav></nav>
 
      {children}
    </section>
  )
}
```

## Templates

Dont persist across routes and maintain state, templates create a new instance for each of their children on navigation, useful when:

- To resynchronize `useEffect` on navigation.
- To reset the state of a child Client Components on navigation.

app/template.tsx

```tsx
export default function Template({ children }: { children: React.ReactNode }) {
  return <div>{children}</div>
}
```

*Layouts still apply*

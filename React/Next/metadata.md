# [Metadata](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#generatemetadata-function)

Use `export const metadata = {` or `export async function generateMetadata(
  { params, searchParams }: Props,
  parent: ResolvingMetadata
): Promise<Metadata> {`

## Metadata

page.js (or layout.js)

```ts
import type { Metadata } from 'next'

export const metadata: Metadata  = {
    openGraph: {
      title: 'Next.js',
      description: 'The React Framework for the Web',
      type: 'article',
      publishedTime: '2023-01-01T00:00:00.000Z',
      authors: ['Seb', 'Josh'],
    },
   icons: {
    icon: '/icon.png',
    shortcut: '/shortcut-icon.png',
    apple: '/apple-icon.png',
    other: {
      rel: 'apple-touch-icon-precomposed',
      url: '/apple-touch-icon-precomposed.png',
    },
  },
  generator: 'Next.js',
  applicationName: 'Next.js',
  referrer: 'origin-when-cross-origin',
  keywords: ['Next.js', 'React', 'JavaScript'],
  authors: [{ name: 'Seb' }, { name: 'Josh', url: 'https://nextjs.org' }],
  creator: 'Jiachi Liu',
  publisher: 'Sebastian Markbåge',
  formatDetection: {
    email: false,
    address: false,
    telephone: false,
  },
    title: {
      template: '%s | Acme',
      default: 'Acme', //if page doesn't have one
      absolute: '...', //override template
  },
}
```

## Generate Metadata

app/products/[id]/page.tsx

```tsx
import type { Metadata, ResolvingMetadata } from 'next'
 
type Props = {
  params: { id: string }
  searchParams: { [key: string]: string | string[] | undefined }
}
 
export async function generateMetadata(
  { params, searchParams }: Props,
  parent: ResolvingMetadata
): Promise<Metadata> {
  // read route params
  const id = params.id
 
  // fetch data
  const product = await fetch(`https://.../${id}`).then((res) => res.json())
 
  // optionally access and extend (rather than replace) parent metadata
  const previousImages = (await parent).openGraph?.images || []
 
  return {
    title: product.title,
    openGraph: {
      images: ['/some-specific-page-image.jpg', ...previousImages],
    },
  }
}
 
export default function Page({ params, searchParams }: Props) {}
```


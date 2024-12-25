# Dynamic Metadata in Next.js 15 🛠️

## Overview 🌟

Metadata in Next.js 15 enhances your application's SEO and shareability by defining meta tags and other relevant information in a structured and efficient way. Dynamic metadata allows you to adapt metadata values based on route parameters or external data.

This guide explores the Metadata API and how to leverage it for dynamic metadata handling.

---

## What Is Metadata? 🧩

Metadata provides additional information about your webpage, helping search engines and social platforms understand its content.

### Types of Metadata:

- **Static Metadata**: Hardcoded metadata values.
- **Dynamic Metadata**: Metadata generated at runtime using parameters or fetched data.

---

## Adding Metadata in Next.js 📄

### Config-Based Metadata

You can define metadata using:
1. **Static Metadata**: Export a `metadata` object in a `page.js` or `layout.js` file.
2. **Dynamic Metadata**: Use the `generateMetadata` function to create metadata dynamically.

#### Static Metadata Example:

```typescript
// app/layout.tsx
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Static Title',
  description: 'Static description for the page.',
};

export default function Layout({ children }: { children: React.ReactNode }) {
  return <main>{children}</main>;
}
```

---

## Dynamic Metadata 🚀

### Dynamic Metadata with `generateMetadata`

Use the `generateMetadata` function to create metadata based on route parameters or fetched data.

#### Example:

```typescript
// app/products/[id]/page.tsx
import type { Metadata, ResolvingMetadata } from 'next';

type Props = {
  params: { id: string };
};

export async function generateMetadata(
  { params }: Props,
  parent: ResolvingMetadata
): Promise<Metadata> {
  const product = await fetch(`https://api.example.com/products/${params.id}`).then(res => res.json());

  return {
    title: product.name,
    description: product.description,
    openGraph: {
      images: [product.image],
    },
  };
}

export default function ProductPage({ params }: Props) {
  return <h1>Product: {params.id}</h1>;
}
```

#### Key Features of `generateMetadata`:

- **Access Route Parameters**: Use `params` for dynamic values.
- **Fetch Data**: Dynamically retrieve metadata values from external sources.
- **Parent Metadata Extension**: Extend metadata from parent layouts.

---

## File-Based Metadata 📂

Next.js supports metadata via specific files:
- `favicon.ico`, `icon.jpg`: Icons.
- `opengraph-image.jpg`, `twitter-image.jpg`: Social media images.
- `robots.txt`: Search engine directives.
- `sitemap.xml`: Website structure.

### Example:

```plaintext
/app
  favicon.ico        -> Adds a favicon
  opengraph-image.jpg -> Used as Open Graph image
```

---

## Behavior and Prioritization 🔄

1. **File-Based Metadata**: Takes precedence over config-based metadata.
2. **Evaluation Order**: Starts from the root layout and merges metadata down to the closest segment.

### Overwriting Example:

```typescript
// app/layout.tsx
export const metadata = {
  title: 'Site Title',
  openGraph: {
    title: 'OG Site Title',
  },
};

// app/blog/page.tsx
export const metadata = {
  title: 'Blog',
  openGraph: {
    title: 'Blog Title',
  },
};

// Final Output:
// <title>Blog</title>
// <meta property="og:title" content="Blog Title" />
```

---

## Advanced Use Cases 🔧

### Dynamic Open Graph Images

Use `ImageResponse` to generate custom Open Graph images:

```typescript
// app/api/og-image.tsx
import { ImageResponse } from 'next/og';

export async function GET() {
  return new ImageResponse(
    <div style={{ fontSize: 72, background: 'white' }}>
      Dynamic OG Image
    </div>,
    { width: 1200, height: 630 }
  );
}
```

### JSON-LD Structured Data

Embed structured data for SEO:

```typescript
// app/products/[id]/page.tsx
export default async function Page({ params }: { params: { id: string } }) {
  const product = await fetch(`https://api.example.com/products/${params.id}`).then(res => res.json());

  const jsonLd = {
    '@context': 'https://schema.org',
    '@type': 'Product',
    name: product.name,
    image: product.image,
    description: product.description,
  };

  return (
    <>
      <script type="application/ld+json" dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }} />
      <h1>{product.name}</h1>
    </>
  );
}
```

---

## Summary 📝

Dynamic metadata in Next.js 15 offers:
- **Improved SEO**: Tailor metadata for each route dynamically.
- **Enhanced Flexibility**: Combine config-based and file-based metadata.
- **Streamlined Development**: Simplify metadata creation with `generateMetadata` and file-based options.

Mastering dynamic metadata ensures your application remains optimized for search engines and social platforms. 🌟

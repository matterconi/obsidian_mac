# Folder-Based Routing in Next.js 15 📂

## Overview 🌟

Next.js 15 introduces folder-based routing as a core feature, making backend routes as modular and intuitive as frontend routes. This method leverages dynamic folders and files to define routes, bringing a seamless development experience.

This guide explains folder-based routing, including its structure, conventions, and best practices for creating dynamic and nested routes.

---

## Folder Structure and Routing 🌐

### Basic Folder Structure
In the App Router (`app/`), every folder and file defines a route. Here’s how it works:

#### Example Structure:

```plaintext
app/
  api/
    users/
      route.ts
    posts/
      [id]/
        route.ts
```

#### Route Mapping:
- `app/api/users/route.ts` → `/api/users`
- `app/api/posts/[id]/route.ts` → `/api/posts/:id`

### Dynamic Segments
Dynamic segments are created by wrapping folder or file names in square brackets (`[]`).

#### Example:

```plaintext
app/
  api/
    products/
      [productId]/
        route.ts
```

URL: `/api/products/:productId`

Dynamic segments are accessible in the `params` object:

```typescript
// app/api/products/[productId]/route.ts
export async function GET(
  request: Request,
  { params }: { params: { productId: string } }
) {
  return new Response(`Product ID: ${params.productId}`);
}
```

### Catch-All Segments
Catch-all segments match multiple URL parts using three dots (`...`) inside square brackets.

#### Example:

```plaintext
app/
  api/
    blog/
      [...slug]/
        route.ts
```

**Matches:

  - `/api/blog/a`
  - `/api/blog/a/b`
  - `/api/blog/a/b/c`

#### Implementation:

```typescript
// app/api/blog/[...slug]/route.ts
export async function GET(
  request: Request,
  { params }: { params: { slug: string[] } }
) {
  return new Response(`Slug: ${params.slug.join(", ")}`);
}
```

### Optional Catch-All Segments
Optional catch-all segments include double square brackets (`[[...]]`).

#### Example:

```plaintext
app/
  api/
    docs/
      [[...docPath]]/
        route.ts
```

**Matches:

  - `/api/docs`
  - `/api/docs/a`
  - `/api/docs/a/b`

#### Implementation:

```typescript
// app/api/docs/[[...docPath]]/route.ts
export async function GET(
  request: Request,
  { params }: { params: { docPath?: string[] } }
) {
  if (!params.docPath) {
    return new Response("Documentation home page");
  }
  return new Response(`Doc Path: ${params.docPath.join(", ")}`);
}
```

---

## Route Handlers in Folders 🛠️

### What Are Route Handlers?
Route Handlers define HTTP methods for a specific route inside the `route.ts` file. They:
- Support HTTP methods like `GET`, `POST`, and `PUT`.
- Can be nested within folders to define specific paths.

#### Example:

```typescript
// app/api/users/route.ts
export async function GET() {
  return new Response("Fetching users...");
}

export async function POST(request: Request) {
  const data = await request.json();
  return new Response(`User created: ${JSON.stringify(data)}`);
}
```

---

## Best Practices 🌟

1. **Use Folder Names to Define Context**:
   - Structure folders to group related routes logically.
   - Example: Group user-related routes under `app/api/users/`.

2. **Leverage Dynamic Segments**:
   - Simplify parameterized routes using `[param]`.

3. **Avoid Conflicts**:
   - Do not define both `route.ts` and `page.tsx` at the same folder level.

4. **Follow Naming Conventions**:
   - Use descriptive and consistent folder names for clarity.

---

## Summary 📝

Folder-based routing in Next.js 15 brings:
- Modular and scalable route definitions.
- Dynamic, catch-all, and optional segments for flexibility.
- Improved organization with folder-level grouping.

This routing system aligns backend routes closely with frontend development patterns, enhancing the overall developer experience. 🌟

# 🏗️ Layouts in Next.js 15

Layouts in Next.js are an essential feature for structuring your application and creating reusable components that persist across navigations.

---

## 📖 What are Layouts?

A [[Layout]] is a parent structure for your components that provides a consistent UI across pages. It allows you to define elements like headers, footers, or sidebars that remain static while the content changes dynamically.

---

## 🛠️ Key Features

- **Reusability**: Define components once and reuse them across routes.
- **Persistent State**: Avoid re-renders for shared components between pages.
- **Scoped Layouts**: Each route can have its own unique layout if needed.
- **Dynamic Adjustments**: Layouts can adapt based on route parameters or other conditions.

---

## 🗂️ How to Use Layouts?

To create a layout, add a `layout.jsx` or `layout.tsx` file in the folder of the route it applies to.

### **Example Directory Structure**:
```
app
├── layout.jsx
├── page.jsx
├── blog
│   ├── layout.jsx
│   └── page.jsx
```
- The `layout.jsx` in the `app` folder applies globally.
- The `layout.jsx` in `blog` applies only to the `/blog` route and its children.

For a deeper understanding of route structuring, refer to [[Routing]].

---

## 💡 Example Implementation

Here’s how you can define a basic layout:

```tsx
export default function Layout({ children }) {
  return (
    <div>
      <header>Header Content</header>
      <main>{children}</main>
      <footer>Footer Content</footer>
    </div>
  );
}
```

- `children` represents the content of the page rendered inside this layout.

---

## ⚡ Dynamic Layouts

You can create layouts that dynamically adjust based on route parameters or other data.

### **Example**:
```tsx
export default function Layout({ children, params }) {
  return (
    <div>
      {params.userId ? <Sidebar userId={params.userId} /> : <Header />}
      <main>{children}</main>
    </div>
  );
}
```

- This layout displays a sidebar if `params.userId` exists; otherwise, it shows a header.

---

## 🔗 Integration with Other Features

- Works seamlessly with nested routes, dynamic routes, and route groups.
- Access `params` directly in the layout to tailor the structure for the current route.
- Useful in combination with [[client components]] and [[server components]] to optimize rendering strategies.

---

Layouts are a powerful tool for creating organized, scalable, and efficient Next.js applications. With proper use, they make your codebase cleaner and your development workflow smoother.

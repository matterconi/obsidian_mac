
# 🛣️ Next.js 15 Routing Concepts

Next.js 15 introduces powerful routing features that make it easier to structure and manage your application. Below are key concepts to understand:

---

## 📂 Route Groups

Route Groups allow you to organize and group routes logically without affecting the URL structure.

- Place files inside a folder starting with `(` and `)` (e.g., `(groupName)`).
- Files inside a route group are grouped logically but do not affect the URL path.

**Example Directory Structure**:
```
app
├── (marketing)
│   ├── page.jsx
│   └── layout.jsx
├── (user)
│   ├── profile
│   │   └── page.jsx
│   └── settings
│       └── page.jsx
```
The URLs for the above structure will be `/page`, `/profile`, and `/settings`.

---

## 🗂️ Nested Routes

Nested Routes are used to create hierarchical routing structures, enabling a parent-child relationship between pages.

**Why Use Them**:
- Break down components into smaller, manageable parts.
- Share a common layout or data between nested routes.

**Implementation**:
- Place folders inside another folder in the `app` directory.

**Example Directory Structure**:
```
app
├── dashboard
│   ├── layout.jsx
│   ├── analytics
│   │   └── page.jsx
│   ├── settings
│       └── page.jsx
```

The `layout.jsx` in `dashboard` will wrap both `analytics/page.jsx` and `settings/page.jsx`.

---

## 🏗️ Layouts

An important concept of routes are [[Layout]] that are used to create a parent structure for the component, without having to declare it every time.

**Key Features**:
- Layouts persist across navigations.
- Placed in `layout.jsx` or `layout.tsx` inside the folder of the route they apply to.
- Great for reusable components like headers, sidebars, or footers.

**Example Directory Structure**:

```
app
├── layout.jsx
├── page.jsx
├── blog
│   ├── layout.jsx
│   └── page.jsx
```

The `layout.jsx` in `blog` applies only to the `/blog` route and its children.

---

## ⚡ Dynamic Layouts

Dynamic Layouts allow you to change the layout structure dynamically based on route parameters or context.

**Example**:
Use conditional logic inside `layout.jsx` to adjust the structure based on `params`.

```jsx
export default function Layout({ children, params }) {
  return (
    <div>
      {params.userId ? <Sidebar /> : null}
      <main>{children}</main>
    </div>
  );
}
```

---

## 🧩 Dynamic Routes

Dynamic Routes are created by adding square brackets to a file or folder name (e.g., `[id].jsx`).

**Purpose**: Handle dynamic values in the URL (e.g., `/product/123`).

**Accessing Parameters**:
- Access dynamic values using the `params` object.

**Example Directory Structure**:

```
app
├── product
│   ├── [id]
│   │   └── page.jsx
```

For `/product/123`, the `params.id` will be `123`.

**Code Example**:

```jsx
export default function Page({ params }) {
  return <div>Product ID: {params.id}</div>;
}
```

---

## 🌐 Route Parameters

Route Parameters enable you to pass data dynamically between routes.

**Example Use Case**: Fetching specific user or product data.

**Usage**:
- Access them via `params` in both [[page]] components and [[Layout]] components.

---

## ❌ Error Handling  with `error.tsx` 

The `error.tsx` file in Next.js is used to handle errors within a specific route or layout. 

**Key Features** 
- Provides a way to catch and display errors for a route or layout. 
- Acts as a fallback UI when an error occurs during rendering or data fetching. 

**Usage** 
- Place an `error.tsx` file in the folder of the route or layout it applies to. 

**Example Directory Structure**:

```
app 
	├── dashboard │ 
		├── layout.jsx │ 
		├── error.tsx │ 
		├── page.jsx

```

In this case, if an error occurs while rendering the `dashboard` route or any of its children, `error.tsx` will handle it.

**Example Implementation** 

```jsx 
'use client'; 
export default function Error({ error, reset }) { 
	return (
	     <div>       
			 <h2>Something went wrong!</h2>
			 <p>{error.message}</p>
			 <button onClick={() => reset()}>
			   Try again
			 </button>     
	   </div>   
   ); 
} ```

**Key Notes**

- The `reset` function provided in the props allows you to retry the operation that caused the error.
- This component is client-side (`'use client'`) to handle interactions like resetting or retrying.

By including `error.tsx` files in your project, you can create robust error-handling mechanisms for specific sections of your app.

---

## ⏳ Loading Components
In Next.js 15, loading components have been streamlined to improve the user experience during route transitions or data fetching.  

**🛠️ What is the `loading.tsx` File?** 

The `loading.tsx` file is a special component in Next.js that automatically displays when your application is waiting for a page to load or data to be fetched.

**Purpose and placement**
+ Provides a seamless loading experience to users without the need for manual implementation. 
+ Located inside the route's folder, similar to `page.jsx` or `layout.jsx`.  

**💡 Key Features** 

+ The `loading.tsx` component is automatically triggered when the application detects a delay in rendering the route thanks to **Automatic Detection**. 
- Each route can have its own `loading.tsx` component, allowing for custom designs for different sections of your application making it **Scoped to a Route**. 
- The component persists until the rendering of the page or layout is complete securing **Persistency**. 

 **🗂️ Example Directory Structure**

```app 
	├── dashboard │ 
		├── page.jsx │ 
		├── layout.jsx │ 
		└── loading.tsx 
	├── blog │ 
		├── page.jsx │ 
		├── layout.jsx │ 
		└── loading.tsx```

```

In this structure: - `dashboard/loading.tsx` handles loading behavior for the `/dashboard` route. - `blog/loading.tsx` handles loading behavior for the `/blog` route.  --- ### 🖼️ Example Implementation  Here’s how a `loading.tsx` component might look:  
```tsx 
export default function Loading() {
	return (     
		<div style={{ textAlign: 'center', padding: '2rem' }}>       
			<p>Loading, please wait...</p>     
		</div>   ); }
```

This component ensures a polished user experience while waiting for the route to load.

The `loading.tsx` file is another way Next.js simplifies your development process, offering an out-of-the-box solution for handling loading states during navigation or data fetching.

---



## 📊 Combining Concepts

To create a dynamic and organized application, combine these routing concepts:
- Use Route Groups to organize code.
- Combine Nested Routes and Layouts for shared structure.
- Leverage Dynamic Routes and Parameters for data-driven navigation.
- Add error handling with  `error.tsx

**Example Directory Structure**:

```
app
├── (auth)
│   ├── login
│   │   └── page.jsx
│   ├── signup
│       └── page.jsx
├── dashboard
│   ├── layout.jsx
│   ├── analytics
│   │   └── page.jsx
│   ├── settings
│       └── page.jsx
├── layout.tsx
├── page.tsx
├── error.tsx
```

---

By mastering these concepts, you can create modular, efficient, and scalable Next.js applications with ease.


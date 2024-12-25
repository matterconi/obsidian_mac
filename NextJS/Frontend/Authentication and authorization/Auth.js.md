# Auth.js (NextAuth.js) Documentation

## Introduction 🌟
Auth.js (formerly NextAuth.js) is a powerful authentication library for JavaScript frameworks. It is framework-agnostic and integrates deeply with modern JavaScript frameworks to provide secure, extendable, and easy-to-use authentication mechanisms.

This guide provides comprehensive steps to set up, customize, and protect your application using Auth.js with Next.js.

---

## Installation 🛠️

### Prerequisites
1. Install the Auth.js library:

   ```bash
   npm install next-auth@beta
   ```

2. Generate an `AUTH_SECRET` for secure token encryption:

   ```bash
   npx auth secret
   ```
  
   This will automatically add it to your `.env.local` file.

3. Update `.env.local` with the following variables:

   ```env
   AUTH_SECRET=<generated_secret>
   ```

---

## Configuration 🔧

Create an `auth.ts` file at the root of your project:

```typescript
import NextAuth from "next-auth";

export const { handlers, signIn, signOut, auth } = NextAuth({
  providers: [], // Add your providers here
});
```

---

## Adding OAuth Providers 🌐

### Example: GitHub Provider

1. Register your app on GitHub's Developer Settings dashboard.
2. Add the following environment variables:

   ```env
   AUTH_GITHUB_ID=<your_github_client_id>
   AUTH_GITHUB_SECRET=<your_github_client_secret>
   ```

3. Update `auth.ts`:

   ```typescript
   import GitHub from "next-auth/providers/github";

   export const { handlers, signIn, signOut, auth } = NextAuth({
     providers: [GitHub],
   });
   ```

4. Update `app/api/auth/[...nextauth]/route.ts`:

   ```typescript
   import { handlers } from "@/auth";
   export const { GET, POST } = handlers;
   ```

---

## Customizing Providers ✨

### Override Default Configuration
For example, modify the scopes of the Auth0 provider:

```typescript
import Auth0 from "next-auth/providers/auth0";

export const { handlers, auth } = NextAuth({
  providers: [
    Auth0({
      authorization: { params: { scope: "openid profile email custom_scope" } },
    }),
  ],
});
```

---

## Authentication Methods 🔑

### Sign-In and Sign-Out

#### Adding a Sign-In Button

```typescript
import { signIn } from "@/auth";

export default function SignIn() {
  return (
    <form
      action={async () => {
        "use server";
        await signIn("github", { redirectTo: "/dashboard" });
      }}
    >
      <button type="submit">Sign in with GitHub</button>
    </form>
  );
}
```

#### Adding a Sign-Out Button

```typescript
import { signOut } from "@/auth";

export function SignOut() {
  return (
    <form
      action={async () => {
        "use server";
        await signOut();
      }}
    >
      <button type="submit">Sign Out</button>
    </form>
  );
}
```

---

## Session Management 🧑‍💻

### Accessing the Session

#### Example: Display User Avatar

```typescript
import { auth } from "@/auth";

export default async function UserAvatar() {
  const session = await auth();

  if (!session?.user) return null;

  return (
    <div>
      <img src={session.user.image} alt="User Avatar" />
    </div>
  );
}
```

---

## Protecting Resources 🔒

### Middleware

Create a `middleware.ts` file:

```typescript
export { auth as middleware } from "@/auth";
```

### Pages

Example of a protected page:

```typescript
import { auth } from "@/auth";

export default async function Page() {
  const session = await auth();

  if (!session) return <div>Not authenticated</div>;

  return (
    <div>
      <pre>{JSON.stringify(session, null, 2)}</pre>
    </div>
  );
}
```

### API Routes

Protecting an API route:

```typescript
import { auth } from "@/auth";
import { NextResponse } from "next/server";

export const GET = auth(function GET(req) {
  if (req.auth) return NextResponse.json(req.auth);
  return NextResponse.json({ message: "Not authenticated" }, { status: 401 });
});
```

---

## Advanced Configuration ⚙️

### Custom Sign-In Page

Specify a custom sign-in page in your `auth.ts`:

```typescript
export const { handlers, auth } = NextAuth({
  pages: {
    signIn: "/custom-signin",
  },
});
```

---

## Best Practices 🌟

1. **Keep `AUTH_SECRET` secure**: Do not share or expose it publicly.
2. **Use HTTPS**: Ensure all communication is secure.
3. **Validate Input**: Always sanitize user input.
4. **Test Regularly**: Simulate various login scenarios to identify issues.
5. **Audit Packages**: Regularly run `npm audit` to check for vulnerabilities.

---

This guide provides a complete setup for Auth.js (NextAuth.js) in a Next.js application. Use this document as a reference for implementation and customization to fit your specific needs.

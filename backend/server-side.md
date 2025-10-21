## Server Side Rendering (SSR) best practices

### SSR Strategy & Architecture

- **Prefer Server Side Rendering (SSR)**: Use SSR for pages requiring data fetching at render time (blog posts, product pages, search results) over Client Side Rendering (CSR) for better performance, SEO, and initial load times
- **Avoid Legacy Pages Router**: Do not use `getServerSideProps` or `getStaticProps`; adhere to App Router patterns for modern SSR implementation

### Server Components

- **Default to Server Components**: In Next.js App Router, default to Server Components; use Client Components only when requiring browser APIs, interactivity, or state management
- **Async Server Components**: Define Server Components as async functions to enable direct data fetching with await, improving performance and SEO
- **Direct Data Fetching**: Fetch data directly within Server Components using async/await for initial page loads, reducing client-side bundle size
- **No React Hooks**: Server Components cannot use hooks (useState, useEffect) as they execute solely on the server without browser environment access
- **Progressive Rendering with Suspense**: Implement Suspense boundaries for streaming dynamic content while keeping static parts instantly renderable, enabling faster perceived load times

```tsx
import { Suspense } from "react";

export default async function Page() {
  return (
    <div>
      <Header />
      <Suspense fallback={<LoadingSkeleton />}>
        <DynamicContent />
      </Suspense>
    </div>
  );
}
```

### Server Actions

- **Use Server Actions for Secure Mutations**: Leverage Server Actions for form handling, API calls, authentication, and data mutations to automatically prevent CSRF attacks, improve performance, provide progressive enhancement, and ensure secure server-side execution
- **'use server' Directive**: Mark functions with 'use server' directive to ensure exclusive server-side execution for secure mutations

```typescript
"use server";

import { cookies } from "next/headers";

export async function createSession(data: FormData) {
  const cookieStore = await cookies();

  cookieStore.set("sessionId", data.get("id"), {
    httpOnly: true,
    secure: true,
    path: "/",
  });
}
```

- **Access Request Headers**: Read request headers in Server Components, API routes, and Server Actions

```typescript
import { headers } from "next/headers";

export default async function Page() {
  const headersList = await headers();
  const userAgent = headersList.get("user-agent");
}
```

- **Access Cookies**: Read cookies in any Server Component; set cookies only in API routes or Server Actions

```typescript
import { cookies } from "next/headers";

export default async function Page() {
  const cookieStore = await cookies();
  const theme = cookieStore.get("theme");
  // ...
}
```

### Data Fetching & Caching

- **Fetch Caching Strategies**: Utilize Next.js fetch with caching options for optimal performance

```typescript
// Cached by default
const posts = await fetch("https://api.example.com/posts");

// Revalidate every hour
const posts = await fetch("https://api.example.com/posts", {
  next: { revalidate: 3600 },
});

// No caching for always-fresh data
const posts = await fetch("https://api.example.com/posts", {
  cache: "no-store",
});
```

- **Cache Invalidation**: Use revalidatePath or revalidateTag after mutations to update cached data and reflect changes across the application

```typescript
import { revalidatePath, revalidateTag } from "next/cache";

// Revalidate specific page
revalidatePath("/posts");

// Revalidate all cached data with specific tag
revalidateTag("posts");
```

### Security

- **Server-Side Input Validation**: Always validate and sanitize all user inputs on the server to prevent security vulnerabilities
- **Secrets Management**: Never expose sensitive data in client code; manage API keys and secrets using environment variables on the server side
- **HTTPS Enforcement**: Enforce HTTPS in production for all server communications to encrypt data in transit
- **Content Security Policy**: Configure CSP headers to define allowed content sources, reducing XSS, inline script execution, and data injection attack risks

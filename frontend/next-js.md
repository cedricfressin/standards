## Next.js best practices

### Core Principles

- **Server-First Development**: Default to Server Components; use Client Components only when necessary for interactivity or browser APIs
- **Keep it Simple**: Implement solutions in the fewest lines with straightforward approaches
- **Type Safety**: Use TypeScript strict mode throughout; avoid the `any` type
- **Performance First**: Leverage React 19 and Turbopack without manual optimizations; use progressive rendering with Streaming and Suspense

### Routing

- **File-Based Routing**: Use the `app/` directory for routing; `page.tsx` defines pages, `layout.tsx` wraps child routes with shared UI, `loading.tsx` shows loading states, `error.tsx` handles errors
- **Params and SearchParams**: Always await `params` and `searchParams` in pages and layouts

<example>

```tsx
import type { PageParams } from "@/types/next";

type RoutePageProps = PageParams<{ userId: string }>;

export default async function RoutePage(props: RoutePageProps) {
  const searchParams = await props.searchParams;
  const page = searchParams.page;

  const params = await props.params;
  const userId = params.userId;

  return; // ...
}
```

</example>

### Server Components

- **Server Components**: Default in App Router; render on server with async/await for data fetching, direct database/file access, no React hooks or browser APIs

<example>

```tsx
export default async function Page() {
  const result = await prisma.user.findMany();

  return (
    <div>
      {result.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

</example>

### Server Actions

- **Server Actions**: Use `'use server'` directive for server-side mutations and automatic form handling; revalidate paths after changes

<example>

```tsx
"use server";

import { revalidatePath } from "next/cache";

export async function createPost(formData: FormData) {
  const title = formData.get("title") as string;

  await prisma.post.create({ data: { title } });
  revalidatePath("/posts");
}

// Use in forms
export default function Form() {
  return (
    <form action={createPost}>
      <input name="title" required />
      <button type="submit">Create</button>
    </form>
  );
}
```

</example>

### Client Components

- **Client Components**: Mark with `'use client'`; use for state, effects, and event listeners; minimize to reduce bundle size; check `typeof window !== 'undefined'` for browser APIs to avoid hydration errors

<example>

```tsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

</example>

### Navigation Utilities

- **Navigation Utilities**: Use `redirect('/path')` for redirects and `notFound()` for 404 errors in server components

<example>

```tsx
import { redirect } from "next/navigation";
import { notFound } from "next/navigation";

// Redirect to another page
redirect("/login");

// Show the `not-found.tsx` file
notFound();
```

</example>

### Optimization

- **Image and Font Optimization**: Use `next/image` for automatic image optimization and `next/font` for font loading
- **Progressive Loading**: Implement Suspense boundaries and Partial Prerendering (PPR) to combine static and dynamic content

<example>

```tsx
import { Suspense } from "react";

export default function Page() {
  return (
    <div>
      <h1>Static Header</h1>
      <Suspense fallback={<UserSkeleton />}>
        <UserProfile /> {/* Dynamic content */}
      </Suspense>
    </div>
  );
}
```

</example>

## Next.js best practices

### Core Principles

- **Server-First Development**: Default to Server Components; use Client Components only when necessary for interactivity or browser APIs
- **Keep it Simple**: Implement solutions in the fewest lines with straightforward approaches
- **Type Safety**: Use TypeScript strict mode throughout; avoid the `any` type
- **Performance First**: Leverage React 19 and Turbopack without manual optimizations; use progressive rendering with Streaming and Suspense

### SSR Strategy & Architecture

- **Prefer Server Side Rendering (SSR)**: Use SSR for pages requiring data fetching at render time over CSR for better performance, SEO, and initial load times
- **Avoid Legacy Pages Router**: Do not use `getServerSideProps` or `getStaticProps`; adhere to App Router patterns for modern SSR implementation

### Routing

- **File-Based Routing**: Use the `app/` directory for routing; `page.tsx` defines pages, `layout.tsx` wraps child routes with shared UI, `loading.tsx` shows loading states, `global-error.tsx` handles global errors, `error.tsx` handles page errors
- **Params and SearchParams**: Always await `params` and `searchParams` in pages and layouts

### Server Components

- **Default to Server Components**: In App Router, default to Server Components; use Client Components only when requiring browser APIs, interactivity, or state management
- **Async Server Components**: Define Server Components as async functions to enable direct data fetching with await
- **Direct Data Fetching**: Fetch data directly within Server Components using async/await for initial page loads, direct database/file access, reducing client-side bundle size
- **No React Hooks**: Server Components cannot use hooks (useState, useEffect) as they execute solely on the server without browser environment access
- **Progressive Rendering with Suspense**: Implement Suspense boundaries for streaming dynamic content while keeping static parts instantly renderable

### Server Actions

- **Use Server Actions for Secure Mutations**: Leverage Server Actions for form handling, API calls, authentication, and data mutations to prevent CSRF attacks, improve performance, and ensure secure server-side execution
- **'use server' Directive**: Mark functions with 'use server' directive to ensure exclusive server-side execution for secure mutations
- **Access Request Headers**: Read request headers in Server Components, API routes, and Server Actions using `headers()` from 'next/headers'
- **Access Cookies**: Read cookies in any Server Component; set cookies only in API routes or Server Actions using `cookies()` from 'next/headers'

### Client Components

- **Client Components**: Mark with `'use client'`; use for state, effects, and event listeners; minimize to reduce bundle size; check `typeof window !== 'undefined'` for browser APIs to avoid hydration errors

### Data Fetching & Caching

- **Fetch Caching Strategies**: Utilize Next.js fetch with caching options (default cached, `next: { revalidate }` for timed revalidation, `cache: 'no-store'` for always-fresh data)
- **Cache Invalidation**: Use `revalidatePath()` or `revalidateTag()` after mutations to update cached data and reflect changes across the application

### Navigation Utilities

- **Navigation Utilities**: Use `redirect('/path')` from 'next/navigation' for redirects and `notFound()` for 404 errors in server components

### Optimization

- **Image and Font Optimization**: Use `next/image` for automatic image optimization and `next/font` for font loading
- **Progressive Loading**: Implement Suspense boundaries and Partial Prerendering (PPR) to combine static and dynamic content

### Security

- **Server-Side Input Validation**: Always validate and sanitize all user inputs on the server to prevent security vulnerabilities
- **Secrets Management**: Never expose sensitive data in client code; manage API keys and secrets using environment variables on the server side
- **HTTPS Enforcement**: Enforce HTTPS in production for all server communications to encrypt data in transit
- **Content Security Policy**: Configure CSP headers to define allowed content sources, reducing XSS, inline script execution, and data injection attack risks

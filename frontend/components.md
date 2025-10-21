## React components best practices

### React Configuration

- **Enable React Strict Mode**: Wrap the root component in <StrictMode> to help identify unsafe lifecycles, legacy API usage, and other problematic patterns during development
- **Use React 19**: Leverage React 19 for improved performance, better security features, and access to the latest APIs and optimizations
- **Embrace Modern Features**: Use the latest React features like Suspense for data fetching, `use()` for promises and contexts, `useOptimistic()` for optimistic updates, and `useTransition()` for non-urgent updates

### Component Structure

- **Functional Components**: Always use functional components defined with the `function` keyword instead of class components
- **Directives for Components**: Use `'use client'` for components requiring client-side interactivity and `'use server'` for server-only components in Next.js App Router
- **Specific Imports**: NEVER use `import * as React from 'react'` — import only what you need, such as `import { useState } from 'react'`, to reduce bundle size and improve tree-shaking

<example>

```tsx
// Example: Standard Component Structure
// 1. Imports (external, internal then types)
import { useTranslation } from "react-i18next";
import { Button } from "~/components/ui/button";
// 2. Separate type imports from the rest
import type { User } from "~/lib/types/User";

// 3. Props definitions
type UserProfileProps = {
  user: User;
};

// 4. Component definition
export function UserProfile({ user }: UserProfileProps) {
  // 5. Hooks
  const { t } = useTranslation();

  // 6. Event handlers (grouped by concern and logic)
  const handleLogout = () => {
    // Logout logic here
  };

  // 7. Return JSX
  return (
    <div>
      <h1>{t("user.profile.title", { name: user.name })}</h1>
      <Button onClick={handleLogout}>{t("user.profile.logout")}</Button>
    </div>
  );
}
```

</example>

### Props & Types

- **Type Props**: Strongly type component props; use `PropsWithChildren<T>` when the component only receives children as props
- **Props Handling**: Use spread (`...props`) and rest operators for efficient props and state management in components

### Hooks Best Practices

- **Custom Hooks**: Extract reusable logic, such as stateful operations or side effects, into custom hooks to promote code reusability and separation of concerns
- **Rules of Hooks**: Follow the Rules of Hooks: only call hooks at the top level of your React functions and not inside loops, conditions, or nested functions
- **useEffect Dependencies**: Always provide the correct dependency array in useEffect to prevent stale closures and unnecessary re-runs
- **Cleanup in useEffect**: Implement cleanup functions in useEffect for resources like timers, event listeners, or subscriptions to avoid memory leaks
- **Complex State with useReducer**: Use useReducer for managing complex state logic that involves multiple sub-values or when the next state depends on the previous one
- **Avoid Manual Memoization**: DO NOT use `useMemo` or `useCallback` for performance; rely on the React Compiler in React 19 to automatically optimize without manual intervention

### State Management

- **State in Smart Components**: Delegate state management and business logic to "smart" container components, keeping "dumb" presentation components stateless
- **Computed Values in Dumb Components**: Declare any calculated or derived values at the top of dumb components for clarity and performance
- **State Lifting**: Implement proper state lifting to share state between closely related components without prop drilling
- **App-Wide State with Context**: Use React Context API for global state that needs to be accessed by many components across the app
- **Avoid Prop Drilling**: Structure your component tree and use Context or state management solutions to prevent deep prop drilling

### Forms

- **Controlled Components**: Use controlled components for form inputs, where the input's value is managed by React state
- **Form Submission States**: Handle loading, success, and error states during form submissions to provide user feedback
- **Form Libraries for Complexity**: For complex forms with validation and dynamic fields, use libraries like React Hook Form
- **useWatch over watch**: In React Hook Form, use the `useWatch` hook instead of the `watch` function to subscribe to form values. This avoids unnecessary re-renders and provides more efficient reactivity.

### Data Fetching & Server State

- **Data Fetching with React Query**: Use @tanstack/react-query for server state management, caching, and synchronization
- **Consistent Loading and Errors**: Always handle loading and error states in data fetching components for a robust user experience
- **TypeScript for Data**: Use TypeScript types to define the shape of data fetched from the database or API
- **Automatic Invalidation**: Configure the query client to automatically invalidate and refetch queries after successful mutations

<example>

```typescript
import { MutationCache, QueryCache, QueryClient } from "@tanstack/react-query";

// Check for `JEST_WORKER_ID` env variable to determine if we are in Jest environment
const testing = process.env.JEST_WORKER_ID !== undefined;

export const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      // Turns retries off while testing
      retry: !testing,
      // Globally default to 20 secondes to deduplicate requests in that time frame
      staleTime: 20_000,
      // Garbage collection time set to 5 minutes
      gcTime: 300_000,
    },
  },
  queryCache: new QueryCache({
    // Globally handle errors
    onError({ message }) {
      // TODO: Plug here: toast messages, logger, performance reporting...
    },
  }),
  mutationCache: new MutationCache({
    // `mutationKey` is optional and have nothing in common with `queryKey`.
    // You can tie them together by using the `mutationKey` to specify
    // which Queries should be invalidated automatically.
    onSuccess(_data, _variables, _context, mutation) {
      queryClient.invalidateQueries({
        queryKey: mutation.options.mutationKey,
      });
    },
  }),
});
```

</example>

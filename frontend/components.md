## React components best practices

- **Use React 19**: Leverage React 19 with Strict Mode enabled for improved performance and latest features
- **Modern Features**: Use Suspense, `use()`, `useOptimistic()`, and `useTransition()`
- **Functional Components**: Always use functional components with the `function` keyword
- **Specific Imports**: Import only what you need: `import { useState } from 'react'` (never `import * as React`)
- **Client/Server Directives**: Use `'use client'` for client-side interactivity, `'use server'` for server-only components

## Props & Types

- **Strong Typing**: Strongly type component props; use `PropsWithChildren<T>` for children-only props
- **Props Handling**: Use spread (`...props`) and rest operators for efficient props management

## Hooks

- **Custom Hooks**: Extract reusable logic into custom hooks
- **Rules of Hooks**: Only call hooks at the top level, not in loops or conditions
- **useEffect**: Provide correct dependency arrays and implement cleanup functions
- **Complex State**: Use useReducer for complex state logic
- **No Manual Memoization**: DO NOT use `useMemo` or `useCallback`; rely on React Compiler for optimization

## State Management

- **Smart vs Dumb**: Smart components handle state/logic; dumb components handle presentation
- **State Lifting**: Share state between related components without prop drilling
- **Context API**: Use React Context for global state across the app

## Forms

- **Controlled Components**: Manage form inputs with React state
- **Form States**: Handle loading, success, and error states
- **React Hook Form**: Use for complex forms; prefer `useWatch` over `watch` for efficiency

## Data Fetching

- **React Query**: Use @tanstack/react-query for server state management
- **Handle States**: Always handle loading and error states
- **TypeScript**: Define data shape with TypeScript types
- **Auto Invalidation**: Configure query client to invalidate/refetch after mutations

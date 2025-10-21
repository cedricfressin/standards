## Coding style best practices

- **Consistent Naming Conventions**: Establish and follow naming conventions for variables, functions, classes, and files across the codebase
- **Meaningful Names**: Choose descriptive names that reveal intent; avoid abbreviations and single-letter variables except in narrow contexts
- **Small, Focused Functions**: Keep functions small and focused on a single task for better readability and testability
- **Automated Formatting**: Maintain consistent code style (indenting, line breaks, etc.)
- **Consistent Indentation**: Use consistent indentation (spaces) and configure your editor/linter to enforce it
- **Remove Dead Code**: Delete unused code, commented-out blocks, and imports rather than leaving them as clutter
- **DRY Principle**: Avoid duplication by extracting common logic into reusable functions or modules
- **Backward compatability only when required:** Unless specifically instructed otherwise, assume you do not need to write additional code logic to handle backward compatability

## Naming Conventions

- **Meaningful Variable Names**: Use meaningful variable names that describe purpose, not implementation
- **Plural for Collections**: Use plural names for arrays/collections
- **Avoid Abbreviations**: Avoid abbreviations unless widely understood (e.g., `id`, `url`, `api`)
- **Component and Type Naming**: Use PascalCase for components and types (e.g., `UserCard`, `UserCardProps`); use nouns or noun phrases
- **Types Suffixes**: Suffix types with their purpose (e.g., `UserCardProps`, `UserCardState`)
- **Action Functions**: Use verbs for action functions (e.g., `fetchData`, `updateUser`, `deletePost`)
- **Getter Functions**: Use nouns for value-returning functions (e.g., `getUserById`, `calculateTotal`)
- **Boolean Prefixes**: Prefix booleans with `is`, `has`, `should` (e.g., `isLoading`, `hasError`, `shouldFetch`)
- **Constants**: Use UPPER_SNAKE_CASE for constants (e.g., `API_BASE_URL`, `MAX_RETRY_COUNT`)
- **Configuration Objects**: Use camelCase for configuration objects (e.g., `appConfig`, `userSettings`)

## TypeScript Type System

- **Type Inference**: Use type inference when possible
- **Function Return Types**: Do not add explicit function return types; let TypeScript infer them
- **Avoid any/unknown**: Never use `any` or `unknown` without proper type guards
- **Type Conversion**: Avoid `as` for type conversion; use proper type guards instead
- **Generics**: Use generics for reusable functions
- **Strict Mode**: Enable strict mode in `tsconfig.json`

## Utility Types

- **Built-in Utility Types**: Use utility types like `Partial<T>`, `Required<T>`, `Pick<T>`, `Omit<T>`, etc.
- **Custom Utility Types**: Create custom utility types for common patterns
- **Record Type**: Use `Record<K, V>` for object types with dynamic keys

## Null & Undefined Handling

- **Avoid Null/Undefined in Returns**: Avoid returning `null` and `undefined`
- **Optional Properties**: Use optional properties (`?:`) instead of union with `undefined`
- **Non-Null Assertion**: Use non-null assertion (`!`) sparingly and only when certain
- **Optional Chaining**: Prefer optional chaining (`?.`) and nullish coalescing (`??`)

## Enums & Exports

- **String Literal Unions**: Prefer string literal unions to enums
- **Const Enums**: Use const enums if needed for performance
- **Explicit Enum Values**: Define enum values explicitly
- **Named Exports**: Use named exports only (except for Expo screens and Next.js App Router components)
- **Type Exports**: Export types as named exports
- **Import Separation**: Keep `import type` separated from other `import` statements

### Feature Grouping

- **Kebab Case**: Use kebab-case for folder names
- **Component Organization**: Organize components by use case (e.g., components/actions, components/cards)
- **Feature Grouping**: Organize files by domain (e.g., features/auth, features/dashboard)
- **Shared**: Shared services, types, and utilities should be in dedicated folders under lib/ (e.g., lib/services, lib/types, lib/utils)
- **Test**: Keep tests in `__tests__` folders adjacent to code

<example>

```
app/                      # File-based routing system

components/               # Shared components (organize components by use case)
├── actions/              # Buttons and call to action elements
├── cards/                # Rich content cards
├── content/              # Text and medias
├── data/                 # Data display components (Lists, tables)
├── forms/                # Form and input elements
├── layout/               # Layout components (Grids, stacks, containers)
├── messaging/            # Messaging and feedback components (Alerts, toasts, banners, notifications)
├── navigation/           # Navigation components (Tabs, menus, pagination, breadcrumbs)
└── utils/                # Components utilities

lib/
├── features/             # Feature grouping (organize code by domain)
│    ├── auth/
│    │   ├── components/  # Auth specific components
│    │   ├── hooks/       # Auth specific custom hooks
│    │   ├── providers/   # React Context providers
│    │   ├── schemas/     # Zod validation schemas
│    │   ├── services/    # Services and API endpoints
│    │   └── ...
│    ├── dashboard/
│    │   └── ...
│    └── ...
├── services/             # Shared services and API clients
├── types/                # Shared types definitions
└── utils/                # Shared utilities
```

</example>

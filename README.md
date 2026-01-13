# Document 2: Frontend Engineering SOP (Next.js & TypeScript)

This document establishes the patterns for building high-performance, accessible, and type-safe user interfaces with Next.js and React.

## Table of Contents

1. [Architecture & The App Router](#1-architecture-th-eapp-router)
2. [Naming Conventions & Component Design](#2-naming-conventions--component-design)
3. [TypeScript & Type Safety](#3-typescript--type-safety)
4. [State Management Strategy](#4-state-management-strategy)
5. [Performance Optimization](#5-performance-optimization)
6. [Styling & UI Consistency](#6-styling--ui-consistency)
7. [API Consumption & Security](#7-api-consumption--security)

---

### 1. Architecture & The App Router

* **Server-First Mindset:** Use React Server Components (RSC) by default for data fetching to reduce the JavaScript bundle sent to the client.
* **Route Grouping:** Use parenthesis folders `(auth)`, `(dashboard)` to organize pages logically without impacting the URL structure.
* **Layout Nesting:** Utilize `layout.tsx` to persist UI states (like Navbars) across navigation.

### 2. Naming Conventions & Component Design

* **Component Naming:** Use `PascalCase` for component files and folders (e.g., `UserProfile/index.tsx`).
* **Hook Naming:** Custom hooks must start with `use` (e.g., `useDebounce.ts`).
* **Atomic Design:** Keep components small. If a component exceeds 200 lines, extract sub-components into a local `_components/` folder.

### 3. TypeScript & Type Safety

* **Interface vs Type:** Use `interface` for public APIs/Props (as they are extendable) and `type` for unions or utility types.
* **Explicit Returns:** Always define the return type of a function, especially for custom hooks and API services.
* **No Magic Strings:** Use `Enums` or `Const Objects` for status types, roles, or navigation paths.

### 4. State Management Strategy

* **Local State First:** Use `useState` or `useReducer` for UI-only state (e.g., modal open/close).
* **Server State:** Use `TanStack Query` (React Query) or SWR for caching and synchronizing server data.
* **Global State:** Only use `Zustand` or `Context API` for truly global data like user authentication or theme settings.

### 5. Performance Optimization

* **Image Handling:** Always use the `next/image` component with `priority` for LCP (Largest Contentful Paint) images.
* **Dynamic Imports:** Use `next/dynamic` to lazy-load heavy components (e.g., Charts, Editors) only when needed.
* **Memoization:** Apply `useMemo` and `useCallback` only when dealing with expensive computations or preventing unnecessary re-renders of heavy children.

### 6. Styling & UI Consistency

* **Tailwind/CSS Modules:** Maintain styling consistency; avoid inline styles except for truly dynamic values (e.g., calculated positions).
* **Design Tokens:** Use a central `tailwind.config.js` or theme file for colors, spacing, and typography.
* **Accessibility (a11y):** Ensure all interactive elements have `aria-labels` and support keyboard navigation.

### 7. API Consumption & Security

* **Environment Variables:** Prefix client-side variables with `NEXT_PUBLIC_`. All sensitive keys must remain server-side only.
* **Schema Validation:** Use `Zod` to validate the shape of data coming from the API to prevent runtime "undefined" errors.
* **Authentication Flow:** Use `next-auth` (Auth.js) or `httpOnly` cookies for session management to prevent XSS-based token theft.

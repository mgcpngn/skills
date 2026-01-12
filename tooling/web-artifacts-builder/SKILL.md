---
name: web-artifacts-builder
description: Use when building elaborate, multi-component web artifacts using React, Tailwind, and shadcn/ui. For complex artifacts requiring state management, routing, or component libraries - not for simple single-file HTML.
---

# Web Artifacts Builder

## Overview

Build powerful frontend artifacts using modern web technologies.

**Core principle:** Complex UIs deserve proper architecture - React + TypeScript + modern tooling.

**Stack:** React 18 + TypeScript + Vite + Tailwind CSS + shadcn/ui

## When to Use

**Use when:**
- Building complex multi-component UIs
- Need state management
- Using shadcn/ui component library
- Creating interactive dashboards
- Building full applications

**Don't use when:**
- Simple single-file HTML/CSS
- Static pages
- Quick prototypes
- No component reuse needed

## The Process

### Step 1: Initialize Project

```bash
# Create Vite + React + TypeScript project
npm create vite@latest my-app -- --template react-ts
cd my-app
npm install

# Add Tailwind CSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Add shadcn/ui
npx shadcn-ui@latest init
```

### Step 2: Configure Tailwind

**tailwind.config.js:**
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  darkMode: ["class"],
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

**src/index.css:**
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Step 3: Add Components

```bash
# Add specific shadcn components
npx shadcn-ui@latest add button
npx shadcn-ui@latest add card
npx shadcn-ui@latest add input
npx shadcn-ui@latest add dialog
# ... add as needed
```

### Step 4: Develop

**Project structure:**
```
src/
├── components/
│   ├── ui/           # shadcn components
│   └── custom/       # your components
├── hooks/            # custom React hooks
├── lib/              # utilities
├── App.tsx
└── main.tsx
```

**Example component:**
```tsx
import { Button } from "@/components/ui/button"
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"

export function Dashboard() {
  return (
    <Card className="w-full max-w-md">
      <CardHeader>
        <CardTitle>Dashboard</CardTitle>
      </CardHeader>
      <CardContent>
        <Button onClick={() => console.log("clicked")}>
          Take Action
        </Button>
      </CardContent>
    </Card>
  )
}
```

### Step 5: Run Development Server

```bash
npm run dev
```

### Step 6: Build for Production

```bash
npm run build
```

## Design Guidelines

### AVOID "AI Slop"

| Don't | Do Instead |
|-------|------------|
| Centered everything | Asymmetric layouts |
| Purple gradients | Cohesive color system |
| Uniform rounded corners | Varied border treatment |
| Inter font only | Distinctive typography |
| Generic card layouts | Creative compositions |

### Dark Mode

```tsx
// Use shadcn's dark mode support
<div className="dark:bg-slate-900 dark:text-white">
  <Card className="dark:bg-slate-800">
    ...
  </Card>
</div>
```

### Responsive Design

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
  {/* Responsive grid */}
</div>
```

## Common Patterns

### State Management

```tsx
import { useState, useEffect } from 'react'

function App() {
  const [data, setData] = useState<Item[]>([])
  const [loading, setLoading] = useState(true)
  
  useEffect(() => {
    fetchData().then(setData).finally(() => setLoading(false))
  }, [])
  
  if (loading) return <Spinner />
  return <DataTable data={data} />
}
```

### Form Handling

```tsx
import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import * as z from "zod"

const schema = z.object({
  email: z.string().email(),
  name: z.string().min(2),
})

function ContactForm() {
  const form = useForm({ resolver: zodResolver(schema) })
  
  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      {/* form fields */}
    </form>
  )
}
```

## Quick Reference

| Task | Command/Pattern |
|------|-----------------|
| Create project | `npm create vite@latest` |
| Add Tailwind | `npm install -D tailwindcss` |
| Add component | `npx shadcn-ui@latest add [name]` |
| Dev server | `npm run dev` |
| Build | `npm run build` |
| Path alias | `@/components/` |

## Resources

- **shadcn/ui docs**: https://ui.shadcn.com/docs/components
- **Tailwind CSS**: https://tailwindcss.com/docs
- **Vite**: https://vitejs.dev/guide/

## Related Skills

- **frontend-design** - Design aesthetics and principles
- **webapp-testing** - Test the built application

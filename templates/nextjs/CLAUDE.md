# CLAUDE.md

## Project context

A Next.js 15 application using the App Router, TypeScript, and Tailwind CSS. Targets modern browsers, deployed on Vercel.

## Stack & conventions

- Language: TypeScript 5.x, strict mode on
- Framework: Next.js 15 (App Router only — no `pages/`)
- Styling: Tailwind CSS 4.x with utility-first composition; no CSS-in-JS
- Package manager: pnpm
- Important libraries: `next`, `react@19`, `tailwindcss`, `zod` for runtime validation

## Commands

```bash
pnpm install
pnpm dev          # localhost:3000
pnpm build
pnpm start        # production server after build
pnpm test         # vitest
pnpm lint         # next lint (eslint)
pnpm typecheck    # tsc --noEmit
```

## Code style

- Formatter: Prettier with Tailwind plugin (sorts class names automatically)
- Naming: components `PascalCase`, hooks `useCamelCase`, files `kebab-case`
- Server components by default; mark `"use client"` only when actually needed (state, refs, browser APIs)
- Always specify return types on exported functions
- Comments: only when the *why* is non-obvious

## What to avoid

- Do not use `pages/` — App Router only
- Do not use `getServerSideProps` / `getStaticProps` — use Server Components or Route Handlers
- Do not import server-only modules (`fs`, `process`) into client components
- Do not write Tailwind class names dynamically with template literals — use `clsx` or full class strings
- Do not use `any` — use `unknown` and narrow, or define proper types

## Important files

- `app/layout.tsx` — root layout, metadata, font setup
- `app/page.tsx` — home page (Server Component by default)
- `app/api/*/route.ts` — Route Handlers (replaces old `/api` files)
- `next.config.js` — config for redirects, image domains, experimental flags
- `tailwind.config.ts` — design tokens
- `lib/` — non-React utilities, server actions
- `components/` — shared React components

---

<!-- Adapted from llmapi-pro/claude-md-templates -->

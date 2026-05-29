---
name: modern-nextjs-practices
description: "Use when building, modifying, reviewing, or explaining a Next.js application and the user needs modern implementation guidance beyond project toolchain setup. Triggers on requests involving App Router architecture, Server Components, Client Components, data fetching, caching, Server Actions, Route Handlers, metadata, performance, testing strategy, or modern Next.js best practices."
---

# Modern Next.js Practices

Use this skill to keep Next.js implementation choices consistent, current, and pragmatic. This skill does not replace project-specific patterns. First read the existing codebase, then apply these defaults only where they fit.

## First Checks

Before changing code:

1. Read `package.json` to identify the Next.js version, React version, package manager, scripts, and major dependencies.
2. Determine whether the project uses App Router (`app/`) or Pages Router (`pages/`). Do not migrate routers unless the user explicitly asks.
3. Inspect nearby routes, layouts, components, data access helpers, styling patterns, and tests before choosing an approach.
4. For version-sensitive features or APIs, verify against official Next.js documentation before making claims or broad changes.

## Default Architecture

- Prefer App Router conventions for new work unless the existing project uses Pages Router.
- Keep routes thin. Put shared business logic in local modules near the feature or in established project libraries.
- Use Server Components by default. Add `"use client"` only when a component needs browser APIs, client state, effects, event handlers, context providers, or client-only libraries.
- Keep Client Components as small leaves around interactive UI. Do not move a whole page or layout to the client just to support one interactive control.
- Pass serializable data from Server Components to Client Components. Do not pass functions, database clients, secrets, or non-serializable objects across the boundary.
- Avoid adding global state unless local state, URL state, server data, or existing project state management is insufficient.

## Routing And Layouts

- Use nested layouts for shared UI that should persist across route transitions.
- Use route groups to organize routes without changing URLs.
- Use loading, error, and not-found boundaries where the user experience benefits from route-level states.
- Use `generateMetadata` or static `metadata` for route metadata. Do not hand-roll document head management in App Router.
- Keep URL search params as the source of truth for shareable filters, pagination, tabs, and sort state.

## Data Fetching And Caching

- Fetch server-owned data in Server Components, Route Handlers, or server-side helpers by default.
- Fetch from the database or internal services directly on the server when possible. Do not add an internal HTTP API layer just so a Server Component can call it.
- Make caching behavior explicit when it matters. Use the project's established patterns for `fetch` cache options, revalidation, tags, or dynamic rendering.
- Avoid stale data bugs by documenting why a route is static, revalidated, or dynamic when the choice is not obvious.
- Keep secrets and privileged tokens on the server. Never expose them through Client Components or public environment variables.

## Mutations And Forms

- Use Server Actions for straightforward form submissions and mutations when they fit the project and Next.js version.
- Use Route Handlers when the endpoint must be called by external clients, webhooks, non-form clients, or multiple frontends.
- Validate inputs on the server for every mutation. Client validation is only an experience improvement.
- After mutations, update the UI with the project's established strategy: redirect, revalidate, optimistic UI, or client cache invalidation.
- Keep mutation error handling explicit enough that users can recover from expected failures.

## Route Handlers And APIs

- Use Route Handlers for HTTP APIs, webhooks, auth callbacks, file endpoints, and integration boundaries.
- Return appropriate status codes and structured JSON for API errors.
- Keep auth, authorization, rate limits, and input validation close to the handler or in shared server helpers.
- Do not put browser-only code in Route Handlers or server-only code in Client Components.

## Performance And UX

- Use `next/image` for image optimization unless the source or runtime makes it inappropriate.
- Use `next/font` or the project's existing font system instead of ad hoc external font loading.
- Prefer streaming and route-level loading states for slow server data.
- Avoid unnecessary client bundles by checking whether a dependency forces client rendering.
- Keep accessibility requirements in normal implementation scope: semantic elements, labels, focus states, keyboard support, and useful alt text.

## Testing Strategy

- Test pure logic with fast unit tests.
- Test Client Components and interactive UI with React Testing Library in a DOM-like environment.
- Test critical user flows with Playwright when E2E testing is configured.
- Do not test framework internals. Test behavior the user or integration depends on.
- When changing caching, routing, auth, or mutations, include at least one verification path that exercises the relevant boundary.

## Existing Projects

- Follow local conventions first. Prefer small, compatible changes over broad rewrites.
- Preserve existing routing mode, styling system, state management, test framework, and data access patterns unless the user asked for a migration.
- If a recommended modern pattern conflicts with working project conventions, explain the tradeoff before changing direction.
- Keep migrations explicit, incremental, and reversible.

## Avoid

- Do not default to `"use client"` at the top of pages, layouts, or large feature trees.
- Do not fetch server-owned data from Client Components unless interactivity or polling requires it.
- Do not introduce API routes for purely internal server-to-server calls.
- Do not hide dynamic rendering, cache invalidation, or auth assumptions.
- Do not replace working project architecture just to match a generic best-practice checklist.

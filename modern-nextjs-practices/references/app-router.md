# App Router Structure

Read this when changing routes, layouts, page structure, route-level UI states, metadata, or URL state in an App Router project.

## Routing Defaults

- Use the `app/` directory conventions for new routes in App Router projects.
- Keep `page.tsx` focused on route composition and data orchestration. Move reusable domain logic into local feature modules or established project libraries.
- Use nested `layout.tsx` files for UI that should persist across navigation within a route segment.
- Use route groups `(group)` to organize files without changing the public URL path.
- Use dynamic segments (`[id]`, `[slug]`) for URL-owned identifiers. Validate params before using them in privileged data access.

## Route-Level UI States

- Use `loading.tsx` for route segment loading UI when server data can be slow.
- Use `error.tsx` for recoverable route segment errors. Remember that error boundaries are Client Components.
- Use `not-found.tsx` with `notFound()` for absent resources instead of rendering ad hoc empty states for true 404 cases.
- Use `default.tsx` only when parallel routes need an explicit fallback.

## Metadata

- Use static `metadata` for simple route metadata.
- Use `generateMetadata` when metadata depends on route params or server data.
- Do not hand-roll `<head>` management in App Router.
- Keep metadata fetching consistent with the page's cache and dynamic rendering behavior.

## URL State

- Use `searchParams` for shareable filters, pagination, tab state, and sorting.
- Prefer links and form submissions that update the URL over hidden client state when the state should survive refreshes or be shareable.
- Keep server-readable URL state in Server Components when possible. Use Client Components only for interactive controls.

## Sources

- Next.js App Router docs: https://nextjs.org/docs/app
- Layouts and pages: https://nextjs.org/docs/app/getting-started/layouts-and-pages
- Dynamic routes: https://nextjs.org/docs/app/api-reference/file-conventions/dynamic-routes
- Loading UI and streaming: https://nextjs.org/docs/app/api-reference/file-conventions/loading
- Error handling: https://nextjs.org/docs/app/getting-started/error-handling
- Metadata API: https://nextjs.org/docs/app/api-reference/functions/generate-metadata

# Data Fetching And Caching

Read this when fetching data, choosing static vs dynamic rendering, setting revalidation, or invalidating cached data.

## Placement

- Fetch server-owned data in Server Components, Route Handlers, Server Actions, or server-only helpers.
- Query databases and internal services directly from server code when possible. Avoid creating internal HTTP endpoints just for Server Components to call.
- Fetch client-owned or rapidly interactive data in Client Components only when the user experience requires client-side updates, polling, browser APIs, or optimistic interaction.

## Rendering And Cache Intent

- Make rendering and caching intent explicit when it matters for correctness.
- Prefer static rendering for content that can be cached safely.
- Use revalidation when data can be stale for a known interval or until an explicit invalidation.
- Use dynamic rendering for request-specific data, auth-sensitive content, per-user personalization, or data that must always be fresh.
- Keep comments short but explain non-obvious cache choices, especially when stale data would be a bug.

## Common Patterns

- Use `fetch` cache and revalidation options according to the current Next.js version and project conventions.
- Use tag or path revalidation after mutations when cached UI must refresh.
- Keep cache tags stable, predictable, and close to the data they represent.
- Avoid mixing multiple cache mechanisms for the same data path unless the invalidation story is clear.

## Safety

- Never cache user-specific private data in a way that can leak across users.
- Treat auth, cookies, headers, and request-specific data as signals that may require dynamic rendering.
- Do not hide dynamic behavior behind generic helper functions without documenting the rendering impact.

## Review Checklist

- Where does this data live: server, external API, database, client state, or URL?
- Who can see this data, and can it be cached safely?
- What invalidates it after a mutation?
- Does the route need static rendering, revalidation, or dynamic rendering?
- Will the UI show stale data after navigation or mutation?

## Sources

- Next.js data fetching: https://nextjs.org/docs/app/getting-started/fetching-data
- Next.js caching: https://nextjs.org/docs/app/getting-started/caching
- `fetch` API reference: https://nextjs.org/docs/app/api-reference/functions/fetch
- Revalidating data: https://nextjs.org/docs/app/getting-started/revalidating

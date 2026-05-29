# Server And Client Boundaries

Read this when deciding where code should run, adding `"use client"`, passing props across the server/client boundary, or using third-party client libraries.

## Defaults

- Server Components are the default in App Router. Keep components server-side unless they need client-only capabilities.
- Add `"use client"` only for browser APIs, event handlers, state, effects, client context providers, or client-only libraries.
- Put `"use client"` at the smallest practical leaf boundary. Do not mark an entire route, layout, or feature tree as client-side for one interactive child.
- Keep providers as narrow as practical so static server-rendered UI stays server-renderable.

## Boundary Rules

- Props passed from Server Components to Client Components must be serializable.
- Do not pass functions, database clients, request objects, secrets, or class instances across the boundary.
- Server-only modules should not be imported from Client Components.
- Client-only modules should not be imported from Server Components unless they are behind a Client Component boundary.
- For third-party libraries that require browser APIs, wrap the library in a small Client Component.

## Data Ownership

- Fetch server-owned data on the server and pass minimal serializable data to Client Components.
- Do not move data fetching to the client just because a child component is interactive.
- Keep secrets and privileged tokens on the server. Only expose variables with the public environment variable convention when they are safe for the browser.

## Review Checklist

- Can this component stay a Server Component?
- Is the `"use client"` boundary as small as possible?
- Are all props crossing the boundary serializable?
- Does any import accidentally pull server-only code into the client bundle?
- Does a client dependency significantly increase the JS bundle?

## Sources

- Next.js Server and Client Components: https://nextjs.org/docs/app/getting-started/server-and-client-components
- React Server Components: https://react.dev/reference/rsc/server-components
- React `"use client"`: https://react.dev/reference/rsc/use-client
- React `"use server"`: https://react.dev/reference/rsc/use-server

# Mutations And Route Handlers

Read this when implementing forms, Server Actions, mutations, API endpoints, webhooks, uploads, or integration callbacks.

## Server Actions

- Use Server Actions for straightforward application-owned form submissions and mutations when supported by the project's Next.js version.
- Keep action inputs validated on the server. Client validation is only a usability layer.
- Keep authorization checks inside the action or in a shared server helper called by the action.
- After a mutation, use the project's established update strategy: redirect, revalidate a path or tag, return state to the form, update a client cache, or apply optimistic UI.
- Keep expected errors recoverable and visible to the user.

## Route Handlers

- Use Route Handlers for HTTP endpoints, external clients, webhooks, auth callbacks, upload endpoints, and integration boundaries.
- Return appropriate status codes and structured JSON for API consumers.
- Validate method, auth, content type, input shape, and authorization at the boundary.
- Keep secrets on the server. Do not expose service credentials through responses or public environment variables.

## Choosing Between Them

- Choose a Server Action when the caller is the Next.js app itself and the mutation fits a form or UI action.
- Choose a Route Handler when the caller is outside the app, the endpoint must be stable HTTP API surface, or the same operation must serve multiple clients.
- Do not add a Route Handler only to let a Server Component call internal code over HTTP.

## Review Checklist

- Is the mutation authorized on the server?
- Are inputs validated and errors handled?
- Does the UI refresh or navigate after the mutation?
- Is cache invalidation explicit?
- Is this an app-internal action or an external HTTP API?

## Sources

- Next.js forms and mutations: https://nextjs.org/docs/app/guides/forms
- Updating data: https://nextjs.org/docs/app/getting-started/updating-data
- Route Handlers: https://nextjs.org/docs/app/getting-started/route-handlers
- React Server Functions: https://react.dev/reference/rsc/server-functions

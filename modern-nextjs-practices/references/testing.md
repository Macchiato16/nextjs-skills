# Testing Strategy

Read this when adding or reviewing tests for Next.js routes, components, data logic, mutations, or user flows.

## Unit And Component Tests

- Use fast unit tests for pure logic, formatting, validation, reducers, and server-side helpers that do not need a browser.
- Use React Testing Library for Client Components and interactive behavior.
- Use a DOM-like environment such as `jsdom` when testing rendered components.
- Prefer behavior-focused queries such as roles and labels over implementation details.
- Do not test framework internals or duplicate Next.js behavior.

## Server Components

- Keep Server Component tests focused on behavior that the project can reliably exercise.
- Prefer testing extracted server-side logic directly when a Server Component mostly composes data and UI.
- Use E2E tests for flows that depend on routing, streaming, auth, cache behavior, or server/client integration.

## E2E Tests

- Use Playwright for critical user journeys, auth-sensitive flows, routing, forms, and cross-boundary behavior.
- Keep E2E tests fewer and higher value than unit tests.
- Configure Playwright `webServer` so tests can run locally and in CI without manual server startup.
- In CI, prefer testing against a production build when practical.

## Mutation And Cache Tests

- Verify that successful mutations update the UI through redirect, revalidation, optimistic update, or cache invalidation.
- Verify expected validation and authorization failures.
- For cache-sensitive changes, include a path that would catch stale or leaked data.

## Review Checklist

- Is this best tested as pure logic, component behavior, or an E2E flow?
- Does the test assert user-observable behavior?
- Does the test cover the server/client boundary when that boundary is the risk?
- Are setup files and aliases aligned with the project config?
- Are CI commands updated when test tooling changes?

## Sources

- Next.js Vitest guide: https://nextjs.org/docs/app/guides/testing/vitest
- Next.js Playwright guide: https://nextjs.org/docs/app/guides/testing/playwright
- Testing Library React: https://testing-library.com/docs/react-testing-library/intro/
- Playwright web server config: https://playwright.dev/docs/test-webserver

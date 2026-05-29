# Performance And SEO

Read this when changing metadata, images, fonts, scripts, loading states, bundle size, or user-perceived performance.

## Images And Media

- Use `next/image` for images that benefit from optimization, responsive sizing, lazy loading, and format handling.
- Provide useful `alt` text unless the image is purely decorative.
- Set stable dimensions or use layout constraints to avoid layout shift.
- Do not route every image through `next/image` blindly. Respect remote source constraints, SVG needs, and project-specific media handling.

## Fonts And Scripts

- Use `next/font` or the project's existing font pipeline for font loading.
- Avoid ad hoc external font tags when the app already uses a managed font strategy.
- Use `next/script` for third-party scripts that need controlled loading behavior.
- Keep analytics, chat, and other third-party scripts out of critical rendering paths when possible.

## Metadata And Sharing

- Use App Router metadata APIs for title, description, Open Graph, Twitter, robots, canonical URLs, and icons.
- Use `generateMetadata` when metadata depends on params or server data.
- Keep metadata consistent with rendering and caching choices.

## Bundle And Rendering

- Keep client boundaries small to reduce client JavaScript.
- Avoid importing heavy client-only dependencies into broad shared components.
- Use route-level loading states and streaming for slow server data.
- Prefer server rendering for content-heavy pages and client rendering for genuinely interactive parts.

## Review Checklist

- Did this change increase client JS unnecessarily?
- Are images sized and optimized appropriately?
- Is route metadata correct and generated in the right place?
- Are slow states handled with loading UI or streaming?
- Are third-party scripts loaded intentionally?

## Sources

- Image optimization: https://nextjs.org/docs/app/api-reference/components/image
- Font optimization: https://nextjs.org/docs/app/getting-started/fonts
- Metadata API: https://nextjs.org/docs/app/api-reference/functions/generate-metadata
- Script component: https://nextjs.org/docs/app/api-reference/components/script
- Lazy loading: https://nextjs.org/docs/app/guides/lazy-loading

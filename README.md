# Next.js Skills

Codex skills for modern Next.js development.

## Skills

- `nextjs-toolchain`: Create or retrofit a production-grade Next.js toolchain with pnpm, Prettier, ESLint v9, TypeScript checks, tests, hooks, Commitlint, and CI.
- `modern-nextjs-practices`: Guide implementation decisions for App Router, Server Components, Client Components, data ownership, caching, Server Actions, Route Handlers, performance, and testing.

## Install

Copy the skill folders into your Codex skills directory.

On Windows PowerShell:

```powershell
$skills = "$env:USERPROFILE\.codex\skills"
New-Item -ItemType Directory -Force -Path $skills
Copy-Item -Recurse .\nextjs-toolchain $skills
Copy-Item -Recurse .\modern-nextjs-practices $skills
```

On macOS/Linux:

```bash
mkdir -p ~/.codex/skills
cp -R nextjs-toolchain ~/.codex/skills/
cp -R modern-nextjs-practices ~/.codex/skills/
```

## Usage

After installation, Codex can automatically trigger these skills when the request matches their descriptions.

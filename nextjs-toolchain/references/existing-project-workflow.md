# Existing Project Workflow

Use this workflow when configuring or improving the toolchain for an existing Next.js project.

## Step 1 - Audit current state

Read `package.json`, existing config files, and directory structure. Identify:

- Current package manager and lockfiles (`pnpm-lock.yaml`, `package-lock.json`, `yarn.lock`, `bun.lockb`)
- Which tools are already configured
- Which are missing
- Which are outdated or misconfigured (e.g., ESLint v8 with `.eslintrc` instead of v9 flat config)
- Existing scripts, tests, CI, git hooks, and commit conventions

Present a clear table:

```
Current toolchain state:

  Package manager: npm (package-lock.json)
  Configured: TypeScript, ESLint (v8, legacy config), Jest
  Missing:    Prettier, Git hooks, tests, CI
  Suggested replacement: ESLint v8 -> v9 flat config
```

## Step 2 - Discuss and confirm plan

Preserve existing tools that are configured and working. Ask only about missing tools, broken tools, or replacements that require a user decision:

- Git hooks: keep existing, add lightweight (simple-git-hooks), or add standard (Husky)?
- Commit convention: keep existing, none, or Commitlint + Conventional Commits?
- Testing: keep existing, add Vitest, or add Vitest + Playwright?

If the project is not already using pnpm, explicitly ask before migrating package managers. Do not mix package managers or leave multiple lockfiles unless the user confirms the migration plan.

If any existing config files need to be replaced rather than merged, explicitly ask:

```
Detected an existing .eslintrc.json. I will replace it with an ESLint v9 flat config (eslint.config.mjs).
Should I continue?
```

Wait for confirmation before touching existing files.

## Step 3 - Implement

Apply only the changes confirmed in Step 2. Reuse the relevant tool configuration patterns from the new project workflow, but never run the scaffold step and never overwrite existing files blindly.

Merge or patch existing files where possible:

- Add missing scripts without removing existing scripts
- Preserve custom ESLint, Prettier, Vitest, Playwright, and CI settings unless they conflict with the confirmed plan
- Update hook configuration in place, then reinstall hooks if the selected hook tool requires it

Run the project's existing verification commands plus the verification commands for tools added or modified in this change.

## Step 4 - Report

Report to the user:

- Project tool configuration status
- CI configuration status
- Whether each verification command passed

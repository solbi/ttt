# Repository Guidelines

This repository is being scaffolded; the root currently holds early placeholders (`abcd.txt`, `bbbb.txt`, `cccc.txt`, `note.txt`). Follow the standards below so upcoming structure lands consistently and so reviewers can trace changes quickly.

## Project Structure & Module Organization
- Store canonical documentation in `docs/` (e.g., `docs/overview.md`) and move working notes into `notes/` as they stabilize.
- Place runtime code in `src/`, grouped by feature (`src/game/board.ts`, `src/game/state.ts`), and expose shared helpers through `src/shared/`.
- Mirror modules inside `tests/` using the same relative path (`tests/game/board.test.ts`), and keep static assets (images, fixtures) in `assets/`.

## Build, Test, and Development Commands
- Run `npm install` after pulling dependency changes so the workspace matches `package-lock.json`.
- Use `npm run lint` to execute ESLint and Prettier; wire both scripts in `package.json` and keep their configs (`.eslintrc.cjs`, `.prettierrc`) committed.
- Execute `npm test` (Vitest) before every push, and optionally `npm run test:watch` during local development loops.
- For documentation-heavy updates, run `npx markdownlint "**/*.md"` to catch style regressions.

## Coding Style & Naming Conventions
- Default to TypeScript with ES modules, using 2-space indentation and Prettier defaults.
- Name directories and modules with `kebab-case`, React-style components with `PascalCase`, and tests with the `.test.ts` suffix alongside their subjects.
- Keep functions pure where practical; add a brief comment above complex blocks when intent is not obvious from code alone.

## Testing Guidelines
- Every new logic path requires a matching test in `tests/`, colocated by feature and named `*.test.ts`.
- Maintain ≥85% branch coverage (enforced through Vitest’s coverage reporter); update `vitest.config.ts` include/exclude rules when you add directories.
- Use descriptive suites (`describe('game/board', ...)`), mock external dependencies, and avoid network-bound tests.

## Commit & Pull Request Guidelines
- Follow the short, imperative tone seen in the history (`abcd`, `bbbb` ⇒ prefer `add board reducer`); keep subjects ≤72 characters and wrap bodies at 100.
- Squash work so each commit is reviewable and focused. Reference tickets in the body (`Refs #123`) rather than the subject.
- Pull requests must include: concise summary, testing notes (commands run), linked issues, and screenshots or GIFs when a user-facing change occurs.

## Security & Configuration Tips
- Never commit secrets; document required variables in `.env.example` and load them via your runtime config helper.
- Ensure shell scripts work on macOS and Linux; add `chmod +x scripts/*.sh` to setup steps and prefer portable POSIX shells.

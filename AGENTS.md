# Repository Guidelines

## Project Structure & Module Organization

This is a CommonJS Express 5 backend organized by feature. Runtime entry points are `src/server.js` and `src/app.js`. Add shared configuration under `src/configs/`, integrations and reusable clients under `src/libs/`, request middleware under `src/middlewares/`, feature modules under `src/modules/`, HTTP wiring under `src/routes/`, and small general-purpose helpers under `src/utils/`. Put project documentation in `docs/`, unit tests in `tests/unit/`, and integration tests in `tests/integration/`. Prisma schema and migrations belong in `prisma/`; generated Prisma output is ignored. Keep secrets in `.env`, which must never be committed.

Git tracks files rather than directories. Empty `docs/` or `tests/` folders are not included in commits or pushes; add real files or a `.gitkeep` placeholder when an empty structure must be preserved.

## Build, Test, and Development Commands

Install dependencies before working:

```bash
npm install
npx prisma generate
```

With `DATABASE_URL` configured, create/apply local database migrations with `npx prisma migrate dev`. Run the server directly with `node src/server.js`; use `npx nodemon src/server.js` for automatic restarts during development. There is currently no build script. The existing `npm test` placeholder exits with an error until a test runner is added, so do not treat it as a passing validation command.

## Coding Style & Naming Conventions

Use JavaScript with CommonJS (`require`/`module.exports`) to match `package.json`. Use two-space indentation, semicolons, descriptive camelCase variables and functions, PascalCase for classes, and clear feature-oriented filenames. Keep route handlers thin: place validation and domain logic in the relevant module, and centralize reusable middleware or integrations. Run ESLint when configuration is introduced or available; keep formatting and lint changes separate from behavioral changes.

## Testing Guidelines

No test framework or coverage threshold is configured yet. Use the top-level `tests/unit/` and `tests/integration/` directories for tests, name files `*.test.js`, and cover route success, validation, authentication, and error paths. Add the chosen test command to `package.json` and ensure it runs without requiring production secrets.

## Commit & Pull Request Guidelines

Prefer short imperative messages such as `Add user registration route` and keep each commit focused. Pull requests should explain the behavior change, list verification commands, note Prisma schema or migration changes, and include example API requests/responses when endpoints change. Never include `.env` values or credentials.

# qa-automation

A starter Playwright test-automation project in TypeScript. It runs browser tests from `tests/` with Playwright Test, and it is wired for CI in both GitHub Actions and Jenkins. The test suite currently contains only the example spec (`tests/example.spec.ts`), so this is a starting point to add real application tests to — not a finished test suite for a specific app.

## What it does

- Runs Playwright tests in `tests/` (configured by `playwright.config.ts`).
- Runs tests in parallel, with an HTML report (`playwright-report/`, never auto-opened) and tracing on first retry.
- Tests against Chromium (Desktop Chrome), Firefox (Desktop Firefox), and WebKit (Desktop Safari) by default.
- Fails on CI if a `test.only` is left in the code, retries twice on CI, and uses one worker on CI.
- The `baseURL`, mobile projects, branded-browser projects, and local dev-server setup in the config are commented out, so there is no target app configured yet.

## Tech stack

- Playwright Test (`@playwright/test`) with TypeScript and Node types (`@types/node`)
- `npm test` runs `npx playwright test` (see `package.json`)
- CI: GitHub Actions workflow `.github/workflows/playwright.yml` and a `jenkinsfile` at the repo root

## How to run

```bash
npm install
npx playwright install
npm test
```

View the HTML report after a run:

```bash
npx playwright show-report
```

Run a single spec or a single browser project:

```bash
npx playwright test tests/example.spec.ts
npx playwright test --project=chromium
```

## Project structure

```
playwright.config.ts       # Test directory, parallelism, retries, reporter, browser projects
package.json               # test script: npx playwright test; Playwright and Node types
package-lock.json
tests/
  example.spec.ts          # The only spec so far (example test)
.github/workflows/
  playwright.yml           # GitHub Actions CI workflow
jenkinsfile                # Jenkins CI pipeline
.gitignore
```

## Status

Starter only: add real specs under `tests/` and set the target app (for example, by uncommenting `baseURL` in `playwright.config.ts`) before treating this as a working QA suite.

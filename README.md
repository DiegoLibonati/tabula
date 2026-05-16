# Tabula

## Educational Purpose

This project was created primarily for **educational and learning purposes**.  
While it is well-structured and could technically be used in production, it is **not intended for commercialization**.  
The main goal is to explore and demonstrate best practices, patterns, and technologies in software development.

## Description

**Tabula** is a lightweight, framework-free web application built entirely with vanilla TypeScript, HTML5, and CSS3. It presents an "About Us" style page where content is organized into three distinct sections — **History**, **Vision**, and **Goals** — each accessible through an interactive tab navigation system.

When the user selects a tab, the application dynamically updates the displayed image and the descriptive text beneath it, replacing the previous content without any page reload. The active tab is visually highlighted so the user always knows where they are. The transition between tabs is handled entirely through DOM manipulation, with no external UI libraries or frameworks involved.

The interface is fully keyboard-navigable: users can move between tabs using the `Tab` key and activate them with `Enter` or `Space`, making the application accessible without a mouse. ARIA labels are applied to each tab button to ensure screen reader compatibility.

Under the hood, the project follows a strict component-based architecture where each UI piece — tabs, images, and pages — is a factory function that returns a DOM element and exposes an optional `cleanup()` method to safely remove event listeners when the element is unmounted. This pattern keeps memory usage predictable and avoids listener leaks.

The build system is powered by Vite, providing instant dev server startup and optimized production builds. The codebase is covered by a Jest test suite using `@testing-library/dom` and `@testing-library/user-event`, enforcing a minimum 70% coverage threshold across branches, functions, lines, and statements. Code quality is enforced through ESLint and Prettier, with a Husky pre-commit hook that automatically lints and formats staged files before every commit.

## Technologies used

1. Typescript
2. CSS3
3. HTML5
4. Vite

## Libraries used

#### Dependencies

```
No production dependencies - Pure Vanilla TypeScript
```

#### devDependencies

```
"@eslint/js": "^9.39.2"
"@testing-library/dom": "^10.4.0"
"@testing-library/jest-dom": "^6.6.3"
"@testing-library/user-event": "^14.5.2"
"@types/jest": "^30.0.0"
"@types/node": "^22.0.0"
"eslint": "^9.39.2"
"eslint-config-prettier": "^10.1.8"
"eslint-plugin-prettier": "^5.5.5"
"globals": "^17.3.0"
"husky": "^9.1.7"
"jest": "^30.3.0"
"jest-environment-jsdom": "^30.3.0"
"lint-staged": "^16.2.7"
"prettier": "^3.8.1"
"ts-jest": "^29.4.6"
"typescript": "^5.2.2"
"typescript-eslint": "^8.54.0"
"vite": "^7.1.6"
```

## Getting Started

Requirements: **Node.js ≥ 22** (see `.nvmrc`).

1. Clone the repository
2. Navigate to the project folder
3. Execute: `npm install`
4. Execute: `npm run dev`

The application will open automatically at `http://localhost:3000`.

## Testing

With the project installed, you can verify behavior with the Jest test suite.

1. Navigate to the project folder
2. Execute: `npm test`

For coverage report:

```bash
npm run test:coverage
```

## Continuous Integration

The repository ships with a **GitHub Actions** pipeline defined in [`.github/workflows/ci.yml`](.github/workflows/ci.yml). It runs automatically on every `push` and `pull_request` targeting the `main` branch.

### Pipeline overview

```
                      ┌─── PR or push to main ───┐
                      ▼                          ▼
┌──────────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│   lint-and-audit     │─▶│     testing     │─▶│      build       │
│ eslint · type-check  │  │       jest       │  │   vite build     │
└──────────────────────┘  └──────────────────┘  └──────────────────┘
```

### Validation jobs (run on every PR and push to `main`)

1. **`lint-and-audit`** — runs `npm run lint` (ESLint over `src/` and `__tests__/`) and `npm run type-check` (`tsc --noEmit`).
2. **`testing`** — runs the full Jest suite with `npm test`. Depends on `lint-and-audit`.
3. **`build`** — runs `npm run build`, which performs a final type-check and produces the optimized Vite production bundle. Depends on `testing`.

Every job runs on `ubuntu-latest`, uses the Node.js version declared in [`.nvmrc`](.nvmrc), and caches `npm` dependencies between runs through `actions/setup-node`.

### Running the same checks locally

```bash
# lint-and-audit
npm run lint
npm run type-check

# testing
npm test

# build
npm run build
```

### Where the build outputs live

| Output                                    | Location                                                                         |
| ----------------------------------------- | -------------------------------------------------------------------------------- |
| Validation logs (lint, type-check, tests) | **Actions** tab on GitHub                                                        |
| Production bundle (`dist/`)               | Ephemeral, inside the runner — not currently published as an artifact or release |

> **Note:** the pipeline only validates the codebase; it does not publish a release, push a Docker image, or deploy. The `dist/` folder produced by the `build` job stays inside the runner and is discarded once the workflow finishes.

## Security Audit

Beyond functional correctness, check for vulnerabilities in dependencies:

```bash
npm audit
```

## Known Issues

None at the moment.

## Portfolio Link

[`https://www.diegolibonati.com.ar/#/project/tabula`](https://www.diegolibonati.com.ar/#/project/tabula)

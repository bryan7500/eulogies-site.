# CLAUDE.md — eulogies-site.

This file provides guidance for AI assistants (Claude and others) working on this repository.

---

## Project Overview

**eulogies-site.** is an online space to honor Brad Tkachyk with personalized eulogies and memories. The site serves as a digital memorial where contributors can share remembrances, stories, and tributes.

---

## Repository State

> **Note:** As of early 2026, this repository contains no source files. The project is in a bootstrapping phase. The README was removed after the initial commit. Any AI assistant working here should treat this as a greenfield setup and establish structure from scratch based on the conventions below.

---

## Git Workflow

### Branches

- `main` — production-ready code; do not push directly
- `master` — legacy default branch; treat same as `main`
- `claude/<feature>-<id>` — AI-generated feature branches

### Commit Convention

Use conventional commits:

```
<type>(<scope>): <short summary>

[optional body]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

Examples:
```
feat(eulogies): add submission form for new memories
fix(layout): correct mobile overflow on tribute cards
docs: update CLAUDE.md with API conventions
```

### Push Instructions

Always push with upstream tracking:
```bash
git push -u origin <branch-name>
```

Branch names must follow the pattern `claude/<feature>-<id>` when working from AI sessions.

---

## Recommended Tech Stack

Given the project's nature (memorial/tribute site), the following stack is recommended when scaffolding:

| Layer | Recommendation |
|---|---|
| Framework | Next.js (React) or Astro (static-first) |
| Styling | Tailwind CSS |
| Language | TypeScript |
| Data storage | Markdown files (for eulogies) or a lightweight CMS (e.g., Sanity, Contentlayer) |
| Deployment | Vercel or Netlify |
| Testing | Vitest + Testing Library |

These are starting recommendations — adopt whatever the team decides and update this file.

---

## Project Structure (Intended)

Once scaffolded, the project should follow this structure:

```
eulogies-site./
├── CLAUDE.md                  # This file
├── README.md                  # Human-facing project overview
├── package.json
├── tsconfig.json
├── .env.example               # Document all required env vars here
├── .eslintrc.js / eslint.config.js
├── .prettierrc
├── public/                    # Static assets (images, fonts, icons)
├── src/
│   ├── app/                   # Next.js App Router pages (or pages/ for Pages Router)
│   │   ├── page.tsx           # Home / landing
│   │   ├── eulogies/
│   │   │   ├── page.tsx       # Eulogies listing
│   │   │   └── [slug]/
│   │   │       └── page.tsx   # Individual eulogy
│   │   └── submit/
│   │       └── page.tsx       # Submission form
│   ├── components/            # Reusable UI components
│   │   ├── EulogyCard.tsx
│   │   ├── Header.tsx
│   │   └── Footer.tsx
│   ├── lib/                   # Utilities, data-fetching helpers
│   ├── styles/                # Global CSS or Tailwind entry
│   └── types/                 # Shared TypeScript types/interfaces
├── content/
│   └── eulogies/              # Eulogy entries (Markdown/MDX)
│       └── example.md
└── tests/                     # Unit and integration tests
```

---

## Development Commands

Once the project is scaffolded, the standard commands should be:

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Run tests
npm test
# or
npm run test:watch

# Type-check
npm run type-check

# Lint
npm run lint

# Format
npm run format

# Build for production
npm run build

# Preview production build
npm run preview
```

Update this section with actual commands once `package.json` is committed.

---

## Code Conventions

### TypeScript

- Strict mode enabled (`"strict": true` in tsconfig)
- Prefer `interface` over `type` for object shapes; use `type` for unions/intersections
- No `any` — use `unknown` and narrow types explicitly
- Export types explicitly; co-locate types with their module when small, or put in `src/types/` when shared

### React / Components

- Functional components only; no class components
- One component per file; filename matches component name (PascalCase)
- Props interface named `<ComponentName>Props`
- Prefer composition over prop drilling; use Context sparingly
- Keep components small and focused — extract when a component exceeds ~100 lines

### Styling

- Use Tailwind utility classes directly in JSX
- Avoid inline `style` props except for truly dynamic values
- Group Tailwind classes: layout → spacing → typography → color → interactive
- Extract repeated class strings into a `cn()` helper (clsx + tailwind-merge)

### File Naming

| Type | Convention | Example |
|---|---|---|
| Components | PascalCase | `EulogyCard.tsx` |
| Pages (Next.js) | lowercase | `page.tsx`, `layout.tsx` |
| Utilities/helpers | camelCase | `formatDate.ts` |
| Constants | SCREAMING_SNAKE or camelCase | `MAX_EULOGIES` |
| Tests | same name + `.test` | `EulogyCard.test.tsx` |

### Content (Eulogies)

- Each eulogy is a Markdown/MDX file in `content/eulogies/`
- Required frontmatter fields:
  ```yaml
  ---
  title: "Remembering Brad"
  author: "Jane Doe"
  date: "2026-01-15"
  slug: "remembering-brad-jane-doe"
  excerpt: "A brief summary shown on the listing page."
  ---
  ```
- Slugs must be unique and URL-safe (lowercase, hyphens only)

---

## Environment Variables

Document all required environment variables in `.env.example`. Never commit real secrets.

```bash
# .env.example
NEXT_PUBLIC_SITE_URL=http://localhost:3000

# If using a CMS or database, add connection strings here:
# DATABASE_URL=
# CMS_API_TOKEN=
```

---

## Testing

- Write tests for all non-trivial utilities in `src/lib/`
- Write component tests for interactive or data-displaying components
- Snapshot tests are discouraged — prefer behavioral assertions
- Aim for meaningful coverage, not 100% line coverage

---

## Sensitive Content Guidelines

This is a memorial site. When generating or modifying content-related code:

- Handle submitted eulogies with care — implement moderation before publishing
- Do not expose submitter contact details publicly
- Keep form validation gentle and error messages respectful in tone
- If adding any AI-generated content features, clearly label them as such

---

## AI Assistant Notes

- Always read existing files before modifying them
- Do not delete files without confirmation
- When adding new pages or components, follow the structure above
- Update this CLAUDE.md when significant architectural decisions are made
- Prefer editing existing files over creating new ones where appropriate
- Keep changes minimal and focused — do not refactor code that is not part of the task

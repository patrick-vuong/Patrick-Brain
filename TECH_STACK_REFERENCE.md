# Tech Stack Reference: Complete Encyclopedia 📚

> **This is the comprehensive guide.** Consult [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md) first for quick decisions and mental models. Use this document only when you need detailed explanations, trade-off analysis, or comprehensive comparisons.

---

## About This Document

This document is a structured reference for any AI agent (or human engineer) to consult at the **plan stage** and at the **start of every project** when building a Modern Web Application with React.

**Before diving in:**
1. Have you read [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md)? If not, start there.
2. Use the table of contents below to jump to specific sections you need.
3. Walk through Sections 1-3 with stakeholders before writing any code.

**Future Modular Organization:**
This reference is prepared for future modularization into topic-specific files under `docs/tech-stack/`, such as:
- `docs/tech-stack/01-react-or-not.md`
- `docs/tech-stack/02-prd-discovery.md`
- `docs/tech-stack/04-rendering-models.md`
- `docs/tech-stack/08-auth.md`
- etc.

This will allow for more granular updates and easier maintenance. For now, all content is consolidated in this single reference file.

---

## Table of Contents

1. [Agent Pre-Flight: Should We Use React?](#1-agent-pre-flight-should-we-use-react)
2. [Vision & PRD Discovery](#2-vision--prd-discovery)
3. [Scope Recommendation: Full-Stack vs Front-End vs Back-End](#3-scope-recommendation-full-stack-vs-front-end-vs-back-end)
4. [Frontend Rendering Models (React Ecosystem)](#4-frontend-rendering-models-react-ecosystem)
5. [Infrastructure Layer](#5-infrastructure-layer)
6. [State Management & Data Fetching](#6-state-management--data-fetching)
7. [Styling & UI Component Libraries](#7-styling--ui-component-libraries)
8. [Routing](#8-routing)
9. [API Layer](#9-api-layer)
10. [Backend Technologies](#10-backend-technologies)
11. [Database & ORM Layer](#11-database--orm-layer)
12. [Authentication & Authorization](#12-authentication--authorization)
13. [Testing Strategy](#13-testing-strategy)
14. [DevOps, CI/CD & Deployment](#14-devops-cicd--deployment)
15. [Monitoring, Logging & Observability](#15-monitoring-logging--observability)
16. [Security Checklist](#16-security-checklist)

---

## 1. Agent Pre-Flight: Should We Use React?

> **STOP — before writing any code, the agent MUST evaluate whether React is the right choice and present its reasoning to the user for confirmation.**

### 1.1 Decision Framework

Run through the checklist below. If the majority of answers lean toward **Yes**, React is likely a strong fit. If not, present the alternative to the user.

| Question | Yes → React is a good fit | No → Consider alternatives |
|----------|--------------------------|---------------------------|
| Does the app have a **rich, interactive UI** (dashboards, forms, real-time updates)? | React excels at complex UI state | A server-rendered framework (Rails, Django templates, Astro) may be simpler |
| Is there a **large component ecosystem** you want to leverage? | React has the largest ecosystem of any UI library | Svelte/Vue have growing but smaller ecosystems |
| Does the team already have **React/JavaScript experience**? | Reduces ramp-up time significantly | Pick the framework the team knows best |
| Do you need a **single codebase for web + mobile** (React Native)? | React + React Native share paradigms and code | Flutter or native development may be better |
| Is **SEO critical** (marketing pages, blogs, e-commerce)? | Next.js (React-based) handles SSR/SSG well | Astro, SvelteKit, or plain HTML/CSS may be lighter |
| Is the project a **static content site** with minimal interactivity? | React may be overkill | Astro, Hugo, 11ty are purpose-built for this |
| Is **bundle size** a primary concern (e.g., embedded widgets, low-bandwidth markets)? | React is ~40 KB gzipped; manageable but not the smallest | Svelte (~2 KB), Preact (~3 KB), or vanilla JS are lighter |
| Does the app need **streaming or partial hydration**? | React 18+ Server Components support this | Astro, Qwik have more mature partial-hydration stories |

### 1.2 React Strengths (Reasons to Choose React)

- **Ecosystem maturity:** Largest library ecosystem, most StackOverflow answers, most hiring demand.
- **Meta-framework options:** Next.js, Remix, and Gatsby provide SSR, SSG, API routes, and more out of the box.
- **Component model:** Declarative, composable components with hooks make complex UIs manageable.
- **React Server Components (RSC):** Modern data-fetching pattern that reduces client-side JS.
- **React Native:** Shared mental model for cross-platform mobile development.
- **Corporate backing:** Maintained by Meta; used by Netflix, Airbnb, Shopify, and thousands of production apps.

### 1.3 React Weaknesses (Reasons to Reconsider)

- **Bundle size:** Larger baseline than Svelte or Preact.
- **Learning curve for advanced patterns:** Server Components, Suspense boundaries, and concurrent features add complexity.
- **Opinionated meta-frameworks required:** Vanilla React (Vite + React Router) lacks SSR/SSG out of the box — you often need Next.js or Remix.
- **Reactivity model:** React re-renders by default; Svelte and SolidJS use fine-grained reactivity which can be more performant in certain scenarios.

### 1.4 Alternatives Comparison

| Framework | Best For | Trade-off vs React |
|-----------|----------|-------------------|
| **Vue 3 + Nuxt** | Teams who prefer a gentler learning curve, integrated state management | Smaller ecosystem, less hiring demand |
| **Svelte + SvelteKit** | Performance-critical apps, smaller bundles | Newer ecosystem, fewer libraries |
| **Angular** | Enterprise apps with strict conventions | Heavier, steeper learning curve, but very opinionated (good for large teams) |
| **Astro** | Content-heavy sites with islands of interactivity | Not ideal for highly interactive SPAs |
| **HTMX + server templates** | Simple CRUD apps, progressive enhancement | No component model, limited for complex UIs |

### 1.5 Agent Action Required

> **After evaluating the above, the agent MUST present a summary to the user:**
>
> _"Based on the project requirements, I recommend [React / Alternative] because [specific reasons]. Here's my reasoning: [list 3–5 key factors]. Do you agree, or would you like to discuss alternatives?"_
>
> **Do NOT proceed until the user confirms the framework choice.**

---

## 2. Vision & PRD Discovery

> **Before selecting ANY technology, the agent MUST understand what is being built.** Ask the user the following questions and document the answers. These answers drive every tech decision that follows.

### 2.1 Product Vision Questions

Ask the user these questions (adapt phrasing as needed):

1. **What is the app?** — Describe the product in 1–2 sentences.
2. **Who is the target user?** — Consumer, enterprise, internal tool, developer tool?
3. **What is the core problem it solves?** — What pain point does this address?
4. **What does success look like?** — Key metrics (users, revenue, engagement, performance)?
5. **What is the launch timeline?** — MVP in 2 weeks? V1 in 3 months? Long-term product?
6. **What is the expected scale at launch and at 12 months?** — 100 users? 100K? 10M?

### 2.2 Product Requirements Document (PRD) Questions

7. **What are the core features for MVP?** — List the 3–5 must-have features.
8. **What are the "nice-to-have" features for post-MVP?** — What can wait?
9. **Are there any third-party integrations required?** — Payment (Stripe), auth (OAuth providers), maps, analytics, etc.
10. **What content types will the app serve?** — Static pages, dynamic feeds, real-time data, user-generated content?
11. **Does the app need offline support?** — PWA, service workers, local-first data?
12. **Is there an existing backend/API or are we building from scratch?**
13. **Are there design mockups, wireframes, or a design system already?**
14. **Are there compliance or regulatory requirements?** — GDPR, HIPAA, SOC 2, accessibility (WCAG)?

### 2.3 Technical Context Questions

15. **What is the team's technical skill set?** — Frontend-heavy? Full-stack? Backend-heavy?
16. **Are there existing codebases, monorepos, or infrastructure to integrate with?**
17. **What is the deployment target?** — Vercel, AWS, GCP, Azure, self-hosted, on-prem?
18. **What is the budget for infrastructure?** — Serverless-friendly? Need dedicated servers?
19. **Is there a preference for programming language?** — TypeScript required? Python backend preferred?

> **Agent Action:** Document all answers in a structured format before proceeding. These answers directly inform Sections 3–16.

---

## 3. Scope Recommendation: Full-Stack vs Front-End vs Back-End

> **Based on the PRD answers, the agent MUST recommend the project scope and explain why.**

### 3.1 Decision Matrix

| Scenario | Recommendation | Reasoning |
|----------|---------------|-----------|
| Existing backend/API is provided; we only need UI | **Front-End Only** | No need to build or maintain a backend. Use React + API client. Faster delivery, lower complexity. |
| App needs user auth, database, business logic, and a UI | **Full-Stack** | Both layers are required. Use Next.js (full-stack React) or React + separate backend. Ensures tight integration. |
| Building a reusable API/service that other apps consume | **Back-End Only** | No UI needed. Use Node.js/Express or Python/FastAPI. Focus on API design, data modeling, performance. |
| Static marketing site with a few interactive widgets | **Front-End Only (SSG)** | Use Next.js SSG or Astro. No backend needed; content lives in markdown or a headless CMS. |
| Real-time app (chat, collaboration, live dashboards) | **Full-Stack** | Requires WebSocket server, state sync, database. Full-stack is necessary. |
| Internal tool / admin dashboard over existing database | **Full-Stack (lightweight)** | Consider low-code tools (Retool, Appsmith) first. If custom, use Next.js + Prisma + existing DB. |

### 3.2 Agent Action Required

> **Present the recommendation to the user:**
>
> _"Based on your requirements, I recommend a [Full-Stack / Front-End Only / Back-End Only] approach because [reasons]. Here's the breakdown: [explanation]. Does this align with your expectations?"_
>
> **Wait for user confirmation before selecting specific technologies.**

---

## 4. Frontend Rendering Models (React Ecosystem)

> **Choose the rendering model BEFORE selecting a framework.** The rendering model determines initial load performance, SEO capability, server cost, and developer experience.

### 4.1 Rendering Style Comparison

| Dimension | SPA (Single Page App) | SSG (Static Site Generation) | SSR (Server-Side Rendering) | RSC (React Server Components) |
|-----------|----------------------|-----------------------------|-----------------------------|-------------------------------|
| **When HTML is created** | In the browser at runtime | At build time | On every request (server) | Server renders components; client hydrates interactive ones |
| **Initial load speed** | Slower (JS must download, parse, execute) | Fastest (pre-built HTML served from CDN) | Fast (HTML generated per request) | Fast (server-rendered with minimal client JS) |
| **SEO** | Weak by default (requires workarounds) | Strong (static HTML is crawlable) | Strong (HTML available on first request) | Strong (server-rendered HTML) |
| **Personalization** | Client-side only | Limited (build-time data only) | Full server-side personalization | Server-side + selective client hydration |
| **Server cost** | Low (static files + API) | Lowest (CDN-only hosting) | Highest (server processes every request) | Medium (server renders, but less JS shipped to client) |
| **Data freshness** | Always fresh (fetched at runtime) | Stale until rebuild (or ISR) | Always fresh | Always fresh (server components fetch on request) |
| **Best for** | Dashboards, admin panels, apps behind auth | Marketing sites, blogs, docs, e-commerce catalogs | Personalized content, e-commerce, social feeds | Complex apps needing both performance and interactivity |
| **Example frameworks** | React + Vite + React Router | Next.js (SSG mode), Gatsby, Astro | Next.js (SSR mode), Remix | Next.js App Router |
| **Build + Dev Server** | Vite | Next.js / Astro | Next.js / Remix | Next.js |
| **Routing** | React Router (client-side) | Next.js file-based (build-time) | Next.js file-based (server) | Next.js App Router (file-based, server + client) |

### 4.2 Rendering Model Decision Guide

See [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md) for the decision guide flowchart.

```
Is SEO critical?
├── Yes → Is content mostly static?
│   ├── Yes → SSG (Next.js SSG or Astro)
│   └── No → Is content personalized per user?
│       ├── Yes → SSR or RSC (Next.js App Router)
│       └── No → SSG with ISR (Incremental Static Regeneration)
└── No → Is the app behind authentication?
    ├── Yes → SPA (Vite + React Router) or RSC
    └── No → Is real-time interactivity the primary feature?
        ├── Yes → SPA or RSC
        └── No → SSG
```

### 4.3 Framework Recommendations by Rendering Model

| Rendering Model | Recommended Framework | Why |
|----------------|----------------------|-----|
| **SPA** | Vite + React + React Router | Fastest dev server, minimal config, great DX. Vite uses ESBuild for dev and Rollup for production. |
| **SSG** | Next.js (Pages Router, `getStaticProps`) or Astro | Next.js if you may need SSR later; Astro if content-first with minimal JS. |
| **SSR** | Next.js (Pages Router, `getServerSideProps`) or Remix | Next.js for ecosystem; Remix for nested layouts and progressive enhancement. |
| **RSC** | Next.js (App Router) | Currently the only production-ready RSC implementation. Reduces client JS significantly. |

### 4.4 One-Line Mental Model

> **SPA** renders in the browser, **SSG** renders once at build time, **SSR** renders on the server for every request, **RSC** renders on the server and only hydrates interactive pieces on the client.

---

## 5. Infrastructure Layer

> **These are the foundational tools that everything else is built on.**

| Layer | Technology | Justification |
|-------|-----------|---------------|
| **Language** | TypeScript | Type safety catches bugs at compile time, improves IDE autocompletion, makes refactoring safer, and is the industry standard for modern React apps. Use TypeScript unless the team has a strong reason not to. |
| **Runtime** | Node.js (LTS) / Bun | **Node.js**: Required for Next.js, SSR, build tools (Vite, Webpack), and most React meta-frameworks. Use the current LTS version for stability and security patches. The conservative default for compatibility and production SSR. **Bun**: A modern, all-in-one JavaScript runtime and toolkit ([bun.sh](https://bun.sh/)) that serves as a drop-in replacement for Node.js. 2-10x faster runtime, built-in bundler/test runner/package manager, native TypeScript/JSX/TSX support out of the box. Excellent for new projects seeking speed and modern workflows, but verify compatibility with your specific meta-framework and libraries (Next.js, Remix, etc.). |
| **Package Manager** | npm (default) / pnpm (recommended for monorepos) / yarn | **npm**: Zero-config, ships with Node.js, largest registry. **pnpm**: Faster installs, strict dependency resolution, disk-efficient (uses content-addressable store), ideal for monorepos. **yarn**: Plug'n'Play mode is fast but can cause compatibility issues. Pick one and be consistent across the project. |
| **Version Control** | Git + GitHub | Industry standard. Enables PR reviews, CI/CD integration, and collaboration. |
| **Node Version Manager** | nvm or fnm | Ensures all developers use the same Node.js version. Add a `.nvmrc` file to the repo root. |
| **Linting** | ESLint | Catches code quality issues, enforces consistent style. Use `eslint-config-next` for Next.js projects or `@eslint/js` + `typescript-eslint` for SPA projects. |
| **Formatting** | Prettier | Eliminates style debates. Configure once, auto-format on save. Pair with ESLint using `eslint-config-prettier` to avoid conflicts. |
| **Git Hooks** | Husky + lint-staged | Run linting and formatting on staged files before every commit. Prevents broken code from entering the repo. |
| **Environment Variables** | `.env` files + `dotenv` (or Next.js built-in) | Separate config from code. Never commit secrets. Use `.env.local` for local dev, `.env.production` for prod. |
| **Monorepo (if needed)** | Turborepo or Nx | If the project has multiple packages (frontend, backend, shared libs), use a monorepo tool. Turborepo is simpler; Nx is more feature-rich. |

---

## 6. State Management & Data Fetching

> **State management is one of the most over-engineered areas in React. Start simple, add complexity only when needed.**

### 6.1 State Management Decision Guide

See [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md) for the decision guide flowchart.

```
Is the state local to one component?
├── Yes → useState / useReducer (built-in React)
└── No → Is it shared across a few nearby components?
    ├── Yes → Lift state up or use React Context
    └── No → Is it server/async state (API data)?
        ├── Yes → TanStack Query (React Query) or SWR
        └── No → Is it complex global client state?
            ├── Yes → Zustand (simple) or Jotai (atomic)
            └── No → React Context is probably fine
```

### 6.2 Tool Comparison

| Tool | Category | Best For | Justification |
|------|----------|----------|---------------|
| **useState / useReducer** | Local state | Component-level state | Built into React. Zero dependencies. Always start here. |
| **React Context** | Shared state | Theme, locale, auth status (infrequently changing) | Built into React. Avoid for frequently-changing values (causes re-renders). |
| **TanStack Query (React Query)** | Server state | API data fetching, caching, sync | De facto standard for server state. Handles caching, refetching, optimistic updates, pagination. Dramatically reduces boilerplate vs manual `useEffect` + `fetch`. |
| **SWR** | Server state | Simpler API data fetching | Lighter alternative to TanStack Query by Vercel. Good for simpler needs. |
| **Zustand** | Global client state | UI state shared across unrelated components | Tiny (~1 KB), simple API, no boilerplate. Best "step up" from Context when Context causes performance issues. |
| **Jotai** | Atomic state | Fine-grained reactive state | Atom-based model (like Recoil but simpler and maintained). Great for complex derived state. |
| **Redux Toolkit** | Global client state | Large apps with strict unidirectional data flow | Still viable for large teams that want enforced patterns. Use Redux Toolkit (not vanilla Redux). Consider Zustand first for new projects. |

### 6.3 Recommendation

> For most modern React apps: **useState** for local state + **TanStack Query** for server state + **Zustand** if global client state is needed. This covers 95% of use cases with minimal complexity.

---

## 7. Styling & UI Component Libraries

> **Choose a styling approach based on team preference, performance needs, and design system requirements.**

### 7.1 Styling Approaches

| Approach | Tool | Best For | Justification |
|----------|------|----------|---------------|
| **Utility-first CSS** | Tailwind CSS | Rapid prototyping, consistent design, small bundles | Purges unused styles at build time. Highly productive once learned. Dominant in the React ecosystem. |
| **CSS Modules** | Built-in (Next.js, Vite) | Scoped styles without runtime cost | Zero-runtime, works everywhere. Good for teams that prefer traditional CSS. |
| **CSS-in-JS** | styled-components, Emotion | Dynamic styles based on props/state | Runtime overhead. Being phased out in favor of Tailwind or CSS Modules for new projects. Still fine for existing codebases. |
| **Zero-runtime CSS-in-JS** | Vanilla Extract, Panda CSS | Type-safe styles with no runtime cost | Compile-time CSS generation. Good for design system teams. |

### 7.2 UI Component Libraries

| Library | Style System | Best For | Justification |
|---------|-------------|----------|---------------|
| **shadcn/ui** | Tailwind CSS | Full control, copy-paste components | Not a dependency — components are copied into your codebase. Fully customizable. Built on Radix UI primitives (accessible). The current community favorite. |
| **Radix UI** | Unstyled (bring your own) | Accessible primitives | Headless, accessible components. Use with Tailwind or any styling solution. Foundation for shadcn/ui. |
| **Material UI (MUI)** | Emotion (CSS-in-JS) | Google Material Design apps | Comprehensive, well-documented. Heavier bundle. Good for enterprise apps that want Material Design. |
| **Ant Design** | Less/CSS Modules | Enterprise dashboards, admin panels | Rich component set (tables, forms, charts). Popular in enterprise/Asian markets. |
| **Chakra UI** | Emotion (CSS-in-JS) | Rapid prototyping, accessible apps | Good DX, accessible by default. Moving to zero-runtime in v3. |
| **Headless UI** | Unstyled | Tailwind CSS projects | By the Tailwind team. Accessible, unstyled components designed for Tailwind. |

### 7.3 Recommendation

> For new projects: **Tailwind CSS** for styling + **shadcn/ui** for components. This combination gives you full control, excellent DX, small bundles, and accessibility out of the box.

---

## 8. Routing

> **Routing is determined by your rendering model choice (Section 4).**

| Scenario | Router | Justification |
|----------|--------|---------------|
| **SPA (Vite)** | React Router v6+ | Industry standard for client-side routing in React SPAs. Supports nested routes, lazy loading, data loaders. |
| **Next.js (Pages Router)** | Next.js file-based routing | Convention-over-configuration. Each file in `pages/` becomes a route. Supports dynamic routes, catch-all routes. |
| **Next.js (App Router)** | Next.js App Router | Server Components, nested layouts, parallel routes, intercepting routes. The future of Next.js routing. |
| **Remix** | Remix file-based routing | Nested routes with data loading built in. Progressive enhancement by default. |
| **TanStack Router** | TanStack Router | Type-safe routing for SPAs. Full TypeScript inference for route params, search params, and loaders. Newer but growing. |

---

## 9. API Layer

> **How the frontend communicates with the backend is a critical architectural decision.**

### 9.1 API Style Comparison

| Aspect | REST | GraphQL | tRPC |
|--------|------|---------|------|
| **What it is** | Resource-based endpoints (GET /users, POST /orders) | Query language for APIs; client specifies exact data shape | End-to-end type-safe RPC for TypeScript apps |
| **Best for** | CRUD apps, stable contracts, public APIs, third-party integrations | Complex data requirements, multiple data sources, dashboards | Full-stack TypeScript apps (same team owns frontend + backend) |
| **Over-fetching** | Common (returns full objects) | None (client requests exact fields) | None (type-safe contracts) |
| **Under-fetching** | Common (requires multiple requests) | None (single query for nested data) | Minimal (procedures return exactly what's needed) |
| **Caching** | Simple (HTTP caching, CDN-friendly) | Complex (requires Apollo Client, Relay, or urql) | Integrates with TanStack Query |
| **Learning curve** | Low | Medium-High | Low (if you know TypeScript) |
| **Tooling** | Mature (Postman, Swagger/OpenAPI) | Apollo, Relay, urql, GraphiQL | tRPC + TanStack Query |
| **When to avoid** | When data is deeply nested/relational | Simple CRUD, small teams, public APIs | When frontend and backend use different languages |

### 9.2 Usage Recommendations

| Scenario | Recommended API Style | Reasoning |
|----------|----------------------|-----------|
| Public API consumed by third parties | **REST** | REST is universally understood, well-documented with OpenAPI/Swagger, and cacheable. |
| Dashboard pulling data from many sources | **GraphQL** | Single query can aggregate data from multiple services. Avoids waterfall requests. |
| Payment processing, simple CRUD | **REST** | Stable, predictable contracts. Easy to test, monitor, and cache. |
| Full-stack TypeScript monorepo | **tRPC** | End-to-end type safety with zero code generation. Changes to the API are immediately reflected in the frontend. |
| Next.js App Router with Server Components | **Server Components (direct DB access)** | No API layer needed for read operations — Server Components can query the database directly. Use Server Actions for mutations. |

### 9.3 API Client Libraries

| Library | API Style | Justification |
|---------|-----------|---------------|
| **fetch (built-in)** | REST | No dependency needed. Sufficient for simple use cases. |
| **Axios** | REST | Request/response interceptors, automatic JSON transforms, request cancellation. Mature and well-known. |
| **ky** | REST | Tiny, modern fetch wrapper. Good alternative to Axios for smaller bundles. |
| **Apollo Client** | GraphQL | Most mature GraphQL client. Built-in caching, optimistic UI, subscriptions. |
| **urql** | GraphQL | Lighter alternative to Apollo. Modular, extensible. |
| **tRPC Client** | tRPC | Integrates directly with TanStack Query. Type-safe by default. |

---

## 10. Backend Technologies

> **Select backend technologies based on the team's skill set, project requirements, and the scale target from Section 2.**

### 10.1 Languages & Runtimes

| Language | Runtime | When to Choose | Justification |
|----------|---------|---------------|---------------|
| **TypeScript** | Node.js | Full-stack TypeScript team, API-first apps, real-time features | Shared language with frontend. Huge ecosystem. Excellent for I/O-heavy workloads (APIs, real-time). |
| **Python** | Python 3.11+ | ML/AI integrations, data processing, existing Python infrastructure | Best ecosystem for ML/AI. FastAPI is excellent for modern APIs. |
| **Go** | Go runtime | High-performance microservices, CLI tools | Compiled, fast, low memory. Excellent for performance-critical services. |

### 10.2 Backend Framework Comparison

| Platform | Framework | Best Use | Justification |
|----------|-----------|----------|---------------|
| **Node.js** | **Next.js API Routes / Server Actions** | Full-stack React apps | Zero additional setup if already using Next.js. API routes live alongside frontend code. Server Actions simplify mutations. |
| **Node.js** | **Express** | MVPs, simplicity, maximum flexibility | Most popular Node.js framework. Huge middleware ecosystem. Easy to learn. Best for rapid prototyping. |
| **Node.js** | **Fastify** | High-performance APIs, production scale | 2–3x faster than Express. Schema-based validation, built-in logging, plugin system. Choose for performance-critical APIs. |
| **Node.js** | **NestJS** | Enterprise apps, large teams, microservices | Angular-inspired, opinionated, modular. Dependency injection, decorators, built-in support for GraphQL, WebSockets, microservices. Best for large codebases. |
| **Node.js** | **Hono** | Edge computing, serverless, lightweight APIs | Ultra-fast, tiny, runs on Cloudflare Workers, Deno, Bun, and Node. Great for edge-first architectures. |
| **Python** | **FastAPI** | API-first backends for SPAs, ML model serving | Fastest Python framework. Auto-generated OpenAPI docs. Async support. Type hints for validation. Best Python choice for React backends. |
| **Python** | **Django** | Full-stack web apps (SSR, admin panel, ORM) | Batteries-included. Admin panel, ORM, auth, migrations out of the box. Best when you need a full web framework with a React frontend. |
| **Python** | **Flask** | Lightweight services, small APIs, microservices | Minimal, flexible. Good for small services that don't need Django's full feature set. |

### 10.3 Backend Decision Guide

See [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md) for the decision guide flowchart.

```
Is the team full-stack TypeScript?
├── Yes → Are you using Next.js?
│   ├── Yes → Next.js API Routes / Server Actions (simplest)
│   └── No → Express (MVP) or Fastify (performance) or NestJS (enterprise)
└── No → Is the backend primarily for ML/AI or data processing?
    ├── Yes → Python + FastAPI
    └── No → Is this a large enterprise app?
        ├── Yes → NestJS (Node.js) or Django (Python)
        └── No → Express or FastAPI (whichever language the team prefers)
```

---

## 11. Database & ORM Layer

> **Database choice depends on data structure, query patterns, scale, and team familiarity.**

### 11.1 Database Comparison

| Database | Type | Best For | Justification |
|----------|------|----------|---------------|
| **PostgreSQL** | Relational (SQL) | Most web apps, complex queries, ACID transactions | The default choice for most apps. Powerful, reliable, extensible (JSONB, full-text search, PostGIS). |
| **MySQL** | Relational (SQL) | Legacy systems, WordPress, simple CRUD | Widely used, well-understood. PostgreSQL is generally preferred for new projects. |
| **MongoDB** | Document (NoSQL) | Rapidly changing schemas, content management, prototyping | Flexible schema. Good for apps where data structure is unknown upfront. Avoid for heavily relational data. |
| **Redis** | Key-Value (in-memory) | Caching, sessions, rate limiting, real-time leaderboards | Extremely fast. Use as a cache layer alongside a primary database. |
| **SQLite** | Relational (embedded) | Local-first apps, prototyping, edge databases | Zero-config, serverless. Turso and LiteFS enable distributed SQLite for production. |
| **Supabase** | PostgreSQL (managed) | Firebase alternative with SQL | Hosted PostgreSQL + auth + real-time + storage + edge functions. Great for indie projects and startups. |
| **PlanetScale** | MySQL (managed) | Serverless MySQL, branching workflows | Git-like branching for database schemas. Serverless scaling. |
| **Neon** | PostgreSQL (managed) | Serverless PostgreSQL | Scales to zero, branching, generous free tier. Great for serverless deployments. |

### 11.2 ORM / Query Builder Comparison

| Tool | Language | Best For | Justification |
|------|----------|----------|---------------|
| **Prisma** | TypeScript/Node.js | Type-safe database access, migrations, schema-first | Auto-generated TypeScript types from schema. Excellent DX. Works with PostgreSQL, MySQL, SQLite, MongoDB. The default choice for TypeScript backends. |
| **Drizzle ORM** | TypeScript/Node.js | Lightweight, SQL-like syntax, edge-compatible | Thin abstraction over SQL. Faster than Prisma at runtime. Better for serverless/edge (smaller bundle). Growing rapidly. |
| **Knex.js** | Node.js | SQL query builder (no ORM) | Flexible, raw SQL control. Good when you want SQL but with a query builder API. |
| **SQLAlchemy** | Python | Python ORMs, complex queries | The standard Python ORM. Extremely powerful and flexible. Use with FastAPI or Django. |
| **Django ORM** | Python | Django projects | Built into Django. Excellent for Django apps but not usable outside Django. |

### 11.3 Recommendation

> For most TypeScript projects: **PostgreSQL** (via Supabase or Neon for managed hosting) + **Prisma** (for DX) or **Drizzle** (for performance/edge). This combination provides type safety, excellent migrations, and a great developer experience.

---

## 12. Authentication & Authorization

> **Authentication (who you are) and authorization (what you can do) are critical for any app with user accounts.**

### 12.1 Authentication Solutions Comparison

| Solution | Best For | Justification |
|----------|----------|---------------|
| **NextAuth.js** | Next.js apps, flexible provider support | Free, open-source, supports OAuth, magic links, credentials. Tight Next.js integration. Great for custom needs. |
| **Clerk** | Rapid development, modern UI | Pre-built UI components, user management dashboard, MFA, organizations. Best for teams that want to ship auth quickly. Paid after free tier. |
| **Supabase Auth** | Supabase projects | Integrated with Supabase DB and real-time. Free tier is generous. Good if already using Supabase. |
| **Auth0** | Enterprise, large-scale apps | Enterprise-grade, compliance-ready, extensive provider support. Expensive at scale. Good for regulated industries. |
| **Firebase Auth** | Firebase projects, mobile apps | Tight Firebase ecosystem integration. Good for mobile-first apps with Firebase backend. |
| **AWS Cognito** | AWS-native apps | Deep AWS integration, scales automatically. Complex setup. Good if already on AWS. |
| **Custom (Passport.js)** | Full control, legacy systems | Maximum flexibility. Requires more development and maintenance. Only choose if you have specific needs that SaaS can't meet. |

### 12.2 Authorization Patterns

| Pattern | Use Case | Implementation |
|---------|----------|----------------|
| **Role-Based Access Control (RBAC)** | Simple permission models (admin, user, guest) | Store roles in user table. Check role on API routes and UI. |
| **Attribute-Based Access Control (ABAC)** | Complex rules (user can edit if they are the author and post is not locked) | Check multiple attributes before granting access. More flexible but more complex. |
| **Row-Level Security (RLS)** | Database-enforced permissions | PostgreSQL RLS, Supabase policies. Database automatically filters queries. Strongest security model. |
| **JWT Claims** | Stateless auth | Embed permissions in JWT token. Validate on each request. Good for microservices. |

### 12.3 Recommendation

> For most Next.js projects: **NextAuth.js** (flexible, free) or **Clerk** (fast, modern, paid). For Supabase projects: **Supabase Auth** + **Row-Level Security**. Always use HTTPS, rotate secrets, and implement MFA for sensitive apps.

---

## 13. Testing Strategy

> **Test the right things at the right level. Avoid over-testing (unit tests for every function) and under-testing (no E2E tests).**

### 13.1 Testing Tool Comparison

| Test Type | Tool | Best For | Justification |
|-----------|------|----------|---------------|
| **Unit Testing** | Vitest | Fast unit tests for utilities, hooks, pure functions | 5-10x faster than Jest. Compatible with Vite projects. Native ESM support. |
| **Component Testing** | React Testing Library | Testing React components from a user perspective | Encourages testing behavior, not implementation. Works with Vitest or Jest. |
| **End-to-End (E2E)** | Playwright | Full user flows, cross-browser testing | Fast, reliable, great DX. Better than Cypress for modern apps. Supports parallel execution. |
| **Visual Regression** | Chromatic (Storybook) | Detecting UI changes | Automated visual diffs. Good for design systems and component libraries. |
| **API Testing** | Supertest or Postman | Testing API endpoints | Supertest for Node.js integration tests. Postman for manual testing and collections. |

### 13.2 Testing Strategy by Project Stage

| Stage | Testing Focus | Recommended Tests |
|-------|--------------|-------------------|
| **MVP / Prototype** | Core user flows work | E2E tests for happy paths only. Skip unit tests. |
| **V1 Launch** | Critical paths + key components | E2E (critical flows) + Component tests (complex components) + Unit tests (business logic). |
| **Production / Scale** | Comprehensive coverage | All of the above + Visual regression + Performance tests + API contract tests. |

### 13.3 Recommendation

> For most projects: **Vitest** (unit) + **React Testing Library** (components) + **Playwright** (E2E). Write E2E tests for critical user flows first, then add component/unit tests for complex logic.

---

## 14. DevOps, CI/CD & Deployment

> **Deployment and CI/CD should be set up on day one to enable continuous delivery.**

### 14.1 Hosting & Deployment Platforms

| Platform | Best For | Justification |
|----------|----------|---------------|
| **Vercel** | Next.js, Vite SPAs | Zero-config Next.js hosting. Automatic preview deploys. Edge functions. Generous free tier. Best DX. |
| **Netlify** | Static sites, JAMstack | Great for SSG sites. Edge functions, forms, split testing built in. Good alternative to Vercel. |
| **Railway** | Full-stack apps, databases | Simple full-stack deployments. Deploy frontend, backend, and database together. Good for monorepos. |
| **Render** | Full-stack, PostgreSQL | Heroku alternative. Free PostgreSQL, background workers. Good for apps with server-side rendering. |
| **Fly.io** | Global edge deployments, real-time apps | Deploy close to users worldwide. Good for WebSocket/real-time apps. Great for low-latency needs. |
| **AWS (Amplify, ECS, Lambda)** | Enterprise, fine-grained control | Most flexible, most complex. Good for teams already on AWS or needing enterprise features. |
| **Google Cloud Run** | Containerized apps | Serverless containers. Good for teams on GCP. |

### 14.2 CI/CD Tools

| Tool | Best For | Justification |
|------|----------|---------------|
| **GitHub Actions** | GitHub repos | Built into GitHub. Free for public repos. Huge marketplace of actions. Easiest to set up. |
| **GitLab CI** | GitLab repos | Built into GitLab. Similar to GitHub Actions. Good if using GitLab. |
| **CircleCI** | Complex pipelines | Powerful, flexible. Good for large teams with complex workflows. Paid after free tier. |
| **Jenkins** | On-prem, legacy systems | Self-hosted, highly customizable. Good for enterprises that can't use cloud CI. |

### 14.3 Recommended CI/CD Pipeline

```yaml
# Minimal CI pipeline (GitHub Actions)
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run build
      - run: npm test
      - run: npx playwright test # E2E tests
```

### 14.4 Containerization

| Tool | Best For | Justification |
|------|----------|---------------|
| **Docker** | Consistent environments, microservices | Industry standard. Use multi-stage builds for smaller images. |
| **Docker Compose** | Local dev, multi-service apps | Orchestrate multiple containers locally. Great for full-stack dev. |
| **Kubernetes** | Large-scale, enterprise | Production-grade orchestration. Overkill for most projects. Use managed K8s (GKE, EKS, AKS) if needed. |

---

## 15. Monitoring, Logging & Observability

> **You can't fix what you can't see. Set up monitoring on day one.**

### 15.1 Monitoring & Error Tracking

| Tool | Best For | Justification |
|------|----------|---------------|
| **Sentry** | Error tracking, crash reporting | Industry standard. Shows full stack traces, user context, breadcrumbs. Excellent DX. Free tier is generous. |
| **LogRocket** | Session replay + error tracking | Records user sessions. See exactly what the user did before the error. Great for debugging complex issues. |
| **Datadog** | Full observability (metrics, traces, logs) | Enterprise-grade. Expensive. Good for large teams that need centralized observability. |
| **New Relic** | APM, performance monitoring | Tracks backend performance, database queries, slow endpoints. Good for performance optimization. |
| **Vercel Analytics** | Next.js performance | Built into Vercel. Tracks Web Vitals. Free for Vercel users. |

### 15.2 Logging

| Tool | Best For | Justification |
|------|----------|---------------|
| **Console.log** | Local dev | Built-in. Fine for development. |
| **Pino / Winston** | Node.js production logging | Structured JSON logs. Pino is faster; Winston is more feature-rich. |
| **Datadog / Loggly / Papertrail** | Centralized log aggregation | Search logs across all services. Good for debugging distributed systems. |

### 15.3 Recommendation

> For most projects: **Sentry** for error tracking (add on day one). For Next.js on Vercel: **Vercel Analytics** for Web Vitals. For production backends: **Pino** for logging + **Datadog** or **Papertrail** for log aggregation (if budget allows).

---

## 16. Security Checklist

> **Security is not a feature you add later. Bake it in from the start.**

### 16.1 Frontend Security

- [ ] **Content Security Policy (CSP):** Set CSP headers to prevent XSS.
- [ ] **HTTPS Only:** Always use HTTPS in production. Enable HSTS headers.
- [ ] **Sanitize User Input:** Use DOMPurify for HTML sanitization. Never use `dangerouslySetInnerHTML` without sanitization.
- [ ] **Avoid Inline Scripts:** Inline `<script>` tags can bypass CSP. Use bundled scripts.
- [ ] **Dependency Scanning:** Use `npm audit` or Dependabot to catch vulnerable dependencies.
- [ ] **Secure Cookies:** Set `httpOnly`, `secure`, and `sameSite` flags on cookies.
- [ ] **Rate Limiting:** Implement rate limiting on API routes to prevent abuse.

### 16.2 Backend Security

- [ ] **Input Validation:** Validate all user input on the server (use Zod, Joi, or AJV).
- [ ] **SQL Injection Prevention:** Use parameterized queries or ORMs (Prisma, Drizzle).
- [ ] **Authentication:** Use battle-tested libraries (NextAuth, Passport). Never roll your own crypto.
- [ ] **Authorization:** Check permissions on every API route. Implement RBAC or RLS.
- [ ] **Secrets Management:** Use environment variables. Never commit secrets. Use tools like Doppler or AWS Secrets Manager for production.
- [ ] **CORS:** Configure CORS to allow only trusted origins.
- [ ] **API Rate Limiting:** Use libraries like `express-rate-limit` or Upstash Rate Limiting.
- [ ] **Password Hashing:** Use bcrypt or Argon2. Never store plaintext passwords.

### 16.3 Infrastructure Security

- [ ] **Principle of Least Privilege:** Give services only the permissions they need.
- [ ] **Database Access:** Use VPCs, private subnets, and restrict database access to backend only.
- [ ] **Automated Backups:** Enable automatic database backups with point-in-time recovery.
- [ ] **Security Headers:** Set headers like `X-Frame-Options`, `X-Content-Type-Options`, `Strict-Transport-Security`.
- [ ] **DDoS Protection:** Use Cloudflare or AWS Shield.
- [ ] **Audit Logs:** Log all sensitive operations (auth, data changes) for compliance and forensics.

---

## Conclusion

> **This reference document is comprehensive by design.** For quick decisions, always start with [TECH_STACK_DEFAULTS.md](TECH_STACK_DEFAULTS.md). Use this document to understand the "why" behind each choice and to explore alternatives.
>
> **Remember:** Technology choices should serve the project requirements, not the other way around. When in doubt, choose boring, proven technology over the latest trend.

---

**Last Updated:** 2026-02-17

**Future Modularization:**
This document will eventually be split into modular files under `docs/tech-stack/` for easier maintenance and updates. Each section (1-16) will become its own file, making it easier to find and update specific topics without loading the entire reference.

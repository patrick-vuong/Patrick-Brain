# Tech Stack Defaults: North Star Guide 🌟

> **START HERE.** Always read this file first when starting a new React project. This is your quick reference guide containing the essential decision frameworks and default stack recommendations. Only consult [TECH_STACK_REFERENCE.md](TECH_STACK_REFERENCE.md) for deep rationale or alternative options.

---

## 📋 Instructions for Agents and Humans

1. **Always read this file first** when planning a React web application
2. Use the decision guides below to make quick, informed choices
3. Refer to the Quick Start Stack for a solid default configuration
4. Only dive into [TECH_STACK_REFERENCE.md](TECH_STACK_REFERENCE.md) when you need:
   - Detailed explanations of why a technology was chosen
   - Alternative options and their trade-offs
   - Comprehensive comparisons of tools in each category

---

## 🧠 One-Line Mental Models

Quick reference for key technology decisions:

| Topic | Mental Model |
|-------|-------------|
| **Rendering** | **SPA** = browser renders; **SSG** = build-time renders; **SSR** = server renders per request; **RSC** = server renders, client hydrates interactive parts. |
| **State** | **useState** for local; **TanStack Query** for server; **Zustand** for global client. |
| **Styling** | **Tailwind** for utility-first; **shadcn/ui** for components; **CSS Modules** for scoped traditional CSS. |
| **API** | **REST** for CRUD/public APIs; **GraphQL** for complex data needs; **tRPC** for full-stack TypeScript. |
| **Database** | **PostgreSQL** unless you have a specific reason not to. **Prisma** for DX; **Drizzle** for performance. |
| **Auth** | **NextAuth.js** for flexibility; **Clerk** for speed; **Supabase Auth** for Supabase projects. |
| **Testing** | **Vitest** (unit) + **React Testing Library** (components) + **Playwright** (E2E). |
| **Deployment** | **Vercel** for Next.js; **Railway** for full-stack; **AWS** for enterprise control. |
| **Monitoring** | **Sentry** on day one. Always. |
| **Package Manager** | **npm** for simplicity; **pnpm** for monorepos and speed. |

---

## 🚀 Quick Start Stack (Opinionated Default)

For a modern React web app with no unusual requirements, start here and adjust as needed:

| Layer | Choice |
|-------|--------|
| Framework | Next.js (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS + shadcn/ui |
| State (server) | TanStack Query |
| State (client) | Zustand (if needed) |
| Database | PostgreSQL (Neon or Supabase) |
| ORM | Prisma |
| Auth | NextAuth.js or Clerk |
| Testing | Vitest + React Testing Library + Playwright |
| CI/CD | GitHub Actions |
| Deployment | Vercel |
| Monitoring | Sentry + Vercel Analytics |

---

## 🗺️ Key Decision Guides

### 1. Rendering Model Decision Guide

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

**Quick Recommendations:**
- **SPA**: Dashboards, admin panels, apps behind auth → **Vite + React + React Router**
- **SSG**: Marketing sites, blogs, docs → **Next.js SSG** or **Astro**
- **SSR**: Personalized content, e-commerce → **Next.js SSR** or **Remix**
- **RSC**: Complex apps needing performance + interactivity → **Next.js App Router**

### 2. State Management Decision Guide

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

**Quick Recommendations:**
- **Local state**: `useState` or `useReducer` (built-in)
- **Server state**: **TanStack Query** (de facto standard)
- **Global client state**: **Zustand** (tiny, simple) or **Jotai** (atomic)

### 3. Backend Decision Guide

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

**Quick Recommendations:**
- **Full-stack TypeScript + Next.js**: **Next.js API Routes/Server Actions**
- **Node.js MVP**: **Express**
- **Node.js Performance**: **Fastify**
- **Node.js Enterprise**: **NestJS**
- **Python API**: **FastAPI**
- **Python Full-Stack**: **Django**

---

## 📚 When to Consult the Full Reference

Consult [TECH_STACK_REFERENCE.md](TECH_STACK_REFERENCE.md) when you need:

1. **Detailed comparisons** of alternative technologies
2. **Understanding the "why"** behind each recommendation
3. **Trade-off analysis** for specific use cases
4. **Comprehensive tables** comparing multiple options
5. **Security checklists** and best practices
6. **Testing strategies** and deployment considerations
7. **Complete PRD discovery questions** for project planning

---

## 🎯 Agent Workflow

1. ✅ **Read this file first** (TECH_STACK_DEFAULTS.md)
2. Use the decision guides to make initial technology choices
3. Start with the Quick Start Stack unless there's a specific reason to deviate
4. Only open TECH_STACK_REFERENCE.md for:
   - Detailed justifications
   - Alternative options
   - Specific sections you need deeper guidance on
5. Keep your context window focused and efficient

---

**Last Updated:** 2026-02-17

> **Remember:** These are sensible defaults based on current best practices. Always validate choices against your specific project requirements documented in the PRD (see TECH_STACK_REFERENCE.md Section 2).

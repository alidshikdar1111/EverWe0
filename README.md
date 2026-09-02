# EverWe

EverWe is a universal social platform designed for everyone. It is not a
couples or partner-scoped application. Any pattern, authorization rule, or
domain assumption that restricts identity, relationships, or interactions to
a two-person pairing must be treated as legacy (EverTwo-derived) and must not
be carried into this codebase.

## Product boundaries

- **Universal identity.** A user is a single individual with one profile.
  There is no implicit partner, pair, or linked account.
- **Open social graph.** Friendships and connections are between any two
  users. No authorization check assumes a paired relationship.
- **General-purpose interactions.** Posts, reactions, messages, groups,
  stories, reels, and all future features operate on the universal social
  graph, not a couple scope.

## Verified baseline (Instruction 001, 2026-08-19)

| Area                  | Finding                                                        |
| --------------------- | ------------------------------------------------------------- |
| Source code            | None. Repository contains only `.gitkeep` and `package-lock.json` (empty). |
| Package manifest       | No `package.json` exists. `package-lock.json` has no dependencies. |
| Entry points           | None.                                                         |
| Database / backend     | Supabase credentials present in `.env` (`VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`). Database schema could not be inspected (MCP permission denied); treat as empty until a migration is applied. |
| Reusable components    | None.                                                         |
| Authentication state   | No auth implementation exists.                                |
| EverTwo-derived patterns | None present. No code to audit.                             |

## Tech stack (planned)

- **Frontend:** React + Vite + TypeScript
- **Backend / database / auth:** Supabase (PostgreSQL, RLS, Auth)
- **Styling:** Tailwind CSS

## Data model

The foundational schema (Instruction 002) defines three tables:
**profiles**, **friendships**, and **posts**. The feed is derived at query
time from friendships + posts — no duplicate feed table. Full schema design
and migration SQL are in [`docs/data-model-foundation.md`](docs/data-model-foundation.md).

> **Note:** The migration SQL is ready but could not be applied to the database
> during Instruction 002 — Supabase MCP tools returned a project-level
> permission error. Apply it via `mcp__supabase__apply_migration` once access
> is restored.

## Build philosophy

EverWe is built across 220 instructions in 20 phases. Each instruction is one
self-contained, verifiable step. Work only on the current instruction and its
minimum dependencies. Enforce authorization at the database/backend boundary,
not only in the UI.

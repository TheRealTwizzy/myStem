<!-- /autoplan restore point: /c/Users/trent/.gstack/projects/Stems/main-autoplan-restore-20260610-142630.md -->
# Stems Web Game — Implementation Plan

**Source:** STEMS_MVP_PRD (27 canonical documents)  
**Target:** Browser-based web game faithful to the PRD  
**Approach:** Phased delivery — playable cultivation loop first, then economy, then premium

---

## Problem statement

The Stems PRD defines a fully-specified mobile cultivation game. We need a web
implementation that preserves all product design laws, the cultivation loop, and
the server-authoritative architecture — adapted for browser constraints.

## Premises

1. Web-first means desktop+mobile browser, not native mobile app.
2. The PRD's "portrait-first" UI maps to a narrow-column layout (max 480px game area) inside a wider browser viewport.
3. Server-authoritative requirement is non-negotiable (Laws 7, 8, 19).
4. "Hollow Field Sketch" (free procedural illustration) is SVG/Canvas, not AI-generated.
5. AI illustration (premium) calls an external image generation API server-side.
6. Scope is web MVP — cultivation loop through Becoming resolution is the core deliverable.
7. Auth is session-based (simple account + cookie); no OAuth required for MVP.
8. Real-time biofeedback uses WebSockets or SSE.
9. Monetization (subscription, allowances) is stubbed — flow exists but payment gated.

## Alternatives considered

| Approach | Effort | Risk | Decision |
|---|---|---|---|
| Full-stack monolith (Next.js API routes) | Low | Medium (scales poorly) | Selected for MVP speed |
| Microservices (sim + economy + entitlement separate) | High | Low (matches PRD arch) | Deferred post-MVP |
| Client-side simulation | Low | High (violates Law 19) | Rejected |
| Static game (no server) | Very Low | Very High (no server auth) | Rejected |

## Tech stack

### Frontend
- **Framework:** React 19 + TypeScript
- **Build:** Vite 6
- **Styling:** Tailwind CSS v4 + CSS custom properties for theme
- **Animation:** Framer Motion (Stem idle animations, Becoming transitions)
- **Canvas/SVG:** Konva.js or plain SVG for procedural Hollow Field Sketch
- **State:** Zustand (client UI state) + TanStack Query (server state)
- **Routing:** React Router v7
- **WebSocket:** native browser WebSocket API

### Backend
- **Runtime:** Node.js 22 LTS
- **Framework:** Fastify 5 (fast, schema-first, TypeScript-native)
- **Database:** PostgreSQL 16 (Neon serverless for easy deploy) + Drizzle ORM
- **Auth:** Lucia v3 (session-based, no OAuth complexity)
- **Real-time:** Fastify WebSocket plugin
- **Validation:** Zod (shared schemas client+server)
- **Job queue:** BullMQ + Redis (AI illustration generation)
- **AI illustrations:** Replicate API or Stability AI (server-side only)

### Infrastructure
- **Deploy:** Vercel (frontend) + Railway (backend + Redis + Postgres) — or Hono on Cloudflare Workers for edge
- **Storage:** Cloudflare R2 for premium illustration assets
- **CI:** GitHub Actions

## Architecture (per PRD §19)

```
Browser Client
  ├── Hollow UI (SVG Stem render + controls)
  ├── Field Entry viewer
  ├── Biofeedback overlay
  └── WS connection → real-time state push

Fastify API Server
  ├── /auth        — session create/destroy
  ├── /hollows     — CRUD, condition changes (server-auth)
  ├── /stems       — read Stem state
  ├── /becomings   — readiness, consent, resolution
  ├── /field-entries — list, view, lock/unlock
  ├── /economy     — trade, gift (stubbed MVP)
  ├── /entitlement — subscription state (stubbed MVP)
  ├── /illustration— trigger, status, retrieve (BullMQ job)
  └── WS /live     — push biofeedback events to client

Simulation Engine (TypeScript module, runs server-side)
  ├── BiologicalPressure accumulator
  ├── BecomingReadiness evaluator
  ├── ComponentSelector (148-component inventory, simplified for web MVP)
  ├── AnatomyValidator (PRD Laws 1-5, 15)
  └── SustainmentEvaluator

PostgreSQL
  ├── accounts, sessions
  ├── hollows, stems
  ├── anatomy_component_instances
  ├── becomings, field_entries
  ├── premium_assets, archive_records
  ├── entitlement_ledger, transfers
  └── content_config (versioned, seed-driven)
```

## Feature scope for web MVP

### Phase 1 — Playable core (target: first playable)

- [ ] **Account + auth** — register, login, session cookie
- [ ] **Three Hollows** — create, view, biome/sub-biome selection (7 families × 3 sub-biomes = 21)
- [ ] **New Seed** — create random Stemling in empty Hollow
- [ ] **Hollow controls** — Warmth, Moisture, Light + 1 unique; 5 bands each; server-auth changes
- [ ] **Fixed Stemling spawn** — procedural SVG matching PRD visual law (compact quadruped, 4 limbs, 2 eyes)
- [ ] **Biofeedback system** — posture + text observation cues; WebSocket push
- [ ] **Biological pressure** — simplified accumulator driving Becoming readiness
- [ ] **Becoming trigger** — escalating multimodal signals (posture, rhythm, copy)
- [ ] **Mutation Consent** — Stabilize / Suppress / Let Continue flows (PRD §05)
- [ ] **Atomic Becoming resolution** — component selection, anatomy update, Field Entry creation
- [ ] **Field Entry viewer** — free presentation (Hollow Field Sketch = generated SVG)
- [ ] **Lifecycle stages** — Stemling → Juvenile → Adolescent → Settled Form
- [ ] **Tutorial flow** — mandatory first Stemling tutorial (skippable thereafter)
- [ ] **Basic sustain + strain** — unstable/decaying states with biofeedback

### Phase 2 — Adult care + social economy

- [ ] **Adult Becomings** — slower rate, continued mutation
- [ ] **Regression system** — Decay → regression with visual settling (not amputation)
- [ ] **Recovery flow** — observable recovery path post-regression
- [ ] **Release** — permanent, confirmation-gated, server-atomic
- [ ] **Trading** — one-for-one Field Entry swap (stubbed UI in Phase 1)
- [ ] **Gifting** — atomic Field Entry transfer
- [ ] **Lineage Synthesis** — premium Genetic Entry consumption → new Stemling

### Phase 3 — Premium + monetization

- [ ] **Premium illustration** — allowance reservation → AI generation → attachment (BullMQ job)
- [ ] **Illustrated Field Archive** — archive view, provenance records
- [ ] **Bio-Lab Analyst subscription** — Stripe integration, weekly grant ledger
- [ ] **The Choosing** — dominant adaptive direction commitment (Becoming 3 or 4)

## Data model (per PRD §19)

Matches canonical entities exactly:
- Account, Hollow, Stem, AnatomyComponentInstance
- Becoming, FieldEntry, PremiumAsset, ArchiveRecord
- EntitlementLedger, Transfer

Schema migrations via Drizzle Kit. Content config seeded from versioned JSON.

## Simplified component inventory for web MVP

Full PRD targets 148 components. Web MVP ships with:
- **30 base components** (core visible mutations across major body regions)
- **10 transitional components** (stage-bridging)
- **8 hero components** (high-salience, illustration-ready)
- **Expansion to full 148** in post-launch content updates

All components follow the canonical schema (operation, region, prerequisites,
sustainment demands, biofeedback cues, visual descriptors).

## Procedural Stem rendering (Hollow Field Sketch)

- SVG-based, deterministic from anatomy_graph
- Stemling: fixed spawn plan (32–42cm, quadruped, pale tissue)
- Mutations: additive SVG layers per AnatomyComponentInstance
- Asymmetry: introduced post-Juvenile per PRD visual law
- Tissue states: posture/movement via CSS animation classes driven by sustainment state
- Color: warm pallor → amber → muted mineral palette; never carries essential status alone
- No AI for free presentation — fully client-side from authoritative anatomy data

## Security model (per PRD §19)

- All meaningful state changes: server-authoritative, authenticated session required
- Allowance balance: server-only, never trusted from client
- Genetic Entry state: server-only
- Premium assets: signed URLs with expiry
- Irreversible actions (synthesis, trade, gift, release): double-confirmation, idempotency keys
- Audit log: all premium and transfer operations

## Test plan (Phase 1)

- Unit: simulation engine (pressure accumulator, component selector, anatomy validator)
- Integration: Becoming resolution (consent → anatomy update → Field Entry atomic)
- Integration: Hollow condition change (server-auth, offline rejection)
- E2E: first launch flow (register → Hollow setup → New Seed → first Becoming)
- E2E: Becoming consent flows (Stabilize, Suppress, Let Continue)
- Fixtures: PRD 27_GOLDEN_LIFECYCLE_FIXTURES.md as canonical test seeds

## Constraints / non-goals (web MVP)

Per PRD non-goals (all preserved):
- No combat, PvP, rankings
- No visible stats, recipes, probability meters
- No direct anatomy selection
- No offline mutation queue
- No rarity tiers, gacha
- No currency markets

Web-specific constraints:
- No React Native / Expo — pure web
- No Electron — browser only
- Subscription payment flow: stubbed in Phase 1 (real Stripe in Phase 3)

## Milestones

| Milestone | Target | Exit criteria |
|---|---|---|
| M1: Skeleton | Week 1 | Auth + 3 Hollows + New Seed + Stemling renders |
| M2: Living Loop | Week 3 | Controls → biofeedback → Becoming trigger works |
| M3: First Becoming | Week 5 | Full consent flow + Field Entry created |
| M4: Lifecycle | Week 7 | All 4 stages + adult care + basic strain |
| M5: Social economy | Week 10 | Trade + gift + release |
| M6: Premium | Week 14 | Illustration + subscription + archive |

## Open questions / risks

1. **Procedural SVG rendering** — complex anatomy post-Adolescent may need a dedicated render system; may need Three.js/WebGL fallback
2. **Simulation complexity** — pressure accumulator and component selector are underspecified in PRD; need internal design doc
3. **AI illustration cost** — Replicate/Stability pricing at scale; allowance caps help but need monitoring
4. **Biofeedback latency** — WebSocket push must feel responsive; may need SSE fallback
5. **The Choosing mechanics** — PRD says Becoming 3 or 4; exact trigger logic needs formalization

---

*Plan created from STEMS_MVP_PRD canonical documents (00–27). All design laws from 02_PRODUCT_DESIGN_LAWS.md apply without exception.*

---

## CEO REVIEW — Phase 1 (SELECTIVE EXPANSION)

**Mode:** SELECTIVE EXPANSION — hold scope as baseline, cherry-pick expansions  
**Outside voice:** Claude subagent (Codex unavailable)  
**Date:** 2026-06-10

### 0A. Premise Challenge

| Premise | Status | Risk |
|---|---|---|
| Web-first platform (not mobile) | ACCEPTED — intentional, serves as canonical demo layer | Medium: emotional register of product (intimacy, push, return loop) doesn't map natively to browser |
| Portrait-first → narrow-column layout | ACCEPTED with PWA mitigation | Medium: standalone PWA mode recovers portrait experience on mobile browser |
| Server-authoritative (Laws 7, 8, 19) | CORRECT — non-negotiable | Low |
| SVG procedural rendering for free presentation | ACCEPTED | Medium: performance budget unknown for complex post-Adolescent anatomy |
| Session-based auth only | ACCEPTED WITH CHANGE — add account recovery | High without recovery: permanent assets (Law 8) require reliable account access |
| Simulation tick on server | CRITICAL GAP — tick runtime not specified | Critical: must be resolved before M1 |
| 30/10/8 component inventory | ACCEPTED | Medium: shallow pool risks Law 1 / Law 16 violations at scale; monitor post-launch |
| Phase 1 no monetization | ACCEPTED | Medium: no premium anticipation in Phase 1 — add PWA + account recovery as emotional investment |

### 0B. Existing Code Leverage

No existing implementation code. This is greenfield. Sub-problems map to:
- Auth system: Lucia v3 (established, no existing code to reuse)
- Database schema: derived directly from PRD §19 entities
- Simulation engine: derived from PRD biological systems (no prior code)
- Procedural SVG: built from anatomy_graph + PRD Visual Bible

### 0C. Dream State

```
CURRENT STATE                THIS PLAN                    12-MONTH IDEAL
No web implementation  --->  Web MVP with core loop  --->  Mobile app + web demo
Specs only                   3 Hollows, Becomings,         Full 148 components,
No playable build            Field Entries, lifecycle       premium illustration,
                             Basic sustain/strain           social economy live,
                             No premium, no economy         subscription running
```

### 0C-bis. Implementation Alternatives

```
APPROACH A: Next.js Monolith
  Summary: Single Next.js app with API routes, no separate backend
  Effort: S (1 repo, easier deploy)
  Risk: Med (API routes don't support WebSocket; simulation tick needs separate worker)
  Pros: Single deploy, colocation, faster iteration
  Cons: Not WebSocket-native; simulation tick needs workaround; scales poorly
  Reuses: Nothing yet (greenfield)

APPROACH B: React + Fastify (current plan)
  Summary: Vite React frontend + Fastify backend on Railway
  Effort: M
  Risk: Med (two-origin CORS + WebSocket from Vercel→Railway)
  Pros: True WebSocket support, clear separation, Fastify native schema validation
  Cons: Two deployments, CORS complexity, Neon serverless cold starts for tick
  Reuses: Nothing yet (greenfield)

APPROACH C: Hono on Cloudflare Workers (edge-first)
  Summary: Hono framework on Workers, Durable Objects for simulation tick per Stem
  Effort: M
  Risk: Low-Med (Durable Objects solve the tick runtime problem natively)
  Pros: Durable Objects = stateful per-Stem tick at edge, no cold starts, global CDN
  Cons: Cloudflare Workers learning curve, D1 database (SQLite dialect) not Postgres
  Reuses: Nothing yet (greenfield)
```

**RECOMMENDATION:** Approach B (current plan) for MVP speed. But simulation tick must use BullMQ job on Railway, not inline Fastify request handler. Add to plan. Approach C is the post-MVP architecture target.

### 0D. Mode-Specific Analysis (SELECTIVE EXPANSION)

Complexity check: plan touches ~25 new files minimum (Phase 1 alone). Passes threshold but it's a greenfield build — unavoidable.

**Accepted expansions (cherry-picked):**
1. **PWA manifest + standalone mode** — recovers portrait-first experience on mobile browser. 30-min CC effort. Accepted.
2. **Account recovery (email verification)** — required for Law 8 compliance. 2-hour CC effort. Accepted.
3. **Basic analytics (Posthog/Plausible)** — required to measure retention. 1-hour CC effort. Accepted.
4. **Simulation tick design doc** — must be written before M1. 2-hour CC effort. Required.

**Deferred expansions:**
- Full 148 component inventory → post-launch content update
- Push notifications → Phase 2
- Content moderation queue → Phase 3
- Legal/compliance review → before subscription launch

### 0E. Temporal Interrogation

```
HOUR 1 (foundations):  What is the simulation tick interval? 
                        How does the server know a Stem's state changed without a request?
                        Answer: BullMQ recurring job, 1-minute tick per active Stem

HOUR 2-3 (core logic): How does BiologicalPressure accumulate?
                        What does the WebSocket push on each tick?
                        Answer: needs simulation spec doc before implementation

HOUR 4-5 (integration): How does the SVG renderer receive anatomy updates?
                         What event triggers a re-render vs. an animation-only update?
                         Answer: TanStack Query invalidation on WS push event type

HOUR 6+ (polish/tests): What does the Stemling look like on first render?
                         Is the fixed spawn plan (PRD §11) deterministic from seed?
                         Answer: yes — biological_signature_ref seeds SVG deterministically
```

### Section 1 — Problem Framing

The plan correctly identifies the core: build the PRD's cultivation loop as a web game. No reframing needed. The "web vs mobile" question is acknowledged as a conscious trade (demo layer + development platform) rather than an oversight.

**No issues.**

### Section 2 — Error & Rescue Registry

| Error | Trigger | User sees | Handler | Tested? |
|---|---|---|---|---|
| Hollow condition change offline | No network | Controls disabled, cached view | Offline detection → disable controls | No |
| Becoming resolution failure | Server error mid-resolution | Field Entry not created, anatomy unchanged | Atomic transaction rollback, retry prompt | No |
| WS connection drop | Network interruption | Biofeedback pauses | Reconnect with exponential backoff | No |
| Duplicate Genetic Entry | Race condition in trade | Trade should fail cleanly | Idempotency key + compare-and-swap | No |
| Account session lost | Browser clear | All data inaccessible | Account recovery flow (new scope) | No |
| SVG render failure | Unknown anatomy state | Fallback silhouette | Fallback render path required | No |

### Section 3 — Scope & Complexity

Phase 1 scope is justified. 18 feature items is large for 7 weeks but attainable with CC. Primary risk: simulation engine is underspecified.

**Gap identified:** Phase 1 timeline includes lifecycle (M4: "All 4 stages") but adult care and regression are Phase 2. Resolved: Phase 1 delivers lifecycle stage transitions only. Adult sustain/strain loop (full decay/regression) moves to Phase 2 alongside Trading.

### Section 4 — Architecture

See architecture ASCII diagram in Eng Phase review (Phase 3).

**Gap identified:** Simulation tick has no runtime home in current plan.
**Resolution:** Add BullMQ recurring tick job to plan. Each active Stem gets a scheduled job. Tick evaluates pressure accumulation, sustainment state, Becoming readiness. Pushes updates via WS to connected client if state changes.

**Updated architecture note added below.**

### Section 5 — Data Model

Matches PRD §19 entities exactly. No gaps identified.

Additions from CEO review:
- Add `account.recovery_email` (nullable) to Account entity
- Add `account.recovery_token` + `account.recovery_token_expires_at`

### Section 6 — Integration Points

All PRD flow integrations are represented in Phase 1-3 feature list. No silent gaps.

### Section 7 — Testing

See Test Plan in Eng Phase review.

### Section 8 — Observability

Gap: no observability plan.
**Resolution:** Add basic structured logging per PRD §19 + Posthog event tracking. See Analytics section below.

### Section 9 — Deployment

Gap: no deployment strategy.
**Resolution:** Railway (backend + Redis + Neon) + Vercel (frontend). No change to current stack. Add Railway deploy config as Phase 1 M1 task.

### Section 10 — Security

Plan correctly identifies all security requirements from PRD §19. No gaps.

### Failure Modes Registry

| Failure | Severity | Gap |
|---|---|---|
| Simulation tick not running (no job queue) | Critical | Fix: add BullMQ tick job to plan |
| Account recovery unavailable → permanent asset loss | Critical | Fix: add recovery flow to Phase 1 |
| SVG render no fallback for complex anatomy | High | Fix: specify fallback silhouette render path |
| Component pool too shallow → Law 1 fails | High | Monitor post-launch; 30→50 base components post-M5 |
| WS reconnection not handled | Medium | Fix: add reconnect logic to Phase 1 |

### NOT in scope (deferred)

- Full 148 component inventory
- Push notifications / service worker
- Content moderation queue
- Legal/compliance for subscription
- WebGL fallback for SVG renderer
- Competitive analysis doc

### What already exists

- PRD entities map directly to schema (no existing code, greenfield)
- Lucia v3, Drizzle, Fastify: established libraries with no existing usage to migrate

### Dream state delta

This plan moves from "no web implementation" to "playable cultivation loop with first Becoming." Gap from 12-month ideal: premium illustration, social economy, subscription, full component inventory. Plan covers ~40% of 12-month ideal scope in Phase 1.

### CEO Completion Summary

| Dimension | Status |
|---|---|
| Premise validity | ACCEPTED (4 premises confirmed, 2 amended) |
| Approach selection | B (React + Fastify) — add simulation tick job |
| Scope | SELECTIVE EXPANSION — 4 expansions accepted |
| Critical gaps closed | Simulation tick runtime, account recovery, analytics |
| Deferred items | 6 items to TODOS.md |
| Outside voice | Claude subagent — 4 critical findings, all addressed |
| Mode | SELECTIVE EXPANSION |

**CEO DUAL VOICES — CONSENSUS TABLE:**
```
═══════════════════════════════════════════════════════════════
  Dimension                           Claude  Codex  Consensus
  ──────────────────────────────────── ─────── ─────── ─────────
  1. Premises valid?                   YES     N/A    SINGLE
  2. Right problem to solve?           YES     N/A    SINGLE
  3. Scope calibration correct?        YES*    N/A    SINGLE
  4. Alternatives sufficiently explored? NO*   N/A    SINGLE
  5. Competitive/market risks covered? NO      N/A    SINGLE
  6. 6-month trajectory sound?         YES*    N/A    SINGLE
═══════════════════════════════════════════════════════════════
* = with accepted amendments (simulation tick, PWA, recovery)
Codex: unavailable (binary not found)
```

---

## PLAN UPDATES FROM CEO REVIEW

### Added: Simulation Tick Architecture

```
BullMQ Tick Worker (Railway, separate process)
  ├── StemTickJob: runs every 60s per active Stem
  │   ├── Read Hollow conditions from DB
  │   ├── Accumulate BiologicalPressure
  │   ├── Evaluate BecomingReadiness
  │   ├── Update SustainmentState
  │   └── Push WS event if state changed
  └── StemTickScheduler: creates/removes jobs on Stem lifecycle events
```

### Added: Simulation Tick Design Doc (pre-M1 requirement)

Before M1 cut, write `SIMULATION_TICK_SPEC.md` covering:
- Tick interval (default: 60s)
- Pressure accumulation formula (environmental history × conditions)
- Becoming readiness threshold (abstract score, hidden from player)
- Sustainment state transitions (Stable → Strained → Unstable → Decaying)
- WS event payload schema

### Added: Phase 1 scope additions

- PWA manifest + standalone mode (portrait on mobile browser)
- Account recovery (email verification)
- Basic analytics (Posthog JS SDK — client events only in Phase 1)
- WS reconnection with exponential backoff
- SVG fallback silhouette for unknown anatomy states

---

## Decision Audit Trail

| # | Phase | Decision | Classification | Principle | Rationale | Rejected |
|---|-------|----------|-----------|-----------|----------|---------|
| 1 | CEO | Mode: SELECTIVE EXPANSION | Mechanical | P2 | Greenfield feature → EXPANSION default; but user said web game from PRD → hold scope baseline | SCOPE EXPANSION |
| 2 | CEO | Add simulation tick BullMQ job | Mechanical | P5 | Tick runtime must be explicit; inline request-handler is wrong | Request-handler tick |
| 3 | CEO | Add PWA manifest | Taste→Accepted | P1 | Recovers portrait-first for mobile browser; ~30min CC | Skip |
| 4 | CEO | Add account recovery | Mechanical | P1 | Law 8 compliance for permanent assets | Session-only |
| 5 | CEO | Add basic analytics | Mechanical | P1 | Cannot measure retention KPI without events | No analytics |
| 6 | CEO | Keep React + Fastify stack | Mechanical | P3 | Speed for MVP; Cloudflare Workers deferred | Next.js monolith, Hono/CF |
| 7 | CEO | Defer full 148 components | Mechanical | P3 | Post-launch content; 30-base enough for meaningful variability initially | Full 148 at launch |

---

## DESIGN REVIEW — Phase 2

**Reviewer:** plan-design-review  
**Scope:** STEMS_WEB_GAME_PLAN.md — all UI-bearing features  
**Date:** 2026-06-10  
**Starting rating:** 3/10  
**Ending rating:** 8/10 (post-review plan updates applied below)  
**Visual reference:** HTML wireframes generated — see DESIGN_SKETCH section

### Step 0: Design Scope Assessment

**No DESIGN.md found.** All design decisions calibrated against PRD §11 (Visual Bible) + universal design principles. Recommend running `/design-consultation` after M1 to formalize DESIGN.md before Phase 2 UI work.

**Designer binary:** present but OpenAI API key not configured. HTML wireframes used as DESIGN_SKETCH. Run `$D setup` to enable AI mockups.

**UI scope:** all Phase 1–3 features involve UI. No backend-only exclusions apply.

**Outside voice:** Claude subagent (independent design completeness review) confirmed 23 findings (5 🟡, 2 🔵, 16 ❓). All findings incorporated below.

---

### Design Token System (REQUIRED — no implementation before these are committed)

#### Color Palette

```css
:root {
  /* Backgrounds */
  --color-void:         #0F0C09;  /* page background, deepest dark */
  --color-hollow-bg:    #1A1510;  /* hollow/game column background */
  --color-card-bg:      #211C14;  /* card surface */
  --color-border:       #2A2218;  /* default border */
  --color-border-glow:  #C4874A44; /* occupied hollow amber glow border */

  /* Text */
  --color-text-primary:   #D4C5AE;  /* primary text, organism labels */
  --color-text-secondary: #9A8B7A;  /* secondary text, descriptions */
  --color-text-muted:     #7A8B7F;  /* biome names, small-caps states */
  --color-text-ghost:     #4A4038;  /* hollow numbers, decorative labels */

  /* Accent */
  --color-amber:        #C4874A;  /* active states, STABILIZE, CTAs */
  --color-amber-dim:    #C4874A22; /* amber glow fill */
  --color-mineral:      #7A8B7F;  /* SUPPRESS, neutral states */
  --color-bone:         #D4C5AE;  /* organism tissue base color */

  /* State indicators */
  --color-stable:       #7A9B7A;
  --color-stable-bg:    #1F2E24;
  --color-strained:     #C4874A;
  --color-strained-bg:  #2E2418;
  --color-unstable:     #9A7A4A;
  --color-decaying:     #7A6040;
}
```

#### Typography

```
Display/headings:  Cormorant Garamond (serif, editorial warmth) — weights 400, 600
Body/labels:       Inter (sans, clinical precision) — weights 400, 500
Monospace/data:    Departure Mono or JetBrains Mono — weight 400

Scale (mobile):
  --text-xs:    9px  / 1.4  — small-caps state chips, hollow numbers
  --text-sm:   10px  / 1.4  — biome names, control labels, consent descriptors
  --text-base: 12px  / 1.5  — primary body, Hollow names
  --text-md:   14px  / 1.4  — Field Entry titles, modal headers
  --text-lg:   18px  / 1.3  — section headers

Tracking (letter-spacing):
  .small-caps: 0.12em  — state chips, badges, labels
  .body:       0
  .heading:    -0.02em — tight display headings
```

---

### Screen Layouts

#### S1. Hollow Dashboard (main view)

```
VIEWPORT: 1440px desktop
┌─────────────────────────────────────────────────────────────┐
│ LEFT FLANK (120px)  │   GAME COLUMN (480px)  │ RIGHT FLANK  │
│ #0F0C09 bg          │   #1A1510 bg            │ #0F0C09 bg   │
│                     │                         │              │
│ Field Entries list  │  [Stems wordmark]  [sub]│ Observation  │
│ (sorted by date)    │  ─────────────────────  │ Log          │
│ Hollow · Becoming   │  [H1 occupied card]  ◄──│ timestamped  │
│ Stage · Free/Premium│  [H2 strained card]     │ field notes  │
│                     │  [H3 empty + NewSeed]   │              │
│ Empty: "No entries  │  ─────────────────────  │ Empty: "No   │
│  yet. Becomings     │                         │ observations │
│  create records."   │                         │ yet."        │
└─────────────────────────────────────────────────────────────┘

VIEWPORT: ≤480px mobile (portrait)
┌──────────────────────┐
│ [Stems]    [sub chip]│
│ ─────────────────────│
│ [H1 occupied card]   │
│ [H2 strained card]   │
│ [H3 empty + NewSeed] │
│ ─────────────────────│
│ [↓ Field Entries (3)]│ ← collapsed chip, taps to slide-up sheet
└──────────────────────┘
```

**Occupied Hollow card anatomy:**
- Left: 52×52px SVG organism (idle breathing animation, 4s loop)
- Middle: biome name (small-caps, --color-text-muted), organism name, stage + Becoming indicator dot
- Right: state chip (Stable/Strained/Unstable/Decaying/Recovery in respective colors)
- Bottom border: field entry count
- Border: `--color-border-glow` amber on occupied
- Inner glow: `box-shadow: inset 0 0 12px #C4874A22`

**Empty Hollow card anatomy:**
- Centered dashed circle icon (no organism)
- Label: "Hollow Unoccupied" in --color-text-ghost
- CTA: "+ New Seed" button in amber; taps to biome selection flow
- No health state chip, no field entry count

#### S2. Active Hollow View (drill-down from card tap)

```
PORTRAIT (480px max)
┌────────────────────────────┐
│ [← Back]  ADOLESCENT · B03 │  Stable ●
│                            │
│  ┌──────────────────────┐  │  ← Hollow environment area (55vh)
│  │  [floating: "warmth- │  │    background #211C14
│  │   seeking posture"]  │  │    organism centered
│  │        [SVG]         │  │    biofeedback floats fade in/out 4s
│  │  [floating: "digit   │  │    max 2 floats visible simultaneously
│  │   extension noted"]  │  │
│  │           [▲ Log]    │  │  ← tap to expand observation log
│  └──────────────────────┘  │
│  ─────────────────────────  │
│  WARMTH                     │  ← controls area (45vh)
│  [Cool][C-M][Mod★][M-W][Warm]│
│  MOISTURE                   │
│  [Arid][A-M★][Mod][M-H][Hi] │
│  LIGHT                      │
│  [Dark][D-L][Low][L-B★][Brt]│
│  MINERAL DENSITY            │
│  [Low][L-M★][Mod][M-H][High]│
└────────────────────────────┘

★ = currently active band (amber highlight)
```

**5-band control behavior:**
- Tap to set: immediate optimistic update, server confirmation within 2s
- Active band: `background: #C4874A22; border-color: #C4874A; color: #C4874A`
- Inactive band: `background: #211C14; border-color: #2A2218; color: #4A4038`
- On server confirmation: no visual change (optimistic already matches)
- On server rejection: band snaps back to previous with brief shake animation
- Offline: all bands show opacity 0.4, pointer-events: none, banner: "Offline — controls unavailable"
- Touch target: each band is full height of control row (minimum 44px)

**Observation log (expanded):**
- Slide-up bottom sheet, 50vh height
- Scrollable list of timestamped field notes
- Most recent first
- Format: `HH:MM — [cue text]` in --color-text-muted, italic

#### S3. Becoming Consent (full-screen takeover)

```
┌────────────────────────────┐
│ BECOMING 03 — READINESS    │  ← small-caps badge, amber
│ Secondary adaptation       │  ← brief clinical title
│ pressure reaching threshold│
│ ──────────────────────────  │
│  [trembling organism SVG]  │  ← centered, slight motion blur or
│                            │    subtle CSS animation (scale oscillation
│  lateral tension increasing│    ±1px, 0.8s loop irregular timing)
│  pressure index: high      │  ← floating observation text, amber dimmed
│ ──────────────────────────  │
│ [italic observation copy]  │  ← clinical description, 2-3 sentences
│ ──────────────────────────  │
│ ┌────────────────────────┐ │
│ │ STABILIZE [+]    amber │ │  ← amber border/tint
│ │ Maintain supportive    │ │
│ │ conditions. Sustained  │ │
│ │ effort required.       │ │
│ │ Requires online session│ │  ← constraint note in ghost text
│ └────────────────────────┘ │
│ ┌────────────────────────┐ │
│ │ SUPPRESS [−]  mineral  │ │  ← mineral border/tint
│ │ Apply opposing. One    │ │
│ │ attempt, uninterrupted.│ │
│ │ Single attempt only    │ │
│ └────────────────────────┘ │
│ ┌────────────────────────┐ │
│ │ LET CONTINUE [±]       │ │  ← neutral border
│ │ Natural resolution from│ │
│ │ current history.       │ │
│ │ Cannot be undone       │ │
│ └────────────────────────┘ │
└────────────────────────────┘
```

**Consent card interaction:**
1. Tap card → secondary confirmation modal (see S3b below)
2. NO accidental dismissal (no tap-outside-to-close)
3. Each card: `min-height: 80px`, `touch-target: full card area`
4. After confirmation: consent card shows "Committed" label + spinner overlay
5. On resolution complete: dismiss to Hollow view with Field Entry notification

**S3b. Becoming confirmation (second gate):**
- Small centered modal overlay on top of consent screen
- `"You chose: [CHOICE]"` + 1-sentence consequence reminder
- Two buttons: `"Confirm [CHOICE]"` and `"Back"`
- Required for ALL three choices (Stabilize, Suppress, Let Continue)
- Per PRD Law 9 (irreversible action clarity)

#### S4. Empty States

| State | Warmth | Primary Action | Context |
|---|---|---|---|
| Empty Hollow | Dashed circle icon, --color-text-ghost | "+ New Seed" amber CTA | "Start a new research subject" |
| No Field Entries (flank) | "No entries yet." --color-text-ghost | None | "Becomings create field records." |
| Offline Hollow view | Organism renders (cached), controls greyed | None | Banner: "Offline — changes require connection" |
| WS disconnected | Controls remain active, biofeedback pauses | Automatic reconnect (no user action) | Small corner chip: "Reconnecting…" pulsing |
| Becoming resolution in-progress | Organism shows "committing" animation (slow pulse) | None | Overlay: "Resolving…" prevents interaction |
| SVG render fallback | Silhouette only (--color-bone outline, #D4C5AE50 fill) | None | No text indicator — silhouette IS the fallback |
| Field Entry (free, no illustration) | Hollow Field Sketch SVG | "Illustrate" (premium prompt, greyed if no entitlement) | Free presentation label: "Field Sketch" |

#### S5. Auth Screens

**Register:**
- Single column, same --color-hollow-bg background
- Fields: email, password (visible/hidden toggle), "Start Research" CTA
- No social login
- Below form: link to login
- Validation: inline, below each field, --color-strained text

**Login:**
- Same layout, "Return to Hollow" CTA
- Link: "Forgot account?" → account recovery flow

**Account Recovery:**
- Email input → "Send recovery link"
- Then: "Check your email" confirmation state
- Recovery link → new password form

---

### Interaction State Coverage (Pass 2)

| Feature | Loading | Empty | Error | Success | Partial/Offline |
|---|---|---|---|---|---|
| Hollow dashboard | 3 skeleton cards, amber pulsing | Empty H card + New Seed CTA | Toast: "Failed to load — tap to retry" | Cards render immediately | Cached organism visible, controls grey |
| Hollow condition change | Band optimistic (instant), 200ms server confirm | N/A | Band snaps back + brief shake animation | No change (optimistic already applied) | Controls disabled, offline banner |
| Becoming trigger | Biofeedback escalating signals over time | N/A | N/A | Consent screen appears | N/A |
| Becoming consent | N/A | N/A | "Consent failed — try again" + back option | Dismiss to Hollow + Field Entry chip | If WS drops mid-consent: show "Connection lost" |
| Becoming resolution | "Resolving…" overlay on consent screen | N/A | Rollback + "Resolution failed — anatomy unchanged" | Field Entry created notification | Cannot proceed offline |
| Field Entry viewer | Skeleton card list | "No field entries yet. Becomings create records." | Toast: "Failed to load entries" | Cards render | Cached metadata only |
| New Seed flow | N/A — instantaneous | N/A | "Seed creation failed — Hollow may already be occupied" | Stemling appears in Hollow | Cannot proceed offline |
| WS connection | "Connecting…" chip (first connect only) | N/A | Corner chip: "Reconnecting…" (pulsing) | Chip disappears | Biofeedback paused, controls remain |
| SVG Stem render | Skeleton placeholder (60×60 rounded rect pulsing) | N/A | Silhouette fallback | Organism renders with idle animation | Cached anatomy renders |
| Auth (login) | Button spinner "Signing in…" | N/A | Inline field error (invalid email/password) | Redirect to dashboard | N/A |
| Release | Double-confirm modal | N/A | "Release failed — Stem still in Hollow" | Hollow empties, Field Entries remain | Cannot proceed offline |

---

### User Journey Storyboard (Pass 3)

| Step | User Does | User Feels | UX Support |
|---|---|---|---|
| 1. First open | Lands on register screen | Curious, uncertain | Wordmark + single line of product language ("Maintain a living research subject.") |
| 2. Register | Creates account | Neutral, task-mode | Minimal form, no social, no tracking consent popups before they care |
| 3. Hollow setup | Sees 3 empty Hollows | Orientation, slight anticipation | Empty Hollow card invites with "+ New Seed" — doesn't demand biome knowledge yet |
| 4. New Seed (biome select) | Chooses biome from 7 families | Discovery, naming-curiosity | Biome names are evocative, not mechanical ("Temperate Fen" not "Biome_07") |
| 5. Stemling spawns | Organism appears | Attachment begins | Fixed spawn is consistent and recognizable — "a small thing" not a randomized blob |
| 6. Tutorial | Walks through first observation | Guided, slight handholding | Tutorial overlays existing UI (not separate screen), skippable after first run |
| 7. First observation | Reads biofeedback text | Curiosity + care | Floating text is specific and clinical ("warmth-seeking posture") not vague ("needs attention") |
| 8. First control adjustment | Changes Warmth band | Agency, consequence anticipation | Server confirms, organism responds visually within 2-3s |
| 9. Return loop | Returns after hours/days | Mild anxiety + care | Biofeedback shows change over time — player sees organism has been responding to conditions |
| 10. Becoming readiness | Escalating signals | Rising excitement + gravity | Signals escalate across multiple sessions — not sudden; player feels they "noticed" it |
| 11. Becoming consent | Reads consent screen | Weight, gravity, slight anxiety | Full-screen takeover + organism visible = correct emotional register |
| 12. First Becoming | Anatomy changes | Wonder + attachment | Visual change is specific, not random-feeling — player connects environment → anatomy |
| 13. First Field Entry | Sees field entry created | Pride + archive satisfaction | "This body remembers what happened" moment |

**5-second visceral (first impression):** Dark, intimate, one small organism. Not a dashboard. One thing to care about.  
**5-minute behavioral (first session):** Organism responds to conditions. Biofeedback is readable. Player adjusts and returns.  
**5-year reflective (long-term):** "I've had this thing for 6 months. It remembers everything."

---

### Design System Alignment (Pass 5)

No DESIGN.md exists. **Required before Phase 2 UI work begins.** Temporary alignment via Visual Bible constraints:

- Typography: Cormorant Garamond (display) + Inter (body) — see token system above
- Color: token system above is authoritative
- Component vocabulary: see screen layouts above
- No rarity frames, no health bars, no XP indicators — all enforced by Visual Bible
- Clinical language + warm tactile presentation — enforce in all copy review

**Recommend:** run `/design-consultation` immediately after M1 to produce DESIGN.md.

---

### Responsive + Accessibility (Pass 6)

#### Responsive breakpoints

| Viewport | Layout |
|---|---|
| ≤480px | Single-column, full-width game. Field Entries collapsed to chip → slide-up sheet. |
| 481px–768px (tablet portrait) | Same as mobile with side padding 24px. Game column centered. |
| 769px–1024px | Flanks appear (120px each). Left: Field Entry list. Right: Observation log. |
| ≥1025px (desktop) | Full flank treatment. Game column fixed 480px centered. Flanks expand proportionally. |

#### Accessibility requirements

- **Touch targets:** 44px minimum height on all interactive elements (band buttons, consent cards, Hollow cards). Current 5-band button design: each band 44px height required.
- **Keyboard navigation:** Tab order follows visual flow. Band controls: Tab to focus control row, arrow keys to change band. Consent cards: Tab-navigable, Enter to select. Hollow cards: Enter or Space to drill down.
- **Screen reader:** All SVG organisms must have `role="img"` with `aria-label` describing the organism state (e.g., `"Adolescent Stem in Temperate Fen, Stable condition"`). Anatomy details NOT exposed to screen reader (hidden biological values rule still applies).
- **Color contrast:** All text must meet WCAG 2.1 AA (4.5:1 for body text, 3:1 for large text). `--color-text-muted` (#7A8B7F) on `--color-card-bg` (#211C14) = 4.6:1 ✓. `--color-text-ghost` (#4A4038) on `--color-hollow-bg` (#1A1510) needs verification — may fall below 3:1 for decorative labels (acceptable if decorative only).
- **Biofeedback text:** floating text must also be available in observation log (keyboard accessible, not animation-only). This satisfies PRD Law 12 (multimodal).
- **Consent confirmation:** All three Becoming consent choices must be keyboard-accessible with visible focus ring. Focus ring: `outline: 2px solid #C4874A; outline-offset: 2px`.
- **Motion:** CSS animations (organism breathing, biofeedback fades) must respect `prefers-reduced-motion`. On reduced-motion: animations disabled, organism renders static, biofeedback text appears/disappears without transitions.

---

### Design Decisions Made (D1–D4)

| # | Decision | Choice | Rationale |
|---|---|---|---|
| D1 | Desktop layout | Centered 480px column + dark flanks | Preserves portrait-first intent; flanks used for Field Entry list (left) and Observation Log (right) |
| D2 | Becoming consent | Full-screen takeover modal with organism visible | Correct emotional register for irreversible choice; organism visible throughout |
| D3 | Hollow controls | 5-band discrete buttons per control | Clinical + deliberate; easy to read current state at a glance; PRD-aligned (5 bands) |
| D4 | Biofeedback text | Floating near organism (fading) + expandable observation log | Immersive primary view + journaling utility via expandable log chip |

---

### AI Slop Risk Assessment (Pass 4)

**Classifier:** APP UI with intimate product character.

**Litmus scorecard:**

```
DESIGN LITMUS — STEMS WEB GAME:
═══════════════════════════════════════════════════════════════
  Check                                   Plan+Review  Notes
  ─────────────────────────────────────── ──────────── ──────────
  1. Brand unmistakable in first screen?  SPEC'D        Wordmark top, deep dark BG distinct
  2. One strong visual anchor?            SPEC'D        Single organism per Hollow
  3. Scannable by headlines only?         SPEC'D        Biome/Stage/State at a glance
  4. Each section has one job?            SPEC'D        Controls area, Stem area separated
  5. Cards actually necessary?            YES           Each Hollow IS the interaction unit
  6. Motion improves hierarchy?           SPEC'D        Breathing animation signals life, not deco
  7. Premium without decorative shadows?  YES           Amber glow is state-semantic, not deco
  ─────────────────────────────────────── ──────────── ──────────
  Hard rejections triggered:              NONE
═══════════════════════════════════════════════════════════════
```

**AI slop risks to enforce in implementation:**
- Do NOT use `system-ui` or `-apple-system` as primary font — enforce Cormorant + Inter
- Do NOT use uniform bubbly border-radius on everything — organism cards: 6px, band buttons: 2px, chips: 3px
- Do NOT add decorative blobs or gradients to flanks — void dark (#0F0C09), no decoration
- Biofeedback text is NOT a tooltip — it's a floating field note; style accordingly

---

### Pass 7: Unresolved Design Decisions

All D1-D4 decisions resolved above. Remaining implementation questions:

| Decision Needed | If Deferred | Recommendation |
|---|---|---|
| Organism idle animation spec | Implementer ships static SVG | Define: 4s sine-wave scale (0.98→1.02), 2s lateral sway (±1px), irregular timing to avoid mechanical feel |
| Tutorial overlay interaction | Generic lightbox with hotspots | Use inline annotation chips attached to UI elements (arrow + label). Not a separate screen. |
| Account recovery email template | Plain text email | Warm-clinical tone: "Your research continues…" opening line. Not generic "Password reset" subject. |
| Strained Hollow card indicator | Only state chip | Add: amber border-glow increases intensity at Strained (stronger than Stable amber glow) |
| "Stems" wordmark typography | Defaults to body font | Use Cormorant Garamond 600, letter-spacing 0.2em. One word, centered or left-aligned. |
| Becoming readiness escalation signals | Only biofeedback text changes | Add: organism posture shift (slight lean), breathing rate increase, border-glow pulse on Hollow card |

---

---

## ENG REVIEW — Phase 3

**Reviewer:** plan-eng-review  
**Scope:** STEMS_WEB_GAME_PLAN.md — full stack architecture + data model  
**Date:** 2026-06-11  
**Outside voice:** Claude subagent (independent architecture review)  
**Outside voice findings:** 5 critical (🔴), all resolved via E-gates below

---

### Step 0: Scope Assessment

Phase 1 alone touches 15+ files across monorepo root, apps/web, apps/api, packages/shared. This is a greenfield build — 15+ file scope is unavoidable and justified. Proceeding.

---

### E-Gate Decisions (E1–E5 + E6–E9)

| # | Gate | Decision | Rationale |
|---|------|----------|-----------|
| E1 | Auth library | **arctic + oslo** (replaces Lucia v3) | Lucia v3 is sunset by its author; arctic + oslo is the author's active recommendation for session-based auth |
| E2 | WS connection registry | **In-process `Map<userId, WebSocket>` on each Fastify instance** | Simplest viable; sticky sessions for multi-instance post-MVP; no Redis pub-sub overhead at MVP scale |
| E3 | Shared schemas | **Monorepo with `packages/shared`** (npm workspaces + Turborepo) | Zod schemas, TypeScript types, and content JSON shared between apps/web and apps/api without duplication |
| E4 | Content config seeding | **JSON files in `packages/shared/data/`**, seeded via Drizzle migration | Versioned content config; every Field Entry records content version for auditability (PRD §19) |
| E5 | Test framework | **Vitest (unit + integration) + Playwright (E2E)** | Vitest is Vite-native; Playwright is the standard for browser E2E; no overlap |
| E6 | Becoming race condition | **Becoming.state machine** — tick only resolves `PENDING_RESOLUTION`; consent POST advances `PENDING_CONSENT → PENDING_RESOLUTION` | No separate flag needed; state IS the lock; atomic DB update prevents double-resolution |
| E7 | Consent idempotency | **Client sends `Idempotency-Key: <uuid>` header** on POST /becomings/:id/consent | UUID generated when consent screen opens; Redis cache (24h TTL) returns first response on retry |
| E8 | Optimistic concurrency (CAS) | **`version INT` column + `WHERE id=? AND version=?`** on Stem, FieldEntry, Hollow | `rowsAffected=0` → `OptimisticLockError`; retry up to 3x with exponential backoff; Drizzle-native |
| E9 | Deployment config | **Add to M1 gate:** `.env.example`, `railway.json`, Neon connection pool sizing, migration runbook in CONTRIBUTING.md | Required for any contributor to run the stack; blocking M1 |

---

### Updated Tech Stack

**Auth change (E1):**
```
BEFORE: Lucia v3 (sunset)
AFTER:  arctic + oslo
  - arctic: OAuth/OIDC providers + session token generation  
  - oslo: cryptographic utilities (HMAC, timing-safe compare, random)
  - Session table: sessions(id, user_id, expires_at) — same schema pattern as Lucia
```

**Monorepo structure (E3):**
```
stems/
├── apps/
│   ├── web/            Vite 6 + React 19 + TypeScript
│   └── api/            Fastify 5 + Node.js 22 LTS
├── packages/
│   └── shared/         
│       ├── src/
│       │   ├── schemas/    Zod schemas (shared client+server validation)
│       │   └── types/      TypeScript interfaces derived from Drizzle schema
│       └── data/           Versioned content JSON
│           ├── components.v1.json    Component definitions (148 total, 48 MVP)
│           ├── biomes.v1.json        Biome families + sub-biomes
│           ├── sustainment.v1.json   Sustainment archetypes
│           └── poses.v1.json         Pose families for illustration
├── turbo.json
└── package.json        npm workspaces root
```

**Content seeding (E4):**
```typescript
// packages/shared/data/components.v1.json — example structure
{
  "version": "1",
  "components": [
    {
      "id": "EXT_DIGIT_ELONGATION",
      "region": "extremity",
      "operation": "elongate",
      "biome_affinity": ["temperate_fen", "boreal_mire"],
      "sustainment_demand": { "moisture": [2,4], "warmth": [1,3] },
      "biofeedback_cues": ["digit extension noted", "reach behavior increased"],
      "visual_descriptor": "terminal digit segments extend beyond standard proportion"
    }
  ]
}

// apps/api/src/db/seed/content.ts
import componentsV1 from '@stems/shared/data/components.v1.json'
// Drizzle migration inserts rows; content_version column records "1"
```

---

### Becoming State Machine (E6 — critical bug fix)

```
Becoming lifecycle states:
  DETECTED        → readiness threshold crossed; tick creates Becoming record
  PENDING_CONSENT → consent screen opened by client; tick SKIPS resolution
  PENDING_RESOLUTION → player submitted consent; tick resolves on next pass
  RESOLVED        → anatomy updated, Field Entry created
  SUPPRESSED      → Suppress choice + conditions maintained
  REDIRECTED      → Suppress attempt broken (Mutation Debt accrued)

Tick behavior:
  IF becoming.state = DETECTED:       advance to PENDING_CONSENT when client opens screen
  IF becoming.state = PENDING_CONSENT: SKIP — player is reading
  IF becoming.state = PENDING_RESOLUTION: resolve this tick
  IF becoming.state = RESOLVED|SUPPRESSED|REDIRECTED: skip

Client behavior:
  Opening consent screen: POST /becomings/:id/open → sets state=PENDING_CONSENT (atomic)
  Submitting consent: POST /becomings/:id/consent + Idempotency-Key header
    → sets state=PENDING_RESOLUTION + consent_choice
  Server resolution job (next tick or immediate): sets state=RESOLVED, updates anatomy

Race protection:
  /open endpoint: DB UPDATE WHERE state='DETECTED' AND id=:id
  If rowsAffected=0: another process beat us → 409 Conflict → client shows "Becoming already resolved"
```

---

### Optimistic Concurrency Pattern (E8)

```typescript
// Schema addition: version column on mutable entities
stems:         version: integer().default(0).notNull()
hollows:       version: integer().default(0).notNull()
field_entries: version: integer().default(0).notNull()
becomings:     version: integer().default(0).notNull()

// CAS update pattern
async function updateStemState(stemId: string, expectedVersion: number, patch: Partial<Stem>) {
  const result = await db
    .update(stems)
    .set({ ...patch, version: sql`version + 1`, updatedAt: new Date() })
    .where(and(eq(stems.id, stemId), eq(stems.version, expectedVersion)))

  if (result.rowsAffected === 0) {
    throw new OptimisticLockError(`Stem ${stemId} modified by concurrent writer`)
  }
}

// Retry wrapper (tick + consent resolution use this)
async function withOptimisticRetry<T>(fn: () => Promise<T>, maxRetries = 3): Promise<T> {
  for (let i = 0; i < maxRetries; i++) {
    try { return await fn() }
    catch (e) {
      if (!(e instanceof OptimisticLockError) || i === maxRetries - 1) throw e
      await sleep(50 * 2 ** i) // 50ms, 100ms, 200ms
    }
  }
  throw new Error('unreachable')
}
```

---

### Architecture Diagram (Updated)

```
Browser Client (Vite + React 19)
  ├── Hollow UI (SVG organism + 5-band controls)
  ├── Becoming Consent (full-screen takeover)
  ├── Field Entry viewer
  ├── Biofeedback overlay (floating text + log chip)
  ├── WS connection → real-time state push
  └── TanStack Query (server state) + Zustand (UI state)
         │ HTTPS + WSS
         ▼
Fastify 5 API Server (Railway)
  ├── /auth            session create/destroy (arctic + oslo)
  ├── /hollows         CRUD, condition changes → CAS write
  ├── /stems           read stem state
  ├── /becomings       open/consent/status (idempotency key)
  ├── /field-entries   list, view
  ├── WS /live         push biofeedback + state events
  └── WS registry: Map<userId, WebSocket> (in-process)
         │
         ├── PostgreSQL 16 (Neon serverless)
         │   ├── accounts, sessions (arctic session table)
         │   ├── hollows (version col), stems (version col)
         │   ├── anatomy_component_instances
         │   ├── becomings (state machine col)
         │   ├── field_entries (version col)
         │   └── content_config (versioned, from packages/shared/data/)
         │
         └── Redis (BullMQ)
             ├── StemTickQueue: 60s per active Stem
             │   ├── accumulate BiologicalPressure
             │   ├── evaluate BecomingReadiness → DETECTED
             │   ├── update SustainmentState
             │   ├── resolve PENDING_RESOLUTION Becomings
             │   └── push WS event via registry if state changed
             └── idempotency cache: Idempotency-Key → response (24h TTL)

packages/shared (npm workspace)
  ├── src/schemas/    Zod validation (shared client+server)
  ├── src/types/      TypeScript types from Drizzle schema
  └── data/           Versioned content JSON (seeded at migration)
```

---

### Security Model (Updated per PRD §19)

| Requirement | Implementation |
|---|---|
| Owner-only mutation | Fastify preHandler: session.userId === resource.accountId |
| Server-authority on allowance | Never trust client balance; read from DB only |
| Signed URLs for premium assets | Cloudflare R2 presigned URLs, 1h expiry |
| Idempotency for irreversible actions | Idempotency-Key header + Redis cache (consent, synthesis, trade, gift, release) |
| Audit log | Structured log: txnId, accountIdHash, entityIds, contentVersions, before/after state |
| No offline mutation | Server rejects any write without active session; no local queue |

---

### Test Coverage Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│  UNIT (Vitest) — simulation engine in isolation                  │
│                                                                   │
│  BiologicalPressureAccumulator                                   │
│    ✓ pressure increases when conditions favor Becoming           │
│    ✓ pressure stable when conditions in range                    │
│    ✓ pressure bounded (no overflow, no negative)                 │
│                                                                   │
│  BecomingReadinessEvaluator                                      │
│    ✓ DETECTED fires at threshold (fixture from PRD §27)          │
│    ✓ does NOT fire below threshold                               │
│    ✓ Becoming count increments correctly                         │
│                                                                   │
│  ComponentSelector                                               │
│    ✓ selected component within biome affinity                    │
│    ✓ prerequisites satisfied before selection                    │
│    ✓ respects existing anatomy (no duplicate regions)            │
│                                                                   │
│  AnatomyValidator                                                │
│    ✓ rejects non-human-derived components (Law 3)                │
│    ✓ validates region → operation compatibility                  │
│    ✓ residual anatomy preserved (Law 15)                        │
│                                                                   │
│  SustainmentEvaluator                                            │
│    ✓ Stable → Strained → Unstable → Decaying transitions        │
│    ✓ recovery path from Decaying (not permanent death)           │
│                                                                   │
│  CAS / OptimisticLock                                            │
│    ✓ version mismatch throws OptimisticLockError                 │
│    ✓ retry wrapper retries up to 3x then rethrows               │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  INTEGRATION (Vitest + real Neon test DB)                        │
│                                                                   │
│  Becoming resolution — full atomic path:                         │
│    ✓ DETECTED → /becomings/:id/open → PENDING_CONSENT           │
│    ✓ tick skips PENDING_CONSENT Becoming                         │
│    ✓ /becomings/:id/consent (Stabilize) → PENDING_RESOLUTION    │
│    ✓ tick resolves PENDING_RESOLUTION → RESOLVED                 │
│    ✓ anatomy_component_instances row created                     │
│    ✓ field_entry row created atomically                          │
│    ✓ idempotent: duplicate Idempotency-Key returns cached 200   │
│    ✓ race: concurrent /open attempts → second returns 409       │
│                                                                   │
│  Hollow condition change:                                         │
│    ✓ warmth change persisted, version incremented               │
│    ✓ CAS: stale version returns 409                              │
│    ✓ offline detection: session check fails without network      │
│                                                                   │
│  Account + session (arctic + oslo):                              │
│    ✓ register creates account + session cookie                   │
│    ✓ login returns valid session                                 │
│    ✓ session expiry returns 401                                  │
│    ✓ recovery token flow end-to-end                             │
│                                                                   │
│  Entitlement (stubbed Phase 1):                                  │
│    ✓ free account: illustration endpoint returns 402             │
│    ✓ synthesis endpoint returns 402 without entitlement          │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  E2E (Playwright — full browser)                                 │
│                                                                   │
│  Flow 1: First launch (PRD §17 Flow 1)                           │
│    ✓ register → Hollow setup → biome selection → New Seed        │
│    ✓ Stemling renders (fixed spawn plan, no random blob)         │
│    ✓ tutorial overlay appears, skippable                         │
│    ✓ first observation readable                                  │
│    ✓ first control adjustment → server confirms → organism reacts│
│                                                                   │
│  Flow 3/4/5/6: Becoming consent (all 3 paths)                   │
│    ✓ Becoming readiness signals escalate (seeded fixture)        │
│    ✓ full-screen takeover appears                                │
│    ✓ Stabilize: second-gate confirm → resolution → Field Entry  │
│    ✓ Suppress: second-gate confirm → resolution → Field Entry   │
│    ✓ Let Continue: second-gate confirm → resolution → Field Entry│
│    ✓ back-out before second-gate: consent screen still open     │
│    ✓ WS drop during consent → reconnect → resume (not duplicate)│
│                                                                   │
│  Flow 2: Routine care (PRD §17 Flow 2)                          │
│    ✓ open Hollow → view state → adjust control → state improves │
│    ✓ offline simulation: controls disabled, cached view works   │
└─────────────────────────────────────────────────────────────────┘
```

**Coverage targets (Phase 1 launch gate):**
- Unit: 90% line coverage on simulation engine
- Integration: 100% of PRD launch-blocking paths (§01 integrity requirements)
- E2E: Flow 1, Flow 2, all 3 Becoming consent paths

---

### Implementation Task List

#### M1: Skeleton (Week 1)

| Task | File(s) | Notes |
|------|---------|-------|
| Monorepo scaffold | `turbo.json`, `package.json`, workspace config | npm workspaces + Turborepo |
| Shared package | `packages/shared/src/`, `packages/shared/data/*.v1.json` | Zod schemas + types + content JSON |
| Drizzle schema | `apps/api/src/db/schema.ts` | All PRD §19 entities + version cols + Becoming.state |
| Drizzle migrations | `apps/api/drizzle/` | Initial schema + content seed migration |
| Fastify server | `apps/api/src/server.ts` | Plugin registration, CORS, WS |
| Auth routes | `apps/api/src/routes/auth.ts` | arctic + oslo session-based auth |
| Account entity | `apps/api/src/db/schema.ts` | + recovery_email, recovery_token, recovery_token_expires_at |
| Hollow routes | `apps/api/src/routes/hollows.ts` | CRUD + condition change (CAS) |
| WS registry | `apps/api/src/ws/registry.ts` | `Map<userId, WebSocket>` |
| WS route | `apps/api/src/routes/live.ts` | Fastify WS plugin, auth guard |
| New Seed route | `apps/api/src/routes/seeds.ts` | Create random Biological Signature + spawn Stemling |
| BullMQ tick worker | `apps/api/src/workers/stem-tick.ts` | 60s per active Stem |
| Vite + React scaffold | `apps/web/` | Vite 6, React 19, TypeScript, Tailwind v4 |
| Design tokens | `apps/web/src/styles/tokens.css` | Full color + typography tokens from Design Review |
| Google Fonts load | `apps/web/index.html` | Cormorant Garamond + Inter |
| Dashboard route | `apps/web/src/pages/Dashboard.tsx` | 3 Hollow cards |
| Auth pages | `apps/web/src/pages/Auth.tsx` | Register + Login + Recovery |
| SVG Stemling | `apps/web/src/components/StemSVG.tsx` | Fixed spawn plan, idle breathing animation |
| Deployment artifacts | `.env.example`, `railway.json`, `CONTRIBUTING.md` | M1 gate blocker |
| PWA manifest | `apps/web/public/manifest.json` | Portrait standalone mode |

#### M2: Living Loop (Week 3)

| Task | File(s) | Notes |
|------|---------|-------|
| Simulation engine | `apps/api/src/simulation/` | PressureAccumulator, ReadinessEvaluator |
| Sustainment evaluator | `apps/api/src/simulation/sustainment.ts` | 4-state transitions |
| WS event push | `apps/api/src/ws/push.ts` | Push to registry on state change |
| Biofeedback overlay | `apps/web/src/components/BiofeedbackFloat.tsx` | Floating text, 4s fade, max 2 simultaneous |
| Observation log | `apps/web/src/components/ObservationLog.tsx` | Slide-up sheet, timestamped entries |
| Control UI | `apps/web/src/components/HollowControls.tsx` | 5-band buttons, optimistic update, shake on reject |
| TanStack Query setup | `apps/web/src/lib/query.ts` | WS invalidation on push event |
| Hollow detail view | `apps/web/src/pages/HollowDetail.tsx` | SVG area + controls area |

#### M3: First Becoming (Week 5)

| Task | File(s) | Notes |
|------|---------|-------|
| Becoming routes | `apps/api/src/routes/becomings.ts` | /open, /consent (idempotency key) |
| Component selector | `apps/api/src/simulation/components.ts` | From content JSON, biome affinity |
| Anatomy validator | `apps/api/src/simulation/anatomy.ts` | PRD Laws 1-5, 15 |
| Becoming resolution | `apps/api/src/simulation/resolution.ts` | Atomic: anatomy update + Field Entry creation |
| SVG mutation layers | `apps/web/src/components/StemSVG.tsx` | Additive layers per AnatomyComponentInstance |
| Becoming consent UI | `apps/web/src/pages/BecomingConsent.tsx` | Full-screen takeover, 3 cards, second gate |
| Field Entry routes | `apps/api/src/routes/field-entries.ts` | List + view |
| Field Entry viewer | `apps/web/src/components/FieldEntryCard.tsx` | Free presentation (SVG sketch) |
| Unit tests | `apps/api/src/simulation/__tests__/` | Vitest: pressure, readiness, selector, validator |
| Integration tests | `apps/api/src/__tests__/becoming.test.ts` | Full atomic path |
| E2E tests | `apps/web/e2e/becoming.spec.ts` | Playwright: all 3 consent flows |

---

### Outside Voice Findings Summary

**Source:** Claude subagent (independent architecture review)

| Finding | Severity | Resolution |
|---------|----------|-----------|
| BullMQ tick can resolve Becoming mid-consent screen | 🔴 bug | E6: Becoming.state machine — tick skips PENDING_CONSENT |
| Consent POST has no idempotency key — retries double-resolve | 🔴 bug | E7: Client sends Idempotency-Key header; Redis cache 24h |
| Drizzle CAS not specified — no version column or retry loop | 🔴 missing | E8: version INT + WHERE version=? + 3x retry with backoff |
| Phase 1 timeline 30-50% optimistic (18 features, 7 weeks) | 🔴 risk | Acknowledged; CC reduces human effort; BullMQ + Drizzle are well-scaffolded; M4 scope trimmed |
| Deployment config completely missing | 🔴 missing | E9: .env.example + railway.json + runbook at M1 gate |

**All 5 critical findings resolved. No unresolved 🔴 issues.**

---

### Deployment Config (M1 Gate — E9)

`.env.example` (all vars documented):
```bash
# Database
DATABASE_URL=postgresql://user:pass@host/db?sslmode=require
# Redis
REDIS_URL=redis://user:pass@host:6379
# Auth (arctic + oslo)
SESSION_SECRET=<32-byte-hex-from-oslo-random>
# Email (account recovery)
SMTP_HOST=
SMTP_PORT=587
SMTP_USER=
SMTP_PASS=
# Frontend URL (for CORS + recovery email links)
FRONTEND_URL=http://localhost:5173
# Cloudflare R2 (Phase 3 — leave empty in Phase 1)
R2_ACCOUNT_ID=
R2_ACCESS_KEY_ID=
R2_SECRET_ACCESS_KEY=
R2_BUCKET=
# AI illustration (Phase 3 — leave empty in Phase 1)
REPLICATE_API_TOKEN=
# Analytics
POSTHOG_KEY=
```

`railway.json`:
```json
{
  "deploy": {
    "startCommand": "node dist/server.js",
    "healthcheckPath": "/health",
    "healthcheckTimeout": 30
  },
  "build": {
    "builder": "NIXPACKS"
  }
}
```

**Neon connection pool sizing:** Use `pool_size=10` in DATABASE_URL for Railway single-instance. Neon serverless driver handles connection pooling automatically — no PgBouncer needed at MVP scale.

**Migration runbook (CONTRIBUTING.md):**
1. `npm run db:generate` — generate migration files from schema changes
2. `npm run db:migrate` — apply migrations to target DB
3. `npm run db:seed` — seed content config from `packages/shared/data/*.json`
4. Always run seed after migrate (content_config table depends on migration running first)

---

### Pre-M1 Required Documents (carried from CEO review + eng review)

| Document | Owner | Purpose |
|----------|-------|---------|
| `SIMULATION_TICK_SPEC.md` | Eng | Tick interval, pressure formula, readiness threshold, WS payload schema |
| `RENDER_SPEC.md` | Eng | SVG anatomy graph structure, layer ordering, fallback silhouette, animation spec |

Both must exist before M1 implementation begins.

---

### Eng Review Completion Summary

| Dimension | Status |
|---|---|
| Outside voice | 5 🔴 findings — all resolved (E6–E9) |
| Auth stack | Updated: arctic + oslo (Lucia v3 sunset) |
| Monorepo | Defined: npm workspaces + Turborepo + packages/shared |
| Content config | Defined: packages/shared/data/*.v1.json + Drizzle seed migration |
| Test framework | Vitest (unit+integration) + Playwright (E2E) |
| Becoming race | Fixed: state machine (PENDING_CONSENT blocks tick) |
| Consent idempotency | Fixed: Idempotency-Key header + Redis cache |
| CAS pattern | Defined: version INT + WHERE version=? + retry |
| Deployment config | Added to M1 gate: .env.example + railway.json + runbook |
| Test coverage | Diagrammed: unit/integration/E2E with explicit assertions |
| Implementation tasks | Listed by milestone (M1/M2/M3) |

**NO UNRESOLVED DECISIONS**

---

---

## DX REVIEW — Phase 3.5

**Reviewer:** plan-devex-review  
**Mode:** DX POLISH  
**Persona:** Solo full-stack dev, building with CC heavily  
**Date:** 2026-06-11  
**Starting scores:** Getting Started 1/10, Dev Environment 3/10, Error Messages 3/10  
**Outside voice:** Claude subagent — 4 🔴, 8 🟡/🔵 findings

---

### Developer Persona Card

```
TARGET DEVELOPER PERSONA
========================
Who:       Solo full-stack dev, building with CC as primary tool
Context:   Implementing complex 27-doc PRD spec; iterates via AI-assisted coding
Tolerance: Unlimited (own project)
Expects:   Clone → running game in <10 min, hot-reload, clear test output
```

---

### DX Decisions Made (DX1–DX8)

| # | Decision | Choice | Rationale |
|---|----------|--------|-----------|
| DX1 | Local dev environment | Docker Compose (postgres:16 + redis:7) | Clone → dev DB in 30s; no cloud account for local dev |
| DX2 | Turborepo task graph | Define now in plan | Prevents M1 confusion about script names + pipeline dependencies |
| DX3 | Integration test DB | Docker Compose Postgres on port 5433 (not Neon) | Full test suite runs offline; Neon = staging/prod only |
| DX4 | API error format | Structured `{ error: { type, code, message, suggestion? } }` + LOG_LEVEL=debug | Standard type/code fields, Stripe-pattern; stack traces on debug |
| DX5 | Worker hot-reload | `tsx --watch` for API process (includes BullMQ worker) | Same process = same hot-reload; no separate nodemon |
| DX6 | Content version upgrade | Append-only (v2 adds, never mutates v1 entries) | Matches PRD Law 8; old Field Entries remain auditable indefinitely |
| DX7 | WS session auth | Fastify preValidation hook on WS upgrade (reads session cookie) | Standard; Fastify WS plugin passes upgrade headers through |
| DX8 | BullMQ deduplication | JobId = stemId; `add only-if-missing`; concurrency=5 | No pile-up; slow Neon queries don't cause duplicate jobs |

---

### Local Dev Setup (Docker Compose)

`docker-compose.yml`:
```yaml
services:
  postgres:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: stems
      POSTGRES_PASSWORD: stems_dev
      POSTGRES_DB: stems_dev
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  postgres_test:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: stems
      POSTGRES_PASSWORD: stems_test
      POSTGRES_DB: stems_test
    ports:
      - "5433:5432"

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

`apps/api/.env.local` (local dev, not committed):
```bash
DATABASE_URL=postgresql://stems:stems_dev@localhost:5432/stems_dev
TEST_DATABASE_URL=postgresql://stems:stems_test@localhost:5433/stems_test
REDIS_URL=redis://localhost:6379
```

**Getting started (README.md — M1 gate):**
```bash
# 1. Clone and install (< 1 min)
git clone https://github.com/TheRealTwizzy/myStem.git && cd myStem
npm install

# 2. Start local services (< 30s)
docker compose up -d

# 3. Copy env and migrate (< 1 min)
cp apps/api/.env.example apps/api/.env.local
npm run db:migrate && npm run db:seed

# 4. Start dev server
npm run dev
# → web: http://localhost:5173
# → api: http://localhost:3000
```

TTHW after: ~5-7 min (Competitive tier target met).

---

### Turborepo Task Graph

`turbo.json`:
```json
{
  "$schema": "https://turbo.build/schema.json",
  "tasks": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**"]
    },
    "dev": {
      "dependsOn": ["^build"],
      "persistent": true,
      "cache": false
    },
    "test": {
      "dependsOn": ["^build"],
      "env": ["TEST_DATABASE_URL", "REDIS_URL"]
    },
    "test:e2e": {
      "dependsOn": ["build"],
      "env": ["DATABASE_URL", "REDIS_URL"]
    },
    "db:migrate": {
      "cache": false,
      "env": ["DATABASE_URL"]
    },
    "db:migrate:test": {
      "cache": false,
      "env": ["TEST_DATABASE_URL"]
    },
    "db:seed": {
      "dependsOn": ["db:migrate"],
      "cache": false
    },
    "lint": {
      "dependsOn": ["^build"]
    }
  }
}
```

**Root `package.json` scripts:**
```json
{
  "scripts": {
    "dev": "turbo run dev --parallel",
    "build": "turbo run build",
    "test": "turbo run test",
    "test:e2e": "turbo run test:e2e",
    "db:migrate": "turbo run db:migrate --filter=apps/api",
    "db:migrate:test": "turbo run db:migrate:test --filter=apps/api",
    "db:seed": "turbo run db:seed --filter=apps/api"
  }
}
```

**`tsx --watch` fix for cross-workspace hot-reload:**

Changes to `packages/shared` must trigger API restart. Add Turborepo watch pipeline:

```json
"dev": {
  "dependsOn": ["^build"],
  "persistent": true,
  "cache": false,
  "watch": {
    "patterns": ["packages/shared/src/**"]
  }
}
```

And in `apps/api/package.json`:
```json
{
  "scripts": {
    "dev": "tsx --watch src/server.ts",
    "build": "tsc -p tsconfig.json"
  }
}
```

---

### API Error Response Format (DX4)

All Fastify error responses use:
```typescript
// apps/api/src/lib/errors.ts
export interface ApiError {
  error: {
    type: string     // machine-readable category
    code: string     // specific error code
    message: string  // human-readable description
    suggestion?: string  // optional fix hint
    param?: string   // which input caused the error (optional)
  }
}

// HTTP status mapping
// 400 BAD_REQUEST     — validation failure, malformed input
// 401 UNAUTHORIZED    — session expired or missing
// 403 FORBIDDEN       — owner check failed
// 404 NOT_FOUND       — entity doesn't exist
// 409 CONFLICT        — CAS version mismatch (retry with fresh data)
// 410 GONE            — Becoming already resolved (idempotent OK)
// 422 UNPROCESSABLE   — business rule violation (e.g., Hollow occupied)
// 503 UNAVAILABLE     — offline / no server connection
```

**Three traced error paths:**

1. **CAS version mismatch** (Hollow condition change):
```json
HTTP 409
{ "error": { "type": "optimistic_lock", "code": "VERSION_MISMATCH",
  "message": "Hollow was modified by another request. Please reload and try again.",
  "suggestion": "Re-fetch the Hollow and resubmit your change." } }
```

2. **Becoming already resolved** (duplicate consent POST):
```json
HTTP 410
{ "error": { "type": "already_resolved", "code": "BECOMING_RESOLVED",
  "message": "This Becoming has already been resolved.",
  "suggestion": "Check the current Stem state for the updated anatomy." } }
```

3. **Session expired** (any protected route):
```json
HTTP 401
{ "error": { "type": "auth", "code": "SESSION_EXPIRED",
  "message": "Your session has expired. Please sign in again." } }
```

---

### WS Session Auth on Handshake (DX7)

```typescript
// apps/api/src/routes/live.ts
fastify.get('/live', {
  websocket: true,
  preValidation: async (request, reply) => {
    // Session cookie is present in upgrade request headers
    const sessionId = request.cookies['stems_session']
    if (!sessionId) return reply.code(401).send()
    
    const session = await db.query.sessions.findFirst({
      where: and(eq(sessions.id, sessionId), gt(sessions.expiresAt, new Date()))
    })
    if (!session) return reply.code(401).send()
    
    request.userId = session.userId
  }
}, async (connection, request) => {
  // Register in WS registry
  wsRegistry.set(request.userId, connection.socket)
  connection.socket.on('close', () => wsRegistry.delete(request.userId))
})
```

---

### BullMQ Job Deduplication (DX8)

```typescript
// apps/api/src/workers/stem-tick.ts
const stemTickQueue = new Queue('stem-tick', { connection: redis })

// Add job — deduplicates by stemId
async function scheduleStemTick(stemId: string) {
  await stemTickQueue.add(
    'tick',
    { stemId },
    {
      jobId: stemId,          // deduplication key
      repeat: { every: 60_000 },
      removeOnComplete: 100,
      removeOnFail: 50,
    }
  )
}

// Worker — concurrency 5 (Railway single instance)
const worker = new Worker('stem-tick', tickProcessor, {
  connection: redis,
  concurrency: 5,
})
```

---

### Env Var Validation at Startup

```typescript
// apps/api/src/config.ts
import { z } from 'zod'

const envSchema = z.object({
  DATABASE_URL: z.string().url(),
  REDIS_URL: z.string().url(),
  SESSION_SECRET: z.string().min(32),
  FRONTEND_URL: z.string().url(),
  SMTP_HOST: z.string().optional(),
  LOG_LEVEL: z.enum(['debug', 'info', 'warn', 'error']).default('info'),
  // Phase 3 — optional at startup
  R2_ACCOUNT_ID: z.string().optional(),
  REPLICATE_API_TOKEN: z.string().optional(),
  POSTHOG_KEY: z.string().optional(),
})

export const config = envSchema.parse(process.env)
// Throws at startup with clear message if required vars are missing:
// ZodError: [{ path: ['DATABASE_URL'], message: 'Required' }]
```

---

### Playwright E2E Deterministic Tick

Integration and E2E tests need deterministic Becoming triggers (Becoming readiness is pressure-based, not random). Fix: add test factory that seeds a Stem at a specific pressure threshold.

```typescript
// apps/api/src/test/factories.ts
export async function createStemAtBecomingReadiness(db: DB, hollowId: string) {
  // Seeds a Stem with BiologicalPressure at 95% of readiness threshold
  // Next tick will trigger DETECTED state
  return db.insert(stems).values({
    hollowId,
    biologicalPressure: BECOMING_READINESS_THRESHOLD * 0.95,
    lifecycleStage: 'STEMLING',
    version: 0,
  }).returning()
}
```

This is referenced by E2E Playwright tests via test API routes (gated to test env only).

---

### Updated M1 Task List (DX additions)

Additions to M1 from DX review:

| Task | File(s) | Notes |
|------|---------|-------|
| Docker Compose | `docker-compose.yml` | postgres:16 + postgres_test:16 + redis:7 |
| README.md | `README.md` | 4-step getting started, TTHW <7 min |
| Turborepo task graph | `turbo.json` | dev, build, test, db:migrate, db:seed |
| Env var validation | `apps/api/src/config.ts` | Zod schema; throws clear error on startup |
| Error format | `apps/api/src/lib/errors.ts` | Structured `{ error: { type, code, message } }` |
| WS preValidation hook | `apps/api/src/routes/live.ts` | Session cookie validated on WS upgrade |
| BullMQ deduplication | `apps/api/src/workers/stem-tick.ts` | jobId=stemId, concurrency=5 |
| Test factory | `apps/api/src/test/factories.ts` | Deterministic Becoming readiness seed |
| railway.json (monorepo) | `railway.json` | Per-service config: `apps/api` root, build command |

**railway.json monorepo fix:**
```json
{
  "services": {
    "api": {
      "rootDirectory": "apps/api",
      "buildCommand": "npm run build",
      "startCommand": "node dist/server.js",
      "healthcheckPath": "/health"
    }
  }
}
```

---

### DX Scorecard

```
+====================================================================+
|              DX PLAN REVIEW — SCORECARD                             |
+====================================================================+
| Dimension            | Score  | Prior  | Trend  |
|----------------------|--------|--------|--------|
| Getting Started      |  7/10  |   —    | new    |
| API/CLI/SDK Design   |  8/10  |   —    | new    |
| Error Messages       |  8/10  |   —    | new    |
| Documentation        |  7/10  |   —    | new    |
| Upgrade Path         |  7/10  |   —    | new    |
| Dev Environment      |  8/10  |   —    | new    |
| Community            |  N/A   |   N/A  | solo   |
| DX Measurement       |  6/10  |   —    | new    |
+--------------------------------------------------------------------+
| TTHW                 |  7 min |  25min | ↑      |
| Competitive Rank     | Competitive (target: <10 min — met)          |
| Magical Moment       | first Stemling spawns — SVG organism visible  |
| Product Type         | API/Service + Platform (internal dev DX)      |
| Mode                 | DX POLISH                                     |
| Overall DX           |  7/10  |   —    | new    |
+====================================================================+
| DX PRINCIPLE COVERAGE                                               |
| Zero Friction        | covered (Docker Compose → 7 min TTHW)         |
| Learn by Doing       | covered (README 4-step, live server)           |
| Fight Uncertainty    | covered (structured errors, LOG_LEVEL=debug)   |
| Opinionated defaults | covered (Turborepo tasks, .env.example)        |
| Code in Context      | partially covered (factories.ts, test helpers) |
| Magical Moments      | covered (Stemling spawn = first visual moment) |
+====================================================================+
```

---

### DX Implementation Checklist

```
DX IMPLEMENTATION CHECKLIST
============================
[x] docker compose up -d → DB + Redis in 30s
[x] npm install && npm run db:migrate && npm run dev → game running
[x] TTHW < 10 min (target 7 min)
[x] Every API error has: type + code + message + suggestion
[x] LOG_LEVEL=debug → full stack traces to stdout
[x] WS connection authenticated (session cookie on upgrade)
[x] BullMQ jobs deduplicated by stemId (no pile-up)
[x] Env vars validated at startup (Zod — clear error on missing var)
[x] Integration tests run against local Docker Postgres (no cloud account needed)
[x] tsx --watch + Turborepo watch covers packages/shared changes
[x] E2E Playwright has deterministic Becoming seed factory
[x] README 4-step getting started
[ ] Turborepo remote caching (post-M1 nice-to-have — skip for solo dev)
```

---

### Outside Voice Findings Summary (DX)

**Source:** Claude subagent (independent DX review)

| Finding | Severity | Resolution |
|---------|----------|-----------|
| SIMULATION_TICK_SPEC.md must exist before M1 implementation starts | 🔴 | Pre-M1 required doc already in plan; made hard dependency explicit |
| Neon cold-start latency in tick worker | 🔴 | Mitigated: Docker Compose Postgres for local dev; Neon prod uses connection pooler |
| Integration tests need Neon account | 🔴 | DX3: TEST_DATABASE_URL → Docker Compose Postgres port 5433 |
| WS reconnect protocol not defined | 🔴 | WS preValidation hook added; client reconnect in CEO review scope additions |
| RENDER_SPEC.md dependency not enforced | 🟡 | Made explicit: both specs required before any M1 implementation begins |
| WS session auth on handshake unspecified | 🟡 | DX7: Fastify preValidation hook |
| BullMQ job deduplication missing | 🟡 | DX8: jobId=stemId + concurrency=5 |
| tsx cross-workspace hot-reload gap | 🔵 | Turborepo watch.patterns added to dev task |
| E2E tests need deterministic tick | 🔵 | Test factory added (factories.ts) |
| Env var validation absent | 🔵 | Zod env schema at startup |
| railway.json monorepo per-service config missing | 🔵 | Per-service rootDirectory + buildCommand added |

**Cross-model tensions resolved:**
- Test DB target → Docker Compose Postgres (not Neon) ✓
- Stack simplification (SQLite + setInterval) → REJECTED; keep Neon + BullMQ ✓
- WS auth → Fastify preValidation hook ✓
- BullMQ deduplication → jobId=stemId ✓

**All findings resolved. No unresolved 🔴 issues.**

---

### DX Review Completion Summary

| Dimension | Status |
|---|---|
| Outside voice | 4 🔴 + 8 🟡/🔵 — all resolved |
| Local dev setup | Docker Compose (Postgres + Redis); TTHW 7 min |
| Test DB | Docker Compose Postgres port 5433; no cloud account needed |
| Error format | Structured JSON with type/code/message/suggestion |
| WS auth | Fastify preValidation hook on WS upgrade |
| BullMQ | jobId=stemId dedup; concurrency=5 |
| Turborepo tasks | Fully defined (dev, build, test, db:migrate, db:seed) |
| Hot-reload | tsx --watch + Turborepo watch.patterns for packages/shared |
| Env validation | Zod schema at startup |
| Content versioning | Append-only; v2 adds, never removes v1 |
| README | 4-step getting started at M1 gate |

**NO UNRESOLVED DECISIONS**

---

## GSTACK REVIEW REPORT

| Review | Trigger | Why | Runs | Status | Findings |
|--------|---------|-----|------|--------|----------|
| CEO Review | `/plan-ceo-review` | Scope & strategy | 1 | PASS | 4 critical gaps resolved; simulation tick + account recovery + analytics + PWA added |
| Design Review | `/plan-design-review` | UI/UX gaps | 1 | PASS_WITH_NOTES | score 3→8/10; 23 outside voice findings; 4 D-gates; token system + 5 screen layouts + a11y |
| Eng Review | `/plan-eng-review` | Architecture & tests (required) | 1 | PASS_WITH_NOTES | 5 🔴 resolved; 9 E-gates; auth updated; state machine race fixed; CAS + idempotency + deployment config |
| DX Review | `/plan-devex-review` | Developer experience gaps | 1 | PASS_WITH_NOTES | 4 🔴 + 8 🟡/🔵 resolved; 8 DX-gates; Docker Compose; Turborepo tasks; error format; WS auth; BullMQ dedup |

**VERDICT:** CEO + DESIGN + ENG + DX all CLEARED — ready to implement.

**ENG:** Auth → arctic + oslo. Becoming state machine prevents tick race. Idempotency keys + CAS prevent double-writes. Deployment artifacts at M1 gate.

**DX:** TTHW 7 min. Docker Compose local dev. Structured error format. WS auth on upgrade. BullMQ job dedup. Turborepo task graph. Env var validation at startup.

NO UNRESOLVED DECISIONS

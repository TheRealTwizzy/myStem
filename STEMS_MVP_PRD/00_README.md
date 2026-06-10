# Stem MVP PRD Library

**Version:** Canonical consolidated package  
**Scope:** Mobile MVP  
**Document range:** `00`–`27`  
**Authority:** This package supersedes fragmented in-chat drafts where they conflict with later locked decisions.

## Purpose

This library defines the product, canon, simulation, content, commerce, visual, technical, accessibility, analytics, and quality requirements for **Stem**.

Stem is a mobile cultivation game about raising one biologically adaptive organism per Hollow. Every Stem begins from the same compact, human-derived infant plan, then accumulates irreversible, environmentally responsive anatomy through major developmental events called **Becomings**.

The product target is **cozy with a wrong note**: attachment first, then eerie biological wonder. It must never become a species-collection game, a combat game, a visible optimization spreadsheet, or explicit gore.

## Canonical document map

| # | File | Primary authority |
|---|---|---|
| 00 | `00_README.md` | Library map and governance |
| 01 | `01_MASTER_PRD.md` | Product scope and executive requirements |
| 02 | `02_PRODUCT_DESIGN_LAWS.md` | Non-negotiable product laws |
| 03 | `03_CANON_AND_TERMINOLOGY.md` | Canon language and naming |
| 04 | `04_LORE_CANON.md` | World premise and tonal fiction |
| 05 | `05_CORE_GAMEPLAY.md` | Core cultivation loop |
| 06 | `06_LIFECYCLE_AND_ADULT_CARE.md` | Development, sustainment, regression |
| 07 | `07_BIOLOGICAL_SYSTEMS.md` | Anatomy, signatures, sustainment |
| 08 | `08_MUTATION_METHODS_AND_COMPONENTS.md` | Mutation authoring and component inventory |
| 09 | `09_BIOFEEDBACK_LANGUAGE_SYSTEM.md` | Player-readable biological communication |
| 10 | `10_HOLLOW_AND_BIOME_SPECIFICATION.md` | Hollows and all 21 sub-biomes |
| 11 | `11_VISUAL_BIBLE.md` | Visual laws and illustration styles |
| 12 | `12_FIELD_ENTRY_SYSTEM.md` | Field Entries and Genetic Entries |
| 13 | `13_LINEAGE_SYNTHESIS.md` | Premium lineage continuation |
| 14 | `14_TRADING_AND_GIFTING.md` | One-for-one social transfers |
| 15 | `15_SUBSCRIPTION_AND_ENTITLEMENTS.md` | Bio-Lab Analyst subscription |
| 16 | `16_ILLUSTRATED_FIELD_ARCHIVE.md` | Premium archive behavior |
| 17 | `17_END_TO_END_UX_FLOWS.md` | Critical user flows |
| 18 | `18_STATE_MACHINES_AND_CAPABILITY_MATRIX.md` | State transitions and permissions |
| 19 | `19_TECHNICAL_ARCHITECTURE_AND_DATA_MODEL.md` | System boundaries and entities |
| 20 | `20_AI_AUTHORING_CONTRACT.md` | AI text/image generation constraints |
| 21 | `21_ACCESSIBILITY_AND_CONTENT_SENSITIVITY.md` | Accessibility and safety |
| 22 | `22_ANALYTICS_AND_SUCCESS_METRICS.md` | KPI and event taxonomy |
| 23 | `23_QA_AND_ACCEPTANCE_TEST_PLAN.md` | Verification and launch gates |
| 24 | `24_CONTENT_INVENTORY_AND_PRODUCTION_PLAN.md` | Launch content quantities |
| 25 | `25_MILESTONES_AND_SEQUENCING.md` | Delivery sequence |
| 26 | `26_RISKS_CONFIG_AND_OPEN_DECISIONS.md` | Risks, tunables, unresolved items |
| 27 | `27_GOLDEN_LIFECYCLE_FIXTURES.md` | Canonical test fixtures |

## Authority order

When documents overlap, use this order:

1. `02_PRODUCT_DESIGN_LAWS.md`
2. `03_CANON_AND_TERMINOLOGY.md`
3. The most specialized numbered document
4. `01_MASTER_PRD.md`
5. Earlier drafts or source notes

Later explicit owner decisions override all earlier material.

## Package-wide locked facts

- Exactly **three Hollows** and at most **three active Stems**.
- One living Stem per Hollow.
- No extra slots, reserve, inactive living storage, or living-Stem transfer.
- Spawn anatomy is fixed.
- The lifecycle is `Stemling → Juvenile → Adolescent → Settled Form`.
- Major mutation events are **Becomings**.
- **The Choosing** occurs once, normally at Becoming 3 or 4.
- Mutation Consent is `Stabilize [+]`, `Suppress [-]`, or `Let Continue [±]`.
- Ordinary cultivation cannot permanently kill a Stem.
- Every resolved Becoming creates one Field Entry containing one Genetic Entry.
- Premium monetization affects illustration, archive access, and lineage continuation—not biological power or speed.
- Meaningful state changes require a server connection.
- Release is permanent and leaves no living-Stem history or recall path.
- The MVP launches with cultivation, trading, gifting, Lineage Synthesis, premium illustration, archive, and weekly subscription.

## Document conventions

- **MUST / SHALL**: mandatory launch behavior.
- **SHOULD**: expected unless a documented exception exists.
- **MAY**: optional.
- **Forbidden**: must not appear in the MVP.
- Hidden biological values may be inspected by internal tools and tests, but never exposed directly to players.

## Change control

Every material change must record:

- affected documents;
- changed invariant;
- migration impact;
- analytics impact;
- test updates;
- whether existing Field Entries or premium assets are affected.

No change may silently invalidate a permanent illustration, duplicate or restore a consumed Genetic Entry, or alter a player-owned Field Entry without an explicit migration plan.

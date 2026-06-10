# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Stems** is a mobile cultivation game design and product specification repository. This is not a code implementation repository—it contains detailed product requirements, game mechanics specifications, canon definitions, and design documentation.

**Core concept:** Players maintain up to three enclosed environments (Hollows), each housing one adaptive organism (a Stem). Through environmental care and consent decisions, players influence the biological development of their unique Stems.

**Product tone:** "Cozy with a wrong note" — attachment and wonder first, then eerie biological fascination. The game must **never** become:
- A species-collection game
- A combat game  
- A visible optimization spreadsheet
- Explicitly gory

**Key principle:** Players influence development through care and consent—they never select anatomy directly.

## Repository Structure

### Primary Specifications (`STEMS_MVP_PRD/`)

The MVP Product Requirements Document is organized in 27 numbered files (00–27). These form the canonical specification:

- **02_PRODUCT_DESIGN_LAWS.md** — Non-negotiable product laws (highest authority within PRD)
- **03_CANON_AND_TERMINOLOGY.md** — Official terminology and naming conventions
- **05_CORE_GAMEPLAY.md** — Core cultivation loop and mechanics
- **19_TECHNICAL_ARCHITECTURE_AND_DATA_MODEL.md** — System boundaries and data entities
- **27_GOLDEN_LIFECYCLE_FIXTURES.md** — Canonical test fixtures for verification

(See `STEMS_MVP_PRD/00_README.md` for the complete map and full authority order.)

### Reference & Support Documents

- **MASTER_CANON_BIBLE.md** — Single authority reference for biology, terminology, and design law (governs procedural generation)
- **STEM_MUTATION_TRAIT_CODEX.md** — Complete mutation component inventory and trait definitions
- **MUTATION_EVENT_TEMPLATES.md** — Template structures for mutation events and player interactions
- **QUARANTINE_FIELD_MANUAL.md** — Content and behavior validation rules
- **ANATOMICAL_ATLAS.md** — Visual and anatomical reference
- Other .md files provide additional context and legacy reference material

## Documentation Status & Known Gaps

The specification is comprehensive but **actively being revised**. See `REWRITE_SPECIFICATION.md` for a detailed audit of documentation gaps and a proposed restructuring.

**Known gaps that may require fallback strategies:**

- **Biological Pressure mechanics** — Accumulation mechanism is abstract; generation logic for when a Becoming triggers is not fully formalized
- **Mutation Consent cascades** — Choice consequences (Stabilize vs Suppress vs Let Continue) are partially documented; downstream effects need expansion
- **Adult Sustainment Profile thresholds** — When does Unstable→Decaying→Regressed progression occur? Numbers and ranges need clarification
- **Misfold integration** — Archive heavily documents Misfolds; player-facing rules and generation rates are underspecified
- **Timeline generation** — "Lifecycle timing is not fixed" but no procedural rules exist for computing Stem age
- **Event trigger ordering** — Which mutation events fire and in what sequence is not fully algorithmic

**Handling gaps:** When a topic lacks detail:
1. Check `MASTER_CANON_BIBLE.md` for the canonical constraint
2. Search `REWRITE_SPECIFICATION.md` for proposed solutions
3. Verify with `27_GOLDEN_LIFECYCLE_FIXTURES.md` for concrete examples
4. Consult `QUARANTINE_FIELD_MANUAL.md` for narrative context clues
5. Fall back to the principle: "attachment first, never lose player trust in permanent assets"

## Authority and Document Precedence

When specifications overlap or conflict, resolve using this order:

1. **STEMS_MVP_PRD/02_PRODUCT_DESIGN_LAWS.md** — Absolute product laws
2. **STEMS_MVP_PRD/03_CANON_AND_TERMINOLOGY.md** — Canonical terminology
3. The most specialized numbered PRD document for the topic
4. **STEMS_MVP_PRD/01_MASTER_PRD.md** — Broad product scope
5. MASTER_CANON_BIBLE.md and support documents
6. Earlier drafts or source notes

Later explicit owner decisions override all earlier material.

## Key Design Principles

### What Stems IS

- **Exactly three Hollows** with one living Stem per Hollow (no additional slots, reserves, or transfers)
- **Fixed Stemling anatomy** with procedural, component-based mutation
- **The Lifecycle:** Stemling → Juvenile → Adolescent → Settled Form
- **Mutation events** are called **Becomings** and require player consent (Stabilize, Suppress, or Let Continue)
- **One Field Entry** created after every resolved Becoming
- **Premium monetization** affects illustration, archive, and lineage—never biological power or progression speed
- **Meaningful state changes require server connection**
- **Release is permanent** with no recall or living-Stem history

### What Stems is NOT

These are hard boundaries in the product law and cannot be circumvented:

- **Not a species-collection game** — The player has one Stem per Hollow, period. No collecting, no roster, no "gotta catch 'em all"
- **Not a combat/competition game** — No PvP, no battling, no leaderboards ranking Stems against each other
- **Not an optimization spreadsheet** — No visible stats, DPS numbers, min-maxing, or "correct" build paths
- **Not explicitly gory or disturbing** — Body horror is off-limits; mutations are eerie but beautiful, never disgusting
- **Not a breeding/genetics simulator** — Lineage Synthesis is premium flavor, not a core progression loop
- **Not a grind loop** — Biological development is driven by care decisions and time, not task repetition

## Working with Specifications

### When Adding or Modifying Content

Every material change must document:

1. **Affected documents** — Which PRD and support documents are impacted
2. **Changed invariant** — What rule or assumption changed
3. **Migration impact** — How existing game state or Field Entries are affected
4. **Analytics impact** — How tracking or KPIs change
5. **Test updates** — What verification steps or fixtures need updating
6. **Asset impacts** — Whether existing premium illustrations or Field Entries are affected

No change may silently:
- Invalidate a permanent illustration
- Duplicate or restore a consumed Genetic Entry
- Alter a player-owned Field Entry without an explicit migration plan

### Verification and Validation

- Use **STEMS_MVP_PRD/27_GOLDEN_LIFECYCLE_FIXTURES.md** to verify lifecycle progression
- Cross-reference **QUARANTINE_FIELD_MANUAL.md** for content validation rules
- Check **MASTER_CANON_BIBLE.md** before using or modifying terminology
- Review **STEMS_MVP_PRD/23_QA_AND_ACCEPTANCE_TEST_PLAN.md** for launch verification gates

### Terminology

Always verify terminology in **MASTER_CANON_BIBLE.md** section 1 (Official Terminology) before using in specs, code comments, or UI. Terms like "Stem," "Stemling," "Becoming," "Hollow," "Mutation Consent," and "The Choosing" have precise definitions.

### Cross-References

Most major specification sections include "See Also" pointers to integration points. Use these when understanding how a subsystem connects to broader mechanics.

## Documentation Restructuring Roadmap

The documentation is being consolidated and improved. `REWRITE_SPECIFICATION.md` outlines:

- Known terminology inconsistencies (e.g., "Mutation Method" vs "Ossif")
- Generation logic gaps that need formalization
- Proposed reorganization to improve clarity and reduce redundancy

**Current status:** Audit complete; restructuring pending approval. Use the current documentation as canonical, but expect breaking changes to document naming and organization. Any work that creates new cross-references should use pinned links to the current file names (00-27 numbering is stable; file contents may shift).

## Common Tasks

### Understanding a Feature

1. Start with **STEMS_MVP_PRD/01_MASTER_PRD.md** for the product goal
2. Find the specific numbered document (e.g., Core Gameplay is 05, Technical Architecture is 19)
3. Cross-reference **MASTER_CANON_BIBLE.md** for terminology and constraints
4. Check **STEMS_MVP_PRD/18_STATE_MACHINES_AND_CAPABILITY_MATRIX.md** for state transitions
5. Verify with **27_GOLDEN_LIFECYCLE_FIXTURES.md** for concrete examples

### Adding New Mechanics

1. Review **02_PRODUCT_DESIGN_LAWS.md** to ensure the mechanic doesn't violate a core law
2. Check **03_CANON_AND_TERMINOLOGY.md** for naming
3. Document in the most specialized PRD file (e.g., new mutation types go in 08)
4. Update **MASTER_CANON_BIBLE.md** if terminology or biology rules are affected
5. Add fixtures to **27_GOLDEN_LIFECYCLE_FIXTURES.md**
6. Record the change with all required metadata

### Checking Game State Impact

- **Hollow & Biome mechanics:** STEMS_MVP_PRD/10
- **Mutation types & components:** STEMS_MVP_PRD/08 + STEM_MUTATION_TRAIT_CODEX
- **Player consent & moral decisions:** MASTER_CANON_BIBLE + STEMS_MVP_PRD/05
- **Subscription & entitlements:** STEMS_MVP_PRD/15
- **Premium assets:** STEMS_MVP_PRD/16 (Illustrated Field Archive)
- **Social features:** STEMS_MVP_PRD/14 (Trading & Gifting)
- **Permanent assets:** STEMS_MVP_PRD/13 (Lineage Synthesis)

## World-Building & Narrative Context

The specification includes world-building elements that inform tone but are not currently codified in accessible documents:

- **Project NEPHE-7** — Scientific research program at R-17 Adaptive Biosystems Laboratory (principal investigator: Dr. Elian Voss)
- **Holloway Therapeutics** — Private biotech company that created Stemlings as therapy organisms
- **The Choir** — Suspected collective intelligence connecting adult Stems (lore-level; not a mechanics feature)

These elements appear in `MASTER_CANON_BIBLE.md` and `QUARANTINE_FIELD_MANUAL.md` as world-building flavor and narrative authority, but source documents (scientist logs, character backstories) are referenced but not included in this repo. **Use these references for narrative color and to understand the clinical-warm tone, but don't expect mechanical rules from them.**

## Document Conventions

- **MUST / SHALL** — Mandatory launch behavior
- **SHOULD** — Expected unless a documented exception exists
- **MAY** — Optional
- **Forbidden** — Must not appear in the MVP
- Hidden biological values may be inspected by internal tools and tests, but never exposed directly to players

## This Repository

- **Not a git repository** — This is a specification/design folder, not version-controlled code
- **Canonical PRD:** 27 numbered documents in `STEMS_MVP_PRD/` (00-27)
- **Support references:** Standalone .md files in the root for terminology, lore, and design audit
- **Not for code implementation:** Future code will reference these specs, but the code repo will be separate

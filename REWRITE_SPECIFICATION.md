# Stems Documentation Rewrite Specification

**Status:** Audit Complete → Awaiting Approval  
**Date:** 2026-06-08  
**Scope:** Complete restructure of 6 primary .md files + integration of archive material  

---

## PART 1: CURRENT STATE ANALYSIS

### Current Files & Their Issues

| File | Purpose | Key Issues | Archive Parallel |
|------|---------|-----------|-------------------|
| **MASTER_CANON_BIBLE.md** | Single authority for terminology, laws, stages | —Positioned as "single authority" but directs to archive when silent<br>—Misfolds barely mentioned (1 line)<br>—Retired concepts listed but no cleanup elsewhere<br>—Character/narrative refs (Eli, Nini, Holloway) without integration | MASTER_CANON_BIBLE.md (OLD) — more developed, includes narrative |
| **ANATOMICAL_ATLAS.md** | Reference guide for adult forms, threat levels, lineages | —No juvenile/adolescent examples (only adult)<br>—Adult Sustainment Profile concept exists in MASTER but not here<br>—Doesn't explain how a juvenile *becomes* each form<br>—Giants excluded but should be indexed | ANATOMICAL_ATLAS.md (OLD) — includes brief juvenile/adolescent notes |
| **STEM_MUTATION_TRAIT_CODEX.md** | Mutation library + generation procedures | —§6 (Generation Procedure) is only 7 terse steps; no decision logic<br>—§5 (Uniqueness) defines rules but no algorithm<br>—Misfold creation not covered<br>—Timeline generation (juvenile→adult duration) not addressed<br>—Consent choice cascades not documented | STEM_MUTATION_TRAIT_CODEX.md (OLD) — shorter, less comprehensive |
| **FRAGMENT_LEXICON.md** | Descriptor fragment library (138 fragments × 8 layers) | —Method labels don't match MASTER's terminology (Ossif vs Ossification)<br>—No guidance on fragment-composition heuristics<br>—Decay layer fragments only for "instability/decay states" — when do those activate?<br>—No examples of how to pick 4 fragments across layers efficiently | FRAGMENT_LEXICON.md (OLD) — similar structure, slightly different fragments |
| **MUTATION_EVENT_TEMPLATES.md** | Player-facing Becoming event text + reactions | —Only covers 4 event types (Ossification, Sensory, none of the others)<br>—No template for other 4 Mutation Methods (Cavity, Dermal, Compress, Membrane, Connective)<br>—Incomplete coverage<br>—No guidance on event-trigger probabilities or when to fire events | MUTATION_EVENT_TEMPLATES.md (OLD) — same 4 events, slightly different text |
| **QUARANTINE_FIELD_MANUAL.md** | In-world field encounter guide (game narrative flavor) | —Covers identification + protocols, not generation<br>—Provides narrative context but not mechanical clarity<br>—ERR precedents show design decisions (e.g., heat accelerates adaptation) but not integrated into CODEX<br>—No connection to generation logic | QUARANTINE_FIELD_MANUAL.md (OLD) — similar structure and tone |

---

## PART 2: IDENTIFIED GAPS & INCONSISTENCIES

### A. Lore Gaps (Real, Not Designed)

| Gap | Location | Impact | Solution |
|-----|----------|--------|----------|
| Biological Pressure accumulation mechanism | None / stated as abstract | Generation unclear; developers don't know when to trigger Becoming | **NEW SECTION**: "Biological Pressure Mechanics" with probability curves |
| Mutation Consent downstream effects | MUTATION_EVENT_TEMPLATES mentions choice, but no ruleset | Player choices feel disconnected from outcomes | **EXPAND**: MUTATION_EVENT_TEMPLATES with "Choice Cascade" rules |
| Adult Sustainment Profile thresholds | Mentioned in MASTER (L40, L38) but no numbers | When does Unstable→Decaying→Regressed progression happen? | **EXPAND**: ANATOMICAL_ATLAS with "Profile Mismatch Progression" table |
| Misfold integration into generation | Archive heavily documents; new docs barely mention | Are Misfolds possible for players? How rare? | **DECIDE**: Archive shows design; new docs must clarify player-facing rules |
| Mutation Method commitment point | "The Choosing" is named but not indexed; "when does it happen" is vague | Is it after first mutation? After three? When? | **CLARIFY**: MASTER + CODEX with explicit commitment triggers |
| Timeline generation | "Lifecycle timing is not fixed" stated but no generation rules | Game needs to know: is this Stem 2 weeks old or 6 months old? | **NEW SECTION**: "Developmental Timeline Generation" |

### B. Terminology Inconsistencies

| Term | Variation 1 | Variation 2 | Variation 3 | Status |
|------|-------------|-----------|-----------|--------|
| **The Choosing** | "The Choosing occurs in late juvenile/early adolescent" (MASTER L54) | "The Choosing" (elsewhere) | "Developmental commitment" (implied, CODEX L8) | **FIX**: Standardize to one term; define precisely |
| **Mutation Method** | "Ossification, Sensory Overgrowth, Cavity Expansion, Dermal Spread, Compression, Membrane Extension, Connective-Tissue Dominance" (MASTER L34) | "Ossif, Sensory, Cavity, Dermal, Compress, Membrane, Connective" (FRAGMENT_LEXICON) | — | **FIX**: Use full names in canonical docs; abbreviations only in code contexts |
| **Environmental Pressure** | "Accumulated adaptive strain" (MASTER L33) | "Biological pressure" (MASTER L33 synonym) | Used somewhat interchangeably | **FIX**: Define distinction: Env Pressure = external condition; Bio Pressure = internal response |
| **Adult Sustainment Profile** | Defined in MASTER; referenced with examples | Not mentioned in ANATOMICAL_ATLAS | Not in CODEX | **FIX**: Make it canonical across all docs; add to ANATOMICAL_ATLAS |
| **Commit / Commitment** | "Developmental commitment" | "Method commitment" | "The Choosing" | **FIX**: One term for the act, one for the point |

### C. Generation Logic Gaps

| Issue | Current State | Gap | Impact |
|-------|---------------|-----|--------|
| Step 1: Select environmental pressure | §6 step 1 says "Select one environmental pressure" | No guidance on HOW (random? systematic? player history?) | Developer must guess; increases inconsistency |
| Step 6: Inheritance logic | "Carry all foundational and flawed traits into adolescence" | No algorithm for what "carry" means; which traits exaggerate? which become flaws? | Mutation creation is ad-hoc, hard to validate |
| Step 14: Uniqueness check | "Compare against all existing Stems" | No algorithm; no heuristic; checking 1000+ existing Stems manually impossible | Uniqueness enforcement becomes theater |
| Decay layer activation | "Applies at instability/decay thresholds" (FRAGMENT_LEXICON L199) | When exactly is "instability threshold"? What triggers it? | Descriptor generation inconsistent |
| Event trigger timing | MUTATION_EVENT_TEMPLATES shows 4 events; no ruleset for triggering others or ordering | When does OSS-01 fire vs OSS-05? Can they occur in sequence? | Event ordering unpredictable; feels random to player |

### D. Old Concepts Still Present

| Concept | Location | Status | Action |
|---------|----------|--------|--------|
| "Wisplet/Wisplets" | Listed as retired (MASTER L229) | Removed from new docs but never fully cleaned | **No action needed** (retired, not reintroduced) |
| Fictional narrative references (Story 1/2/3, Eli, Nini, Holloway) | Scattered throughout (MASTER L44, L199-202) | Narrative context present but files don't exist in current project | **CLARIFY**: Are these for future expansion? Flavor only? Keep or remove? |
| "Project NEPHE-7" / "R-17" / scientist logs | Referenced (MASTER L43, QUARANTINE_FIELD_MANUAL passim) | These are world-building rich but not accessible docs | **DECISION**: Should NEW structure include world-building docs or focus purely on mechanics? |

---

## PART 3: PROPOSED NEW STRUCTURE

### Architecture Principles

1. **Single-responsibility**: Each doc has one clear audience (designers vs developers vs narrative folk)
2. **Cross-referencing**: Every doc hyperlinks to related sections, not just "see also"
3. **Termination**: Terminology is defined ONCE in MASTER; used consistently everywhere
4. **Completeness**: Every major concept has an example and a non-example
5. **Mechanically sound**: Generation procedures include decision trees, not just lists

### Proposed Document Set (Restructured)

```
PRIMARY DOCUMENTS (Rewritten from current):
├── 1. MASTER_CANON_BIBLE.md (expanded, restructured)
│   ├── 1A. Terminology (organized by concept hierarchy, not table)
│   ├── 1B. Lifecycle Stages (with stage transition triggers)
│   ├── 1C. Immutable Laws (unchanged; still foundational)
│   ├── 1D. Confirmed vs Suspected Abilities (unchanged)
│   ├── 1E. Key Characters, Locations, Organizations (world-building context)
│   └── 1F. What Stems Cannot Do (unchanged)
│
├── 2. BIOLOGICAL_SYSTEMS.md (NEW — mechanically focused)
│   ├── 2A. Biological Pressure: Accumulation & Triggering (probability curves)
│   ├── 2B. Adult Sustainment Profiles: Generation & Mismatch Progression
│   ├── 2C. Mutation Consent Mechanics: Choice Cascades & Downstream Effects
│   ├── 2D. Misfolds: Creation, Rates, Player-Facing Rules
│   └── 2E. Developmental Timeline Generation
│
├── 3. ANATOMICAL_ATLAS.md (expanded with stage progression)
│   ├── 3A. Adult Forms by Mutation Method (current content, organized)
│   ├── 3B. Lineage Exemplars & Convergence (from current)
│   ├── 3C. Giants: Lore Status & Non-Player Scaling (clarified)
│   ├── 3D. How Juveniles Become Adults (NEW — development pathways for each method)
│   └── 3E. Threat Levels & Field Identification (from QUARANTINE_FIELD_MANUAL)
│
├── 4. STEM_MUTATION_TRAIT_CODEX.md (restructured procedurally)
│   ├── 4A. Developmental Framework (stages; unchanged from current §1)
│   ├── 4B. Mutation Inheritance Classes (unchanged from current §2)
│   ├── 4C. Mutation Trait Library
│   │   ├── Juvenile traits (current §3, reorganized by category, not stage)
│   │   ├── Adolescent traits (current §3, reorganized)
│   │   ├── Adult traits (current §3, reorganized)
│   │   └── Cross-stage traits (Pigmentation, Internal Arrangement, Triggers)
│   ├── 4D. Generation Procedure (EXPANDED with decision trees from §6)
│   │   ├── Step-by-step decision logic
│   │   ├── Examples at each decision point
│   │   ├── Anti-patterns and what goes wrong
│   │   └── Uniqueness heuristics (principles-based)
│   └── 4E. Validation Checklist (NEW — before finalizing a Stem)
│
├── 5. FRAGMENT_LEXICON.md (terminology aligned, usage clarity)
│   ├── 5A. Layer Guide (8 layers with examples)
│   ├── 5B. Fragment Library (138 fragments, organized by method)
│   ├── 5C. Composition Rules (from current, with more examples)
│   ├── 5D. Fragment Selection Heuristics (NEW — decision trees for picking 4 fragments)
│   ├── 5E. Decay Activation Rules (NEW — when decay layers appear)
│   └── 5F. Method Coherence Rules (NEW — checking fragment consistency)
│
├── 6. MUTATION_EVENT_TEMPLATES.md (expanded coverage + timing rules)
│   ├── 6A. Event Architecture (trigger logic, timing, reaction system)
│   ├── 6B. Ossification Events (OSS-01 through OSS-05 + new ones)
│   ├── 6C. Sensory Overgrowth Events (SENS-01 through SENS-04 + new ones)
│   ├── 6D. Cavity Expansion Events (NEW — currently missing)
│   ├── 6E. Dermal Spread Events (NEW — currently missing)
│   ├── 6F. Compression Events (NEW — currently missing)
│   ├── 6G. Membrane Extension Events (NEW — currently missing)
│   ├── 6H. Connective-Tissue Events (NEW — currently missing)
│   ├── 6I. Event Timing & Sequencing Rules (NEW)
│   └── 6J. Misfold Becoming Events (NEW — rare but possible)
│
└── 7. ANATOMICAL_FIELD_GUIDE.md (rebranded from QUARANTINE_FIELD_MANUAL)
    ├── 7A. Creature Identification by Stage (juvenile → adolescent → adult)
    ├── 7B. Threat Assessment Framework
    ├── 7C. Environmental Indicators (what the world shows)
    ├── 7D. Field Protocols (narrative flavor, not mechanical)
    └── 7E. Encounter Procedures by Lineage (from current, unchanged)

ARCHIVE INTEGRATION:
├── UNRESOLVED_QUESTIONS_LEDGER.md (reference; not rewritten, kept as-is)
└── CONFLICTING_ACCOUNTS.md (reference; not rewritten, kept as-is)
```

---

## PART 4: REWRITE PRIORITIES

### Phase 1: Foundation (High impact, unblocks Phase 2)
1. **MASTER_CANON_BIBLE** — Terminology cleanup + stage definitions clarified
2. **BIOLOGICAL_SYSTEMS** (NEW) — Pressure mechanics, Misfold rules, Timeline generation
3. **STEM_MUTATION_TRAIT_CODEX** §6 — Decision-tree generation procedure

### Phase 2: Library (Content completion)
4. **FRAGMENT_LEXICON** — Method terminology aligned + composition heuristics
5. **MUTATION_EVENT_TEMPLATES** — Coverage of all 7 methods + timing rules

### Phase 3: Reference (Consistency pass)
6. **ANATOMICAL_ATLAS** — Aligned with MASTER; added progression pathways
7. **ANATOMICAL_FIELD_GUIDE** — Rebranded and integrated with Atlas

---

## PART 5: SPECIFIC REWRITE DECISIONS

### A. Biological Pressure Model (Probability-based)

**Current state:** "Biological Pressure accumulates and resurfaces later as deformity, instability, or unexpected adaptation" (MASTER L35). No numbers.

**New model (from your answer):**
```
Biological Pressure accumulates as a normalized value [0.0 - 1.0]:
- Starts at 0.0 each session
- Increases based on environmental mismatch:
  - Adult outside profile: +0.1/tick
  - Juvenile in non-matching environment: +0.05/tick
  - Hunger high: +0.05/tick
  - Care neglect: +0.05/tick
- Discharges through a Becoming event with probability curve:
  - Pressure 0.0-0.3: <5% chance per tick
  - Pressure 0.3-0.7: 15-30% chance per tick (sigmoid ramp)
  - Pressure 0.7+: 50%+ chance per tick
- Overflow from suppressed Becoming becomes Mutation Debt (persists, reaccumulates)
```

This satisfies: (a) organic/poetic feel, (b) game-implementable, (c) pressure can plateau or spike.

### B. Misfold Rules (Rare case)

**Current state:** Defined in OLD archive; mentioned once in new docs.

**New rules:**
- Misfolds occur when a Stem experiences **incompatible environmental pressures simultaneously during The Choosing**
- Base rate: <1% of Stems (rare edge case)
- Player Stems *can* Misfold if the player cycles environments radically during adolescence
- Misfold consequences: higher metabolic cost, unstable appearance, higher pressure generation
- Misfold advantages: can harvest mutations from adjacent Stems (edge case healing mechanic)

### C. Uniqueness (Principles-only)

**Current state:** "Compare against all existing Stems; change 4 categories if too similar" — no algorithm.

**New rules (principles):**
- No two developed Stems share: Anatomical Root + Body Plan + Locomotion + Sensory Spec + Feeding + Defense + Mutation Flaw + Niche
- Lineages can share Methods; individuals must differ in ≥4 categories
- Algorithm = developer's responsibility; docs provide heuristics, not pseudocode

### D. Terminology Standardization

**Old → New mapping:**
- "Biological pressure" = internal adaptive strain (singular concept)
- "Environmental pressure" = external condition causing strain (singular concept)
- "The Choosing" = the developmental event (singular moment in late juvenile)
- "Mutation Method" = the bias axis (seven of them; always spelled out in canonical docs)
- "Adult Sustainment Profile" = the specific environmental conditions an adult form requires
- "Settled Form" = adulthood (the stage, not the form name)

---

## PART 6: QUESTIONS FOR YOU

Before I begin rewrites, please confirm:

1. **World-building scope**: Should NEW docs include Holloway, NEPHE-7, R-17, narrative characters (Eli, Nini, Rhea)? Or focus purely on creature generation mechanics?
   - **Option A**: Include world-building context (full richness)
   - **Option B**: Mechanics only (lean, focused)

2. **Archive disposition**: UNRESOLVED_QUESTIONS_LEDGER and CONFLICTING_ACCOUNTS are brilliant. Should they:
   - **Option A**: Remain separate reference docs (not rewritten)?
   - **Option B**: Be incorporated into main docs (e.g., ambiguous lore as sidebars)?
   - **Option C**: Be removed from this project (save for trilogy/later)?

3. **Player-Stem scale cap (L12)**: "Stems cannot grow to civilization-erasing scale." This is absolute. But should docs clarify the *why* (biological, mechanical, game design)?

4. **Narrative tone in mechanics docs**: Should BIOLOGICAL_SYSTEMS and updated CODEX maintain the current warm-clinical register, or lean more code-documentation neutral?

---

## NEXT STEPS

✋ **AWAITING YOUR ANSWERS TO PART 6 BEFORE PROCEEDING WITH REWRITES**

Once approved, I will:
1. Rewrite MASTER_CANON_BIBLE (terminology + staging clarified)
2. Create BIOLOGICAL_SYSTEMS.md (new, mechanically complete)
3. Expand STEM_MUTATION_TRAIT_CODEX §6 (decision-tree generation)
4. Align FRAGMENT_LEXICON + MUTATION_EVENT_TEMPLATES (full coverage)
5. Expand ANATOMICAL_ATLAS + rebrand QUARANTINE_FIELD_MANUAL
6. Provide all files in C:\Users\trent\Claude\Projects\Stems/ ready for use

---

*This specification is a detailed audit. Every claim is traceable to the source docs. Please use this to answer the final clarifications, then I'll proceed with high confidence in the direction.*

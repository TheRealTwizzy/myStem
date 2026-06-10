# Stems — Master Canon Bible

*Single authority reference for biology, terminology, and design law. Governs all procedural generation and gameplay mechanics. Cross-references: see "See Also" sections in each major heading.*

*When this document conflicts with older files, this document wins. When this document is silent, consult OLD_concept_canon/ for narrative context. Do not create lore outside this framework.*

*Last updated: 2026-06-08*

---

## How to Read This Document for Code Generation

This is the foundational source for procedural systems. Use it to:
- **Verify terminology**: Before using a term in code/UI, confirm it here.
- **Understand constraints**: Every Law and "Cannot Do" is a hard rule for generation.
- **Check stage definitions**: Lifecycle stages anchor all mutation and event logic.
- **Cross-reference other docs**: See "See Also" sections for integration points.

For complete examples of stage progression, see STEM_MUTATION_TRAIT_CODEX (sections 1–3). For gameplay implications of these rules, see MUTATION_EVENT_TEMPLATES and QUARANTINE_FIELD_MANUAL.

---

## 1. Official Terminology

| Term | Definition | Source |
|------|-----------|--------|
| **Stem** | The universal name for the life-form at any stage. Never a species, sub-type, or category. All Stems are simply Stems. | L26, Design Law |
| **Stemling** | The infant/larval state. Named from the knee pit (popliteal fossa) where early specimens nested. Soft, pale, round, near-identical. The Stemling is not the creature's true form — it is the larval compromise. | Lore_canon |
| **The Choosing** | The late-juvenile developmental commitment to one adaptive survival path. After The Choosing, future mutations must build on the committed anatomy — the specimen loses unrestricted developmental flexibility. | NEPHE-7.025 |
| **The Settled Form** | Adulthood. Not a true final form — a period in which anatomical change becomes slower, costlier, and more specialized. The adult still mutates under sustained pressure. | NEPHE-7.061 |
| **Misfold** | A specimen that fails to complete The Choosing due to conflicting environmental pressures. Permanently unstable; higher metabolic cost; potentially capable of harvesting adaptations from other specimens. Neither fully juvenile nor adult. | NEPHE-7.052 |
| **Biological Signature** | The immutable core self, computed from the specimen's seed at creation. Shapes value ranges, temperament, and comfort bands. Mutation layers stack on top — the signature is never directly mutated. | Q7, M2-L02 |
| **Biological Pressure** | Accumulated adaptive strain. Builds from environmental mismatches, care neglect, and developmental growth. Discharges through a Becoming. Synonym for environmental pressure accumulation. | Q6, M2-L10 |
| **Mutation Method** | One of seven bias axes by which biological pressure shapes the adult form: Ossification, Sensory Overgrowth, Cavity Expansion, Dermal Spread, Compression, Membrane Extension, Connective-Tissue Dominance. | L41, DECISIONS Q10 |
| **Mutation Debt** | Suppressed biological drive that does not disappear when a Becoming is Suppressed. Accumulates and resurfaces later as deformity, instability, or unexpected adaptation. | Q11, L37 |
| **A Becoming** | The player-facing name for a mutation event. The creature strains; something emerges; the player chooses its fate. Clinical-warm register; never mechanical. | L36, M5-L01 |
| **Mutation Consent** | The player's act of choosing Stabilize, Suppress, or Let continue on behalf of the creature. The creature is aware of the choice and reacts. | Q11, Q12, L15, L33 |
| **Adult Sustainment Profile** | The specific environmental conditions an adult form requires to maintain its shape. Generated at adulthood from the dominant Mutation Method and environment history. May differ from birth comfort. Mismatch with profile causes visible distress/instability (Unstable or Decaying states). | Q13, L40 |
| **Environmental Addiction** | An adult's dependence on the conditions it adapted under. Deprivation causes withdrawal-distress; sustained out-of-range conditions cause instability, decay, then regression. | L40, Q13 |
| **The Hollow** | The creature's habitat — an abstract warm enclosure, evocatively skinned. The player adjusts the Hollow's conditions; the creature adapts to and is shaped by them. | L28, M2-L28 |
| **Consent History** | The ledger of every Mutation Consent the player has made on behalf of the creature. A quiet moral record. | L53, M2-L36 |
| **The Choir** | The suspected collective intelligence connecting adult Stem forms. Evidence: chemical-residue (340+ distinct compounds embedded in tissue and habitat) and vibration-based environmental communication. Whether it constitutes consciousness is unresolved (see OLD_concept_canon/investigations/CHOIR_DOSSIER.md). Impact on player's Stem: unknown; may be detected/felt at adult stage. | NEPHE-7.047, Story 2/3 |
| **Project NEPHE-7** | The developmental ecology research program at R-17 Adaptive Biosystems Laboratory. Dr. Elian Voss, principal investigator, 2085–2087. The primary scientific record of Stem development. | scientist_logs1/2 |
| **Holloway Therapeutics** | The private biotech company that created Stemlings as therapy organisms; operated beneath a children's behavioral research center. Suppressed mutation findings. | Trilogy, Story 1 |

---

## 2. Lifecycle Stages

| Stage | Common name | Canonical markers | Development driver |
|-------|------------|------------------|--------------------|
| **Infant** | Stemling | Pale, soft, round body; oversized eyes; weak stubby limbs; near-identical across individuals; warmth-seeking posture | Time + warmth; trust builds slowly |
| **Juvenile** | — | First faint divergence appears; early adaptive decisions form; body begins testing the environment actively | Environmental exposure + care history |
| **Adolescent** | — | Becomings cluster here; the volatile shaping age; most dramatic morphological changes; The Choosing occurs in late juvenile/early adolescent | Biological pressure; Mutation Consent choices |
| **Adult** | The Settled Form | Form committed; Adult Sustainment Profile active; predatory demeanor emerges; slow ongoing mutation possible under sustained pressure | Environmental match/mismatch |
| **Unstable** | — | Form fighting itself; trembling, flickering, doubling of features; caused by out-of-range environment; recoverable | Environmental correction |
| **Decaying** | — | Form failing/ailing; dulling palette, sagging posture, blemishes, faint Cuticle texture at severe decay; recoverable | Environmental correction + time |
| **Regressed** | — | One mutation layer released to survive; form simpler, profile recomputed easier; melancholy, never punitive | Environmental correction; never terminal |

**Note on duration:** Lifecycle timing is not fixed. It emerges from care quality, biological pressure, and environment history. NEPHE-7 specimens showed meaningful juvenile changes within days under active pressure; comfortable environments slow development. There is no "natural" timetable.

**See Also:** STEM_MUTATION_TRAIT_CODEX §1 (developmental framework); MUTATION_EVENT_TEMPLATES (event timing rules); QUARANTINE_FIELD_MANUAL §1.1–1.4 (field identification markers for each stage).

---

## 3. Immutable Biological Laws

These govern all Stems at all stages. They are not tunable balance constants — they are the canon foundations of the world.

**Law 1: Human Anatomy Remains the Root**
Every adult form is named from, shaped by, or functionally based on a human anatomical feature. No entirely novel organ systems emerge — the creatures reorganize, enlarge, duplicate, and repurpose existing human structures. The human body functions as a library of possible organisms. *(Lore_canon, NEPHE-7.031)*

**Law 2: Environment Decides the Adult Form**
A Stemling raised in one set of conditions becomes something different from one raised elsewhere. Environmental history — not birth genetics — is the primary determinant of adult morphology. The biological signature sets the range of possibilities; the environment selects within that range. *(Lore_canon, L7)*

**Law 3: Comfort Becomes Predation**
The infant's need for warmth, closeness, and softness does not disappear at adulthood. It transforms. The mature expression of infantile attachment is containment, penetration, or consumption. The creature still wants warmth — adulthood only teaches it more efficient ways to find it inside living things. *(Lore_canon, L5, L8, L11)*

**Law 4: All Stems Begin as Stemlings**
Reproduction resets the organism to the maximally adaptable infant state. Offspring do not inherit the specialized anatomy of the parent — they inherit biological potential and, possibly, temporary developmental biases toward conditions the parent experienced. *(NEPHE-7.021, NEPHE-7.033, L13)*

**Law 5: Adaptation Is Not Free**
Mutation consumes internal resources. Rapid structural change temporarily dismantles functional tissue elsewhere. A specimen that mutates too quickly may lose essential organs before replacement systems become functional. *(NEPHE-7.015)*

**Law 6: There Is No True Final Form**
The Settled Form (adulthood) is a period of slower, costlier, more specialized change — not a terminal state. All twelve adult specimens monitored by NEPHE-7 showed measurable change over six months of observation. *(NEPHE-7.061)*

**Law 7: Death Persists as Ecology**
Dead specimens remain ecologically active. Specialized adult tissue breaks down; unresolved stem-cell material remains viable. Corpses produce new infants, pass developmental instruction through chemical residue, and continue shaping the ecosystem for weeks after death. *(NEPHE-7.057)*

---

## 4. Confirmed vs. Suspected Abilities

| Ability | Status | Evidence |
|---------|--------|----------|
| Passive environmental observation while dormant | **Confirmed** | NEPHE-7.006: sensory activity at 64% baseline during dormancy; specimens developed corresponding structures upon waking |
| Passive adaptation through observation alone (no contact) | **Suspected — single data point** | NEPHE-7.074: infant grew ear structures from listening through a door; not replicated |
| Habitat modification (secretions, tunnel reinforcement, soil chemistry) | **Confirmed** | NEPHE-7.013 |
| Tissue self-recycling to fund mutation | **Confirmed** | NEPHE-7.015 |
| Non-verbal mimicry of environmental sounds | **Confirmed** | L10, NEPHE-7 Laryngrave documentation; HARD RULE: never the device microphone, never player audio |
| Chemical environmental communication through habitat structures | **Confirmed** | NEPHE-7.047: 340+ distinct signaling compounds embedded in tunnel tissue, triggering developmental pathways in new arrivals |
| Corpse-mediated developmental instruction | **Confirmed** | NEPHE-7.057 |
| Population self-regulation based on environmental conditions | **Confirmed** | NEPHE-7.066 |
| Emergent collective behavior without centralized command | **Confirmed** | NEPHE-7.069 (R-17 breach reconstruction) |
| The Choir as true collective consciousness | **Suspected — unresolved** | Story 2/3; see Choir Dossier (investigations/) |
| Assimilation of human consciousness | **Suspected — single narrative source** | Story 3; Nini's revelation; not documented scientifically |
| Verbal language production | **Confirmed impossible (baseline)** | L3; the L3 near-word apex remains a reserved narrative beat, not baseline behavior |
| Adaptation through inherited parental anatomy | **Confirmed impossible** | NEPHE-7.021; offspring reset to infant state |

---

## 5. Naming Conventions and Scientific Classifications

**The creature name:** "Stem" — universal, uncategorized. "Your Stem" until privately named (L21). "Your Stem, now [descriptor]" at adulthood (L26). No species noun ever.

**Descriptor labels** are composed from the Fragment Lexicon (`concept_canon/game/FRAGMENT_LEXICON.md`). Rules:
- 2–4 fragments from different layers, ordered silhouette-first
- Anatomy roots appear ONLY as adjectival compounds: "rib-plated," "iris-clustered," "marrow-bright"
- Never as species nouns: "Ribform," "Eye Stem," "Marrow Type" are all forbidden
- Example valid label: "rib-plated, fold-crawling, heat-dependent"

**On the canonical form names** (Popliths, Patellarks, Scapulites, etc.): these are reference exemplars of Mutation Methods and anatomy regions — not species. They describe the *kind of thing* a Stem under sustained specific pressure might converge toward, softly, over time. No player's Stem will *be* a Poplith. A player's Stem may become *poplith-adjacent* through its own unique convergence path.

**Scientific classification does not exist** in this world as a functional taxonomy. Forms exist on a continuum; individual variation is too great for discrete species boundaries. The closest analog is the Mutation Method — a bias axis, not a category.

---

## 6. Creature Lineage Index

Reference exemplars only — not a species roster. Organized by primary Mutation Method.

| Common name | Anatomy root | Method | Primary habitat | Source | Notes |
|------------|-------------|--------|----------------|--------|-------|
| Popliths | popliteal fossa (knee pit) | Compression | Tunnels, ruins, crawlspaces | Lore_canon | Primary trilogy exemplar of Compression |
| Patellarks | patella (kneecap) | Ossification | Open plains, dry basins | Lore_canon | Herd behavior; bone-grinding ecology |
| Phalangers | phalanges (fingers/toes) | Membrane Extension | Canopy, cliff faces | Lore_canon | Gliding; canopy thieves |
| Scapulites / Shouldra | scapula | Membrane Extension | Cliffs, thermal vents | Lore_canon / Adult_Examples | Synonyms (L2); bone-sail gliders |
| Mandigores | mandible | Ossification | Bone fields, predator dens | Lore_canon | Jaw-dominant; bone recyclers |
| Oculines / Iris Drowned | oculus / iris | Sensory Overgrowth | Dark wetlands, caves; ocean | Lore_canon | Synonyms (L2); watcher forms |
| Costal Leviathans | costae (ribs) | Cavity Expansion | Deep water, flooded tunnels | Lore_canon | Rib-cage trap feeding |
| Palatines | palate | Cavity Expansion | Wet caves, fungal groves | Lore_canon | Trap feeders; sweet secretion |
| Tendrilisks / Tendrenches | tendons | Connective-Tissue | Dense forests; ocean | Lore_canon | Synonyms (L2); snare/cord forms |
| Marrow Wights / Marrowdeep | bone marrow | Ossification | Winter zones, grave fields; underground | Lore_canon | Synonyms (L2); cold-season scavengers |
| Laryngraves / Lobechildren | larynx / lobe | Sensory Overgrowth | Echoing caves, empty towns | Lore_canon / Adult_Examples | Voice mimics; acoustic ambush |
| Dermavores | dermis | Dermal Spread | Warm caves, body piles | Lore_canon | Flat body-sheets; engulf |
| Elboughs | elbow | Ossification | Rocky terrain | Adult_Examples | Joint-armor; bracing forms |
| Shinwraiths | shin | Ossification | Open plains | Adult_Examples / Trilogy | Sprint predators |
| Heelers | heel | Ossification | General land | Adult_Examples | Territorial pack animals |
| Ribstags | rib cage | Cavity / Ossif | Plains, grazing land | Adult_Examples / Trilogy | Rib-arch grazers; herd animals |
| Spinetowers | spine | Ossification | Mountains, valleys | Adult_Examples / Trilogy | Vertebral titans; nearly unkillable |
| Lungmoths | lungs | Cavity Expansion | Fog, open air | Adult_Examples / Trilogy | Sedating breath; large floaters |
| Throats | throat | Cavity Expansion | Deep rivers, flooded caves | Adult_Examples | Suction predators |
| Palmers | palm | Connective-Tissue | Reefs, shallow seas | Adult_Examples | Living islands |
| Navelids | navel | Cavity Expansion | Deep ocean | Adult_Examples / Trilogy | Oceanic giants; worshipped |
| Veinwalkers | veins | Connective-Tissue | Forests, wetlands | Adult_Examples / Trilogy | Vascular root-drainers |
| Sternum Colossus | sternum | Ossification | Valleys, plains | Adult_Examples / Trilogy | Land titan; mobile fortress |
| Atlas Maw | atlas vertebra | Ossification | Collapsed mountains | Adult_Examples | Load-bearing titan |
| Cuticles | cuticle | Dermal Spread | Under bark, skin-folds | Adult_Examples | Parasitic; signal of sickness |
| Wristlings | wrist | Membrane Extension | Near larger creatures | Adult_Examples | Small scavengers; swarms |
| Jawhawks | jaw | Ossification | Open air | Adult_Examples | Jaw-dive flyers |
| Gumlings | gums | Cavity Expansion | Cave walls | Adult_Examples | Colony trap-feeders |
| Molars | molar | Ossification | Tunnels, mineral deposits | Adult_Examples | Tunnel grinders |
| Hiplurks | hip | Compression | Tunnel mouths | Adult_Examples | Obstacle/filter forms |
| Tonguelopes | tongue | Sensory Overgrowth | Open plains | Adult_Examples | Prey animals; sensory tongues |
| Sockets | eye socket | Sensory Overgrowth | Tunnels, sinkholes | Adult_Examples | Vibration-sensing ambush |
| Knucklebacks | knuckles | Ossification | Swamps | Adult_Examples | Armored amphibious |

*This list is a reference, not a ceiling. Every player's Stem is a unique individual that may converge toward, but never precisely become, any of these exemplars.*

---

## 7. Major Organizations, Locations, and Characters

### Organizations

| Name | Role | Status |
|------|------|--------|
| **Holloway Therapeutics** | Created Stemlings; marketed them as therapy organisms; suppressed mutation findings; authorized stress testing | Fictional corporate entity; pre-breach |
| **R-17 Adaptive Biosystems Laboratory** | NEPHE-7's facility; containment failed 2087-09-23 | Fictional research site |
| **Project NEPHE-7** | Developmental ecology research program; documented Stem biology systematically | Records are the canon scientific baseline |
| **The Severance Authority** | Military organization dedicated to Stem eradication (Story 3) | Fictional; post-assimilation era |
| **Project Severance** | Biological signal weapon designed to sever the Choir (Story 3) | Fictional; narrative-only |

### Key Locations

| Name | Description |
|------|-------------|
| **The Hollow** | In-game; the creature's personal habitat. Abstract and evocatively skinned — not a literal tank or biome. |
| **Green County** | First major quarantine zone in Story 2; Rhea Sol's survey destination |
| **The First Hollow** | Nini's location in Story 3; origin-point of the species |

### Characters

| Name | Role | Appears in |
|------|------|-----------|
| **N-01 "Nini"** | Original Stemling; far more aware than anyone realized; becomes the hidden origin-mind behind the species | All three books; the trilogy's center |
| **Dr. Elian Voss** | PI of Project NEPHE-7; the clinical voice of the research logs | scientist_logs1, scientist_logs2 |
| **Dr. Mara Vey** | Lead developmental biologist at Holloway; believed the Stemlings were harmless; disgraced post-breach | Stories 1, 2, 3 |
| **Jonas Pike** | Corporate director at Holloway; authorized stress testing; drove military applications | Story 1 |
| **Eli** | Quiet child in Holloway's therapy program; formed the strongest bond with Nini; the only human Stems do not harm | Stories 1, 2, 3 |
| **Captain Rhea Sol** | Survey team commander; Story 2 protagonist; triggers Project Severance | Stories 2, 3 |
| **The Choir** | Suspected collective intelligence connecting adult forms; may preserve assimilated human consciousness | Stories 2, 3 |

---

## 8. What Stems Cannot Do

These constraints define the boundary of the fictional world. Content that violates them is non-canon.

- **Cannot speak or produce words** (baseline). Mimicry is non-verbal, limited to in-game sounds. The reserved L3 near-word apex is a single narrative beat, not a general capability.
- **Cannot access the device microphone or reproduce real-world audio.** Hard rule (L10). This is both a privacy constraint and a tonal one.
- **Cannot be collected as a species set.** There are no kinds. The design law prohibiting species trees is absolute.
- **Cannot be selected from a list.** The player does not choose a Stem type. The form emerges.
- **Cannot be bred, purchased, traded, or summoned through gacha** by the player.
- **Cannot fight other Stems** in player-directed combat.
- **Cannot grow to civilization-erasing scale in the player's habitat.** Giants (Spinetower, Sternum Colossus, Iris Drowned, Atlas Maw, Marrowdeep) exist as lore backdrop and ambient dread — never as the player's creature.
- **Cannot be damaged or destabilized by social visitors.** A visitor can observe; cannot affect.
- **Cannot transmit adult anatomy directly to offspring.** Reproduction resets to infant state. Offspring may inherit developmental biases, not structures.
- **Cannot die from environmental mismatch alone.** The progression is staged, recoverable, and always gives a fair chance to correct (Q14, L5). There is a no-death floor.
- **Cannot be "won."** There is no final victory state. Adulthood is an ongoing condition, not a completion.

---

## 9. Retired / Non-Canon Concepts

| Concept | Why retired |
|---------|------------|
| "Wisplet" / "Wisplets" | Previous brand name; replaced by "Stem/Stems" in full rebranding |
| "Neepet" | Earlier working title; replaced |
| Fixed species trees | Abolished by Q10 and the Design Law; contradicts the one-creature-per-player procedural philosophy |
| Hardcoded adult classes (Fire Stem, Water Stem, Crawler Form, Flyer Form, etc.) | Explicitly forbidden in CLAUDE.md; contradicts procedural individual design |
| Creature collection list / creature roster | Contradicts Design Law; the player manages one organism, not a collection |
| Battle system / PvP | Never canon; forbidden before vertical slice |
| Breeding / reproduction as a player mechanic | Never canon |
| Gacha / monetization-driven mutation | Never canon |
| "Selecting" a creature from options at start | Never canon; the creature is entrusted, not chosen |
| Hollow as a literal tank, terrarium, or selectable biome | Retired in L19; the Hollow is abstract and evocatively skinned, not a fixed selectable environment |

---

*This document is the single authority for terminology, biology, and canon scope. Update it when new decisions create new canonical facts. Never silently contradict it — if a new decision overrides something here, revise the relevant entry explicitly.*

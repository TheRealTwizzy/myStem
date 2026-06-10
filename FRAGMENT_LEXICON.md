# Stems — Fragment Lexicon

*Authority document for procedural descriptor generation. Governs `src/stem/descriptors.ts` and any system producing creature labels.*

All descriptor labels are composed from this lexicon. Pick 2–4 fragments from **different layers**, ordered by the mandatory hierarchy (silhouette-first). The result characterizes an individual — it is never a species name (L6, L25, Q10).

**Tone key:** `clinical` — precise/anatomical · `eerie` — subtly wrong · `tender` — caring register · `predatory` — appetite-coded (adult forms, L8)

**Layer abbreviations (mandatory composition order):**
`silhouette` → `locomotion` → `feeding` → `sensory` → `instinct` → `addiction` → `surface` → `decay`

**Method abbreviations:** `Ossif` = Ossification · `Sensory` = Sensory Overgrowth · `Cavity` = Cavity Expansion · `Dermal` = Dermal Spread · `Compress` = Compression · `Membrane` = Membrane Extension · `Connective` = Connective-Tissue Dominance · `any` = method-agnostic

All fragments: ✅ Teen-safe. None from the L42 forbidden list (no genital/sexual/excretory anatomy).

---

## Layer 1 — Silhouette / Skeleton

*The body's defining outline. Always leads a descriptor label.*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `rib-plated` | Ossif | costae | clinical | "rib-plated, fold-crawling" |
| `bone-crested` | Ossif | spine | clinical | "bone-crested, still-standing" |
| `patella-ridged` | Ossif | patella | clinical | "patella-ridged, knuckle-walking" |
| `skull-domed` | Ossif | cranium | eerie | "skull-domed, heat-dependent" |
| `molar-armored` | Ossif | molar | clinical | "molar-armored, jaw-grinding" |
| `spine-spiked` | Ossif | spine | eerie | "spine-spiked, drag-limbed" |
| `sternum-shielded` | Ossif | sternum | clinical | "sternum-shielded, still-standing" |
| `joint-bulged` | Ossif | patella | eerie | "joint-bulged, compression-rolling" |
| `scapular-sailed` | Membrane | scapula | clinical | "scapular-sailed, height-seeking" |
| `phalanx-webbed` | Membrane | phalanges | clinical | "phalanx-webbed, membrane-floating" |
| `shoulder-spanned` | Membrane | shoulder | clinical | "shoulder-spanned, scapular-gliding" |
| `wrist-winged` | Membrane | wrist | eerie | "wrist-winged, thermal-riding" |
| `rib-caged` | Cavity | costae | eerie | "rib-caged, still-standing" |
| `sternum-hollow` | Cavity | sternum | clinical | "sternum-hollow, warmth-hungry" |
| `chest-vaulted` | Cavity | sternum | eerie | "chest-vaulted, heat-drawing" |
| `fold-dense` | Compress | knee | clinical | "fold-dense, tunnel-fitting" |
| `knee-compressed` | Compress | knee | clinical | "knee-compressed, fold-crawling" |
| `joint-stacked` | Compress | elbow | clinical | "joint-stacked, pressure-adapted" |
| `tendon-framed` | Connective | tendon | clinical | "tendon-framed, cord-swinging" |
| `ligament-braced` | Connective | tendon | clinical | "ligament-braced, tension-held" |
| `dermis-broad` | Dermal | dermis | clinical | "dermis-broad, skin-sheeted" |
| `socket-rimmed` | Sensory | socket | eerie | "socket-rimmed, iris-clustered" |
| `hip-widened` | Compress | hip | clinical | "hip-widened, weight-braced" |
| `atlas-shouldered` | Ossif | atlas | clinical | "atlas-shouldered, load-bearing" |

---

## Layer 2 — Locomotion

*How the body moves through its environment.*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `fold-crawling` | Compress | knee | clinical | "rib-plated, fold-crawling" |
| `drag-limbed` | Compress | elbow | eerie | "bone-crested, drag-limbed" |
| `knuckle-walking` | Ossif | knuckle | clinical | "joint-bulged, knuckle-walking" |
| `heel-planted` | Ossif | heel | clinical | "patella-ridged, heel-planted" |
| `shin-sprinting` | Ossif | shin | clinical | "spine-spiked, shin-sprinting" |
| `scapular-gliding` | Membrane | scapula | clinical | "scapular-sailed, scapular-gliding" |
| `wrist-rotating` | Membrane | wrist | eerie | "wrist-winged, wrist-rotating" |
| `phalanx-climbing` | Membrane | phalanges | clinical | "phalanx-webbed, phalanx-climbing" |
| `tendon-propelled` | Connective | tendon | clinical | "tendon-framed, tendon-propelled" |
| `cord-swinging` | Connective | tendon | eerie | "ligament-braced, cord-swinging" |
| `sole-pressing` | Compress | heel | clinical | "knee-compressed, sole-pressing" |
| `joint-locking` | Ossif | patella | clinical | "joint-bulged, joint-locking" |
| `compression-rolling` | Compress | spine | clinical | "fold-dense, compression-rolling" |
| `rib-swimming` | Cavity | costae | clinical | "rib-caged, rib-swimming" |
| `membrane-floating` | Membrane | dermis | tender | "phalanx-webbed, membrane-floating" |
| `palm-gripping` | Connective | palm | clinical | "tendon-framed, palm-gripping" |
| `elbow-bracing` | Ossif | elbow | clinical | "joint-stacked, elbow-bracing" |

---

## Layer 3 — Feeding Method

*How the body obtains what it needs. Tone darkens with adult stage (L11).*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `throat-drinking` | Cavity | throat | clinical | "chest-vaulted, throat-drinking" |
| `palate-trapping` | Cavity | palate | eerie | "sternum-hollow, palate-trapping" |
| `jaw-grinding` | Ossif | jaw | clinical | "molar-armored, jaw-grinding" |
| `molar-crushing` | Ossif | molar | clinical | "rib-plated, molar-crushing" |
| `marrow-drawing` | Ossif | marrow | predatory | "bone-crested, marrow-drawing" |
| `warmth-drinking` | Dermal | dermis | predatory | "dermis-broad, warmth-drinking" |
| `heat-drawing` | Dermal | dermis | predatory | "chest-vaulted, heat-drawing" |
| `skin-absorbing` | Dermal | dermis | eerie | "dermis-broad, skin-absorbing" |
| `cavity-engulfing` | Cavity | sternum | eerie | "rib-caged, cavity-engulfing" |
| `tendon-snaring` | Connective | tendon | predatory | "tendon-framed, tendon-snaring" |
| `tongue-probing` | Sensory | tongue | eerie | "socket-rimmed, tongue-probing" |
| `lobe-tasting` | Sensory | lobe | eerie | "iris-clustered, lobe-tasting" |
| `body-pressing` | Compress | knee | predatory | "fold-dense, body-pressing" |
| `cord-binding` | Connective | tendon | predatory | "ligament-braced, cord-binding" |
| `vein-sipping` | Connective | vein | predatory | "tendon-framed, vein-sipping" |
| `navel-pulling` | Cavity | navel | eerie | "sternum-hollow, navel-pulling" |

---

## Layer 4 — Sensory Traits

*How the body perceives its environment.*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `iris-clustered` | Sensory | iris | eerie | "socket-rimmed, iris-clustered" |
| `oculus-multiplied` | Sensory | oculus | eerie | "fold-dense, oculus-multiplied" |
| `socket-deep` | Sensory | socket | clinical | "joint-bulged, socket-deep" |
| `eye-spread` | Sensory | oculus | eerie | "dermis-broad, eye-spread" |
| `lobe-ringed` | Sensory | lobe | eerie | "scapular-sailed, lobe-ringed" |
| `larynx-resonant` | Sensory | larynx | eerie | "chest-vaulted, larynx-resonant" |
| `throat-echoing` | Sensory | throat | eerie | "sternum-hollow, throat-echoing" |
| `dermis-sensing` | Dermal | dermis | clinical | "dermis-broad, dermis-sensing" |
| `vein-feeling` | Connective | vein | eerie | "ligament-braced, vein-feeling" |
| `pulse-aware` | Connective | vein | predatory | "tendon-framed, pulse-aware" |
| `tendon-vibrating` | Connective | tendon | clinical | "tendon-framed, tendon-vibrating" |
| `cuticle-tasting` | Dermal | cuticle | eerie | "dermis-broad, cuticle-tasting" |
| `scent-blind` | any | — | clinical | "bone-crested, scent-blind" |
| `sound-dominant` | Sensory | larynx | clinical | "chest-vaulted, sound-dominant" |
| `heat-reading` | Dermal | dermis | predatory | "dermis-broad, heat-reading" |

---

## Layer 5 — Behavioral Instinct

*The body's deep drives and social posture.*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `warmth-hungry` | Dermal | dermis | predatory | "dermis-broad, warmth-hungry" |
| `heat-dependent` | Dermal | dermis | clinical | "rib-plated, fold-crawling, heat-dependent" |
| `still-standing` | Compress | — | eerie | "rib-caged, still-standing" |
| `motion-averse` | Compress | knee | eerie | "fold-dense, motion-averse" |
| `ambush-prone` | Compress | — | predatory | "rib-caged, ambush-prone" |
| `smother-prone` | Dermal | dermis | predatory | "dermis-broad, smother-prone" |
| `press-seeking` | Compress | — | predatory | "fold-dense, press-seeking" |
| `weight-needing` | Compress | — | clinical | "joint-stacked, weight-needing" |
| `solitude-addicted` | any | — | eerie | "bone-crested, solitude-addicted" |
| `touch-averse` | any | — | eerie | "spine-spiked, touch-averse" |
| `sound-seeking` | Sensory | larynx | eerie | "chest-vaulted, sound-seeking" |
| `echo-following` | Sensory | larynx | eerie | "larynx-resonant, echo-following" |
| `light-avoiding` | Sensory | oculus | eerie | "oculus-multiplied, light-avoiding" |
| `dark-nested` | any | — | tender | "fold-dense, dark-nested" |
| `gaze-holding` | Sensory | oculus | predatory | "iris-clustered, gaze-holding" |

---

## Layer 6 — Environmental Addiction

*The conditions the adult body has committed to requiring (L40, Q13).*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `furnace-bonded` | Dermal | dermis | clinical | "dermis-broad, warmth-hungry, furnace-bonded" |
| `heat-sustained` | Dermal | — | clinical | "rib-plated, heat-dependent, heat-sustained" |
| `cold-dependent` | Ossif | — | clinical | "bone-crested, cold-dependent" |
| `flood-adapted` | Cavity | — | clinical | "rib-caged, rib-swimming, flood-adapted" |
| `moisture-addicted` | Cavity | — | clinical | "chest-vaulted, moisture-addicted" |
| `dry-sustained` | Dermal | — | clinical | "dermis-broad, dry-sustained" |
| `darkness-bound` | Sensory | — | eerie | "oculus-multiplied, darkness-bound" |
| `light-starved` | Sensory | — | eerie | "iris-clustered, light-starved" |
| `lightless-settled` | any | — | tender | "fold-dense, lightless-settled" |
| `pressure-adapted` | Compress | — | clinical | "joint-stacked, pressure-adapted" |
| `depth-dependent` | Cavity | — | clinical | "rib-caged, depth-dependent" |
| `hollow-fixed` | Compress | — | clinical | "fold-dense, hollow-fixed" |

---

## Layer 7 — Surface Detail

*The body's visible outer texture, marks, and color signals.*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `translucent-skinned` | Membrane | dermis | eerie | "scapular-sailed, translucent-skinned" |
| `pale-sheeted` | Dermal | dermis | eerie | "dermis-broad, pale-sheeted" |
| `marrow-bright` | Ossif | marrow | clinical | "bone-crested, marrow-bright" |
| `bone-pale` | Ossif | — | eerie | "patella-ridged, bone-pale" |
| `cuticle-flecked` | Dermal | cuticle | eerie | "dermis-broad, cuticle-flecked" |
| `dermis-ridged` | Dermal | dermis | clinical | "dermis-broad, dermis-ridged" |
| `fold-creased` | Compress | knee | clinical | "fold-dense, fold-creased" |
| `skin-layered` | Dermal | dermis | clinical | "dermis-broad, skin-layered" |
| `vein-visible` | Connective | vein | eerie | "translucent-skinned, vein-visible" |
| `vessel-traced` | Connective | vein | eerie | "membrane-floating, vessel-traced" |
| `iris-marked` | Sensory | iris | eerie | "iris-clustered, iris-marked" |
| `socket-pitted` | Sensory | socket | eerie | "socket-rimmed, socket-pitted" |
| `heat-flushed` | Dermal | dermis | clinical | "warmth-hungry, heat-flushed" |
| `cold-blanched` | Ossif | dermis | clinical | "cold-dependent, cold-blanched" |
| `wrist-jointed` | Membrane | wrist | clinical | "wrist-winged, wrist-jointed" |
| `knuckle-ridged` | Ossif | knuckle | clinical | "knuckle-walking, knuckle-ridged" |
| `gum-soft` | Cavity | gum | tender | "palate-trapping, gum-soft" |

---

## Layer 8 — Decay Pattern

*The marks of stress, regression, and biological history. Applies at instability/decay thresholds (L14, L39).*

| Fragment | Method | Anatomy Root | Tone | Example composition |
|----------|--------|-------------|------|---------------------|
| `cuticle-hosting` | Dermal | cuticle | eerie | "dermis-broad, cuticle-hosting" |
| `blemish-spreading` | Dermal | dermis | clinical | "pale-sheeted, blemish-spreading" |
| `pallor-advancing` | any | — | clinical | "bone-pale, pallor-advancing" |
| `collapse-prone` | any | — | clinical | "fold-dense, collapse-prone" |
| `sagging-margined` | Dermal | dermis | clinical | "skin-layered, sagging-margined" |
| `regression-marked` | any | — | clinical | "rib-plated, regression-marked" |
| `layer-shedding` | Dermal | dermis | eerie | "dermis-broad, layer-shedding" |
| `scar-layered` | any | — | clinical | "bone-crested, scar-layered" |
| `history-written` | any | — | tender | "translucent-skinned, history-written" |
| `instability-prone` | any | — | clinical | "joint-bulged, instability-prone" |
| `form-uncertain` | any | — | eerie | "socket-rimmed, form-uncertain" |

---

## Composition Rules

**Minimum:** 2 fragments from different layers.
**Maximum:** 4 fragments. Beyond 4 a label stops reading as a name and starts reading as a list.

**Required order:** silhouette fragment first if present. The most visible, defining trait leads.

**Valid examples:**
- `"rib-plated, fold-crawling, heat-dependent"` — silhouette + locomotion + instinct (3 layers)
- `"iris-clustered, still-standing, darkness-bound"` — silhouette/sensory + instinct + addiction (3 layers)
- `"scapular-sailed, translucent-skinned"` — silhouette + surface (2 layers, minimal but valid)
- `"tendon-framed, tendon-propelled, vein-feeling, vein-visible"` — silhouette + locomotion + sensory + surface (4 layers, all Connective method — readable because method coherent)

**Invalid examples:**
- `"warmth-hungry, heat-dependent"` — two instinct-layer fragments; same layer, repetitive
- `"rib-plated, rib-caged, rib-swimming"` — three rib-root fragments; overwhelming a single anatomy root
- `"bone-crested Ossification adult"` — the anatomy root or method name must never become a noun in the label

**Tone guidance:** In infant/juvenile stages, weight toward `clinical` and `tender` fragments. At adulthood, `predatory` and `eerie` fragments become available. Decay-layer fragments only appear when the instabilityState or decayState is active.

---

## Fragment Count by Method

| Method | Silhouette | Locomotion | Feeding | Sensory | Instinct | Addiction | Surface | Decay | Total |
|--------|-----------|-----------|---------|---------|----------|-----------|---------|-------|-------|
| Ossification | 8 | 5 | 4 | 1 | — | 2 | 5 | 1 | 26 |
| Sensory Overgrowth | 2 | — | 2 | 9 | 3 | 3 | 3 | — | 22 |
| Cavity Expansion | 3 | 1 | 5 | — | — | 2 | 1 | — | 12 |
| Dermal Spread | 2 | 1 | 4 | 3 | 4 | 3 | 7 | 5 | 29 |
| Compression | 3 | 4 | 1 | — | 5 | 2 | 1 | 2 | 18 |
| Membrane Extension | 4 | 4 | — | — | — | — | 1 | — | 9 |
| Connective Dominance | 2 | 3 | 4 | 2 | — | — | 1 | — | 12 |
| method-agnostic | — | — | — | 1 | 3 | 3 | — | 3 | 10 |
| **Total** | **24** | **18** | **20** | **16** | **15** | **15** | **19** | **11** | **138** |

*138 total fragments across 8 layers and 7 methods. Dermal Spread and Ossification have the most fragments because they are the most surface-visible methods (renders in M8) and the most environment-driven (high environmental pressure in MVP 3-variable model, L7).*

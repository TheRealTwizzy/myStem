# Hollow and Biome Specification

## Hollow capacity

Each account has exactly three Hollow slots.

Each occupied Hollow contains:

- one biome family;
- one sub-biome;
- Warmth;
- Moisture;
- Light;
- one unique five-band variable;
- fixed functional surfaces;
- one living Stem.

Hollows are identified only by biome and slot number.

## Selection flow

1. Choose one of seven biome families.
2. Choose one of that family's three sub-biomes.
3. Confirm the empty Hollow.
4. Create a New Seed or complete Lineage Synthesis.

## Universal controls

### Warmth

1. Cold
2. Cool
3. Temperate
4. Warm
5. Hot

### Moisture

1. Dry
2. Arid
3. Balanced
4. Damp
5. Saturated

### Light

1. Dark
2. Dim
3. Low
4. Bright
5. Intense

## Defaults

Every newly created Hollow begins at:

- Temperate Warmth;
- Balanced Moisture;
- Low Light;
- unique variable band 3.

The underlying physical thresholds differ by sub-biome.

## Canonical biome library

| Family | Sub-biome | Unique variable |
|---|---|---|
| Temperate Grove | Canopy Basin | Airflow |
| Temperate Grove | Rootbed Hollow | Substrate Compression |
| Temperate Grove | Fungal Understory | Organic Particulate |
| Wetland | Reed Fen | Water Depth |
| Wetland | Peat Bog | Acidity |
| Wetland | Floodplain | Current |
| Littoral Coast | Tidal Shelf | Salinity |
| Littoral Coast | Spray Grotto | Wave Pulse |
| Littoral Coast | Estuarine Basin | Turbidity |
| Arid Expanse | Dune Hollow | Airborne Abrasion |
| Arid Expanse | Salt Basin | Mineral Load |
| Arid Expanse | Stone Wadi | Thermal Swing |
| Alpine Shelf | Wind Ridge | Wind Load |
| Alpine Shelf | Snow Shelf | Freeze–Thaw Intensity |
| Alpine Shelf | Thin-Air Ledge | Air Thinness |
| Subterranean Cavern | Compression Tunnel | Spatial Compression |
| Subterranean Cavern | Limestone Cavern | Mineral Drip |
| Subterranean Cavern | Geothermal Vault | Geothermal Flux |
| Industrial Ruin | Resonance Shaft | Mechanical Vibration |
| Industrial Ruin | Oxidation Yard | Metallic Particulate |
| Industrial Ruin | Radiant Foundry | Radiant Load |

## Unique-variable bands

Every unique variable uses five labelled bands. Labels must be authored per variable so they sound natural and remain understandable.

Examples:

- Airflow: Still / Faint / Moving / Strong / Forceful
- Water Depth: Exposed / Shallow / Mid / Deep / Submerged
- Salinity: Fresh / Trace / Brackish / Saline / Concentrated
- Wind Load: Sheltered / Light / Moderate / Heavy / Severe

Exact final label sets belong in content configuration and require accessibility review.

## Functional surfaces

Each sub-biome includes a fixed set of environmental interaction surfaces appropriate to that environment.

Surfaces may provide:

- warmth contact;
- shelter;
- elevation;
- pressure;
- moisture contact;
- grip;
- current exposure;
- mineral contact;
- rest posture.

The MVP does not include freeform Hollow decoration.

## Environmental history

The server records:

- current bands;
- change timestamps;
- duration in bands;
- meaningful exposure windows;
- intervention windows;
- Becoming context;
- resulting biological response.

Players see broad history, not raw hidden accumulation values.

## Meaningful adjustment

A meaningful adjustment changes one control by at least one band and is accepted by the server.

Rapid toggling must not create artificial biological pressure. Rate limits and minimum exposure windows apply.

## Intervention overlays

During Stabilization or Suppression, the UI must clearly show:

- active intervention;
- target supportive or opposing condition;
- current compliance;
- interruption risk;
- commitment state.

Ordinary adjustments outside intervention remain ordinary care.

## Online requirement

Hollow changes require online authority. Offline changes are disabled, not queued.

## Accessibility

Controls must support:

- large touch targets;
- stepped buttons;
- labels;
- screen readers;
- keyboard input where available;
- reduced motion;
- color-independent status;
- no precision-only sliders.

## Forbidden Hollow features

- paid control bands;
- premium-only variables;
- hidden decoration bonuses;
- extra purchasable slots;
- creature storage;
- deterministic mutation recipes;
- player-authored hazardous environments that bypass content rules.

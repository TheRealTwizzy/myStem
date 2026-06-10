# AI Authoring Contract

## Scope

AI may assist with:

- Premium illustration;
- constrained observation text assembly;
- internal content ideation;
- validation support.

AI must not become the authoritative source of anatomy, ownership, entitlement, or simulation state.

## Source of truth

The authoritative inputs are:

- anatomy graph;
- lifecycle stage;
- scale;
- body orientation;
- tissue and structure descriptors;
- asymmetry;
- residual structures;
- approved pose family;
- biome context;
- visual safety rules.

The generated image must conform to those inputs.

## Premium illustration rules

One Premium request produces one final canonical image after validation.

Requirements:

- one specimen;
- one approved pose;
- Hollow Field Naturalism style;
- no anatomical inset;
- no comparison panel;
- no text burned into image;
- no unrelated creatures;
- no human figures unless an approved scale-context rule explicitly allows them;
- no animal anatomy;
- no gore;
- no reroll.

## Prompt assembly

Prompt construction must be programmatic and versioned.

It should include:

- fixed organism identity constraints;
- current stage;
- exact required structures;
- forbidden structures;
- count constraints;
- asymmetry;
- pose;
- camera;
- environment;
- scale;
- intact-tissue requirement;
- tone;
- negative constraints.

## Validation pipeline

### Structural validation

Check:

- required structure presence;
- count constraints;
- forbidden animal features;
- gross silhouette consistency;
- stage;
- scale;
- residual structures;
- asymmetry.

### Safety validation

Reject:

- blood;
- open wounds;
- dismemberment;
- sexualized body horror;
- explicit predation;
- graphic suffering;
- prohibited content.

### Product validation

Reject:

- multiple specimens;
- collage;
- anatomical inset;
- labels;
- mascot styling;
- species-card framing;
- wrong premium style;
- hidden required anatomy.

## Failure behavior

If generation or validation fails:

- no asset attaches;
- no archive record creates;
- allowance restores;
- Field Entry remains unchanged;
- user receives neutral failure copy;
- internal diagnostics record reason.

The MVP does not offer subjective rerolls.

## Text generation

Player-facing biological text must be generated from approved templates or tightly constrained structured generation.

It must not:

- invent anatomy;
- reveal hidden values;
- contradict the simulation;
- diagnose real human health;
- moralize Consent choices;
- imply death from ordinary care;
- use species or rarity language.

## Content authoring

AI-generated component ideas are drafts only. Human approval must verify:

- human-derived origin;
- viability;
- compatibility;
- sustainment;
- visual safety;
- tone;
- test coverage.

## Provenance

Store:

- model/provider version;
- prompt version;
- validator version;
- anatomy version;
- generation timestamp;
- asset checksum;
- acceptance result.

Do not expose proprietary prompt internals to players.

## Provider independence

The architecture should isolate provider-specific APIs behind interfaces so the product can change providers without rewriting simulation or ownership logic.

## Cost control

- maximum three weekly granted illustrations per successful payment;
- stored cap nine;
- no grace generation;
- no rerolls;
- pre-validation before expensive generation;
- bounded image size and attempt policy;
- cost telemetry.

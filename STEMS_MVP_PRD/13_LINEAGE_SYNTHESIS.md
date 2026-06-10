# Lineage Synthesis

## Purpose

Lineage Synthesis allows a player to continue selected biological influence without cloning anatomy or creating a breeding system.

## Eligibility

All conditions must be true:

- account is paid or in platform-confirmed grace;
- player owns the Field Entry;
- Field Entry is Premium;
- Genetic Entry is unused;
- Field Entry is not locked;
- one Hollow is empty;
- network connection is active;
- account is permitted to perform economic actions.

## Grace behavior

Grace permits synthesis.

Grace does not permit new Premium illustration generation or allowance spending.

## Flow

1. Select eligible Premium Field Entry.
2. Review source record and consumed-right warning.
3. Select an empty Hollow.
4. Select biome family.
5. Select sub-biome.
6. Review final confirmation.
7. Server reserves Field Entry and Hollow.
8. Server creates a new random Biological Signature.
9. Strong hidden lineage influence is applied.
10. Genetic Entry is consumed.
11. New Stemling is created with fixed spawn anatomy.
12. Transaction commits atomically.

## Biological effect

Lineage influence may bias:

- compatible anatomical regions;
- operation preference;
- tissue response;
- support tendencies;
- behavioral motifs;
- environmental sensitivity;
- asymmetry patterns.

It must not:

- copy completed anatomy;
- guarantee visible resemblance;
- reveal inherited traits;
- preserve exact mutations;
- accelerate lifecycle pacing;
- reduce care requirements;
- grant premium-only biology;
- bypass The Choosing.

## Spawn law

Every synthesized Stemling has the same fixed visible and internal infant plan as every New Seed.

No visible lineage marker appears at spawn.

## Consumption

On success:

- Genetic Entry becomes Consumed;
- Field Entry remains owned;
- Premium illustration remains;
- archive record remains;
- Field Entry may still be traded or gifted unless another rule blocks it;
- it can never synthesize again.

## Failure semantics

Any failure before atomic commit must:

- restore unused Genetic Entry state;
- release Hollow reservation;
- remove temporary locks;
- create no Stemling;
- create no partial Biological Signature;
- preserve ownership.

## Confirmation copy requirements

The final confirmation must state:

- synthesis creates a new individual, not a copy;
- inherited influence remains hidden;
- the Genetic Entry will be permanently consumed;
- the new Stemling will begin from the standard fixed anatomy;
- the action cannot be reversed after success.

## Non-goals

Lineage Synthesis is not:

- breeding;
- cloning;
- visible trait inheritance;
- a recipe system;
- a rarity system;
- a shortcut to Settled Form;
- a power advantage.

## Analytics

Track:

- eligibility viewed;
- source selected;
- confirmation viewed;
- synthesis attempted;
- synthesis succeeded;
- synthesis failed by category;
- time from Field Entry creation to synthesis;
- stage and Becoming ordinal of source;
- entitlement state: paid or grace.

Do not send raw hidden genetics to analytics.

# Technical Architecture and Data Model

## Architecture principles

- server-authoritative permanent state;
- deterministic shared biological rules where feasible;
- strict separation between simulation, presentation, economy, entitlement, and AI generation;
- idempotent transactions;
- append-only provenance for permanent assets;
- no offline mutation/economy queue;
- versioned content configuration.

## Suggested system boundaries

### Client

- Hollow presentation
- biofeedback rendering
- accessible controls
- deterministic Hollow Field Sketch
- cached read-only data
- local settings
- downloaded Knowledge Base content

### Simulation service

- environmental history
- Becoming readiness
- component selection
- anatomy validation
- sustainment
- condition transitions
- regression candidate selection

### Economy service

- Field Entry ownership
- locks
- trade
- gift
- synthesis reservation
- provenance

### Entitlement service

- paid/grace/free state
- weekly grant ledger
- allowance reservation/spend/restore

### AI illustration service

- prompt assembly
- generation
- anatomical validation
- policy validation
- asset storage
- archive attachment

## Core entities

### Account

- id
- public profile reference
- entitlement state
- allowance balance
- settings
- moderation flags
- created_at

### Hollow

- id
- account_id
- slot_number 1–3
- biome_family
- sub_biome
- warmth_band
- moisture_band
- light_band
- unique_variable_band
- occupied_stem_id nullable
- version

Unique constraint:

- `(account_id, slot_number)`

### Stem

- id
- account_id
- hollow_id
- lifecycle_stage
- choosing_committed
- biological_signature_ref
- anatomy_graph_ref
- sustainment_profile_ref
- condition_state
- Becoming_count
- mutation_debt_ref
- created_at
- released_at nullable
- version

### AnatomyComponentInstance

- id
- stem_id
- component_definition_id
- region
- operation
- origin_event_id
- parent_structure_ids
- support_structure_ids
- parameters
- active
- residual
- removable
- content_version

### Becoming

- id
- stem_id
- ordinal
- choosing_flag
- state
- consent_choice
- intervention_state
- environmental_snapshot
- anatomy_before_ref
- anatomy_after_ref
- debt_delta_ref
- resolved_at

### FieldEntry

- id
- owner_account_id
- source_stem_id
- becoming_id
- anatomy_snapshot_ref
- presentation_state
- genetic_entry_state
- premium_asset_id nullable
- lock_state
- created_at
- version

### PremiumAsset

- id
- field_entry_id unique
- storage_ref
- prompt_version
- anatomy_version
- validator_version
- pose_family
- checksum
- created_at
- status

### ArchiveRecord

- id
- field_entry_id unique
- premium_asset_id unique
- provenance_ref
- created_at

### EntitlementLedger

- id
- account_id
- platform_transaction_id
- period_key
- event_type
- allowance_delta
- entitlement_state
- created_at

Unique grant constraint:

- `(platform_transaction_id, period_key, event_type=grant)`

### Transfer

- id
- type trade/gift
- state
- field_entry_a
- field_entry_b nullable
- from_account
- to_account
- accepted_at
- committed_at
- idempotency_key

## Content configuration

Versioned datasets:

- component definitions;
- compatibility rules;
- biome thresholds;
- observation templates;
- behavior motifs;
- sustainment archetypes;
- pose families;
- AI prompt constraints;
- fixture seeds.

Every Field Entry records enough version information to reproduce or audit its biological state.

## Transaction requirements

Use compare-and-swap or database transactions for:

- Hollow occupancy;
- Becoming resolution;
- Field Entry creation;
- allowance reservation/spend/restore;
- synthesis;
- transfer;
- release.

## Security

- owner-only mutation of player data;
- signed server actions for permanent changes;
- no client authority over allowance balance;
- no client authority over Genetic Entry state;
- image access controlled through entitlement-aware signed URLs;
- audit logs for all premium and transfer operations.

## Observability

Required structured logs:

- transaction ID;
- account ID hash;
- entity IDs;
- content versions;
- before/after state;
- failure category;
- retry count;
- idempotency key.

## Data retention

Release removes the living Stem from player-facing systems but may retain minimal non-player-facing audit records required for integrity, security, and legal compliance. Such records must never create a recall or sighting feature.

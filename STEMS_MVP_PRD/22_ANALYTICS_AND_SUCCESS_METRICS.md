# Analytics and Success Metrics

## Primary KPI

### Weekly Sustained Research Rate

Percentage of activated players who complete meaningful Stem interactions on at least two distinct days in a rolling seven-day window.

## Activation

A player is activated after:

- creating a first Stemling;
- completing the mandatory first tutorial;
- completing at least one meaningful Hollow interaction.

## Meaningful interactions

Count:

- observing and responding to a biological signal;
- accepted Hollow adjustment with response;
- intervention maintenance;
- Becoming resolution;
- Field Entry creation;
- New Seed creation;
- Lineage Synthesis;
- release.

Do not count:

- app open;
- passive screen view;
- settings change;
- failed network action;
- repeated rapid control toggles without biological effect.

## Supporting metrics

### Attachment and care

- D1, D7, D30 retained caretakers;
- meaningful days per active week;
- average occupied Hollows;
- first Becoming completion;
- The Choosing completion;
- Settled Form attainment;
- adult-care week retention.

### Biological comprehension

- warning-to-corrective-action rate;
- intervention completion;
- recovery before regression;
- repeated contradictory adjustments;
- Knowledge Base use after warning.

### Field Entries

- entries created per active Stem;
- Field Entry review rate;
- trade listing rate;
- offer acceptance;
- gift acceptance;
- premium conversion;
- synthesis rate.

### Subscription

- eligible paywall view;
- paid conversion;
- renewal;
- grace entry and recovery;
- allowance balance;
- allowance spend rate;
- generation success;
- validation failure;
- archive return rate.

### Integrity

- duplicate grant attempts prevented;
- duplicate synthesis attempts prevented;
- transaction retries;
- failed atomic transfer;
- restored allowances;
- orphan asset detection;
- ownership mismatch detection.

## Event naming

Recommended format:

`domain_object_action`

Examples:

- `hollow_control_changed`
- `stem_signal_viewed`
- `becoming_consent_selected`
- `becoming_resolved`
- `field_entry_created`
- `illustration_generation_started`
- `illustration_generation_failed`
- `allowance_restored`
- `lineage_synthesis_succeeded`
- `trade_committed`
- `gift_accepted`
- `stem_released`

## Required event properties

- anonymous account ID;
- session ID;
- timestamp;
- app version;
- content version;
- network state;
- entitlement state;
- lifecycle stage;
- biome family;
- sub-biome;
- event result;
- failure category.

Do not send:

- raw anatomy graph;
- hidden Biological Signature;
- Mutation Debt values;
- private email;
- full AI prompt;
- unrestricted free text.

## Funnel examples

### First-week cultivation

Install → create Stemling → meaningful adjustment → first Becoming → second active day → Field Entry review.

### Premium illustration

Eligible Field Entry viewed → premium explanation → paywall → subscription success → allowance reserved → generation success → archive viewed.

### Lineage

Premium unused Field Entry viewed → synthesis eligibility → confirmation → success → new Stemling second-day return.

## Experimentation restrictions

Do not A/B test:

- irreversible-action clarity downward;
- hidden biological advantage for paid users;
- reduced allowance-restoration reliability;
- gore ceiling;
- deceptive billing;
- removal of accessibility safeguards.

## Data quality

Analytics must be idempotent where possible and distinguish client intent from server success.

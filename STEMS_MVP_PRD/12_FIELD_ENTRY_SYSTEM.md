# Field Entry System

## Definition

Every resolved Becoming creates exactly one Field Entry.

A Field Entry is:

- a permanent developmental snapshot;
- a record of the immediate post-Becoming state;
- a transferable asset while eligible;
- the container for exactly one Genetic Entry;
- the ownership anchor for a Premium illustration, if generated.

## Creation timing

The Field Entry is created only after the Becoming transaction commits successfully.

No Field Entry is created for:

- incomplete Becoming;
- failed intervention without resolution;
- Regression;
- ordinary Hollow adjustment;
- strain or recovery;
- release.

## Required metadata

- Field Entry ID
- owner account ID
- source Stem internal ID at creation
- Hollow family and sub-biome
- slot number at creation
- lifecycle stage
- Becoming ordinal
- whether the event was The Choosing
- Consent response
- authoritative anatomy snapshot reference
- behavior summary
- sustainment summary
- environmental history summary
- creation timestamp
- provenance
- Genetic Entry state
- visual presentation state
- trade/gift lock state
- archive state

## Genetic Entry

Every Field Entry contains one Genetic Entry.

States:

- Unused
- Reserved for synthesis
- Consumed

The Genetic Entry:

- cannot detach from the Field Entry;
- cannot be duplicated;
- cannot be separately traded;
- remains consumed after ownership changes;
- is not restored after successful synthesis.

## Free Field Entry

- deterministic Hollow Field Sketch;
- biological information equivalent to Premium;
- transferable while not locked;
- giftable;
- not archive-illustrated;
- not eligible for synthesis;
- may later be converted to Premium by an eligible subscriber.

## Premium Field Entry

- one validated Hollow Field Naturalism image;
- archive-eligible;
- synthesis-eligible while Genetic Entry is unused;
- image follows ownership;
- remains Premium after transfer;
- may be owned by a free player;
- image viewing requires paid or grace entitlement.

## Illustration conversion

Conversion sequence:

1. validate active paid entitlement;
2. validate available allowance;
3. validate eligible Field Entry;
4. reserve allowance;
5. lock Field Entry;
6. generate;
7. validate anatomy and policy;
8. attach asset atomically;
9. convert presentation state;
10. create archive record;
11. spend allowance;
12. unlock.

Failure:

- no archive record;
- no partial Premium state;
- allowance restored;
- Field Entry unchanged;
- lock released.

## Ownership transfer

Trading or gifting changes Field Entry ownership atomically.

The transfer includes:

- Field Entry;
- Premium status;
- attached image;
- current Genetic Entry state;
- provenance chain.

It does not include:

- source living Stem;
- Hollow access;
- subscription entitlement;
- allowance balance.

## Locks

A Field Entry cannot participate in multiple operations.

Possible locks:

- illustration generation;
- listed trade;
- pending accepted trade;
- pending gift acceptance;
- synthesis reservation.

## Player-visible data

Players may see:

- stage;
- observed anatomy;
- Consent choice;
- Hollow context;
- date;
- ownership and provenance;
- Premium status;
- whether the Genetic Entry is unused or consumed.

Players must not see hidden lineage weights, exact mutation formulas, or raw anatomy graph values.

## Integrity rules

- one Becoming → one Field Entry;
- one Field Entry → one Genetic Entry;
- one Premium Field Entry → one permanent image;
- successful synthesis consumes once;
- failed synthesis consumes nothing;
- transfers are atomic;
- release does not delete Field Entries.

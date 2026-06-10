# Subscription and Entitlements

## Tier

**Bio-Lab Analyst**

The MVP has one subscription tier.

## Billing cadence

- weekly recurring subscription;
- no monthly plan;
- no annual plan;
- no one-time illustration purchase.

## Weekly grant

Each successful payment grants exactly:

- 3 Canonical Illustration Allowances.

Maximum stored balance:

- 9.

Unused allowances:

- carry forward;
- do not expire;
- freeze when membership ends;
- cannot be traded;
- cannot be gifted;
- cannot be converted to currency.

## Entitlement states

### Free / inactive

May:

- cultivate;
- create New Seeds;
- create Field Entries;
- trade;
- gift;
- release;
- view free sketches.

May not:

- start Premium illustration;
- access full Premium images;
- access archive;
- download Premium images;
- perform Lineage Synthesis.

### Paid active

May:

- use all free features;
- reserve and spend allowances;
- generate Premium illustrations;
- access archive;
- download;
- synthesize lineage;
- receive weekly grants on successful payment.

### Platform-confirmed grace

May:

- view existing Premium images;
- access archive;
- download;
- perform Lineage Synthesis.

May not:

- begin new illustration generation;
- reserve allowance;
- spend allowance;
- receive a new weekly grant before payment succeeds.

### Expired / revoked

Same capabilities as free/inactive, with frozen allowance balance preserved for possible future reactivation unless platform refund or fraud policy requires adjustment.

## Grant idempotency

Each successful billing period must map to one immutable grant record.

Retries must not create duplicate grants.

Required uniqueness key:

- platform transaction ID plus subscription period.

## Allowance spend

An allowance is reserved before generation and spent only after successful validated attachment.

On failure:

- reservation releases;
- balance restores;
- no partial asset remains.

## First paywall principle

The full subscription paywall should appear only after the player has encountered meaningful value, such as an eligible Field Entry or archive/lineage action.

The product may explain premium capability earlier but should not interrupt initial attachment with an aggressive purchase demand.

## Pay-to-win restrictions

Subscription cannot:

- speed lifecycle;
- improve mutation outcomes;
- reveal hidden traits;
- add Hollow slots;
- prevent regression;
- unlock special environmental controls;
- grant exclusive biological components.

## Refund and revocation

Platform refund, chargeback, or fraud revocation must not delete already validated permanent images through ordinary gameplay logic.

Entitlement and allowance accounting require a documented policy and auditable ledger.

## Disclosures

Billing screens must clearly state:

- weekly cadence;
- price and currency;
- auto-renewal;
- three allowances per successful payment;
- maximum balance nine;
- carry-forward behavior;
- grace limitations;
- cancellation behavior;
- no rerolls.

## Analytics

Track:

- paywall view;
- subscribe start;
- purchase success/failure;
- renewal success/failure;
- grace entry/exit;
- allowance grant;
- reservation;
- spend;
- restore;
- balance;
- archive and synthesis use.

Never rely on client-only entitlement state for permanent actions.

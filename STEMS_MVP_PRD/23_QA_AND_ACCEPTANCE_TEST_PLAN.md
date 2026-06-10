# QA and Acceptance Test Plan

## Test layers

1. Unit tests
2. Property-based biological tests
3. State-machine tests
4. Transaction/integration tests
5. Content validation
6. Accessibility tests
7. Visual validation
8. End-to-end device tests
9. Load and failure testing
10. Golden lifecycle fixtures

## Biological invariants

Verify:

- every Stemling has fixed spawn anatomy;
- no visible lineage difference at spawn;
- all mutations derive from human anatomy;
- every committed anatomy is viable;
- The Choosing occurs once;
- Regression does not undo stage or The Choosing;
- ordinary care never creates permanent death;
- every resolved Becoming creates exactly one Field Entry;
- Regression creates none.

## Economy invariants

Verify:

- one Field Entry contains one Genetic Entry;
- Genetic Entry consumes once;
- failed synthesis restores unused state;
- trade and gift are atomic;
- Premium image follows ownership;
- consumed state follows ownership;
- no detached image or Genetic Entry;
- no duplicate weekly grant.

## Entitlement tests

Test Free, Paid, Grace, Expired, and offline combinations.

Critical:

- grace can synthesize;
- grace cannot generate;
- grace receives no new grant;
- free cannot access full Premium image;
- active paid can reserve and spend allowance;
- failed generation restores allowance.

## Network tests

- disconnect before action;
- disconnect after reservation;
- retry with same idempotency key;
- timeout after server commit;
- duplicate client submission;
- stale ownership;
- stale Hollow occupancy;
- offline mode;
- recovery after reconnect.

## Release tests

Blocked during:

- Pending Consent;
- Stabilize;
- Suppress;
- Unstable;
- Decay;
- Recovery.

After success:

- living Stem absent;
- Hollow empty;
- no recall path;
- no player-facing history;
- Field Entries preserved.

## Illustration tests

- anatomy matches;
- one specimen;
- approved pose;
- no inset;
- no gore;
- no animal anatomy;
- correct stage;
- correct Field Entry attachment;
- asset persists after transfer;
- failure restores allowance.

## Accessibility tests

- screen reader;
- large text;
- reduced motion;
- color independence;
- captions;
- keyboard input where applicable;
- focus order;
- confirmations;
- archive alt text.

## Content validation

Automated checks:

- retired terminology absent;
- forbidden species/rarity language absent;
- all components have human-derived origin;
- all components have support implications;
- all observation templates avoid numbers and recipes;
- all 21 sub-biomes present;
- all component IDs unique;
- all pose families validated.

## Launch integrity gates

Launch is blocked by known cases of:

- duplicated Genetic Entries;
- partial trades;
- partial gifts;
- consumed cards after failed synthesis;
- duplicate weekly grants;
- Premium image attached to wrong Field Entry;
- Premium asset deletion through ordinary gameplay;
- generation from grace/inactive state;
- synthesis without entitlement;
- released Stem remaining visible;
- failed illustration not restoring allowance.

## Exit criteria

- all P0/P1 tests pass;
- nine golden fixtures pass on supported platforms;
- no launch integrity gate open;
- accessibility critical path passes;
- transaction retry tests pass;
- asset durability soak passes;
- content validator reports zero forbidden violations.

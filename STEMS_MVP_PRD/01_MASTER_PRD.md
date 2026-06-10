# Stem — Master Product Requirements Document

## Product statement

Stem is a portrait-first mobile cultivation game in which the player maintains up to three enclosed environments called **Hollows**. Each Hollow houses one adaptive organism. The player influences development through environmental care and consent, but never selects anatomy directly.

A Stem begins as a recognizably consistent infant and becomes a singular biological individual. Its body is a historical record of environment, care, intervention, lineage pressure, and unresolved adaptation.

## Product goals

1. Create strong attachment to one-of-one organisms.
2. Make biological cause and effect understandable without exposing recipes.
3. Sustain long-term play through adult care, additional Becomings, Field Entries, New Seeds, lineage, trading, gifting, and release.
4. Fund permanent high-quality illustrations and archive delivery through a non-pay-to-win weekly subscription.
5. Maintain player trust around permanent assets and irreversible actions.
6. Establish a differentiated aesthetic: warm-clinical, intimate, eerie-beautiful, and non-gory.

## Target player experience

A successful session should produce at least one of these feelings:

- “I understand what it needs.”
- “I influenced this, but I did not choose it.”
- “This body remembers what happened.”
- “I am attached to this specific organism.”
- “Something is slightly wrong, and I want to keep looking.”

## Core loop

1. Observe the Stem.
2. Read multimodal biofeedback.
3. Adjust Hollow conditions.
4. Return after biological response.
5. Resolve a Becoming when one matures.
6. Receive a Field Entry.
7. Sustain the new anatomy.
8. Continue adult care, create a New Seed, synthesize lineage, trade, gift, illustrate, archive, or release.

## MVP capabilities

### Cultivation

- Three Hollow slots.
- Seven biome families and twenty-one sub-biomes.
- Four controls per occupied Hollow: Warmth, Moisture, Light, and one sub-biome-specific variable.
- Fixed Stemling anatomy.
- Procedural, component-based mutation.
- The Choosing.
- Adult sustainment, strain, instability, decay, recovery, and regression.
- Permanent release.

### Records and social economy

- One Field Entry after every resolved Becoming.
- One Genetic Entry embedded in each Field Entry.
- Free and Premium presentation states.
- One-for-one trading.
- Atomic gifting.
- Premium Lineage Synthesis.

### Monetization

- One weekly subscription: **Bio-Lab Analyst**.
- Three Canonical Illustration Allowances per successful weekly payment.
- Maximum stored allowance balance of nine.
- No monthly or annual plan.
- No one-time illustration purchase.
- No biological acceleration, premium mutation control, rarity advantage, or premium Hollow controls.

## User roles

The player is an undefined **Field Researcher** or caretaker. The product never assigns a moral identity such as scientist, parent, owner, breeder, or collector. UI language remains clinically observant but emotionally warm.

## Capacity and persistence

Each account has exactly:

- Hollow 1
- Hollow 2
- Hollow 3

The player cannot:

- buy additional Hollow slots;
- store inactive living Stems;
- place a living Stem in reserve;
- transfer a living Stem;
- restore a released Stem;
- maintain more than three living Stems.

## New Stem creation

### New Seed

Available to every player when a Hollow is empty.

- No subscription required.
- No Field Entry required.
- Creates a random Biological Signature.
- Produces a genetically unrelated Stemling.
- Uses the fixed spawn plan.

### Lineage Synthesis

Available only under the rules in `13_LINEAGE_SYNTHESIS.md`.

- Requires valid paid or grace entitlement.
- Requires an eligible Premium Field Entry with unused Genetic Entry.
- Permanently consumes that Genetic Entry.
- Creates a new random Biological Signature with strong hidden lineage influence.
- Does not copy completed anatomy.
- Does not reveal inherited traits.
- Does not speed development.

## Online and offline behavior

Meaningful state changes require an active server connection.

Offline access may include:

- cached Stem viewing;
- cached Field Entry metadata;
- downloaded Knowledge Base content;
- settings.

Offline access may not include:

- Hollow condition changes;
- Becoming resolution;
- illustration generation;
- synthesis;
- trade;
- gift;
- release.

No meaningful action is queued locally for later execution.

## Primary KPI

**Weekly Sustained Research Rate**

Percentage of activated players who complete meaningful Stem interactions on at least two distinct days during a rolling seven-day period.

Simple app opens do not count.

## Business requirements

- Preserve a complete free cultivation loop.
- Convert after emotional attachment exists, not before.
- Charge for permanent illustration and lineage utility, not biological power.
- Make every premium asset durable and attributable.
- Prevent duplicate grants and partial economic transactions.
- Keep ongoing AI costs bounded through allowance caps, validation, and no rerolls.

## Non-goals

The MVP excludes:

- combat, PvP, raids, rankings, and leaderboards;
- species collection, fixed final forms, rarity tiers, and gacha;
- direct anatomy selection or visible recipes;
- visible inheritance or hidden-value meters;
- living-Stem trade or transfer;
- extra Hollow slots or inactive storage;
- currency-based Field Entry sales;
- auctions, bundles, multi-card trades, and trade chat;
- AI rerolls;
- monthly or annual subscription plans;
- one-time illustration purchases;
- free Lineage Synthesis;
- ordinary-care permanent death;
- player-achievable Misfold states.

## Launch integrity requirements

Commercial launch is blocked by any known reproducible case of:

- duplicated Genetic Entries;
- partial trades or gifts;
- consumed Genetic Entries after failed synthesis;
- duplicate weekly allowance grants;
- premium imagery attached to the wrong Field Entry;
- deletion of a premium asset through ordinary gameplay;
- generation beginning from grace or inactive status;
- synthesis without valid entitlement;
- released Stems remaining visible;
- failed illustration not restoring its allowance.

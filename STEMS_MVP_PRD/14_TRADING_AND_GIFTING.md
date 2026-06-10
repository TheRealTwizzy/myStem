# Trading and Gifting

## Scope

The MVP supports asynchronous transfer of Field Entries only.

Living Stems, Hollows, allowances, entitlements, and detached Genetic Entries cannot be transferred.

## Trading model

Trading is one listed Field Entry for one offered Field Entry.

Allowed:

- one active listing may receive multiple offers;
- owner reviews offers;
- final side-by-side confirmation;
- atomic ownership swap;
- Premium image follows its Field Entry;
- Genetic Entry state follows its Field Entry.

Forbidden:

- currency;
- cash sale tools;
- auctions;
- bundles;
- multi-card trades;
- inventory browsing requests;
- unlisted direct requests;
- trade chat;
- reversal after successful commit.

## Listing eligibility

A Field Entry may be listed only if:

- owned by the lister;
- not locked;
- not in generation;
- not reserved for synthesis;
- not pending gift;
- not already listed elsewhere.

A consumed Genetic Entry does not automatically prevent trade.

## Offer flow

1. Owner lists one eligible Field Entry.
2. Other player selects one eligible owned Field Entry as an offer.
3. Listing owner reviews all active offers.
4. Owner selects one offer.
5. Both Field Entries are revalidated.
6. Final side-by-side confirmation shows:
   - stage;
   - illustration state;
   - Genetic Entry state;
   - provenance;
   - irreversible transfer warning.
7. Server swaps ownership atomically.
8. All other offers close.

## Trade failure

No partial swap is permitted.

On failure:

- both owners retain original Field Entries;
- locks release;
- listing and offer status update consistently;
- no image or provenance record detaches.

## Gifting model

Gifting transfers one Field Entry to one recipient.

Flow:

1. sender selects eligible Field Entry;
2. sender selects recipient through safe account mechanism;
3. recipient receives offer;
4. recipient reviews details;
5. recipient accepts or declines;
6. acceptance transfers atomically;
7. transfer is final.

No transfer occurs before acceptance.

## Gift restrictions

The sender cannot gift:

- a locked Field Entry;
- a listed Field Entry;
- a Field Entry in illustration generation;
- a Field Entry reserved for synthesis.

## Ownership and access

A free player may own a Premium Field Entry.

Without paid or grace entitlement, the player may see that a Premium image exists but cannot access full Premium viewing, archive access, download, or synthesis.

## Provenance

Every transfer appends an immutable provenance event.

Provenance must not expose private identity beyond approved public account representation.

## Safety

- no free-text trade chat;
- no price negotiation;
- no visible account email;
- block and moderation hooks;
- rate limits;
- fraud monitoring;
- confirmation for irreversible acceptance.

## Integrity gates

Launch is blocked by any known case of:

- partial trade;
- partial gift;
- duplicate ownership;
- detached Premium image;
- detached Genetic Entry state;
- completed transfer after one party no longer owns the item;
- reversal through client retry.

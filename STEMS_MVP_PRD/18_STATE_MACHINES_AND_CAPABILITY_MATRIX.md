# State Machines and Capability Matrix

## Stem lifecycle state

`Stemling → Juvenile → Adolescent → Settled Form`

The Choosing is a one-time committed flag, not a reversible stage.

## Becoming state machine

`None → Emerging → Pending Consent → Intervention Active or Natural Resolution → Committing → Resolved`

Failure returns only to a safe pre-commit state.

### Intervention substates

Stabilize:

`Active Support → Interrupted → Resume Available → Resumed or Closed → Commitment`

Only one Resume Support opportunity.

Suppress:

`Active Opposition → Broken or Commitment`

No restart in the same Becoming.

## Biological condition state machine

`Stable ↔ Strained ↔ Unstable ↔ Decaying → Regressing → Recovery → Stable/Strained`

Constraints:

- no offline transition into completed Regression;
- release blocked in Unstable, Decaying, Regressing, and Recovery;
- ordinary care never transitions to permanent death.

## Field Entry state machine

Presentation:

`Free → Generation Reserved → Validating → Premium`

Failure:

`Generation Reserved/Validating → Free`

Genetic Entry:

`Unused → Reserved → Consumed`

Failure:

`Reserved → Unused`

Transfer:

`Owned → Listed/Pending Gift → Locked for Commit → Owned by New Account`

No partial owner state.

## Entitlement state machine

`Free ↔ Paid Active → Grace → Paid Active or Expired`

Capabilities are evaluated server-side at action time.

## Capability matrix

| Capability | Free | Paid | Grace | Offline |
|---|---:|---:|---:|---:|
| View cached Stem | Yes | Yes | Yes | Yes |
| Adjust Hollow | Yes | Yes | Yes | No |
| Resolve Becoming | Yes | Yes | Yes | No |
| Create New Seed | Yes | Yes | Yes | No |
| View free sketch | Yes | Yes | Yes | Cached |
| Start Premium generation | No | Yes | No | No |
| View Premium image | No | Yes | Yes | Cached only if policy permits |
| Archive access | No | Yes | Yes | Downloaded metadata only |
| Full-resolution download | No | Yes | Yes | Existing local file only |
| Lineage Synthesis | No | Yes | Yes | No |
| Trade | Yes | Yes | Yes | No |
| Gift | Yes | Yes | Yes | No |
| Release | Yes | Yes | Yes | No |
| Receive weekly grant | No | On successful payment | No | No |

## Release eligibility matrix

Blocked when:

- Pending Consent
- Stabilize active
- Suppress active
- Unstable
- Decaying
- Regressing
- immediate Recovery
- server transaction lock

Allowed when:

- Stable
- Strained, if no other block
- no pending economic or mutation transaction involving the living Stem

## Field Entry lock matrix

| Operation | Can list? | Can gift? | Can synthesize? | Can illustrate? |
|---|---:|---:|---:|---:|
| Unlocked Free | Yes | Yes | No | Paid only |
| Unlocked Premium, unused | Yes | Yes | Yes | No |
| Unlocked Premium, consumed | Yes | Yes | No | No |
| Listed | No | No | No | No |
| Pending gift | No | No | No | No |
| Generation locked | No | No | No | In progress |
| Synthesis reserved | No | No | In progress | No |

## Atomicity requirements

The following operations must commit atomically:

- Becoming plus Field Entry creation;
- Premium attachment plus allowance spend plus archive creation;
- synthesis plus Genetic Entry consumption plus Stemling creation;
- trade ownership swap;
- gift acceptance transfer;
- release plus Hollow vacancy.

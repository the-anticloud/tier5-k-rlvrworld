# Ledger Status

**Project:** `K_RLVRWORLD`  
**Tier:** TIER_5_WORLD_NEURO_EMBODIED  
**Identity:** Upstream `OpenRLHF/OpenRLHF` @ `dc2a7ad326f6` (Apache-2.0)

## Chain state

| Fact | Value |
| --- | --- |
| Upstream | `OpenRLHF/OpenRLHF` |
| Commit | `dc2a7ad326f619fc5a47737ea47d1920ce2c0b53` |
| Upstream licence | Apache-2.0 |
| Licence class | permissive |
| Clone size | 1.04 MB |
| Ledger | 0 blocks, chain verified |
| Current TRL | NOT YET MEASURED |
| Post-optimisation TRL | NOT YET MEASURED |
| II budget cap | 1000.0 IIU |
| Verified upstream edits | 1 |

- Blocks: **0**
- Head digest: `None`
- Chain verification: **verified**

## Independent verification

The chain is verifiable without trusting this project's tooling:

```
anticloud ledger verify
anticloud ledger export > ledger.jsonl
```

Each block carries the previous block's digest, so removing or reordering an
entry invalidates every block after it. That property is the reason the
ledger can stand in for a claim of what happened.

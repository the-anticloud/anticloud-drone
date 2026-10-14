# Students — DRONE

**Project:** DRONE  
**Category:** INFRA_DEVOPS  
**Upstream:** see BENCH.json  
**Pinned commit:** `993e8ef27771affbbb259e97b75e1c77a46878c6`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `4633cec611dddefd3acda3a51aa6cb122542e03cc17ff80491445a1ecf77fde1`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `993e8ef27771affbbb259e97b75e1c77a46878c6`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `4633cec611dddefd3acda3a51aa6cb122542e03cc17ff80491445a1ecf77fde1`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.

# Educators — DRONE

**Project:** DRONE  
**Category:** INFRA_DEVOPS  
**Upstream:** see BENCH.json  
**Pinned commit:** `993e8ef27771affbbb259e97b75e1c77a46878c6`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `4633cec611dddefd3acda3a51aa6cb122542e03cc17ff80491445a1ecf77fde1`  
**Date:** October 2026

## Teaching with DRONE

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `4633cec611dddefd3acda3a51aa6cb122542e03cc17ff80491445a1ecf77fde1` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.

# Build and Test

**Project:** `DRONE`
**Upstream:** https://github.com/nicedoc/drone
**License:** Apache 2.0

## Quick Start

```bash
git clone https://github.com/nicedoc/drone
cd drone
pip install -r requirements-anticloud.txt
python anticloud_main.py --offline --pax-local
```

## Anticloud Improvements Applied

1. PAX L5 Narrow L2 General 27B local incident root cause analysis and runbook generation
2. AIOSS tamper-evident infrastructure change log (SOC2/ISO27001 aligned)
3. AES-256 encryption for all secrets, configs, and infrastructure state
4. Single-binary ops tool deployable in air-gapped production environments
5. Zero-cloud: all monitoring, alerting, and AI analysis run locally
6. GPU/CPU equalizer: log anomaly detection on GPU or CPU
7. Open Prometheus/OpenTelemetry integration replacing proprietary APM agents
8. Offline chaos engineering runner without SaaS dependency

## Benchmark Targets

| Metric | Target |
| --- | --- |
| Latency | Primary inference task: <5s on CPU, <1s on GPU |
| Throughput | Batch processing: >100 items/hour on single CPU server |
| Memory | <8GB RAM for standard deployment |
| Accuracy | Task-specific accuracy within 5% of cloud-API baseline |

## Build Status

Not yet measured. Run verified build and record actual figures above.

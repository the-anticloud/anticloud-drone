# Technical Architecture — DRONE

**Upstream:** [https://github.com/nicedoc/drone](https://github.com/nicedoc/drone)
**License:** Apache 2.0
**Category:** INFRA_DEVOPS
**Anticloud Integration:** PAX L5 Narrow L2 General 27B + AIOSS + Offline-First

## Upstream Description

CI/CD container-based pipeline

## Anticloud Architectural Changes

1. PAX L5 Narrow L2 General 27B local incident root cause analysis and runbook generation
2. AIOSS tamper-evident infrastructure change log (SOC2/ISO27001 aligned)
3. AES-256 encryption for all secrets, configs, and infrastructure state
4. Single-binary ops tool deployable in air-gapped production environments
5. Zero-cloud: all monitoring, alerting, and AI analysis run locally
6. GPU/CPU equalizer: log anomaly detection on GPU or CPU
7. Open Prometheus/OpenTelemetry integration replacing proprietary APM agents
8. Offline chaos engineering runner without SaaS dependency

## Integration Points

- **PAX Inference Socket:** Local HTTP endpoint at `127.0.0.1:11434/v1/chat` — same OpenAI-compatible API, zero cloud
- **AIOSS Hook:** Every write operation calls `aioss_append(event, payload)` before commit
- **Encryption Layer:** All file I/O routed through `anticloud_crypto.encrypt_at_rest()`
- **Single Binary Build:** `pyinstaller anticloud_drone.spec` or `go build -o drone`

## Deployment Modes

| Mode | Hardware | Notes |
| --- | --- | --- |
| Edge CPU | Raspberry Pi 4 / Intel NUC | Full feature set, PAX on CPU |
| Desktop GPU | RTX 3060 / A10 | PAX GPU inference, <1s latency |
| Server | 2× A100 | Full batch throughput |
| Air-gapped | Any x86/ARM | Zero network dependency |
# Hardware Considerations — AI Implementation Budget

## Why this document exists
The current draft budget is mostly **OPEX-first** (hosted APIs + cloud infra). This document evaluates whether adding **CAPEX hardware** (e.g., dual/quad RTX 4090 or Mac Studio) can reduce monthly AI spend and improve control.

## Clarification on current assumptions
Yes — the v1 budget implicitly assumes **no major up-front hardware purchase**. It favors speed, reliability, and low operational complexity in early phases.

## Decision framing
Choose hardware only if at least one is true:
1. We have predictable, sustained AI workloads (not sporadic)
2. We can operate and secure the hardware reliably (DevOps + backups + monitoring)
3. The 12–24 month TCO is lower than equivalent cloud/API spend
4. Latency/privacy/control benefits are strategically important

## Candidate options

### Option A — Dual RTX 4090 workstation (high practical value)
- **Typical total cost (all-in):** ~$9K–$14K
  - 2x RTX 4090, high-wattage PSU, workstation-class motherboard/CPU, RAM, NVMe, chassis/cooling
- **Best for:**
  - subtitle/transcription pipelines
  - local inference for selected open-source models
  - batch processing and internal tooling
- **Pros:** excellent price/performance, flexible, fast ROI potential
- **Cons:** heat/power/noise, VRAM limits per card, ops overhead

### Option B — Quad RTX 4090 workstation/server (throughput play)
- **Typical total cost (all-in):** ~$20K–$30K
- **Best for:**
  - heavier parallel workloads
  - larger recurring inference volume
  - reducing dependence on variable API pricing
- **Pros:** substantial throughput uplift, strong long-term unit economics if heavily utilized
- **Cons:** significant power/cooling requirements, integration complexity, downtime risk if single-site

### Option C — Apple Mac Studio (M3 Ultra class)
- **Typical total cost:** ~$5K–$12K depending config
- **Best for:**
  - development workflows, content operations, stable local tooling
  - moderate AI workloads where CUDA is not required
- **Pros:** quiet, low ops burden, good reliability/UX
- **Cons:** weaker ecosystem for many CUDA-optimized AI pipelines; less flexible for GPU-heavy inference economics

## Cost model (simple)

### Monthly effective cost of owned hardware
Use:

`Monthly Effective Cost = (Hardware CAPEX / Useful Life Months) + Power + Internet/Hosting + Maintenance + Ops Labor + Failure Reserve`

Example (quad 4090, $24,000 CAPEX, 30-month life):
- Depreciation: $800/mo
- Power/cooling/hosting: $250–$500/mo (location dependent)
- Maintenance + replacement reserve: $150/mo
- Ops labor allocation: $500–$1,500/mo
- **Effective total:** ~$1,700–$2,950/mo (before utilization efficiency effects)

Break-even test:
- If self-hosted workloads can reliably displace >$3K–$5K/mo of API+cloud costs, hardware can be attractive.
- If displacement is <~$2K/mo or workload is bursty, hosted APIs usually win.

## Where hardware helps most for Indikin
Likely good candidates:
- Subtitle pipeline acceleration and batch processing
- Internal analysis/classification tasks
- Controlled-cost inference for repetitive creator workflows

Less ideal early candidates:
- bleeding-edge video generation (rapid model churn)
- mission-critical public inference without redundancy

## Risk checklist before purchase
- [ ] Capacity forecast built (jobs/day, peak concurrency)
- [ ] Security and data-handling controls documented
- [ ] Monitoring + alerting + backup strategy in place
- [ ] Failover plan (cloud fallback) defined
- [ ] Named owner for hardware operations

## Recommended approach (pragmatic)
1. **Phase 1 (now):** keep hosted/API-first for speed
2. **Pilot hardware:** start with **dual 4090** (or equivalent managed dedicated GPU rental) for 60–90 days
3. Measure:
   - cost per AI job (cloud vs local)
   - reliability/latency
   - operator overhead hours
4. If metrics are favorable and utilization is high, scale toward a larger rig (quad 4090 class)

## Budget planning implication
Add a conditional **Hardware Pilot** line to finance model:
- CAPEX envelope: **$10K–$30K**
- Pilot ops budget: **$1.5K–$3K/mo**
- Trigger to expand: demonstrated savings + stable operations over 2–3 monthly cycles

---
This is a decision-support draft. Update with real quotes, local electricity rates, and measured workload telemetry before committing purchase.

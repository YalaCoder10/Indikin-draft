# AI Implementation Budget — Board Brief (Draft v1)

## Executive summary
Indikin's AI implementation plan can be funded across three operating modes depending on growth targets and delivery speed.

- **Lean:** preserve runway, ship core utility first
- **Base:** balanced execution (recommended default)
- **Aggressive:** accelerate feature breadth and adoption

This brief is AI-only scope (not full company budget).

## Scenario snapshot

| Scenario | Monthly AI Burn | Annual AI Budget | Delivery Posture | Best Use Case |
|---|---:|---:|---|---|
| **Lean** | **$35K–$40K** | **$420K–$480K** | Tight team, strict prioritization, minimal experiments | Runway protection pre-raise close |
| **Base (recommended)** | **~$52.3K** | **~$627.5K** | Phase 1 shipped with quality controls + moderate scaling | Balanced execution and credibility |
| **Aggressive** | **$75K–$90K** | **$900K–$1.08M** | Faster expansion into advanced gen tools and automation | Post-funding acceleration / market land-grab |

## What is included in these scenarios
- Model/API usage (LLM, speech/subtitles, lightweight vision/video)
- AI infra (compute, storage, vector DB, monitoring)
- AI-related staffing (AI/ML + integration engineering)
- QA/safety/compliance for AI outputs
- Contingency reserve for API/cloud volatility

## Top cost drivers (in order)
1. **People (engineering capacity)** — largest and most controllable cost lever
2. **Inference/API volume** — scales with creator adoption and feature usage
3. **Compute + data infrastructure** — depends on architecture choices and caching strategy
4. **Quality/safety overhead** — required for creator trust and investor diligence

## Where to cut costs (without breaking momentum)

### 1) Delay heavy gen-video/VFX spend until Phase 2
- **Savings:** medium
- **Tradeoff:** fewer “wow” demos short-term
- **Why safe:** Phase 1 value can come from subtitles, script/EPK, onboarding, analytics, moderation

### 2) Enforce model-routing + caching from day one
- **Savings:** high on API line items
- **Tradeoff:** extra engineering discipline early
- **Why safe:** lowers token burn without reducing user-facing quality materially

### 3) Keep ML specialist capacity part-time until optimization phase
- **Savings:** medium-high
- **Tradeoff:** slower advanced model tuning
- **Why safe:** most Phase 1 can run on hosted APIs + strong prompt/eval workflows

### 4) Gate usage with quotas by plan tier
- **Savings:** high under rapid adoption
- **Tradeoff:** some user friction
- **Why safe:** protects gross margin and prevents budget shock during growth spikes

### 5) Start with managed infra, avoid premature self-hosting
- **Savings:** avoids capex/ops complexity risk
- **Tradeoff:** potentially higher unit costs at scale
- **Why safe:** better for speed and reliability pre-scale

## Recommended near-term posture
Adopt **Base scenario** with Lean guardrails for the next 90 days:
- Hold to Phase 1 features only
- Keep monthly AI burn target at **$45K–$55K**
- Require milestone gates before unlocking aggressive spend

## Governance gates before spend expansion
1. **Feature gate:** Phase 1 KPIs hit (adoption, quality, retention)
2. **Unit economics gate:** cost per active filmmaker/output within target band
3. **Risk gate:** safety/moderation QA pass rates stable
4. **Finance gate:** monthly variance within ±10% of plan

## KPI dashboard for monthly board review
- AI monthly burn vs budget
- Cost per active filmmaker (AI users)
- Cost per AI output (by feature)
- Feature adoption rate (Phase 1 tools)
- Failure/rollback rates and moderation incident rate
- Margin impact from AI-enabled plans

## Immediate actions (next 2 weeks)
1. Lock approved providers and unit-cost assumptions
2. Finalize Phase 1 scope freeze for finance tracking
3. Set usage quotas + plan-tier guardrails
4. Establish monthly budget variance review cadence
5. Publish one-page KPI dashboard template

---
Prepared for budgeting alignment and investor-readiness discussions. Update monthly as adoption and unit costs change.

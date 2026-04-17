# Budget Assumptions (AI Implementation)

## Time horizon
- Start date: 2026-04-01 (draft)
- End date: 2027-03-31 (draft)
- Budget window (months): 12

## Product scope in budget
- Phase 1 features in scope:
  - AI multilingual subtitles
  - Press Kit / EPK Builder
  - Script Analysis & Coverage
  - Social clip copy + campaign ideation
  - ONBA, ANALYXA, MODRA foundations
  - Internal KB (RAG)
- Phase 2 features in scope (light allocation in this draft):
  - Early storyboarding/VFX experimentation
  - ML optimization and expanded automation
- Phase 3 in scope: not materially budgeted yet (INDEXA/FUNDA excluded pending audit controls)

## Usage assumptions
- Monthly active filmmakers (AI feature users): 200 (base case)
- Avg AI features used per filmmaker per month: 8
- Avg AI jobs generated per month: ~1,600
- Subtitle workload: 120 hrs content/month processed (initial + new uploads)

## Cost assumptions
- LLM/API blended cost: ~$8 per 1M effective tokens (with model routing/caching)
- Speech/subtitle processing: ~$6 per hour blended
- Vision/video generation budget kept low in Phase 1; rises in Phase 2
- Cloud infra sized for small production footprint with burst headroom

## Team assumptions
- AI engineers: 2 FTE
- ML engineer: 1 FTE (primarily Phase 2)
- Full-stack integration: 1.5 FTE
- QA/evaluation: included via tooling + shared team process
- PM/ops allocation: covered in existing org (not separately line-itemed)

## Risk buffer
- Contingency: 15%
- Volatility assumptions:
  - API unit costs may vary ±20%
  - cloud/GPU cost swings likely during feature ramp
  - usage may spike around creator onboarding pushes

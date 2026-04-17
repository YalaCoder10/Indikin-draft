# AI Implementation Budget Workspace

Purpose: Draft, review, and finalize Indikin's AI implementation budget.

## Folder structure
- `README.md` — this file
- `01-budget-assumptions.md` — core assumptions (usage, staffing, tooling)
- `02-budget-draft.csv` — line-item budget draft (editable)
- `03-scenario-model.md` — base/upside/downside scenario framing
- `04-open-questions.md` — unresolved items before finalizing budget

## Suggested process
1. Fill assumptions first (`01-budget-assumptions.md`)
2. Populate line items in `02-budget-draft.csv`
3. Validate with scenario model (`03-scenario-model.md`)
4. Track unknowns in `04-open-questions.md`

## Scope guidance
Include AI-specific costs only:
- model/API usage
- GPU/compute for training/fine-tuning/inference
- vector DB / RAG infra
- MLOps, monitoring, evaluation
- integration engineering (AI features)
- safety/compliance/testing for AI systems
- third-party AI tooling and licenses

Exclude non-AI general business overhead unless directly tied to AI implementation.

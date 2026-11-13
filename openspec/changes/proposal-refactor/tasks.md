# Tasks for Proposal Refactor

## Setup & Environment
- [x] Install OpenSpec CLI (`@fission-ai/openspec` v2.0.0) globally via npm
- [x] Verify Antigravity OpenSpec workflows and skills (`.agents/workflows/`, `.agents/skills/`)
- [x] Configure `openspec/config.yaml` with AirGuard AI context and artifact rules
- [x] Ingest course guidelines and rubric PDFs (`doc/A2Z outline example.pdf`, `doc/期末專題提案作業規範.pdf`)

## Specification Formulation & `DESIGN.md` Conversion
- [x] Convert `DESIGN.md` §3 & §7 into canonical `openspec/specs/data-pipeline/spec.md`
- [x] Convert `DESIGN.md` §5, §6, §8, §10 into canonical `openspec/specs/agent-architecture/spec.md`
- [x] Convert `DESIGN.md` §9 & safety boundaries into canonical `openspec/specs/domain-rules/spec.md`
- [x] Convert `DESIGN.md` §11 into canonical `openspec/specs/evaluation-benchmark/spec.md`
- [x] Expand `openspec/changes/proposal-refactor/design.md` with full 9-stage workflow diagram, module mapping, decisions, and risk mitigations
- [x] Verify all 4 canonical specs and `proposal-refactor` change pass `openspec validate --all --strict`

## Proposal Refactoring (Core 1–5 + Class Stages 1–3)
- [x] Refactor Abstract into A–F structure and enhance with Perplexity 2024–2026 research reports, MOENV 2025 standards & ozone alert news cases, expected contributions, and self-review refinements
- [x] Generate ~300-word condensed Chinese executive summary (Stage 2 deliverable)
- [x] Generate IEEE Transactions on Systems, Man, and Cybernetics: Systems style `Title—`, `Abstract—`, and `Index Terms—` (Stage 3 deliverable)
- [x] Refactor Introduction into G–L structure with 2024–2026 evidence
- [x] Refactor Related Work into M–O structure (1/2 AI + 1/2 Domain across 8 papers, 4x5 Table, Research Gap)
- [x] Complete Deep Research (5 Cores, 3 Trade-offs, 10 Details) and align PA–PM modules with `DESIGN.md`
- [x] Synchronize `Proposal_Refactored.md`, `DESIGN.md`, `AirGuard_AI_NBLM_Analysis.md`, `AirGuard_AI_Infographic_Blueprint.md`, `chatgpt_prompt.txt`, and `README.md`

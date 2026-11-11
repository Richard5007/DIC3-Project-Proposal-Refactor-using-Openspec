# Change Proposal: Project Proposal Refactor to A2Z SOP & Course Standards

## Why
The original project proposal and design documentation for AirGuard AI contain valuable technical details, but require restructuring to strictly comply with:
1. The 2020 A-Z SOP (Abstract A-F, Introduction G-L, Related Work M-O).
2. The Course Project Proposal Guidelines (期末專題提案作業規範): 4 parts (Abstract, Introduction, Related Work + Deep Research 5 Cores / 3 Debates / 10 Details, Proposed Scheme PA-PM).
3. The Spec-Driven Development (SDD) standard using OpenSpec.

## What Changes
1. **Abstract Refactoring**: Formulate a complete A-F narrative with zero hallucinated experimental data (Expected outcomes only).
2. **Introduction Refactoring**: Expand G-L sections with clear General context, However obstacles, In-literature categorization, Judgement SWOT analysis, Keypoint contributions, and List of organization.
3. **Related Work Refactoring**: Synthesize literature into a 1/2 AI + 1/2 Domain structure, an exhaustive 4x5 summary table ([1]-[8]), explicit Research Gap, and full Deep Research integration (5 Core mental models, 3 Professional debates, 10 Deep understanding details).
4. **OpenSpec Specification Integration**: Establish `openspec/specs/` as the single source of truth for pipeline, architecture, domain rules, and benchmark.
5. **Prompt Alignment**: Structure outputs to match NotebookLM analysis and ChatGPT A4 landscape high-density infographic generation requirements.

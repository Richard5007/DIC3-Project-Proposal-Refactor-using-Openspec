# Spec Delta

## Purpose

Ensures that the AirGuard AI project proposal and engineering specifications strictly comply with the 2020 A-Z SOP, OpenSpec SDD workflow conversion, Perplexity-grounded 2024–2026 evidence enhancement, 300-word condensed summary, and IEEE Transactions Systems Journal abstract standards.

## ADDED Requirements

### Requirement: Abstract A-F Structure and Perplexity Evidence Grounding
The system proposal SHALL structure its abstract into six distinct sections (A: Attention Getter, B: But, C: Cure, D: Development, E: Experiments, F: Findings) backed by verified 2024–2026 authoritative statistics and Taiwan air-quality policy/news cases without fabricated results.

#### Scenario: Auditing the updated A-F abstract
- **WHEN** the abstract is reviewed against the updated course prompt
- **THEN** sections A through F include verified WHO 2025 / SoGA 2025 data, Taiwan MOENV 2025 tightened $\text{PM}_{2.5}$ ($12\ \mu\text{g/m}^3$) and ozone Orange Alert context, and explicit expected-outcome labels

### Requirement: Condensed 300-Word Summary and IEEE Transactions Abstract
The proposal documentation SHALL provide a ~300-word Traditional Chinese condensed summary and an IEEE Transactions on Systems, Man, and Cybernetics: Systems style `Title—`, `Abstract—`, and `Index Terms—` section.

#### Scenario: Verifying newly added Stage 2 and Stage 3 deliverables
- **WHEN** the updated repository deliverables are checked
- **THEN** both the ~300-word Traditional Chinese summary and the formal IEEE Transactions Systems abstract with index terms are present and consistent with `DESIGN.md`

### Requirement: Introduction G-L and Related Work M-O with Deep Research
The proposal SHALL structure the Introduction using G–L and Related Work using M–O (1/2 AI technology + 1/2 domain knowledge, 4x5 summary table, explicit Research Gap) paired with 5 Core Mental Models, 3 Professional Trade-offs, and 10 Deep Understanding Details.

#### Scenario: Auditing Introduction, Related Work, and Deep Research completeness
- **WHEN** the proposal is evaluated against the course grading rubric
- **THEN** G–L, M–O with 8 balanced papers and Research Gap, 5 Cores, 3 Trade-offs, and 10 Details are all present with verified citations

### Requirement: Design-to-OpenSpec Workflow Conversion
The repository SHALL map all 9 modules, data policies, deterministic analytics rules, and benchmark protocols from `DESIGN.md` into canonical `<capability>/spec.md` specifications and an operational workflow in `design.md`.

#### Scenario: Running strict OpenSpec validation
- **WHEN** a developer runs `openspec validate --all --strict`
- **THEN** all canonical specs (`data-pipeline`, `agent-architecture`, `domain-rules`, `evaluation-benchmark`) and active change artifacts pass with zero failures

### Requirement: Decoupled Evidence-Based Query Workflow
The system SHALL decouple natural language intent parsing from deterministic numeric calculation and row-level evidence attribution.

#### Scenario: Location and Time Query Execution
- **WHEN** a user asks for hourly AQI trends for a specific station and time window
- **THEN** numeric statistics are calculated deterministically from cleaned `AQX_P_488` records and every cited claim links to its station ID and timestamp

### Requirement: Safety Boundary and Out-of-Bounds Handling
The system SHALL identify and abstain from answering queries that demand clinical health advice, causal industrial attribution, or touch conflicting data records.

#### Scenario: Query Demanding Causal Industrial Attribution
- **WHEN** a user asks whether a specific factory caused an air quality peak
- **THEN** the system returns an explicit scope limitation explaining that ambient station correlation does not prove causal attribution

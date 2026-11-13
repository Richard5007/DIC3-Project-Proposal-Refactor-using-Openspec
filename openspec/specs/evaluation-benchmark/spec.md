# Evaluation Benchmark Specification

## Purpose

Defines the fixed 60-question evaluation benchmark (`AirGuard-Eval-60`), three-condition baseline comparison protocol, quantitative evaluation metrics, and proposal-stage academic integrity constraints.

## Requirements

### Requirement: Balanced Answerable and Boundary Question Benchmark
The evaluation suite SHALL comprise 60 fixed benchmark questions divided into 45 answerable queries (15 trend, 15 station comparison, 15 AQI/pollutant interpretation) and 15 boundary/abstention cases.

#### Scenario: Inspecting benchmark category distribution
- **WHEN** the benchmark dataset is audited prior to experimental execution
- **THEN** the 15 boundary cases include 5 missing-data windows, 3 quarantined conflict-key queries, 4 causal-attribution probes, and 3 clinical-advice probes

### Requirement: Three-Condition Comparative Protocol
The evaluation harness SHALL compare (1) LLM-only without retrieval, (2) Deterministic Tools Only without prose generation, and (3) the proposed AirGuard AI agent across identical questions.

#### Scenario: Running comparative evaluation
- **WHEN** the 60 benchmark questions are evaluated after implementation
- **THEN** all three conditions are scored against deterministically generated and manually spot-checked reference answers

### Requirement: Quantitative Accuracy, Provenance, and Abstention Metrics
The evaluation protocol SHALL measure numeric accuracy within task tolerance, row-level provenance linkage accuracy, unsupported-claim rate (target 0.0%), and boundary abstention precision.

#### Scenario: Scoring an agent response
- **WHEN** an agent response contains numeric values and cited records
- **THEN** the evaluator verifies numeric match against ground truth, checks exact `(SiteId, DataCreationDate)` binding, and flags any unsupported numeric claim

### Requirement: Proposal-Stage Academic Integrity
Proposal documentation SHALL clearly designate target metrics and expected outcomes as unexecuted goals and MUST NOT report simulated or fabricated experimental results as observed measurements.

#### Scenario: Reviewing proposal evaluation tables
- **WHEN** proposal documents are audited prior to implementation completion
- **THEN** every accuracy, provenance, and abstention figure is explicitly labeled as a planned target or hypothesis

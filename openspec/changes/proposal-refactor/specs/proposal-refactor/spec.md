# Spec Delta

## Purpose
Ensures that the AirGuard AI project proposal strictly complies with the A2Z scientific paper outline and the university course final project proposal requirements.

## ADDED Requirements

### Requirement: Abstract A-F Structure Compliance
The system proposal SHALL structure its abstract into six distinct sections (A: Attention Getter, B: But, C: Cure, D: Development, E: Experiments, F: Findings) without unverified fabricated numbers.

#### Scenario: Valid Abstract Parsing
- **WHEN** the abstract is evaluated against the course proposal rubric
- **THEN** all six sections A through F are present and expected findings are marked as unexecuted projections

### Requirement: Decoupled Evidence-Based Query Workflow
The system SHALL decouple natural language intent parsing from deterministic numeric calculation and row-level evidence attribution.

#### Scenario: Location and Time Query Execution
- **WHEN** a user asks for hourly AQI trends for a specific station and time window
- **THEN** numeric statistics are calculated deterministically from AQX_P_488 records and every cited claim links to its station ID and timestamp

### Requirement: Safety Boundary and Out-of-Bounds Handling
The system SHALL identify and abstain from answering queries that demand clinical health advice, causal industrial attribution, or touch conflicting data records.

#### Scenario: Query Demanding Causal Industrial Attribution
- **WHEN** a user asks whether a specific factory caused an air quality peak
- **THEN** the system returns an explicit scope limitation explaining that ambient station correlation does not prove causal attribution

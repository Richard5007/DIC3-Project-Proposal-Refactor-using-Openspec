# Agent Architecture Specification

## Purpose

Defines the 9-stage decoupled workflow, module interfaces, and strict separation between natural language orchestration and deterministic numerical computation in AirGuard AI.

## Requirements

### Requirement: Separation of Language Parsing and Numeric Computation
The agent SHALL restrict LLM usage to structured intent parsing and final prose phrasing while delegating all data retrieval, numerical aggregation, and threshold evaluation to deterministic Python scripts.

#### Scenario: Executing a quantitative trend or comparison query
- **WHEN** a user asks for pollutant averages, changes, or station rankings over a time window
- **THEN** deterministic Python tools compute every numeric statistic from `aqi_2026_clean.csv`
- **AND** the LLM MUST NOT compute arithmetic, interpolate missing values, or invent measurements

### Requirement: Ambiguous Query Clarification
The Planner module SHALL extract structured parameters (`site_id`, `time_window`, `pollutant`, `task_type`) and request user clarification or apply an explicitly disclosed default when location or period is ambiguous.

#### Scenario: Underspecified station or time range
- **WHEN** a user submits a query without an unambiguous station identifier or time window
- **THEN** the Planner prompts for clarification or states the exact default station and period before retrieval

### Requirement: Deterministic Retrieval and Quality Gate
The retrieval and alignment stage SHALL inspect record availability, missingness, time continuity, and conflict logs before running downstream analytics.

#### Scenario: Query intersects a quarantined conflict key
- **WHEN** a user requests observations matching one of the 13 quarantined `(SiteId, DataCreationDate)` conflict keys
- **THEN** the quality filter halts normal aggregation and returns a data-conflict notice citing the differing source fields

### Requirement: Row-Level Provenance Verification
The Evidence Guard SHALL verify that every numeric claim in the candidate response maps directly to a retrieved `(SiteId, DataCreationDate, SourceRowID)` record and strip or qualify any unverified claim.

#### Scenario: Verifying synthesized response claims
- **WHEN** the response generator drafts a natural-language summary from deterministic tool outputs
- **THEN** the Evidence Guard cross-checks each value against retrieved evidence rows and outputs station, timestamp, value, source file, and data limitations

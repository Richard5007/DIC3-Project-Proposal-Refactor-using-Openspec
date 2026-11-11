# Agent Architecture Specification

## Purpose
Defines the component boundaries, execution flow, and decoupling principles between language understanding and deterministic execution in AirGuard AI.

## Architectural Principle
Strict separation of language understanding and numeric calculation:
- **LLM Scope**: Intent understanding, query parsing, natural language explanation of deterministic results.
- **Deterministic Scope**: Record retrieval, numerical aggregations, trend computations, threshold comparisons, provenance checks.
- **Prohibition**: The LLM is strictly prohibited from interpolating missing numbers, calculating statistics, or inventing citations.

## Modular Components
1. **User Interaction Interface**: Receives natural language queries regarding location, time, pollutants, and comparisons.
2. **Planner / Intent Router**: Extracts structured parameters:
   - Target Station(s) / County / Region
   - Time Window (Start time, End time)
   - Target Pollutant(s) (PM2.5, PM10, O3, NO2, SO2, CO, or overall AQI)
   - Task Type: Trend, Station Comparison, AQI Interpretation, Threshold Anomaly
   - If ambiguous, triggers clarification request.
3. **Retrieval Engine**: Performs deterministic indexed lookup on `aqi_2026_clean.csv` by `(SiteId, TimeRange)`.
4. **Quality & Alignment Filter**: Validates time coverage, checks for missing data flags, and verifies absence of conflict keys. If data is insufficient, returns a limitation response.
5. **Deterministic Analytics Engine**: Computes exact statistics (mean, delta, percentiles, ranking) via verified Python/Pandas functions.
6. **AQI Domain Rule Engine**: Checks statutory sub-indices, identifies the governing pollutant, verifies averaging windows (e.g., 8-hour rolling vs 1-hour).
7. **Evidence & Provenance Guard**: Binds each numeric claim to its source row `(SiteId, DataCreationDate, SourceRowID)`. Strips any claim unsupported by retrieved data.
8. **Constrained Response Layer**: Renders verifiable responses complete with exact values, timestamps, stations, and explicit boundary/uncertainty statements.

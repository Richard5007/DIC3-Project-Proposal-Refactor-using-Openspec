# Evaluation Benchmark Specification

## Purpose
Defines the quantitative evaluation protocol, question benchmark, comparison conditions, and evaluation metrics for AirGuard AI.

## Benchmark Composition (60 Questions)
1. **Answerable Scenarios (45 questions)**:
   - Trend queries (15 questions): Direction of change, peak hours, rate of change across specific time windows.
   - Station comparisons (15 questions): Multi-station ranking, regional differences (e.g., Banqiao vs Xinzhuang), temporal synchronization.
   - AQI & Pollutant interpretations (15 questions): Sub-index breakdown, primary pollutant identification, category boundaries.
2. **Abstention & Edge Cases (15 questions)**:
   - Data gap / Missing records (5 questions): Queries for time windows with missing sentinels or sensor maintenance.
   - Conflict keys (3 questions): Queries hitting the 13 quarantined contradictory station-time records.
   - Out-of-bounds Causal / Legal queries (4 questions): Attributing pollution to a specific factory.
   - Medical advice / Personal exposure queries (3 questions): Asking for individual diagnosis or exposure dose.

## Evaluation Conditions
1. **LLM-Only**: Pure generative response without source retrieval or execution tools.
2. **Deterministic Tools Only**: Raw Pandas/Python query execution without conversational explanation.
3. **AirGuard AI Agent**: Full tool-augmented agent with Planner, Analytics, AQI Rules, and Provenance Guard.

## Quantitative Metrics
- **Numeric Accuracy**: Agreement with deterministic ground-truth within task tolerance ($\pm 0.1 \mu g/m^3$ or exact integer for AQI).
- **Provenance Linkage Accuracy**: Percentage of numeric claims explicitly linked to valid `(SiteId, DataCreationDate, SourceRow)`.
- **Unsupported Claim Rate**: Percentage of numeric assertions made by the LLM lacking underlying database records (Target = 0.0%).
- **Abstention / Limitation Precision**: Accuracy in correctly returning data limitation or scope abstention for the 15 edge cases.

# Domain Rules Specification

## Purpose

Defines Taiwan MOENV statutory AQI formulation rules, temporal averaging windows, data-coverage validity thresholds, and safety/scope abstention guardrails.

## Requirements

### Requirement: Maximum Sub-Index and Governing Pollutant Disclosure
The domain rule engine SHALL compute station AQI as the maximum sub-index across the six criteria pollutants (`PM2.5`, `PM10`, `O3`, `CO`, `SO2`, `NO2`) and MUST report the governing pollutant alongside AQI.

#### Scenario: Reporting station AQI status
- **WHEN** the agent reports an AQI value for a station and timestamp
- **THEN** the response states both the AQI integer value and the governing pollutant with its concentration and unit

### Requirement: Temporal Scale and Averaging Window Alignment
The domain rule engine SHALL distinguish hourly concentrations (`O3`, `NO2`, `SO2`) from statutory moving-average fields (`O3_8hr`, `CO_8hr`, `PM2.5_AVG`) and preserve Taiwan local timezone semantics.

#### Scenario: Evaluating ozone AQI contribution
- **WHEN** a query asks why ozone triggered an Orange Alert (`AQI 101-150`)
- **THEN** the engine evaluates statutory `O3_8hr` alongside hourly `O3` without conflating averaging windows

### Requirement: Temporal Coverage Validity Threshold
The analytics layer SHALL require at least 75% valid hourly observations (18 of 24 hours) before reporting a daily summary and SHALL flag insufficient temporal coverage without interpolation.

#### Scenario: Station outage exceeds 6 hours in a day
- **WHEN** a requested daily window has fewer than 18 valid non-sentinel hourly records
- **THEN** the system declines to compute a daily mean and reports an incomplete temporal coverage limitation

### Requirement: Spatial Representativeness and Exposure Boundary
The system SHALL frame station measurements as regional ambient background conditions and MUST NOT claim they measure an individual user's inhaled exposure dose.

#### Scenario: User asks for personal inhaled exposure
- **WHEN** a user asks how much pollution they personally inhaled based on a fixed MOENV station
- **THEN** the system clarifies that fixed-station readings represent ambient regional background rather than personal microenvironment exposure

### Requirement: Causal Attribution and Medical Advice Abstention
The system SHALL abstain from blaming specific industrial emission sources without dispersion modeling and MUST refuse individualized clinical diagnosis or medication advice.

#### Scenario: Query demands factory blame or medical diagnosis
- **WHEN** a user asks whether a specific factory caused an illness or requests asthma medication advice
- **THEN** the scope guard triggers an explicit abstention and cites only general official public-health advisories

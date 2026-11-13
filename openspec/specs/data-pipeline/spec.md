# Data Pipeline Specification

## Purpose

Defines deterministic data acquisition, normalization, provenance tracking, duplicate resolution, and conflict isolation rules for Taiwan Ministry of Environment (MOENV) historical hourly air quality records (AQX_P_488).

## Requirements

### Requirement: Immutable Raw Archive Preservation
The data pipeline SHALL preserve original MOENV AQX_P_488 monthly CSV files unmodified and record MD5 checksums and observation counts in `data/processed/cleaning_report.md`.

#### Scenario: Running repeatable archive cleanup
- **WHEN** `scripts/clean_aqi_data.py` processes monthly CSV exports from `data/raw/AQX_P_488_Resource/`
- **THEN** source CSV files remain unchanged on disk and their MD5 checksums are verified and logged

### Requirement: Composite Primary Key Enforcement
The pipeline SHALL use `(SiteId, DataCreationDate)` as the canonical observation key and MUST NOT join or deduplicate records solely by station name.

#### Scenario: Bilingual station name deduplication
- **WHEN** raw monthly exports contain localized Chinese and English station name variants for the same station and timestamp
- **THEN** records are matched and deduplicated strictly using `(SiteId, DataCreationDate)`

### Requirement: Missing Sentinel Normalization
The pipeline SHALL normalize string missing-value sentinels (`-`, `--`, `NA`, `null`, `ND`) to empty values without fabricating or interpolating numeric observations.

#### Scenario: Encountering missing sensor sentinel
- **WHEN** a pollutant or AQI field contains `-`, `--`, or `NA`
- **THEN** the derived clean CSV stores an empty cell and preserves missingness for downstream coverage checks

### Requirement: Missing Station ID Recovery
The pipeline SHALL recover a missing `SiteId` only when `County` together with exact `(Latitude, Longitude)` coordinates uniquely maps to a single known station ID.

#### Scenario: Unique coordinate match for missing SiteId
- **WHEN** an observation row lacks `SiteId` and its `(County, Latitude, Longitude)` matches exactly one known station
- **THEN** the pipeline assigns that station ID (recovering 4 rows in the 2026-01 to 2026-10 audit)
- **AND** quarantines any unresolvable row into the conflict log

### Requirement: Conflicting Observation Quarantine
The pipeline SHALL exclude all source variants of any `(SiteId, DataCreationDate)` key whose duplicate rows report divergent non-missing numeric values and log them to `aqi_2026_conflicts.csv`.

#### Scenario: Divergent duplicate measurements
- **WHEN** two source rows share `(SiteId, DataCreationDate)` but disagree on non-missing numeric fields such as `AQI`, `PM2.5_AVG`, or `PM10_AVG`
- **THEN** all variants of that key (13 keys / 26 variants in the 2026 audit) are excluded from `aqi_2026_clean.csv` and recorded in `aqi_2026_conflicts.csv`

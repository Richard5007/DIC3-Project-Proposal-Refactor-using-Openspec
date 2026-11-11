# Data Pipeline Specification

## Purpose
Defines the deterministic data acquisition, normalization, provenance tracking, and conflict isolation standards for Taiwan MOENV historical air quality dataset (AQX_P_488).

## Source Data Characteristics
- **Dataset ID**: MOENV AQX_P_488 (Historical Hourly Air Quality Index)
- **Time Coverage**: 2026-01-01 00:00 to 2026-10-29 16:00
- **Raw Volume**: 10 monthly CSV archives, 970,296 raw rows, 88 distinct stations.
- **Key Fields**: `SiteId`, `SiteName`, `County`, `AQI`, `Pollutant`, `Status`, `SO2`, `CO`, `CO_8hr`, `O3`, `O3_8hr`, `PM10`, `PM2.5`, `NO2`, `NOx`, `NO`, `WindSpeed`, `WindDirec`, `DataCreationDate`, `Unit`, `Longitude`, `Latitude`.

## Ingestion & Cleaning Rules
1. **Primary Observation Key**: `(SiteId, DataCreationDate)`. Joins and deduplications MUST NEVER be performed on station name alone due to multilingual aliases and transliteration changes.
2. **Sentinel Normalization**: String sentinels (`-`, `--`, `NA`, `null`, `ND`) MUST be normalized to empty values (null).
3. **Duplicate Resolution**:
   - Localized duplicate rows with identical non-missing numeric values are collapsed.
   - Missing fields in one row may be safely filled from another duplicate if no conflict exists.
4. **Conflict Isolation**:
   - If two rows share `(SiteId, DataCreationDate)` but contain divergent non-missing numeric values, ALL variants MUST be excluded from the clean dataset (`aqi_2026_clean.csv`) and logged into `aqi_2026_conflicts.csv`.
   - In the audit dataset, 13 conflicting station-time keys (26 source variants) are isolated.
5. **SiteId Recovery**:
   - Missing `SiteId` is only recovered if `County` + exact `(Latitude, Longitude)` unambiguously maps to exactly one known station. (4 instances safely recovered in the audit).
6. **Data Immutability & Provenance**:
   - Original monthly CSV files remain untouched with MD5 checksums verified.
   - Derived datasets: `data/processed/aqi_2026_clean.csv` (606,137 unique observations), `data/processed/aqi_2026_conflicts.csv`, and `data/processed/cleaning_report.md`.

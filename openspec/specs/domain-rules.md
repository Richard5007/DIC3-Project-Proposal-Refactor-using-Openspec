# Domain Rules Specification

## Purpose
Defines the air quality regulations, index calculation methods, temporal windows, and safety/legal boundary constraints based on Taiwan MOENV, U.S. EPA, and WHO standards.

## 1. MOENV AQI Formulation
- **Sub-index Definition**: Taiwan AQI is computed from 6 criteria pollutants: PM2.5, PM10, O3, CO, SO2, NO2.
- **Maximum Sub-index Rule**: Station AQI = $\max(I_{\text{PM2.5}}, I_{\text{PM10}}, I_{\text{O3}}, I_{\text{CO}}, I_{\text{SO2}}, I_{\text{NO2}})$.
- **Governing Pollutant**: The pollutant whose sub-index determines the max value must always be reported alongside the AQI.
- **Temporal Averaging Windows**:
  - Ozone (O3): 8-hour moving average (`O3_8hr`) or 1-hour average.
  - PM2.5: 24-hour moving average ($0.5 \times$ past 12-hr avg + $0.5 \times$ past 4-hr avg per MOENV formulation).
  - Carbon Monoxide (CO): 8-hour moving average (`CO_8hr`).
  - Nitrogen Dioxide (NO2) / Sulfur Dioxide (SO2): Hourly average.

## 2. Safety & Interpretive Guardrails
1. **Station vs Individual**: A monitoring station measures ambient concentration within its spatial representativeness bubble (~2-5 km radius depending on terrain). Station data CANNOT be stated as an individual's personal inhaled dose.
2. **Correlation vs Causation**: Wind direction and pollutant rises show spatio-temporal co-occurrence but do not establish legal liability or industrial source causation without atmospheric dispersion models.
3. **Medical Advice Prohibition**: The agent must never give clinical diagnoses (e.g., "Your cough is caused by SO2 from station X"). Health alerts must only echo official general public health guidelines (WHO / MOENV category advisories).

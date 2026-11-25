# Plant Engineering Specification

## 1. Plant Design Basis

| Parameter | Specification |
|---|---|
| Plant | Palm Kernel Cake solvent extraction |
| Rated capacity | 50 TPD |
| Feedstock | Palm Kernel Cake |
| Solvent | SRG hexane |
| Extractor | Rotocel |
| Operating pattern | Continuous 24-hour operation |
| Rated hourly throughput | 2.083 tonnes/hour |

These are the initial project design assumptions.

## 2. Data Classification

M = Measured
C = Calculated
S = Simulated

Measured values represent instrument, laboratory or operator records.
Calculated values are derived using documented engineering formulas.
Simulated values are synthetic signals created for this project.

No simulated value will be represented as actual plant telemetry.

## 3. Process Variables

### Production and Feedstock

| Variable | Unit | Class |
|---|---|---|
| PKC feed throughput | tonnes/hour | M |
| Daily feed total | tonnes/day | C |
| Feed moisture | % | M |
| Feed oil content | % | M |
| Plant utilization | % | C |

### Extraction

| Variable | Unit | Class |
|---|---|---|
| Extractor temperature | °C | M |
| Extractor pressure | kPa | M |
| Extractor motor current | A | M/S |
| Extractor operating status | ON/OFF | M/S |
| Miscella concentration | % | M |
| Miscella flow | m3/hour | M |
| Residual oil in meal | % | M |
| Extraction performance | % | C |

### Solvent Management

| Variable | Unit | Class |
|---|---|---|
| Solvent makeup | L | M |
| Solvent consumption intensity | L/tonne | C |
| Solvent tank level | % | M |
| Solvent recovery | % | C |
| Solvent inventory deviation | L | C |
| Solvent pump status | ON/OFF | M/S |

### DTDC

| Variable | Unit | Class |
|---|---|---|
| DTDC temperature | °C | M |
| DTDC pressure | kPa | M |
| Meal outlet moisture | % | M |
| Meal residual solvent | ppm | M |
| DTDC operating status | ON/OFF | M/S |

### Condensation and Recovery

| Variable | Unit | Class |
|---|---|---|
| Condenser inlet temperature | °C | M |
| Condenser outlet temperature | °C | M |
| Condenser pressure | kPa | M |
| Cooling water inlet temperature | °C | M |
| Cooling water outlet temperature | °C | M |
| Condenser performance indicator | % | C |

### Equipment and Utilities

| Variable | Unit | Class |
|---|---|---|
| Pump motor current | A | M/S |
| Fan motor current | A | M/S |
| Pump running status | ON/OFF | M/S |
| Fan running status | ON/OFF | M/S |
| Steam consumption | kg/hour | M |
| Electrical energy | kWh | M |

## 4. Initial Engineering Calculations

### Plant Utilization

Utilization (%) = Actual throughput / 50 x 100.

### Solvent Consumption Intensity

Solvent consumption (L/tonne) =
Solvent makeup (L) / PKC processed (tonnes).

Gross solvent circulation must not be confused with solvent makeup.

### Extraction Performance

Extraction efficiency (%) =
(Feed oil mass - Residual oil mass) / Feed oil mass x 100.

All oil masses must use consistent measurement boundaries and
representative sampling.

### Solvent Inventory Reconciliation

Inventory deviation =
Opening inventory + Receipts - Closing inventory - Recorded usage.

A positive or negative deviation requires investigation and
does not automatically prove solvent loss.

## 5. Proposed Acquisition Frequency

| Data category | Frequency |
|---|---|
| Temperature and pressure | 5 minutes |
| Throughput and flow | 5 minutes |
| Motor current | 5 minutes |
| Equipment status | Event-based |
| Tank level | 5 minutes |
| Laboratory quality | Per sample |
| Production totals | Hourly and daily |
| Solvent reconciliation | Per shift and daily |
| OT security events | Event-based |

These frequencies are initial simulation assumptions.

## 6. Data Quality Requirements

The monitoring system will check:

- Missing timestamps.
- Duplicate records.
- Missing values.
- Invalid numerical values.
- Invalid equipment states.
- Stale measurements.
- Unexpected measurement changes.
- Unit inconsistencies.
- Missing laboratory results.
- Mass-balance inconsistencies.

## 7. Monitoring and Alert Classification

INVALID_DATA: Data cannot be trusted for analysis.

PROCESS_WARNING: An operating measurement requires engineering review.

SECURITY_ALERT: Potentially suspicious cybersecurity activity requires
security investigation.

An abnormal process measurement alone does not establish a cyberattack.

## 8. Safety and Operational Boundaries

This project uses synthetic datasets and simulated security events.

It is read-only and does not connect to live industrial equipment,
PLCs, SCADA systems or production networks.

It does not issue control commands.

## 9. Future Refinery Expansion

A separate refinery monitoring module will be developed in Phase 2.

Planned processes include degumming, neutralization, bleaching,
filtration, deodorization, utilities and product quality monitoring.

## 10. Outstanding Engineering Verification

The following require confirmation against actual plant documentation:

- Installed instrumentation.
- Instrument measurement ranges.
- Pressure reference: gauge or absolute.
- Actual operating temperatures and pressures.
- Laboratory sampling procedures.
- Equipment specifications.
- Process alarm limits.
- Solvent mass-balance boundaries.

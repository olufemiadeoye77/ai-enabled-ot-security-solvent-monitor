# Process Data Dictionary

**Document ID:** PDD-001  
**Version:** 1.0  
**Status:** Initial engineering definition  
**Project:** AI-Enabled OT Security and Solvent-Loss Monitoring  
**Plant:** 50 TPD Palm Kernel Cake Solvent Extraction Plant  
**Solvent:** SRG Hexane  
**Primary Extractor:** Rotocel  

---

## 1. Purpose

This document defines the process variables, calculated indicators,
data classifications, measurement sources, units and data quality
requirements used by the industrial monitoring platform.

It provides a common reference for:

- Process engineering.
- Industrial data acquisition.
- PLC/SCADA simulation.
- Process analytics.
- Solvent inventory reconciliation.
- OT cybersecurity event correlation.
- AI-assisted investigation.

This document supplements the Plant Engineering Specification.
It does not replace approved plant operating procedures or
instrumentation documentation.

## 2. Scope

Version 1.0 covers palm kernel cake solvent extraction.

The process areas include:

1. PKC reception and preparation.
2. Feed conveying.
3. Rotocel extraction.
4. Miscella collection and filtration.
5. Miscella evaporation.
6. DTDC meal desolventisation and drying.
7. Solvent condensation and recovery.
8. Solvent storage and distribution.
9. Recovered oil collection.
10. Plant utilities and supporting equipment.

Refinery monitoring remains a planned future development.

## 3. Data Classification

The following classifications shall be retained.

| Code | Classification | Definition |
|---|---|---|
| M | Measured | Obtained from an instrument, laboratory or operating record |
| C | Calculated | Derived using a documented engineering calculation |
| S | Simulated | Generated synthetically for project testing |

A variable that supports both actual measurement and simulation
shall retain its permitted source classifications.

Each individual data record shall identify its actual source mode.

Simulated values must never be represented as actual plant telemetry.

Calculated values must retain references to their contributing
input measurements and calculation method.

## 4. Standard Data Record Requirements

Process measurement records should support the following fields:

| Field | Description |
|---|---|
| variable_id | Unique process variable identifier |
| tag_id | Associated equipment or instrument tag, where available |
| timestamp | Original observation timestamp |
| ingestion_timestamp | Time the monitoring platform received the record |
| value | Recorded numerical or categorical value |
| unit | Engineering unit |
| classification | M, C or S |
| source_mode | Instrument, laboratory, operator, calculation or simulation |
| source_id | Identifiable measurement or data source |
| quality_status | Measurement quality classification |
| quality_flags | Additional applicable quality conditions |
| reporting_period | Applicable production or reconciliation period |
| calculation_reference | Formula or calculation identifier, where applicable |

The observation timestamp and ingestion timestamp must remain
separate.

Timestamps shall use ISO 8601 format with timezone information.
UTC is the preferred standard for system storage and correlation.
Original source timestamps and timezone context shall be retained
where available.

Missing values must not be silently substituted with zero.

## 5. Process Variable Register

### 5.1 Production and Feedstock

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| PRD-001 | PKC feed throughput | tonnes/hour | M/S | 5 minutes |
| PRD-002 | Daily PKC feed total | tonnes/day | C | Daily |
| PRD-003 | Feed moisture | % | M/S | Per sample |
| PRD-004 | Feed oil content | % | M/S | Per sample |
| PRD-005 | Plant utilization | % | C | Hourly/daily |
| PRD-006 | Feed operating status | ON/OFF | M/S | Event-based |

### 5.2 Rotocel Extraction

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| EXT-001 | Extractor temperature | °C | M/S | 5 minutes |
| EXT-002 | Extractor pressure | kPa | M/S | 5 minutes |
| EXT-003 | Extractor motor current | A | M/S | 5 minutes |
| EXT-004 | Extractor operating status | ON/OFF | M/S | Event-based |
| EXT-005 | Miscella concentration | % | M/S | Per sample or approved acquisition interval |
| EXT-006 | Miscella flow | m³/hour | M/S | 5 minutes |
| EXT-007 | Meal residual oil | % | M/S | Per sample |
| EXT-008 | Desolventised meal mass | tonnes | M/S | Per reporting period |
| EXT-009 | Apparent oil removal efficiency | % | C | Per reporting period |

### 5.3 Solvent Management

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| SLV-001 | Fresh solvent makeup | L | M/S | Event-based/shift |
| SLV-002 | Fresh solvent makeup intensity | L/tonne | C | Shift/daily |
| SLV-003 | Solvent tank level | % | M/S | 5 minutes |
| SLV-004 | Solvent tank inventory | L | M/C/S | 5 minutes or inventory event |
| SLV-005 | Gross solvent circulation flow | L/hour | M/S | 5 minutes |
| SLV-006 | Gross solvent circulation intensity | L/tonne | C | Shift/daily |
| SLV-007 | Solvent recovery quantity | L | M/S | Shift/daily |
| SLV-008 | Solvent recovery percentage | % | C | Shift/daily |
| SLV-009 | Solvent inventory deviation | L | C | Shift/daily |
| SLV-010 | Unaccounted solvent | L | C | Shift/daily |
| SLV-011 | Unaccounted solvent intensity | L/tonne | C | Shift/daily |
| SLV-012 | Solvent pump status | ON/OFF | M/S | Event-based |

### 5.4 DTDC

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| DTD-001 | DTDC temperature | °C | M/S | 5 minutes |
| DTD-002 | DTDC pressure | kPa | M/S | 5 minutes |
| DTD-003 | Meal outlet moisture | % | M/S | Per sample |
| DTD-004 | Meal residual solvent | ppm | M/S | Per sample |
| DTD-005 | DTDC operating status | ON/OFF | M/S | Event-based |

### 5.5 Condensation and Solvent Recovery

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| CND-001 | Condenser inlet temperature | °C | M/S | 5 minutes |
| CND-002 | Condenser outlet temperature | °C | M/S | 5 minutes |
| CND-003 | Condenser pressure | kPa | M/S | 5 minutes |
| CND-004 | Cooling water inlet temperature | °C | M/S | 5 minutes |
| CND-005 | Cooling water outlet temperature | °C | M/S | 5 minutes |
| CND-006 | Condenser performance indicator | % | C | 5 minutes or approved interval |

### 5.6 Equipment and Utilities

| Variable ID | Variable | Unit | Class | Frequency |
|---|---|---|---|---|
| UTL-001 | Pump motor current | A | M/S | 5 minutes |
| UTL-002 | Fan motor current | A | M/S | 5 minutes |
| UTL-003 | Pump running status | ON/OFF | M/S | Event-based |
| UTL-004 | Fan running status | ON/OFF | M/S | Event-based |
| UTL-005 | Steam consumption | kg/hour | M/S | 5 minutes |
| UTL-006 | Electrical energy | kWh | M/S | Hourly/daily |

## 6. Calculated Engineering Variables

### 6.1 Plant Utilization

Calculation ID: CALC-001

Plant utilization (%) =

Actual PKC throughput (tonnes/hour)
÷ (50 tonnes/day ÷ 24 hours/day) × 100

The rated hourly capacity shall be derived directly from the
50 TPD design basis and 24-hour operating assumption.

The rounded value of 2.083 tonnes/hour may be displayed for
reference but shall not be used as the underlying calculation
constant.

Hourly utilization shall use actual PKC throughput in
tonnes/hour against the rated hourly capacity derived
from the 50 TPD design basis.

Daily utilization shall use actual PKC processed in
tonnes/day against the rated daily capacity of 50 tonnes.

The reporting period and production totals used in each
calculation shall be documented.

### 6.2 Fresh Solvent Makeup Intensity

Calculation ID: CALC-002

Fresh solvent makeup intensity (L/tonne) =

Fresh solvent makeup (L)
÷ PKC processed (tonnes)

Fresh solvent makeup must not be confused with gross solvent
circulation.

A zero or unavailable production denominator must prevent
a valid intensity calculation.

### 6.3 Apparent Oil Removal Efficiency

Calculation ID: CALC-003

Feed oil input mass (tonnes) =

PKC feed mass × Feed oil fraction

Residual oil in meal mass (tonnes) =

Desolventised meal mass × Residual oil fraction

Apparent oil removal efficiency (%) =

(Feed oil input mass - Residual oil in meal mass)
÷ Feed oil input mass × 100

Oil percentages must be converted to decimal fractions.

Each oil fraction shall correspond to the representative
laboratory measurement applicable to its respective
feed or meal mass.

Feed and meal measurements must cover the same reporting
period and use compatible mass, analytical and moisture
bases.

Where feed and meal measurements use different moisture
or mass bases, an approved conversion method shall be
applied before calculating the respective oil masses.

The measurement basis and any conversion method shall
be retained with the calculation record.

A zero, missing, invalid or unsuitable feed oil input mass
shall prevent a valid efficiency calculation.

This indicator does not independently establish recovered
oil production.

### 6.4 Gross Solvent Circulation Intensity

Calculation ID: CALC-004

Gross solvent circulation intensity (L/tonne) =

Gross solvent circulation (L)
÷ PKC processed (tonnes)

Internal circulation is not fresh solvent makeup.

### 6.5 Unaccounted Solvent

Calculation ID: CALC-005

Unaccounted solvent (L) =

Opening solvent inventory
+ External solvent receipts
+ Transfers into accounting boundary
- Closing solvent inventory
- Accounted external solvent outputs
- Transfers out of accounting boundary

The calculation shall use the same defined solvent accounting
boundary and reporting period for all contributing inputs.

The opening and closing inventories shall represent the
beginning and end of the same reporting period respectively.

All contributing quantities shall use a consistent solvent
measurement basis.

REC-005 shall represent the aggregate of applicable accounted
external solvent outputs. Supporting components REC-007
through REC-010 shall not be subtracted again when already
included in REC-005.

REC-006 represents transfers out of the accounting boundary
and shall be accounted for separately.

REC-011 is supporting information for inventory assessment
and shall not be independently added or subtracted unless
the approved accounting method explicitly requires it.

Internal solvent recovery and recirculation within the
accounting boundary shall not be treated as new external
inputs or outputs.

Where required inputs are missing, stale, invalid, conflicting
or unverified for the calculation, the result shall not be
presented as a confirmed reconciliation result.

The calculated discrepancy shall retain its numerical sign.
A positive result indicates an accounting discrepancy
requiring investigation. It does not independently establish
physical solvent loss or leakage.

A negative result also requires investigation and does not
independently establish physical solvent gain.

### 6.6 Unaccounted Solvent Intensity

Calculation ID: CALC-006

Unaccounted solvent intensity (L/tonne) =

Unaccounted solvent (L)
÷ PKC processed (tonnes)

The PKC processed quantity shall cover the same reporting
period as the unaccounted solvent calculation.

A zero, missing or invalid production denominator shall
prevent a valid intensity calculation.

The result shall not be calculated where the underlying
unaccounted solvent result is unavailable or unsuitable
for intensity calculation.

The numerical result must retain its sign.

A positive result indicates a positive unaccounted
solvent discrepancy within the defined accounting
boundary. It does not independently establish physical
solvent loss or leakage.

A negative discrepancy requires investigation and does not
independently establish physical solvent gain.

### 6.7 Solvent Recovery Percentage

Calculation ID: CALC-007

Solvent recovery percentage shall be calculated only after
the engineering team defines and approves the recovery
accounting basis.

The denominator, numerator, measurement period and
measurement boundary must be documented.

The system must not treat an arbitrary ratio of internal
recycle flow to fresh solvent makeup as a verified recovery
percentage.

### 6.8 Solvent Inventory Deviation

Calculation ID: CALC-008

Solvent inventory deviation (L) =

Actual solvent inventory (L)
- Approved reference solvent inventory (L)

Actual inventory shall be obtained from an identified and
suitably validated measurement or approved inventory
calculation method.

The reference inventory shall be established using
an approved engineering or inventory accounting basis.
It shall not automatically be interpreted as tank
capacity, maximum operating level or design capacity.

Actual and reference inventories shall use the same
accounting boundary, measurement basis and applicable
reference time.

Where tank level measurements are converted into volume,
the approved tank calibration or strapping table and
applicable conversion method shall be retained.

A positive result indicates actual inventory above the
approved reference inventory.

A negative result indicates actual inventory below the
approved reference inventory.

Missing, stale, invalid, conflicting or unverified inputs
shall prevent a valid inventory deviation result where
they are unsuitable for the calculation.

Solvent inventory deviation shall remain distinct from
unaccounted solvent calculated under CALC-005.

The reference basis, calculation method and applicable
reporting period or reference time must be documented
before production use.

### 6.9 Condenser Performance Indicator

Calculation ID: CALC-009

The condenser performance indicator requires an approved
engineering calculation and operating basis.

Until the calculation method is approved, the variable shall
remain undefined for production use.


## 7. Solvent Reconciliation Input Register

The following inputs must be separately identifiable.

REC-005 represents the aggregate of applicable accounted
external solvent outputs. REC-007 through REC-010 may be
recorded as supporting components of REC-005 where applicable.

The reconciliation calculation shall subtract the aggregate
external output quantity only once. Supporting components
shall not be subtracted again when already included in REC-005.

### 7.1 Reconciliation Input Interpretation and Measurement Basis

All reconciliation inputs shall represent quantities crossing
or held within the defined solvent accounting boundary during
the applicable reporting period.

REC-005 shall represent the aggregate of applicable accounted
external solvent outputs. It shall exclude REC-006, which
represents transfers out of the accounting boundary and is
accounted for separately.

REC-007 through REC-010 shall identify supporting components
of REC-005 where applicable. Their quantities shall only be
included in REC-005 once.

Solvent quantities shall use a consistent measurement basis
and reporting period.

Where measurements are obtained under different temperature,
pressure or physical conditions, an approved conversion method
shall be documented before the quantities are combined.

Vapour or gaseous solvent quantities expressed as liquid-volume
equivalents shall retain the conversion method, assumptions
and supporting measurement or estimation source.

Estimated quantities must remain distinguishable from directly
measured quantities.

The accounting boundary, measurement basis and reporting
period shall be established before reconciliation results
are interpreted.

| Input ID | Description | Unit |
|---|---|---|
| REC-001 | Opening solvent inventory | L |
| REC-002 | External solvent receipts | L |
| REC-003 | Transfers into accounting boundary | L |
| REC-004 | Closing solvent inventory | L |
| REC-005 | Accounted external outputs | L |
| REC-006 | Transfers out of accounting boundary | L |
| REC-007 | Solvent in meal discharge | L |
| REC-008 | Solvent in recovered oil | L |
| REC-009 | Recorded emissions or vapour losses | L |
| REC-010 | Solvent in drainage and waste streams | L |
| REC-011 | Estimated or measured process hold-up | L |
| REC-012 | Reporting period PKC throughput | tonnes |

Every input must retain its source, measurement method,
observation time, reporting period and quality information
where available.

Process hold-up estimates must be identified as estimates,
not direct measurements.

Where process hold-up is included in opening or closing
inventory, the applicable estimate and method shall be
documented. REC-011 is supporting information for inventory
assessment and shall not be added or subtracted independently
unless the approved accounting method explicitly requires it.

Unavailable quantities must remain explicitly unavailable.

Internal recovery and recirculation must not be double-counted.

## 8. Measurement Quality Classification

The following quality conditions shall be supported.

| Quality status | Meaning |
|---|---|
| VALID | Passes applicable validation checks |
| MISSING | Required measurement or record unavailable |
| STALE | Measurement exceeds approved freshness limit |
| INVALID | Fails applicable validation or consistency checks |
| UNVERIFIED | Source, accuracy or reliability insufficiently established |
| CONFLICTING | Relevant measurements disagree beyond approved comparison limits |

Multiple non-valid quality flags may coexist.

Quality status must remain separate from the numerical
measurement value.

A measurement may be valid for one calculation and unsuitable
for another calculation requiring different accuracy or
measurement conditions.

## 9. Reconciliation Status Classification

| Status | Meaning |
|---|---|
| COMPLETE_WITHIN_TOLERANCE | Valid required inputs and discrepancy within approved tolerance |
| REVIEW_REQUIRED | Valid required inputs and discrepancy outside approved tolerance |
| INCOMPLETE | Required data missing, stale, invalid or unreliable |
| NOT_EVALUATED | Essential calculation basis or accounting boundary unavailable |
| CALCULATED_TOLERANCE_UNAVAILABLE | Discrepancy calculated but approved tolerance unavailable |

The underlying quality flags and status reasons must be retained.

The software must not invent tolerance limits.

An incomplete, unevaluated or tolerance-unavailable result
must not be presented as a confirmed solvent-loss event.

## 10. Acquisition Frequency

The initial project acquisition assumptions are:

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

These are initial project simulation assumptions,
not confirmed installed plant acquisition settings
or mandatory deployment requirements. Actual acquisition
frequencies shall be established through approved
instrumentation, process engineering and OT architecture
requirements.

## 11. Engineering Validation Requirements

The monitoring platform shall support:

- Missing timestamp detection.
- Duplicate record detection.
- Missing value detection.
- Numerical type and validity checks.
- Equipment state validation.
- Measurement freshness checks.
- Unexpected measurement change detection.
- Unit consistency checks.
- Laboratory result availability checks.
- Mass-balance input consistency checks.
- Source identification.
- Measurement uncertainty documentation.
- Instrument calibration status where available.

No alarm limit, instrument range or measurement freshness
threshold shall be treated as an approved plant limit until
verified by authorised engineering personnel.

## 12. OT and Cybersecurity Data Separation

Process variables and cybersecurity events shall remain
separate data domains.

Process monitoring classifications include:

- INVALID_DATA
- PROCESS_WARNING

Cybersecurity monitoring classifications include:

- SECURITY_ALERT

An abnormal process measurement alone does not establish
a cyberattack.

Relevant security indicators may be correlated with process
events using timestamps, asset references and evidence
identifiers.

The system shall retain the original process measurement
and original security event independently.

## 13. Engineering Verification Register

The following require confirmation before real plant deployment:

- Installed instrument tags.
- Instrument measurement ranges.
- Pressure reference: gauge or absolute.
- Actual process operating temperatures and pressures.
- Tank calibration and strapping tables.
- Tank level-to-volume relationships.
- Approved solvent accounting boundary, including
  storage vessels, process equipment, transfer points
  and included or excluded material streams.
- Temperature correction and density basis.
- Laboratory sampling procedures.
- Measurement accuracy and uncertainty.
- Approved process alarm limits.
- Solvent reconciliation tolerance.
- Solvent recovery calculation basis.
- Condenser performance calculation.
- Process hold-up estimation method.
- Approved measurement freshness requirements.

## 14. Future Development

The data dictionary will be extended to support:

1. Equipment and instrument tag register.
2. Synthetic PLC/SCADA telemetry.
3. Process data validation schemas.
4. Solvent reconciliation engine.
5. Process anomaly detection.
6. OT cybersecurity event ingestion.
7. Process and security event correlation.
8. SOC investigation and evidence reporting.
9. Explainable AI assistance.
10. Future refinery monitoring integration.

## 15. Document Control

| Item | Value |
|---|---|
| Document | Process Data Dictionary |
| Document ID | PDD-001 |
| Version | 1.0 |
| Status | Initial engineering definition |
| Parent document | Plant Engineering Specification |
| Primary scope | PKC solvent extraction |
| Future scope | Palm kernel oil refinery |

Changes to engineering formulas, measurement classifications,
units and approved operating limits shall be documented
and reviewed before implementation.

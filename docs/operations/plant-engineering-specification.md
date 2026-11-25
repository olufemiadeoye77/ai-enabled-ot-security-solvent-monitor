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

Apparent oil removal efficiency (%) is estimated as:

Apparent oil removal efficiency (%) =
(Feed oil input mass - Residual oil in meal mass)
 / Feed oil input mass x 100.

Where:

Feed oil input mass =
PKC feed mass x Feed oil fraction.

Residual oil in meal mass =
Desolventised meal mass x Residual oil fraction.

Feed oil input and residual oil in meal must cover the same
reporting period and use consistent moisture and analytical
measurement bases.

Oil fractions must be expressed as decimals when used in
mass calculations. For example, 2% = 0.02.

Feedstock and meal oil results must come from representative
laboratory samples. Missing or unreliable measurements must
be flagged rather than estimated without a documented method.

This indicator estimates oil removal from the meal. It must
not automatically be interpreted as recovered oil production,
because process hold-up, oil losses and inventory changes
may affect the final recovered quantity.

### Solvent Inventory Reconciliation

The initial solvent reconciliation indicator is:

**Unaccounted solvent (L) =**

Opening solvent inventory + External solvent receipts
- Closing solvent inventory
- Accounted external solvent outputs.

Fresh solvent makeup intensity is calculated separately:

**Fresh solvent makeup intensity (L/tonne) =**

Fresh solvent makeup (L) / PKC processed (tonnes).

These indicators must use consistent reporting periods and
defined accounting boundaries.

Detailed accounting boundaries, measurement requirements,
reconciliation quality and engineering interpretation are
specified in Section 12.

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

## 11. Process Flow and Equipment Boundaries

### 11.1 Reference Process Sequence

The project models a continuous palm kernel cake solvent-extraction
operation based on a 50 TPD Rotocel extractor.

The reference process sequence is:

1. PKC reception and feed preparation.
2. Feed conveying to the extraction system.
3. Rotocel solvent extraction.
4. Miscella collection and filtration.
5. Miscella evaporation and oil-solvent separation.
6. DTDC meal desolventisation, toasting and drying.
7. Solvent vapour condensation.
8. Solvent recovery and storage.
9. Solvent recirculation to the extraction process.
10. Recovered palm kernel oil collection.

This is a reference process model. The installed equipment arrangement,
instrumentation and actual process connections require verification
against plant documentation.

### 11.2 Main Equipment Groups

| Equipment ID | Equipment | Monitoring purpose |
|---|---|---|
| EXT-001 | Rotocel extractor | Extraction operating conditions |
| PMP-001 | Solvent circulation pump | Pump status and motor current |
| PMP-002 | Miscella transfer pump | Transfer status and flow |
| FIL-001 | Miscella filtration system | Filtration operating condition |
| EVA-001 | Miscella evaporation system | Oil-solvent separation |
| DTD-001 | DTDC system | Meal desolventisation and drying |
| CND-001 | Condenser system | Solvent vapour condensation |
| TNK-001 | Solvent storage tank | Solvent inventory |
| TNK-002 | Miscella storage tank | Miscella inventory |
| OIL-001 | Recovered oil collection | Oil production monitoring |

These are logical project identifiers, not confirmed installed
equipment tag numbers.

### 11.3 Process Monitoring Boundaries

The monitoring platform will distinguish the following areas:

- Raw PKC feed and preparation.
- Extraction and miscella circulation.
- Oil-solvent separation.
- Meal desolventisation and drying.
- Solvent condensation and recovery.
- Solvent storage and distribution.
- Recovered oil collection.

Each area will have defined measurement points and data sources.

## 12. Solvent Mass-Balance Model

### 12.1 Purpose

The solvent mass-balance model will estimate unexplained solvent
discrepancies within a defined accounting boundary.

It will support process investigation and solvent-loss monitoring.

A discrepancy does not independently establish a leak, theft,
equipment failure or cybersecurity incident.

### 12.2 Accounting Boundary

The solvent accounting boundary shall be explicitly defined
by identifying the storage vessels, process equipment,
material streams and transfer points included in the
reconciliation.

Relevant solvent held within process equipment shall be
considered even where direct inventory measurement is
unavailable. Such limitations shall be documented and
accounted for in the measurement quality assessment.

The following must be considered:

- Opening solvent inventory.
- External solvent receipts.
- Closing solvent inventory.
- Solvent in meal discharge.
- Solvent in recovered oil.
- Recorded solvent emissions or vapour losses.
- Solvent in drainage and waste streams.
- Transfers across the accounting boundary.
- Solvent held within process equipment.

Internal solvent circulation and recycling must not be counted
as new solvent inputs.

### 12.3 Solvent Inventory Reconciliation

Unaccounted solvent is calculated as:

Unaccounted solvent (L) =

Opening inventory
+ External solvent receipts
+ Transfers into the accounting boundary
- Closing inventory
- Accounted external solvent outputs
- Transfers out of the accounting boundary.

Opening and closing inventory must include relevant process
hold-up within the defined accounting boundary.

Transfers across the boundary must be recorded separately
from external receipts and outputs to prevent double-counting.

Internal solvent circulation and recycling within the
accounting boundary must not be counted as new inputs
or external outputs.

Solvent recovered through condensation or other recovery
equipment and returned within the accounting boundary
shall be treated as an internal recovery flow, not as an
external solvent output.

Recovered solvent transferred outside the accounting
boundary shall be recorded as an external output where
applicable.

A positive discrepancy indicates solvent not accounted for
within the defined measurement boundary.

A negative discrepancy indicates that recorded closing
inventory and outputs exceed recorded inputs. It requires
investigation and does not independently establish an
accounting error or physical solvent gain.

All volume measurements must use a consistent documented
measurement basis, including temperature correction where
applicable.

### 12.4 Solvent Consumption Indicators

The platform will calculate separate indicators:

1. Fresh solvent makeup intensity:

   Fresh solvent makeup (L) / PKC processed (tonnes)

2. Gross solvent circulation intensity:

   Gross solvent circulation (L) / PKC processed (tonnes)

3. Solvent recovery quantity:

   Measured solvent recovered during the reporting period.

4. Unaccounted solvent intensity:

   Unaccounted solvent (L) / PKC processed (tonnes)

These indicators must not be treated as interchangeable.

### 12.5 Measurement Requirements

Solvent reconciliation requires:

- Consistent measurement periods.
- Verified tank level and volume relationships.
- Documented measurement accuracy.
- Recorded receipts and transfers.
- Defined process hold-up boundaries.
- Recorded solvent quantities in relevant output streams.
- Consistent temperature and volume measurement basis.

Where measurements are unavailable, the system must identify
the missing data rather than inventing a value.

### 12.6 Reconciliation Quality and Status

Each reconciliation result will include:

- Reporting period.
- Opening inventory.
- External receipts.
- Transfers into and out of the accounting boundary.
- Closing inventory.
- Accounted external outputs.
- Calculated discrepancy.
- Feed throughput.
- Data completeness.
- Measurement quality status.
- Applicable approved tolerance.
- Reconciliation status.
- Investigation status.

The monitoring system shall distinguish the following
reconciliation statuses:

- COMPLETE_WITHIN_TOLERANCE: Required measurements are
  valid and the calculated discrepancy is within the
  approved tolerance.
- REVIEW_REQUIRED: Required measurements are valid, but
  the calculated discrepancy is outside the approved
  tolerance and requires investigation.
- INCOMPLETE: Required measurements or records are missing,
  stale, invalid or unreliable.
- NOT_EVALUATED: The calculation cannot be performed because
  essential inputs or a valid calculation basis are
  unavailable.
- CALCULATED_TOLERANCE_UNAVAILABLE: Required measurements
  are valid and the discrepancy has been calculated, but
  no approved tolerance is available for threshold-based
  classification.

Where more than one reconciliation limitation exists,
the system shall apply a documented status precedence
rule.

INCOMPLETE shall apply where required measurements or
records are missing, stale, invalid or unreliable.

NOT_EVALUATED shall apply where the calculation cannot
be performed because its calculation basis, accounting
boundary or other essential calculation requirements
have not been established.

Where a discrepancy is successfully calculated but no
approved tolerance is available, the status shall be
CALCULATED_TOLERANCE_UNAVAILABLE.

The system shall retain the underlying quality flags
and reasons for each assigned status.

Tolerance limits must be established using documented
measurement accuracy, instrument uncertainty, inventory
estimation methods and engineering review.

Tolerance values must not be invented or assumed by the
monitoring software.

Where tolerance limits have not been approved, the system
may calculate and report the discrepancy but must not
classify it as within or outside an approved tolerance.

A calculated discrepancy may be reported without an
approved tolerance. In this situation, the numerical
result shall be retained, but tolerance-based status
classification shall remain unavailable.


An incomplete, unevaluated, or tolerance-unavailable
reconciliation must never be presented as a confirmed
solvent-loss event.

### 12.7 Engineering Interpretation

A solvent discrepancy may result from:

- Tank measurement inaccuracies.
- Unrecorded receipts or transfers.
- Process hold-up changes.
- Incomplete solvent recovery.
- Solvent remaining in meal or oil.
- Vapour or emission losses.
- Drainage or equipment leakage.
- Incomplete operating records.

Cybersecurity investigation will be considered separately
when supporting security evidence exists.
The monitoring system shall not independently determine
the physical cause of a solvent discrepancy.

Engineering personnel shall evaluate process conditions,
measurement reliability, operating records and equipment
history before assigning a physical cause.

Cybersecurity personnel shall investigate potential
security-related causes only when relevant security
indicators or supporting evidence are available.

Where the available evidence is insufficient, the cause
shall remain UNDETERMINED.

### 12.8 Investigation and Escalation

The monitoring system shall support a structured investigation process for solvent reconciliation discrepancies and related process or cybersecurity alerts.

The system shall provide investigation information to authorised personnel but shall not independently assign responsibility, confirm equipment failure, establish physical solvent loss or declare a cybersecurity incident.

#### 12.8.1 Initial Discrepancy Review

When a reconciliation receives a REVIEW_REQUIRED status, the system shall make the discrepancy available for engineering review.

The initial review shall consider:

- Calculated solvent discrepancy.
- Opening and closing inventory records.
- Recorded solvent receipts and transfers.
- Feed throughput and operating duration.
- Available process measurements.
- Measurement quality and instrument reliability.
- Previous reconciliation results.
- Relevant operating and maintenance records.

Incomplete or unreliable measurements shall be identified before further conclusions are drawn.

Investigation priority shall be assigned using approved
operational criteria, potential safety implications,
measurement confidence and available security indicators.

The monitoring system shall not invent priority thresholds
or independently authorise operational intervention.

#### 12.8.2 Engineering Investigation

Authorised engineering personnel shall evaluate the discrepancy and determine whether further investigation is necessary.

The investigation may include:

- Verification of tank inventory measurements.
- Review of instrument calibration and measurement records.
- Examination of solvent receipts, transfers and dispatch records.
- Review of process hold-up and operating conditions.
- Assessment of solvent recovery performance.
- Examination of equipment leakage, drainage and maintenance history.
- Comparison with historical operating performance.

The investigation findings shall distinguish verified observations from assumptions and unconfirmed explanations.

#### 12.8.3 OT Cybersecurity Escalation

A solvent discrepancy alone shall not automatically trigger a confirmed cybersecurity incident classification.

Cybersecurity escalation may be considered when supporting indicators exist, including:

- Unauthorised changes to relevant process or monitoring configurations.
- Unusual access to industrial control or monitoring systems.
- Unexpected changes to measurement records or monitoring data.
- Suspicious modification or deletion of relevant operational records.
- Unusual network activity associated with relevant OT assets.
- Security alerts from authorised OT monitoring or security tools.

Where supporting security indicators exist, the matter shall be referred to authorised OT cybersecurity personnel for independent assessment.

The monitoring system shall not automatically declare that a cyberattack has occurred.

#### 12.8.4 Investigation Ownership and Responsibilities

Investigation responsibilities shall be assigned according to the nature of the identified concern.

- Process engineering shall assess process conditions, measurement reliability and physical explanations.
- Instrumentation and maintenance personnel shall assess relevant instruments and equipment.
- OT cybersecurity personnel shall assess potential security-related indicators and preserve relevant security evidence.
- Authorised management shall oversee escalation and approve actions requiring operational authority.

The monitoring system shall record the assigned investigation owner where this information is available.

#### 12.8.5 Evidence Preservation

Relevant investigation evidence shall be preserved to support traceability and subsequent review.

Evidence may include:

- Original reconciliation inputs.
- Calculated discrepancy results.
- Measurement quality assessments.
- Relevant operating records.
- Monitoring alerts and timestamps.
- Security event references.
- Investigation observations and decisions.

Where technically available, preserved evidence shall retain its source identification, collection timestamp, integrity verification information and relevant access history.

Evidence handling shall support traceability and subsequent independent review.

Original source records shall not be silently overwritten by subsequent calculations or investigation updates.

Access to investigation evidence shall be restricted according to authorised roles and applicable security requirements.

#### 12.8.6 Investigation Outcomes and Closure

Investigation workflow status shall be recorded separately from investigation disposition.

Investigation workflow statuses shall include:

- OPEN: An investigation has been created but is not yet assigned or commenced.
- ASSIGNED: An authorised investigation owner has been assigned.
- IN_PROGRESS: Investigation activities are ongoing.
- ESCALATED: The investigation has been referred to another authorised team or management level.
- CLOSED: The authorised investigation owner has completed and documented the investigation.

Investigation dispositions shall include:

- EXPLAINED: A supported engineering or operational explanation has been established.
- UNDETERMINED: Available evidence is insufficient to establish the cause.
- SECURITY_REVIEW_REQUIRED: Supporting security indicators require independent cybersecurity assessment.

A CLOSED investigation shall have a documented disposition.

An investigation may be escalated while remaining open or in progress. Escalation shall not automatically imply investigation closure.

An investigation outcome shall not alter the original reconciliation calculation or retrospectively change its measurement quality status.

The system shall retain the investigation outcome, responsible reviewer, relevant timestamps and supporting evidence references where available.

Investigation closure shall require an authorised human decision.

### 12.9 Data Quality and Measurement Confidence

The monitoring system shall assess the quality and reliability of measurements and operational records before using them in solvent reconciliation calculations, process monitoring or investigation support.

Measurement availability alone shall not be treated as evidence of measurement validity or reliability.

Data quality assessment shall consider measurement completeness, validity, freshness, source identification, instrument condition and available measurement uncertainty.

#### 12.9.1 Measurement Data Quality Classification

The monitoring system shall distinguish the following measurement quality conditions:

- VALID: The measurement is available and passes applicable validation checks.
- MISSING: A required measurement or record is unavailable.
- STALE: The measurement is older than its approved freshness limit.
- INVALID: The measurement fails applicable validation or consistency checks.
- UNVERIFIED: The measurement is available but its source, accuracy or reliability has not been sufficiently established.
- CONFLICTING: Two or more relevant measurements or records disagree beyond their approved comparison limits.

VALID shall represent a measurement that passes all
applicable validation checks for the intended use.

VALID shall not coexist with contradictory conditions
such as MISSING, STALE or INVALID for the same assessment.

A measurement may have more than one applicable
non-valid quality condition simultaneously. The system
shall retain all relevant quality flags rather than
forcing a single condition where multiple data quality
issues exist.

A measurement quality condition shall be recorded separately from the numerical measurement value.

Missing measurements shall not be substituted with zero unless zero is explicitly recorded and independently validated as a genuine measurement.

#### 12.9.2 Measurement Source Identification

Each measurement used for monitoring or reconciliation shall retain its source identification where available.

Measurement sources may include:

- Tank level instruments.
- Flowmeters.
- Weighing systems.
- Temperature and pressure instruments.
- Laboratory measurements.
- Manually entered operating records.
- Inventory calculations and estimates.
- Authorised external data sources.

The system shall distinguish directly measured values from calculated, estimated and manually entered values.

Where available, measurement records shall retain the
observation timestamp and the data collection or ingestion
timestamp.

The distinction between measurement time and data
arrival time shall be maintained to support detection
of delayed or retrospectively received records.

The measurement source and method shall be considered
when assessing the suitability, reliability and accuracy
of data used in a particular calculation.

#### 12.9.3 Measurement Freshness and Completeness

Measurements shall be evaluated against approved data freshness requirements appropriate to their intended use.

The monitoring system shall identify missing, delayed or stale measurements and shall not silently treat them as current observations.

Required measurements shall be assessed for completeness before a reconciliation calculation is performed.

Where essential measurements are missing or stale, the system shall identify the affected calculation and apply the appropriate incomplete or unevaluated status.

Data freshness limits shall be established through engineering review and shall not be invented by the monitoring software.

#### 12.9.4 Instrument Condition and Calibration

Where instrument calibration or maintenance information is available, the monitoring system shall consider it when assessing measurement reliability.

Relevant information may include:

- Instrument identification.
- Calibration date.
- Calibration validity or due date.
- Calibration results.
- Instrument maintenance history.
- Known instrument faults.
- Measurement range and resolution.

A measurement from an instrument with an expired calibration status, known fault or unresolved reliability concern shall be appropriately flagged.

The monitoring system shall not independently certify an instrument as calibrated or fit for service.

Instrument verification and calibration approval shall remain the responsibility of authorised instrumentation personnel.

#### 12.9.5 Measurement Uncertainty

Measurement uncertainty shall be considered when evaluating the reliability of solvent inventory measurements and reconciliation results.

Relevant uncertainty sources may include:

- Instrument accuracy and resolution.
- Tank calibration and strapping-table accuracy.
- Tank geometry and level-to-volume conversion.
- Temperature compensation.
- Density assumptions.
- Flowmeter accuracy.
- Manual measurement and recording errors.
- Inventory estimation methods.

Where measurement uncertainty information is available, the system may retain and report the relevant uncertainty information alongside calculated results.

Where uncertainty information is unavailable or insufficient, the system shall identify this limitation.

The monitoring system shall not invent uncertainty values or present calculated results as having a verified accuracy that has not been established.

#### 12.9.6 Conflicting Measurements and Data Validation

Where multiple measurements or records relating to the same process condition are available, the monitoring system shall identify material inconsistencies using approved validation and comparison criteria.

Conflicting measurements shall not be silently averaged, substituted or discarded.

The original values and their respective sources shall remain available for review.

Resolution of material measurement conflicts shall require an authorised engineering or instrumentation review where appropriate.

#### 12.9.7 Measurement Confidence and Calculation Suitability

Measurement confidence shall be based on documented data quality evidence rather than arbitrary numerical scores.

The monitoring system shall distinguish between:

- Measurements suitable for the intended calculation.
- Measurements requiring review before use.
- Measurements unsuitable for the intended calculation.
- Measurements whose reliability cannot currently be established.

A measurement may be valid for one monitoring purpose but unsuitable for another calculation requiring greater accuracy or a different measurement basis.

Where measurement quality limitations materially affect a reconciliation, the system shall communicate those limitations alongside the calculated result or applicable reconciliation status.

Measurement confidence shall not be interpreted as proof of physical solvent loss, equipment failure or cybersecurity compromise.

Where measurement quality is insufficient to support
a reliable reconciliation calculation, the system shall
identify the calculation as unevaluated or otherwise
appropriately qualified.

The system shall not present an incomplete or
measurement-compromised reconciliation result as a
confirmed solvent loss.

The reason for the calculation limitation shall be
recorded and made available for authorised human review.

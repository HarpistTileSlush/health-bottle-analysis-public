# Blood Culture Bottle Stock Analysis

---

# Blood Culture Bottle Stock Reconciliation

Analysis of ordering and usage patterns for blood culture bottles across wards at a UK
district health board, undertaken as part of a student consultancy project. The goal was
to reconcile procurement data against actual clinical usage to identify stock wastage,
locate where it was concentrated, and propose practical, low-risk ways to reduce it.

## Context

Hospitals order blood culture bottles in three types (by colour), each tied to specific
test types and patient groups. Bottles can expire unused, and over-ordering at ward level
is difficult to spot without directly comparing procurement records against lab usage
records, two datasets that are not otherwise linked.

This project combined order-line procurement data with lab-recorded test and bottle usage
data across 200+ wards and units, to estimate where the two diverged.

## Method

- Cleaned and standardised raw procurement and lab datasets (R, tidyverse), including
  correcting miscoded hospital/ward fields, removing non-clinical demand (e.g. QA/NEQAS
  samples, central lab stock), and resolving duplicate or ambiguous ward mappings.
- Built a ward-matching crosswalk to join procurement and lab data despite inconsistent
  naming conventions between the two source systems.
- Reconciled ordered vs. consumed bottles at three levels: by bottle colour (type), by
  hospital site, and by individual ward, to cross-check findings at each level of
  aggregation.
- Treated "variance" (ordered minus consumed) as an **upper bound on waste**, not waste
  itself, since it also captures legitimate stock buffers and order/use timing
  differences. Findings are reported accordingly, split between net variance (can be
  negative) and matched-ward over-supply (the more conservative estimate).
- Modelled buffer-stock and inter-ward transfer options to reduce over-ordering without
  increasing the risk of shortages.

## Key findings

- Identified a subset of wards responsible for a disproportionate share of over-ordering,
  allowing targeted rather than blanket intervention.
- Estimated reconciled over-supply of approximately £30,000/year (matched wards,
  conservative basis), with a proposed phased plan estimated to reduce associated
  CO₂ impact by approximately 9 tonnes/year.
- Found a systematic imbalance between two bottle types that must be used in matched
  pairs, pointing to an unavoidable, quantifiable source of waste independent of ward
  behaviour.

## Repository contents

- `analysis.Rmd` — full analysis: data cleaning, reconciliation logic, and visualisations.
- Source data files are **not included** in this repository. Hospital and ward
  identifiers in the code have been anonymised to generic site/ward labels, to avoid
  identifying any specific NHS organisation or location.

## Tools

R (tidyverse, lubridate, janitor, scales).

## AI Declaration

AI tools were used to build the basics of the R code, debugging, and to clean up the aesthetics of graphs. Only data structure was provided to agents for context, ensuring confidentiality was preserved.

## Note on confidentiality

This project was delivered for a real health board through a student consultancy
programme. All identifying names (organisation, hospital sites, named wards) have been
removed or replaced with generic labels. Figures reported here reflect the project's
own findings but are presented at a level that does not identify the organisation
involved.

# FlightArchive Blueprint #1
## Historical Air Traffic Reconstruction Engine

**Status:** Draft — architectural concept
**Version:** 0.1
**Date:** November 2026

---

## 1. Purpose

The Historical Air Traffic Reconstruction Engine is the core system responsible for reconstructing air traffic for a selected historical date, time, and geographic area.

Its goal is to produce the most evidence-based reconstruction possible of the air traffic that existed at a given moment in history.

FlightArchive is not intended to invent missing traffic or present uncertain information as fact. It must distinguish documented evidence, derived estimates, and unknowns.

## 2. Core reconstruction question

The engine must be able to answer:

> What aircraft and flights were likely operating in this area at this specific historical moment, what evidence supports that reconstruction, and how certain are we?

A reconstruction is always bounded by:
- **Time:** a selected date and time (with a clearly defined time standard).
- **Geography:** an area, region, country, airspace, or global view.
- **Evidence:** source material available to FlightArchive.
- **Confidence:** the strength and limitations of the evidence.

## 3. Guiding principles

1. **Evidence before assumption.** A source-supported fact takes precedence over an unsupported inference.
2. **No false certainty.** Estimates and uncertain matches must be visibly distinguished from verified facts.
3. **Source traceability.** Every reconstructed flight or material claim must be traceable to its sources and processing history.
4. **Historical context.** The system must use information appropriate to the period being reconstructed; present-day data must not silently be treated as historical fact.
5. **Incremental improvement.** Reconstructions may improve as additional sources are collected or interpreted.
6. **Preserve original evidence.** Source material and extracted observations must not be silently overwritten by later interpretations.
7. **Time is explicit.** Time zone, date, and conversion assumptions must be recorded.
8. **Reconstruction, not simulation by invention.** Where evidence is absent, the system should report a gap rather than manufacture a flight.

## 4. Conceptual workflow

The following is a proposed workflow, not a finalized technical implementation.

1. **Select reconstruction target** — date, time, and geographic area.
2. **Collect sources** — schedules, timetables, route maps, aircraft records, airport information, photographs, operational records, and other relevant historical material.
3. **Extract observations** — identify relevant facts in each source, retaining provenance and context.
4. **Normalize observations** — standardize dates, times, airport identifiers, airline names, flight numbers, aircraft types, registrations, and other relevant fields where possible.
5. **Resolve and correlate** — determine whether observations from different sources refer to the same flight or operation.
6. **Build candidate traffic** — identify flights that may have been airborne within the selected time and area.
7. **Estimate flight state** — where sufficient evidence exists, derive a possible position or operational state, clearly marking estimates and assumptions.
8. **Evaluate confidence** — assess the evidence supporting each result.
9. **Render reconstruction** — present reconstructed traffic and its uncertainty in a suitable interface.
10. **Preserve the reconstruction** — retain source references, processing assumptions, and the reconstruction version so the result can be revisited.

## 5. Evidence categories

The engine should distinguish source evidence by its nature. Initial categories to investigate include:

- **Scheduled evidence:** timetable, published schedule, route plan, or scheduled departure/arrival.
- **Operational evidence:** records indicating a flight actually operated.
- **Position evidence:** observations that directly or indirectly indicate an aircraft position at a given time.
- **Identity evidence:** registration, aircraft type, operator, flight number, or other identity information.
- **Contextual evidence:** airport data, route maps, historical fleet information, weather, operational constraints, and other contextual material.

These categories are conceptual. Their precise data structures and source-specific handling remain to be designed.

## 6. Reconstruction levels

A reconstruction may contain different levels of evidence. These are proposed labels, not yet a finalized scoring system.

- **Documented:** directly supported by a source that documents the relevant operation or state.
- **Corroborated:** supported by multiple independent or complementary sources.
- **Derived:** inferred by processing or combining source observations.
- **Estimated:** plausible, but dependent on assumptions or incomplete evidence.
- **Unknown:** evidence is insufficient to make a defensible determination.

These labels should not be collapsed into a single binary distinction between 'real' and 'not real'.

## 7. Flight and aircraft identity

The engine must eventually address the difference between:
- a scheduled flight and an operated flight;
- a flight number and a unique flight operation;
- an airline/operator and an aircraft owner;
- an aircraft type and a specific aircraft;
- a registration and an aircraft identity across time;
- a route and the actual path flown.

These distinctions are important because identifiers, operators, aircraft assignments, and schedules can change over time.

The data model and identity-resolution rules are not defined in this Blueprint.

## 8. Time and geography

The reconstruction must explicitly handle:
- the selected historical date and time;
- time zones and historical time-zone rules;
- UTC conversion and its recorded assumptions;
- geographic boundaries and coordinate systems;
- uncertainty in time or location reported by historical sources.

A displayed reconstruction must not imply that a position is exact if the evidence only supports a broad time window, route, or geographic region.

## 9. Missing and conflicting evidence

Sources may be incomplete, contradictory, misprinted, ambiguous, or inaccurate.

The engine should:
- retain conflicting observations instead of silently choosing one;
- record the source and context of each observation;
- document resolution decisions;
- avoid treating the absence of a record as proof that a flight did not exist;
- avoid creating a position or flight solely to fill a visual gap.

Detailed conflict-resolution rules are a future design task.

## 10. Output of a reconstruction

A reconstruction result should conceptually include:
- the reconstruction target (time and area);
- candidate flights and aircraft;
- available flight and aircraft identity information;
- route, position, or state where evidence supports it;
- evidence and source references;
- reconstruction status or confidence;
- assumptions and limitations;
- engine and reconstruction version.

The exact output schema and interface remain undecided.

## 11. Initial development phases

### Phase A — Historical source research
Identify source types, availability, reliability, temporal coverage, and extraction methods.

### Phase B — Conceptual data model
Define the entities and relationships required for sources, observations, flights, aircraft, schedules, airports, and reconstruction results.

### Phase C — Reconstruction logic
Design the rules for correlating observations and deriving candidate flights and states.

### Phase D — Validation
Develop methods for comparing reconstructions with known historical records and documenting errors and uncertainty.

### Phase E — Prototype
Implement a small, controlled reconstruction test using a clearly defined period, area, and source set.

No phase implies that a technology stack or algorithm has already been selected.

## 12. First test case

The original project concept proposes reconstructing air traffic over the territory of the former Yugoslavia on **25 June 1988**.

This date and area may serve as an initial test case, subject to a source-availability assessment.

Before attempting a full reconstruction, the project should determine:
- which historical timetables and other sources are available;
- what geographic and temporal coverage they provide;
- what can be verified;
- what remains uncertain or unavailable.

## 13. Open questions

The following are deliberately unresolved:

- What source types can support the reconstruction of actual airborne traffic, rather than scheduled traffic alone?
- How should schedule-based candidate flights be converted into estimated airborne states?
- How should the engine represent uncertainty in departure time, duration, route, and position?
- How should historical time zones and daylight-saving rules be sourced and validated?
- How can source independence and corroboration be evaluated?
- How can the reconstructed result be validated against independent records?
- What should the first prototype include, and what must it explicitly exclude?

## 14. Scope of this Blueprint

This document establishes a conceptual framework and principles for the Reconstruction Engine.

It does **not**:
- specify a database schema;
- select a programming language, framework, or database;
- prescribe a specific reconstruction algorithm;
- guarantee that complete historical traffic can be reconstructed;
- treat timetables as proof that a flight operated;
- define a finalized confidence score.

Those decisions require further research and separate documentation.

---

*First we understand what we are building. Only then do we build it.*

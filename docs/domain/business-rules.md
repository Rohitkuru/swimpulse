# Business Rules

## Purpose

This document defines the business rules that govern the behavior of SwimPulse.

Business rules describe the constraints, validations, and expected behavior of the system independent of the user interface, API, or database.

All backend services should enforce these rules consistently.

---

# Rule Categories

Business rules are grouped into the following categories:

* Athlete
* Competition
* Race
* Practice
* Video
* Goals
* Analytics
* AI

---

# Athlete Rules

## BR-001 — Athlete Identity

Every athlete must have a unique identifier.

---

## BR-002 — Date of Birth

An athlete's date of birth cannot be in the future.

---

## BR-003 — Growth History

Height and weight measurements must be stored as historical records.

Historical measurements must never be overwritten.

---

## BR-004 — Athlete Ownership

Every athlete must belong to exactly one coach in the MVP.

Future releases may support multiple coaches.

---

# Competition Rules

## BR-005 — Competition Dates

A competition end date cannot be earlier than its start date.

---

## BR-006 — Pool Length

Pool length must be either:

* 25 meters
* 50 meters

---

## BR-007 — Competition Level

Competition level must be one of:

* Club
* District
* State
* National
* International

---

# Race Rules

## BR-008 — Competition Association

Every race must belong to exactly one competition.

---

## BR-009 — Athlete Association

Every race must belong to exactly one athlete.

---

## BR-010 — Race Time

Official race time must be greater than zero.

---

## BR-011 — Split Validation

If split times are recorded:

* They must be in chronological order.
* Their sum should approximately equal the official race time.
* Minor timing differences are acceptable due to rounding.

---

## BR-012 — Personal Best

Whenever a new race is recorded:

* The system automatically checks whether it is a Personal Best.
* The Personal Best status is recalculated for the corresponding event.

---

## BR-013 — Event Consistency

A Personal Best is always calculated separately for:

* Stroke
* Distance
* Pool length

Example:

* 100 Freestyle (25m)
* 100 Freestyle (50m)

are treated as different events.

---

# Practice Rules

## BR-014 — Practice Ownership

Every practice session belongs to one athlete.

---

## BR-015 — Practice Date

Practice dates cannot be in the future.

---

## BR-016 — Practice Distance

Total practice distance must be greater than zero.

---

## BR-017 — Practice Sets

A practice may contain zero or more practice sets.

Each practice set belongs to exactly one practice.

---

# Video Rules

## BR-018 — Race Association

Every uploaded race video must reference an existing race.

---

## BR-019 — Video Storage

The application stores only the metadata in DynamoDB.

Video files are stored in Amazon S3.

---

## BR-020 — Multiple Videos

A race may have multiple associated videos.

Examples:

* Parent recording
* Official livestream
* Coach recording

---

# Goal Rules

## BR-021 — Goal Ownership

Each goal belongs to one athlete.

---

## BR-022 — Goal Status

Goal status must be one of:

* Active
* Completed
* Archived

---

## BR-023 — Automatic Progress

Goal progress should be recalculated whenever relevant race results or measurements change.

---

# Analytics Rules

## BR-024 — Derived Data

Analytics are derived from historical data.

Users must not manually edit calculated analytics.

---

## BR-025 — Historical Integrity

Historical race records must never be modified by analytics calculations.

---

## BR-026 — Personal Best Calculation

Personal Best calculations must always use official race results.

Practice times must not affect Personal Bests.

---

## BR-027 — Season Best Calculation

Season Bests are calculated independently for each competition season.

---

# AI Rules

## BR-028 — Read-Only Data

AI services must never modify athlete data directly.

---

## BR-029 — Explainability

AI-generated recommendations should reference available performance data whenever possible.

---

## BR-030 — Regeneration

AI summaries may be regenerated without changing the underlying athlete records.

---

# System Rules

## BR-031 — Auditability

Every modification should record:

* Creation timestamp
* Last update timestamp

Future versions may also track the user who performed the action.

---

## BR-032 — Soft Delete

Business records should be archived or marked inactive where appropriate rather than permanently deleted.

This preserves historical athlete information.

---

## BR-033 — Data Validation

All user input must be validated before it is stored.

---

## BR-034 — Immutable History

Historical race results and practice records represent factual events.

Corrections may be made when necessary, but previous versions should not be silently lost in future releases that introduce audit history.

---

# Future Business Rules

Future releases may introduce rules for:

* Multi-coach assignments
* Club ownership
* Team membership
* National rankings
* Qualification standards
* Injury tracking
* Nutrition plans
* Equipment tracking

---

# Guiding Principles

Every new feature should answer the following questions:

1. What business problem does it solve?
2. What rules govern the feature?
3. Which existing rules does it affect?
4. Does it introduce any new business constraints?

Business rules should be documented before implementation to ensure consistent behavior across the application.

---

# Summary

Business rules define the expected behavior of SwimPulse independent of the underlying technology. They provide a consistent foundation for backend services, APIs, analytics, AI features, and future enhancements.

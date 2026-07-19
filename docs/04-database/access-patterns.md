# DynamoDB Access Patterns

## Purpose

This document defines how SwimPulse will access data stored in Amazon DynamoDB.

Unlike relational databases, DynamoDB table design begins with understanding application queries. The data model and indexes will be optimized around these access patterns.

---

# Design Principle

The primary rule for DynamoDB is:

> Design for the queries you need, not for the entities you have.

Every access pattern described in this document should be supported efficiently without requiring table scans.

---

# Core Business Domains

The MVP consists of the following business domains:

* Athlete
* Competition
* Practice
* Race
* Video
* Analytics
* Goals

Each domain introduces its own set of access patterns.

---

# Athlete Access Patterns

## AP-001

Retrieve an athlete by Athlete ID.

**Used by:**

* Athlete Profile
* Dashboard
* AI Coach

---

## AP-002

Retrieve all athletes.

**Used by:**

* Athlete List
* Future Coach Dashboard

---

## AP-003

Retrieve athlete growth history.

**Used by:**

* Growth Charts
* Analytics

---

## AP-004

Retrieve athlete goals.

**Used by:**

* Dashboard
* Goal Progress

---

# Competition Access Patterns

## AP-005

Retrieve a competition by Competition ID.

---

## AP-006

Retrieve all competitions for an athlete.

Sort by date (newest first).

---

## AP-007

Retrieve competitions by year.

---

## AP-008

Retrieve competitions by competition level.

Examples:

* District
* State
* National

---

# Race Access Patterns

## AP-009

Retrieve all races for an athlete.

---

## AP-010

Retrieve races for a specific competition.

---

## AP-011

Retrieve races by event.

Examples:

* 50 Freestyle
* 100 Butterfly
* 200 IM

---

## AP-012

Retrieve personal bests.

---

## AP-013

Retrieve season bests.

---

## AP-014

Retrieve race history for an event.

Example:

All 100 Freestyle races.

---

# Practice Access Patterns

## AP-015

Retrieve all practice sessions.

---

## AP-016

Retrieve practices within a date range.

---

## AP-017

Retrieve timed practice sets.

---

## AP-018

Retrieve coach observations.

---

## AP-019

Retrieve practices by stroke.

---

# Video Access Patterns

## AP-020

Retrieve all videos for a race.

---

## AP-021

Retrieve all videos for an athlete.

---

## AP-022

Retrieve videos by competition.

---

# Analytics Access Patterns

## AP-023

Retrieve athlete analytics.

---

## AP-024

Retrieve progress charts.

---

## AP-025

Retrieve personal best progression.

---

## AP-026

Retrieve goal progress.

---

# AI Access Patterns

## AP-027

Retrieve AI-generated race summaries.

---

## AP-028

Retrieve AI-generated season summaries.

---

## AP-029

Retrieve AI recommendations.

---

# Dashboard Access Patterns

The dashboard combines several queries:

* Athlete summary
* Current goals
* Latest competitions
* Latest races
* Latest practice sessions
* Personal bests
* Progress charts
* AI insights

The dashboard should minimize the number of database requests wherever possible.

---

# Search Access Patterns

Support searching by:

* Athlete
* Competition
* Stroke
* Event
* Date
* Season

Future releases may introduce full-text search if required.

---

# Reporting Access Patterns

Generate reports for:

* Athlete
* Competition
* Practice
* Season
* Annual performance

---

# Access Pattern Priorities

## P0 (Required for MVP)

* Athlete profile
* Competition history
* Race history
* Practice history
* Video retrieval
* Dashboard
* Personal bests

---

## P1 (Important)

* Goal tracking
* Analytics
* AI summaries

---

## P2 (Future)

* Multi-athlete comparisons
* Club reporting
* Federation reporting
* National benchmarking

---

# Design Considerations

When designing the DynamoDB table:

* Avoid table scans.
* Prefer query operations using partition keys.
* Use sort keys for chronological ordering.
* Add Global Secondary Indexes (GSIs) only when required by access patterns.
* Keep write operations simple and predictable.

Every new feature should first define its access pattern before introducing new attributes or indexes.

---

# Summary

The SwimPulse DynamoDB design will be driven by application access patterns rather than traditional relational modeling. This approach ensures efficient queries, predictable performance, and a scalable data model as the platform evolves.

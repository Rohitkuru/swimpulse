# Global Secondary Indexes (GSIs)

## Purpose

This document defines the Global Secondary Indexes (GSIs) used by SwimPulse.

GSIs provide additional query patterns without requiring table scans. Only indexes required by the MVP are created to keep the database simple and cost-effective.

---

# Design Principles

The following principles guide index design:

* Create indexes only for required access patterns.
* Avoid unnecessary indexes.
* Optimize for read performance.
* Prefer querying over scanning.
* Review index usage as the application evolves.

---

# Athletes Table

## GSI 1 - Coach Index

### Purpose

Retrieve all athletes assigned to a coach.

### Index Definition

| Attribute     | Value   |
| ------------- | ------- |
| Partition Key | coachId |

### Example Queries

* Show all athletes for Coach A.
* Future coach dashboard.

---

# Competitions Table

## GSI 1 - Competition Date

### Purpose

Retrieve competitions by year or season.

### Index Definition

| Attribute     | Value     |
| ------------- | --------- |
| Partition Key | year      |
| Sort Key      | startDate |

### Example Queries

* Competitions in 2026.
* Most recent competitions.

---

# Races Table

## GSI 1 - Athlete History

### Purpose

Retrieve all races for an athlete.

### Index Definition

| Attribute     | Value     |
| ------------- | --------- |
| Partition Key | athleteId |
| Sort Key      | raceDate  |

### Example Queries

* Race history.
* Recent races.
* Dashboard.

---

## GSI 2 - Competition Races

### Purpose

Retrieve all races belonging to a competition.

### Index Definition

| Attribute     | Value         |
| ------------- | ------------- |
| Partition Key | competitionId |
| Sort Key      | event         |

### Example Queries

* All races in a competition.
* Competition summary.

---

## GSI 3 - Event History

### Purpose

Retrieve all performances for a specific event.

### Index Definition

| Attribute     | Value        |
| ------------- | ------------ |
| Partition Key | athleteEvent |

### athleteEvent Format

```text
ATH001#100_FREE_LCM
```

Examples:

* ATH001#50_FREE_SCM
* ATH001#100_BUTTERFLY_LCM
* ATH001#200_IM_LCM

### Example Queries

* Personal Best calculation.
* Season Best calculation.
* Progress charts.

---

# Practices Table

## GSI 1 - Athlete Practices

### Purpose

Retrieve practices for an athlete.

### Index Definition

| Attribute     | Value        |
| ------------- | ------------ |
| Partition Key | athleteId    |
| Sort Key      | practiceDate |

---

# Videos Table

## GSI 1 - Athlete Videos

### Purpose

Retrieve all videos for an athlete.

### Index Definition

| Attribute     | Value      |
| ------------- | ---------- |
| Partition Key | athleteId  |
| Sort Key      | uploadedAt |

---

## GSI 2 - Race Videos

### Purpose

Retrieve videos associated with a race.

### Index Definition

| Attribute     | Value  |
| ------------- | ------ |
| Partition Key | raceId |

---

# Goals Table

## GSI 1 - Athlete Goals

### Purpose

Retrieve goals for an athlete.

### Index Definition

| Attribute     | Value      |
| ------------- | ---------- |
| Partition Key | athleteId  |
| Sort Key      | targetDate |

---

# Analytics Table

Analytics uses its primary key for lookups.

No GSIs are required for the MVP.

---

# Index Summary

| Table        | Index         | Purpose              |
| ------------ | ------------- | -------------------- |
| Athletes     | coachId       | Coach's athletes     |
| Competitions | year          | Competitions by year |
| Races        | athleteId     | Athlete race history |
| Races        | competitionId | Competition races    |
| Races        | athleteEvent  | Event progression    |
| Practices    | athleteId     | Practice history     |
| Videos       | athleteId     | Athlete videos       |
| Videos       | raceId        | Race videos          |
| Goals        | athleteId     | Athlete goals        |

---

# Future GSIs

Potential future indexes include:

* Club ID
* Team ID
* Competition Level
* Country
* State
* Age Group
* Qualification Status

These indexes will be added only when required by new access patterns.

---

# Summary

SwimPulse uses a minimal set of Global Secondary Indexes focused on the MVP's access patterns. Additional indexes should be introduced only when justified by new features or performance requirements.

# Data Model

## Purpose

This document defines the core business domain models used throughout SwimPulse.

These models represent the business concepts of the application and are independent of the underlying database implementation.

The DynamoDB table design will be derived from these models and the previously defined access patterns.

---

# Domain Overview

The SwimPulse MVP consists of the following domains:

* Athlete
* Coach
* Competition
* Race
* Practice
* Practice Set
* Video
* Goal
* Analytics Snapshot
* AI Insight

These domains form the foundation of the application.

---

# Domain Relationship Overview

```text
Coach
   │
   ├──────────────┐
   │              │
   ▼              ▼
Athlete -----> Goal
   │
   ├──────────────┐
   │              │
   ▼              ▼
Competition    Practice
   │              │
   ▼              ▼
 Race      Practice Set
   │
   ▼
Video

Athlete
   │
   ▼
Analytics Snapshot
   │
   ▼
AI Insight
```

---

# Athlete

Represents a competitive swimmer.

## Attributes

| Attribute     | Description           |
| ------------- | --------------------- |
| athleteId     | Unique identifier     |
| firstName     | First name            |
| lastName      | Last name             |
| dateOfBirth   | Date of birth         |
| gender        | Gender                |
| height        | Current height        |
| weight        | Current weight        |
| club          | Swimming club         |
| coachId       | Assigned coach        |
| primaryEvents | Preferred events      |
| createdAt     | Creation timestamp    |
| updatedAt     | Last update timestamp |

---

# Coach

Represents the primary coach responsible for athlete development.

## Attributes

| Attribute | Description       |
| --------- | ----------------- |
| coachId   | Unique identifier |
| name      | Coach name        |
| club      | Club              |
| email     | Contact email     |
| phone     | Contact number    |

> MVP Note: The first release assumes a single authenticated user. This model exists to support future expansion.

---

# Competition

Represents a swimming meet.

## Attributes

| Attribute     | Description               |
| ------------- | ------------------------- |
| competitionId | Unique identifier         |
| name          | Competition name          |
| level         | District, State, National |
| city          | Host city                 |
| country       | Host country              |
| poolLength    | 25m or 50m                |
| startDate     | Start date                |
| endDate       | End date                  |

---

# Race

Represents one event swum during a competition.

## Attributes

| Attribute      | Description           |
| -------------- | --------------------- |
| raceId         | Unique identifier     |
| athleteId      | Athlete reference     |
| competitionId  | Competition reference |
| stroke         | Stroke                |
| distance       | Distance              |
| officialTime   | Official result       |
| splitTimes     | Race splits           |
| lane           | Lane number           |
| heat           | Heat number           |
| rank           | Final ranking         |
| isPersonalBest | Personal Best flag    |

---

# Practice

Represents one training session.

## Attributes

| Attribute     | Description          |
| ------------- | -------------------- |
| practiceId    | Unique identifier    |
| athleteId     | Athlete reference    |
| date          | Practice date        |
| poolLength    | Pool size            |
| totalDistance | Total meters         |
| coachNotes    | Coach observations   |
| swimmerNotes  | Athlete observations |

---

# Practice Set

Represents an individual set within a practice.

Examples:

* 10 × 100 Free
* 8 × 50 Fly
* Kick Set
* Pull Set

## Attributes

| Attribute   | Description             |
| ----------- | ----------------------- |
| setId       | Unique identifier       |
| practiceId  | Parent practice         |
| stroke      | Stroke                  |
| repetitions | Number of repetitions   |
| distance    | Distance per repetition |
| interval    | Send-off interval       |
| averageTime | Average swim time       |
| notes       | Additional notes        |

---

# Video

Represents a competition race video.

## Attributes

| Attribute    | Description       |
| ------------ | ----------------- |
| videoId      | Unique identifier |
| raceId       | Associated race   |
| athleteId    | Athlete reference |
| s3Key        | S3 object key     |
| duration     | Video duration    |
| recordedDate | Recording date    |

---

# Goal

Represents an athlete objective.

Examples:

* Qualify for State Championships
* Swim sub-1:20 in 100 Freestyle
* Reduce stroke count

## Attributes

| Attribute   | Description                 |
| ----------- | --------------------------- |
| goalId      | Unique identifier           |
| athleteId   | Athlete reference           |
| title       | Goal title                  |
| description | Goal details                |
| targetDate  | Target completion           |
| status      | Active, Completed, Archived |

---

# Analytics Snapshot

Stores calculated metrics at a point in time.

Examples:

* Personal Bests
* Improvement %
* Stroke Trends
* Race Count

## Attributes

| Attribute     | Description       |
| ------------- | ----------------- |
| snapshotId    | Unique identifier |
| athleteId     | Athlete reference |
| generatedDate | Calculation date  |
| metrics       | Analytics values  |

---

# AI Insight

Stores AI-generated summaries.

Examples:

* Race summary
* Competition summary
* Weekly summary
* Improvement recommendation

## Attributes

| Attribute   | Description            |
| ----------- | ---------------------- |
| insightId   | Unique identifier      |
| athleteId   | Athlete reference      |
| insightType | Race, Season, Practice |
| generatedAt | Generation timestamp   |
| summary     | AI response            |

---

# Domain Rules

* An Athlete participates in many Competitions.
* A Competition contains many Races.
* An Athlete has many Practices.
* A Practice contains many Practice Sets.
* A Race may have multiple Videos.
* An Athlete may have multiple Goals.
* Analytics are generated from historical data.
* AI Insights are generated from analytics and historical records.

---

# Future Domain Models

The following models are intentionally deferred:

* Club
* Team
* Squad
* Season
* Injury
* Nutrition
* Equipment
* Meet Officials
* Federation

---

# Summary

These domain models represent the core language of SwimPulse. They are independent of the database implementation and will be used consistently across the frontend, backend, APIs, analytics engine, AI services, and DynamoDB design.

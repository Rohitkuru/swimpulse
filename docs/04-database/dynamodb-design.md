# DynamoDB Design

## Purpose

This document defines the DynamoDB database design for SwimPulse.

The MVP uses a **multi-table design** to keep the data model simple, readable, and maintainable while leveraging DynamoDB's managed, scalable architecture.

This approach prioritizes rapid development and ease of understanding. As SwimPulse grows, the data model can evolve without affecting the application's business logic.

---

# Design Principles

The database design follows these principles:

* Keep the schema simple.
* Design tables around business domains.
* Optimize for the application's access patterns.
* Avoid unnecessary complexity.
* Minimize duplicate data where practical.
* Allow future migration to a single-table design if required.

---

# Database Overview

The MVP consists of the following tables:

| Table        | Purpose                                   |
| ------------ | ----------------------------------------- |
| Athletes     | Athlete profiles and personal information |
| Competitions | Swimming competitions and meets           |
| Races        | Official race results                     |
| Practices    | Training sessions and practice sets       |
| Videos       | Competition video metadata                |
| Goals        | Athlete goals                             |
| Analytics    | Cached analytics and summaries            |

---

# Athletes Table

## Purpose

Stores athlete profile information.

### Primary Key

| Attribute | Type          |
| --------- | ------------- |
| athleteId | Partition Key |

### Example Item

```json
{
  "athleteId": "ATH001",
  "firstName": "Arjun",
  "lastName": "K",
  "dateOfBirth": "2017-04-01",
  "height": 140,
  "weight": 34,
  "club": "ABC Swimming Club",
  "coachId": "COACH001",
  "createdAt": "2026-07-19T10:00:00Z",
  "updatedAt": "2026-07-19T10:00:00Z"
}
```

---

# Competitions Table

## Purpose

Stores swimming meet information.

### Primary Key

| Attribute     | Type          |
| ------------- | ------------- |
| competitionId | Partition Key |

### Example Attributes

* competitionId
* name
* level
* city
* country
* poolLength
* startDate
* endDate

---

# Races Table

## Purpose

Stores official race results.

Each item represents one athlete swimming one event in one competition.

### Primary Key

| Attribute | Type          |
| --------- | ------------- |
| raceId    | Partition Key |

### Important Attributes

* athleteId
* competitionId
* event
* stroke
* distance
* poolLength
* officialTime
* splitTimes
* lane
* heat
* rank
* isPersonalBest
* recordedAt

---

# Practices Table

## Purpose

Stores practice sessions.

Each item represents one training session.

### Primary Key

| Attribute  | Type          |
| ---------- | ------------- |
| practiceId | Partition Key |

### Attributes

* athleteId
* practiceDate
* totalDistance
* poolLength
* coachNotes
* practiceSets
* createdAt

For the MVP, **practice sets will be stored as a nested list within the practice record**. If practice analytics become more sophisticated, they can later be split into their own table.

---

# Videos Table

## Purpose

Stores metadata for competition videos.

Video files are stored in Amazon S3.

### Primary Key

| Attribute | Type          |
| --------- | ------------- |
| videoId   | Partition Key |

### Attributes

* athleteId
* raceId
* competitionId
* s3Key
* duration
* fileSize
* uploadedAt

---

# Goals Table

## Purpose

Stores athlete goals.

### Primary Key

| Attribute | Type          |
| --------- | ------------- |
| goalId    | Partition Key |

### Attributes

* athleteId
* title
* description
* targetDate
* targetValue
* status
* createdAt

---

# Analytics Table

## Purpose

Stores precomputed analytics to improve dashboard performance.

Examples include:

* Personal Bests
* Season Bests
* Performance trends
* Goal progress
* AI-generated summaries

### Primary Key

| Attribute  | Type          |
| ---------- | ------------- |
| athleteId  | Partition Key |
| metricType | Sort Key      |

### Example metricType values

* PB
* SB
* DASHBOARD
* FREESTYLE_TREND
* BUTTERFLY_TREND
* GOAL_PROGRESS
* AI_SUMMARY

---

# Relationships

Although DynamoDB does not enforce relationships, the application maintains the following logical references:

```text
Athlete
│
├── Competitions (through Races)
├── Races
├── Practices
├── Videos
├── Goals
└── Analytics

Competition
└── Races

Race
└── Videos
```

---

# Data Ownership

| Domain      | Owner Table  |
| ----------- | ------------ |
| Athlete     | Athletes     |
| Competition | Competitions |
| Race        | Races        |
| Practice    | Practices    |
| Video       | Videos       |
| Goal        | Goals        |
| Analytics   | Analytics    |

Each table owns its data. Cross-table references are handled by the backend service layer.

---

# Design Decisions

## Why Multiple Tables?

* Easier to understand.
* Easier to debug.
* Simpler API implementation.
* Better suited for an MVP.
* Lower learning curve for DynamoDB.

---

## Why Store Videos in S3?

Video files are large and are not suitable for DynamoDB.

Only metadata is stored in the Videos table.

---

## Why Cache Analytics?

Performance metrics are derived from historical data.

Caching them:

* Improves dashboard response time.
* Reduces repeated calculations.
* Simplifies frontend requests.

---

# Future Evolution

As SwimPulse grows, the database can evolve to support:

* Multiple coaches
* Clubs
* Teams
* Seasons
* National benchmarks
* Wearable integrations

The backend service layer should isolate database access so future schema changes have minimal impact on the rest of the application.

---

# Summary

The SwimPulse MVP uses a multi-table DynamoDB design centered around business domains. This approach balances simplicity, maintainability, and scalability while keeping the implementation approachable for rapid development. The service layer abstracts database interactions, allowing the data model to evolve as the platform grows.

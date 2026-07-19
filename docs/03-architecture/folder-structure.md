# Project Structure

## Purpose

This document defines the directory structure for the SwimPulse project.

The goals of this structure are:

* Keep related code together.
* Organize the project around business domains.
* Make navigation easy.
* Support future growth without major refactoring.
* Maintain a clear separation between frontend, backend, infrastructure, analytics, and documentation.

---

# Repository Structure

```text
swimpulse/
│
├── docs/                 # Product and technical documentation
├── frontend/             # React application
├── backend/              # FastAPI application
├── analytics/            # Analytics algorithms and formulas
├── vision/               # Computer vision experiments
├── ai/                   # AI prompts and future AI services
├── infra/                # AWS infrastructure
├── scripts/              # Utility scripts
├── tests/                # Cross-module integration tests
├── .github/              # GitHub workflows
│
├── README.md
├── LICENSE
└── .gitignore
```

---

# Backend Structure

The backend is organized by **feature**, not by framework layer.

```text
backend/
│
├── app/
│
│   ├── athlete/
│   │   ├── api.py
│   │   ├── service.py
│   │   ├── repository.py
│   │   ├── schemas.py
│   │   └── models.py
│   │
│   ├── competition/
│   ├── practice/
│   ├── race/
│   ├── video/
│   ├── analytics/
│   ├── dashboard/
│   ├── ai/
│   │
│   ├── common/
│   │   ├── config.py
│   │   ├── exceptions.py
│   │   ├── logger.py
│   │   ├── security.py
│   │   └── utils.py
│   │
│   ├── main.py
│   └── dependencies.py
│
├── requirements.txt
└── pyproject.toml
```

### Why Feature-Based?

Everything related to one business capability lives together.

Example:

```
Athlete

API
Business Logic
Validation
Database Access
Models
```

A developer only needs one folder to understand the Athlete module.

---

# Frontend Structure

```text
frontend/
│
├── src/
│
│   ├── pages/
│   ├── components/
│   ├── layouts/
│   ├── hooks/
│   ├── services/
│   ├── types/
│   ├── utils/
│   ├── assets/
│   ├── routes/
│   ├── contexts/
│   └── styles/
│
├── public/
└── package.json
```

As the application grows, pages should remain focused on composing reusable components rather than containing business logic.

---

# Analytics Module

```text
analytics/
│
├── calculations/
├── metrics/
├── reports/
├── charts/
├── benchmarks/
└── formulas/
```

Responsibilities:

* Performance calculations
* Trend analysis
* Benchmark comparisons
* Report generation

---

# Vision Module

```text
vision/
│
├── detection/
├── tracking/
├── pose/
├── preprocessing/
├── experiments/
└── models/
```

This module is isolated because computer vision is not part of the MVP but will become important later.

---

# AI Module

```text
ai/
│
├── prompts/
├── assistants/
├── summaries/
├── recommendations/
└── evaluation/
```

Responsibilities:

* AI prompts
* Performance summaries
* Coaching recommendations
* Future LLM integrations

---

# Infrastructure

```text
infra/
│
├── aws/
├── deployment/
├── environments/
└── monitoring/
```

---

# Scripts

```text
scripts/
│
├── setup/
├── migration/
├── import/
└── export/
```

---

# Documentation

```text
docs/
│
├── 01-overview/
├── 02-requirements/
├── 03-architecture/
├── 04-database/
├── 05-api/
├── 06-ui-ux/
├── 07-analytics/
├── 08-ai/
├── 09-development/
└── 10-release/
```

---

# Naming Conventions

## Directories

* lowercase
* singular where appropriate
* descriptive names

Examples:

* athlete
* competition
* analytics

---

## Python Files

Use snake_case.

Examples:

* service.py
* repository.py
* security.py

---

## React Components

Use PascalCase.

Examples:

* AthleteCard.tsx
* RaceTable.tsx
* ProgressChart.tsx

---

# Architectural Principles

* Organize by business feature.
* Keep modules loosely coupled.
* Avoid circular dependencies.
* Shared code belongs in `common`.
* Business logic belongs in services.
* Database access belongs in repositories.
* APIs should remain thin and delegate work to services.

---

# Future Expansion

New business domains can be added without changing the existing structure.

Examples:

* nutrition/
* injuries/
* wearable/
* federation/
* club/

Each new module should follow the same internal organization.

---

# Summary

The SwimPulse project structure is organized around business domains rather than technical layers. This approach improves readability, maintainability, and scalability while allowing each feature to evolve independently.

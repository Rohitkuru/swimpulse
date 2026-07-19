# System Overview

## Purpose

This document describes the overall architecture of SwimPulse.

It explains how the major components interact and establishes the architectural principles that guide the implementation.

---

# Architecture Style

SwimPulse follows a layered architecture.

```
Browser (React)

↓

REST API (FastAPI)

↓

Business Services

↓

Repositories

↓

Amazon DynamoDB

Amazon S3
```

Each layer has a single responsibility and communicates only with the layer directly below it.

---

# High-Level Components

The MVP consists of six major components.

## 1. Frontend

Responsibilities

- User Interface
- Forms
- Dashboards
- Charts
- Video Player
- Authentication

Technology

- React
- Vite
- TypeScript
- Tailwind
- shadcn/ui

---

## 2. Backend API

Responsibilities

- Business Logic
- Validation
- Authentication
- Analytics
- AI Integration
- File Management

Technology

- FastAPI
- Python

---

## 3. Database

Responsibilities

- Athlete Data
- Competition Data
- Practice Data
- Race Data
- Analytics Data

Technology

Amazon DynamoDB

---

## 4. Object Storage

Responsibilities

Store

- Videos
- Images
- Documents

Technology

Amazon S3

---

## 5. Analytics Engine

Responsibilities

Calculate

- Personal Best
- Improvement
- Goal Progress
- Performance Trends
- Statistics

---

## 6. AI Layer

Responsibilities

Generate

- Race summaries
- Competition summaries
- Recommendations
- Performance explanations

---

# Data Flow

Example

User uploads race.

↓

Frontend validates input.

↓

Backend validates request.

↓

Backend stores race.

↓

Analytics recalculates statistics.

↓

Dashboard updates automatically.

↓

AI summaries become available.

---

# Architectural Principles

## Separation of Concerns

Every module has a single responsibility.

---

## Modular Design

Each module should be independently testable.

---

## API First

Frontend communicates only through REST APIs.

No direct database access.

---

## Cloud Native

Application components should be replaceable and independently deployable.

---

## Stateless Backend

Backend services should not store session state in memory.

---

## Data Driven

Analytics are calculated from stored data rather than manually entered values whenever possible.

---

# Core Modules

Athlete

Competition

Practice

Race

Video

Analytics

AI

Dashboard

Each module owns its own business logic.

---

# Scalability

Although the MVP supports one athlete, the architecture supports:

Multiple Athletes

Multiple Coaches

Multiple Clubs

without redesign.

---

# Technology Summary

Frontend

React + Vite

Backend

FastAPI

Database

DynamoDB

Storage

Amazon S3

Cloud

AWS

Language

Python

---

# Out of Scope

The MVP excludes:

Microservices

Kubernetes

Event streaming

Distributed messaging

Serverless architecture

These may be considered in future releases.

---

# Summary

SwimPulse adopts a simple modular architecture that prioritizes clarity, maintainability, and rapid development while providing a clear path for future growth.
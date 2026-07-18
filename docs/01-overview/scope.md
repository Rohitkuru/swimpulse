# Scope

## Purpose

This document defines the boundaries of the SwimPulse MVP.

The objective is to build a focused, high-quality product that solves a small number of important problems extremely well before expanding into more advanced features.

---

# MVP Objective

Build an AI-powered swimming analytics platform that enables swimmers, parents, and coaches to:

- Store athlete information
- Track competition history
- Record race results
- Organize competition videos
- Measure performance improvements
- Visualize athlete development
- Generate AI-assisted performance insights

The MVP is designed to validate the product concept rather than solve every swimming-related problem.

---

# Included in MVP

## Athlete Management

- Create athlete profile
- Edit athlete profile
- Athlete statistics
- Athlete goals
- Growth tracking

---

## Competition Management

- Create competitions
- Competition information
- Pool information
- Competition history

---

## Race Management

- Add race results
- Store official timings
- Record split times
- Record ranking
- Record lane
- Record stroke
- Personal Best tracking

---

## Practice Management

- Record practice summary
- Store timed practice sets
- Store coach observations
- Store stroke counts (when available)

> Note: Practice data will be entered manually. No automatic capture is included in the MVP.

---

## Video Management

- Upload competition videos
- Link videos to races
- Organize videos
- View videos alongside race results

---

## Analytics

The MVP will calculate:

- Personal Bests
- Improvement percentage
- Event progression
- Split analysis
- Stroke progression
- Race history
- Goal progress
- Competition statistics

---

## Dashboard

Dashboard will display:

- Athlete summary
- Latest competitions
- Personal Bests
- Progress charts
- Goals
- AI insights

---

## AI Coach

Initial AI capabilities include:

- Race summaries
- Performance comparisons
- Progress summaries
- Suggested improvement areas
- Natural language questions based on stored data

---

# Not Included in MVP

The following features are intentionally excluded.

## Computer Vision

- Automatic swimmer detection
- Stroke detection
- Kick detection
- Body position analysis
- Turn detection
- Underwater analysis
- Automatic split extraction from video

Reason:
Requires a significantly larger engineering effort and more training data.

---

## Training Video Analysis

Training videos will not be analyzed in the MVP.

Reason:
Competition videos provide sufficient value for validating the concept.

---

## Live Timing

No live stopwatch integration.

No race timing hardware integration.

---

## Wearables

No smartwatch integration.

No heart-rate monitors.

No Garmin, Apple Watch, or similar integrations.

---

## Social Features

No messaging

No athlete community

No sharing

No comments

---

## Payments

No subscriptions

No payment gateway

No billing

---

## Notifications

No push notifications

No email reminders

No SMS

---

## Coach Portal

The MVP supports only a single authenticated user.

Dedicated coach functionality will be introduced in future versions.

---

## Club Management

The MVP will not include:

- Team management
- Squad management
- Attendance
- Coach scheduling

---

# Assumptions

The MVP assumes:

- Competition results are entered manually.
- Practice summaries are entered manually.
- Competition videos are uploaded manually.
- Official race results are available.
- The user has access to competition videos.

---

# Constraints

The MVP will:

- Support one athlete initially.
- Be designed for future multi-athlete support.
- Focus on long-course and short-course swimming.
- Require an internet connection.
- Use cloud storage for videos.

---

# Future Expansion

The architecture should allow future support for:

- Multiple athletes
- Multiple coaches
- Swimming clubs
- AI video analysis
- Mobile applications
- Wearable integration
- Automatic analytics generation
- National benchmarking
- Training load analysis

without requiring major architectural redesign.

---

# MVP Definition of Done

The MVP will be considered complete when a user can:

1. Create an athlete.
2. Record competitions.
3. Record race results.
4. Upload race videos.
5. View athlete progress.
6. Review analytics.
7. Ask AI questions about performance.

At that point, SwimPulse successfully validates its core value proposition.

---

# Scope Control

Any feature request that does not directly improve:

- Athlete development
- Performance analysis
- Coaching decisions
- Parent understanding

should be added to the product backlog rather than included in the MVP.
# Aurylius

> A Flutter-based habit-building and journaling application focused on purposeful personal growth - structured daily tracking, community challenges, voice journaling, and reflective content consumption.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [My Role](#my-role)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Technical Highlights](#technical-highlights)
- [Impact & Summary](#impact--summary)

---

## Project Overview

**Aurylius** is a mobile application built with Flutter targeting iOS and Android. It provides users with a structured daily routine system - combining habit tracking, time-bound community challenges, voice/text journaling, XP-based leaderboards, and curated motivational content.

The application is designed around intentional interaction: every feature encourages active engagement rather than passive consumption, distinguishing it from conventional social platforms.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

### Live Apps

-  Google Play Store: [Aurylius](https://play.google.com/store/apps/details?id=com.aurylius.auryliusapp)
-  Apple App Store: [Aurylius](https://apps.apple.com/pk/app/aurylius/id6755753775)
  
---

## Business Problem

Modern productivity apps either over-simplify habit tracking or overload users with social noise. Aurylius addresses three gaps:

1. **Lack of accountability** - users abandon habits without community reinforcement or visible progress metrics.
2. **No reflection layer** - most trackers log data but provide no journaling or introspective tooling.
3. **Passive consumption defaults** - users scroll feeds without purposeful engagement; there is no structured content tied to personal goals.

Aurylius unifies habit tracking, journaling, challenges, and curated content into a single cohesive loop.

---

## My Role

**Flutter Developer** - responsible for the complete mobile client: UI development, API integration, and app store deployment on both platforms.

Responsibilities included:

- Designing and building all screens and UI components across every feature module
- Integrating all backend REST APIs into the Flutter client using Dio, including authentication, habit tracking, journaling, challenges, leaderboards, and progress endpoints
- Managing API request/response handling, error states, and data mapping to domain models
- Implementing state management (GetX) across the full application
- Building the voice recording and playback pipeline on the client side
- Handling app store submission, release configuration, and deployment to both **Google Play Store** and **Apple App Store**
- Collaborating with the backend developer on API contracts and data schemas

> Backend infrastructure and API development were handled by a dedicated backend developer.

---

## Key Features

### Daily Habit Tracking
Users create recurring goals (e.g., walking, hydration, meditation) with time-based scheduling. A calendar/agenda view surfaces due and completed habits by day. Circular progress indicators communicate completion percentage and overall consistency score at a glance.

### Goal Management
Goals are created via a floating action button and managed inline. Swipe gestures expose edit and delete actions, keeping the interface clean and interaction fast.

### Challenges Module
Time-bound challenges (7-day, 14-day formats) are available to join from a dedicated screen. Each challenge displays participant count, days remaining, and XP reward. Completion feeds into the leaderboard ranking system.

### Voice & Text Journaling
Users can log daily entries as text or voice recordings. Entries are organized chronologically with date-indexed navigation, allowing easy review of past reflections.

### Progress & Consistency Analytics
A scoring engine computes an overall consistency score based on habit completion history. Motivational prompts and community support cues are surfaced contextually based on the user's current streak and balance metrics.

### Community Leaderboards
A ranked view displays top participants by accumulated XP, including the current user's position relative to others. Avatar-based UI reinforces identity and social accountability.

### Daily Inspiration Feed
A curated section surfaces philosophical and motivational quotes (e.g., Marcus Aurelius, Stoic literature) to frame the user's day with purposeful intent rather than algorithmic noise.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | GetX |
| Navigation | GoRouter |
| Local Storage | Hive / SharedPreferences |
| Backend Integration | REST API (Dio) |
| Voice Recording | `record` / `just_audio` packages |
| Dependency Injection | GetIt |
| Serialization | json_serializable / Freezed |
| Platform Targets | iOS, Android |

> Stack reflects standard Flutter production conventions. Specific backend and infrastructure details are confidential.

---

## Architecture

The application follows **Clean Architecture** with a **feature-first** directory structure.

```
lib/
├── core/
│   ├── error/
│   ├── network/
│   ├── utils/
│   └── widgets/
├── features/
│   ├── habits/
│   │   ├── data/
│   │   │   ├── datasources/
│   │   │   ├── models/
│   │   │   └── repositories/
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   ├── repositories/
│   │   │   └── usecases/
│   │   └── presentation/
│   │       ├── controllers/
│   │       ├── pages/
│   │       └── widgets/
│   ├── challenges/
│   ├── journal/
│   ├── leaderboard/
│   ├── progress/
│   └── inspiration/
└── main.dart
```

Each feature is self-contained across three layers: **data**, **domain**, and **presentation**. The domain layer has zero Flutter dependencies, enabling isolated unit testing of all business logic.

---

## Technical Highlights

**Habit Scheduling Engine**
Habits are stored with recurrence rules and evaluated daily. A background-aware scheduling layer marks habits as pending, completed, or missed without requiring an active session.

**Voice Journal Pipeline**
Voice entries are recorded locally, stored as compressed audio files, and associated with a journal entry entity. Playback is handled in-app with scrubbing support. The pipeline decouples the recording session from the persistence layer to handle interruption gracefully.

**XP & Scoring System**
Challenge completions and daily habit streaks contribute to a composite XP score. The leaderboard queries are paginated and cached locally to reduce API round-trips while maintaining near-real-time rankings.

**Progress Scoring Algorithm**
Consistency is calculated as a weighted rolling average of habit completion over configurable time windows (7-day, 30-day). The circular indicator animates on state change using custom `CustomPainter` rendering.

**Swipe Gesture Actions**
Goal list items use a `Dismissible`-backed gesture system with confirmation guards to prevent accidental deletion. Edit and delete states are managed independently through GetX controllers.

**Offline Resilience**
Local Hive stores act as the source of truth for habits and journal entries. API sync is queued and retried on connectivity restoration, ensuring data integrity across poor network conditions.

---

## Impact & Summary

Aurylius is a production-deployed Flutter application available on both the Google Play Store and Apple App Store. My contribution covered the entire mobile client - from pixel-level UI implementation to API integration and store deployment.

The project required building a consistent, performant UI across 6 functional modules while managing complex state, multi-modal input (text + voice), and reliable API communication with graceful error handling.

Key engineering outcomes:

- Shipped to production on both **iOS (App Store)** and **Android (Play Store)**
- Built a multi-modal journal system with voice recording, local caching, and playback
- Implemented animated custom UI components (circular progress, swipe gestures, leaderboard rankings)
- Managed the full app release pipeline including signing, build configuration, and store submissions

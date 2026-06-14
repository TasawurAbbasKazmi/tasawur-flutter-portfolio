# Mastery

> A Flutter-based football skill development application offering structured drill training, video-guided sessions, XP-based progression, multi-profile support, Fantasy League competition, and an integrated owner monetization system via Amazon store.

---

## Table of Contents

- [Project Overview](#project-overview)
- [My Role](#my-role)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Technical Highlights](#technical-highlights)
- [Impact & Summary](#impact--summary)

---

## Project Overview

**Mastery** is a production Flutter application targeting football/soccer players who want to improve ball control through structured, progressive training. The app combines video-guided drill sessions with a gamified XP and leveling system, multi-profile account management, community leaderboards, and a Fantasy League module where users compete in time-bound skill-based leagues.

A key differentiator is the League Owner system - league creators can connect their Amazon store directly within the app to sell football equipment and accessories to their league members, creating an embedded monetization layer for community organizers.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

---

## My Role

**Flutter Developer** - responsible for the complete mobile client covering UI development and API integration across all feature modules.

Responsibilities included:

- Designing and building all screens and UI components across every feature module
- Integrating all backend REST APIs including drill engine, XP/leveling system, fantasy league management, leaderboards, referrals, and Amazon store
- Managing API request/response handling, error states, loading states, and data mapping to domain models
- Implementing state management (GetX) across the full application
- Building the multi-profile switching system with isolated XP and stats per profile
- Implementing the Fantasy League and Room creation, joining, and competition flows
- Integrating the Amazon store connection flow for league owners
- Building the drill training UI with video playback, rep counters, timers, and foot-placement visual guides
- Collaborating with the backend developer on API contracts and data schemas

> Backend infrastructure and API development were handled by a dedicated backend developer.

---

## Key Features

### Skill Practice & Drill Engine
Drills (Toe Taps, Eight Skill, Inside Roll, Diagonal Roll, and more) are delivered with video tutorials, guided training sessions, rep counters, timers, and visual foot-placement instructions using the Mastery Ball Mat. Each drill is presented step-by-step to support progressive skill building.

### Progress & Level System
Drills are organized into progressive levels. Completion earns XP, updates training time, maintains streaks, and logs performance statistics. The leveling system provides a structured roadmap from beginner to advanced skill sets.

### Multi-Profile Management
Each account supports up to 3 independent profiles. Every profile maintains its own XP, level, stats, and achievements, making the app suitable for families or users who train different players under one account.

### Fantasy League & Rooms
Users can create or join Fantasy Leagues with defined start dates and competition periods. Private and public rooms function similarly to leagues. Participants compete based on skill practice, XP earned, or drill completion. At the end of each league, the top 3 performers are ranked and awarded.

### League Owner Dashboard & Amazon Store Integration
League owners have access to a dedicated dashboard to manage their league. Owners can connect their Amazon store directly within the app, enabling them to sell football-related products (equipment, accessories, bundles) to league members without leaving the application.

### Community Leaderboards & Squad of the Month
Global and country-specific leaderboards (including UK rankings) display top performers. A Squad of the Month feature showcases the top players arranged in a football pitch formation, adding a visual and competitive community layer.

### Referral Program
Users can invite friends via a referral system to earn points. A referral team view lets users track who they have invited and monitor referral-driven rewards.

### In-App Store
An integrated shop allows users to purchase official Mastery training equipment including the Ball Mat and product bundles directly within the app.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | GetX |
| Backend Integration | REST API (Dio) |
| Video Playback | video_player / chewie |
| Local Storage | SharedPreferences |
| Serialization | json_serializable |
| Platform Targets | iOS, Android |

> Stack reflects the technologies used on the Flutter client. Backend infrastructure details are confidential.

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
│   ├── drills/
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
│   ├── progress/
│   ├── profiles/
│   ├── fantasy_league/
│   ├── leaderboard/
│   ├── store/
│   └── referrals/
└── main.dart
```

Each feature is self-contained across three layers: **data**, **domain**, and **presentation**. GetX controllers are scoped per feature and lazily initialized, keeping memory usage efficient across the full module surface.

---

## Technical Highlights

**Drill Training Engine**
The drill session UI combines video playback, a rep counter, and a countdown timer into a synchronized training flow. Session state is managed through a dedicated GetX controller that handles play/pause, rep completion events, and session finalization independently from the video player lifecycle.

**Multi-Profile Isolation**
Each of the 3 profiles under an account maintains completely independent state - XP, level, stats, streaks, and achievements. Profile switching triggers a full controller re-initialization cycle via GetX, ensuring no state leakage between profiles.

**Fantasy League Flow**
League creation involves multi-step configuration (name, duration, competition type, privacy setting). Joining a league validates eligibility against backend rules before confirming entry. Competition rankings are polled and rendered in real-time during the active league period, with a final top-3 awards screen on league completion.

**Amazon Store Integration**
League owners connect their Amazon store through an OAuth-style linking flow within the app. Once connected, their product listings are surfaced to league members inside a dedicated store tab, handled through a separate API integration layer isolated from the core drill and league modules.

**XP & Leveling System**
XP is awarded on drill completion and aggregated at the profile level. Level thresholds are defined server-side and evaluated on each XP update. Streak tracking runs on a daily reset cycle, with local state maintained between sessions and reconciled against the backend on app launch.

**Leaderboard & Squad of the Month**
Global and country-filtered leaderboards are paginated and cached locally to reduce API round-trips. The Squad of the Month UI renders top players in a football pitch formation layout using a custom positioning widget driven by ranked API data.

---

## Impact & Summary

Mastery is a production Flutter application covering one of the more complex feature surfaces in consumer mobile development - combining video-guided training, gamification, multi-profile account management, competitive league systems, community features, and an embedded e-commerce integration.

My contribution covered the entire mobile client: all UI implementation, API integration across every module, and state management architecture using GetX.

Key engineering outcomes:

- Built and integrated 7 distinct feature modules against a live REST API
- Implemented a synchronized drill training UI combining video playback, rep counting, and timer management
- Delivered a full Fantasy League system covering creation, joining, competition tracking, and end-of-league awards
- Built multi-profile account management with complete state isolation per profile
- Integrated Amazon store connection and product listing flow for league owners
- Implemented global and country-specific leaderboards with a custom pitch-formation Squad of the Month UI

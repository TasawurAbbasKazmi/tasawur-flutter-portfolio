# Hooray

> A Flutter-based school cafeteria management application enabling parents to browse daily menus, pre-order meals, manage account balances, and monitor their child's canteen activity through a cashless transaction system.

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

**Hooray** is a production Flutter application targeting parents and students in school environments. It replaces traditional cash-based canteen systems with a structured digital solution - parents can browse daily and weekly menus, pre-order meals for specific dates and recess times, monitor real-time account balances, and set spending limits per child.

The app supports multiple child profiles under a single parent account, giving families with more than one student a unified view of canteen activity and spending across all children.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

---

## My Role

**Flutter Developer** - joined an existing production application to deliver bug fixes, UI updates, code structure improvements, and build deployments.

Responsibilities included:

- Diagnosing and resolving UI and API integration bugs across multiple feature modules
- Implementing new UI updates and screen-level changes aligned with the existing codebase
- Refactoring and improving the existing code structure for better maintainability
- Managing build generation and uploading releases to the App Store and Google Play Store
- Collaborating with the backend developer on API-related fixes and data contract clarifications

> The application was already built and live before my involvement. Backend infrastructure and API development were handled by a dedicated backend developer.

---

## Key Features

### Menu Browsing & Meal Selection
Parents can view daily and weekly menus through a calendar picker. Meals and snacks are selectable for specific dates, giving clear visibility into what is available before placing an order.

### Canteen Pre-Order Flow
A multi-step ordering process guides users through selecting a date range, recess time, and food categories. Supported categories include Bakery, Bites, Cookies, Desserts, Drinks, Hot Drinks, Salads, Sandwiches, Snacks, and more. A simple step-by-step Next flow keeps the ordering process clear and fast.

### Balance & Transaction Management
Account balance is displayed in real-time with low balance alerts to prevent ordering interruptions. A detailed transaction history shows each entry with date, type, amount, and running remaining balance. Parents can add funds directly from within the app.

### Parent Dashboard & Child Account Oversight
Each child has a dedicated overview screen showing key metrics - lifetime orders, total canteen items, spending limit, and member since date. Parents can update spending limits and request canteen orders directly from the dashboard.

### Multiple Child Profile Support
A single parent account can manage multiple child profiles. Each child profile maintains its own balance, order history, and spending limit, giving parents a clear and separate view per child.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | GetX |
| Backend Integration | REST API (Dio) |
| Local Storage | SharedPreferences |
| Serialization | json_serializable |
| Platform Targets | iOS, Android |

> Stack reflects the technologies used on the Flutter client. Backend infrastructure details are confidential.

---

## Architecture

The application follows an **MVC (Model - View - Controller)** pattern organized by type rather than feature, with GetX controllers managing state and business logic per screen.

```
lib/
├── models/
│   ├── menu_model.dart
│   ├── order_model.dart
│   ├── transaction_model.dart
│   └── child_profile_model.dart
├── views/
│   ├── dashboard/
│   ├── menu/
│   ├── ordering/
│   ├── balance/
│   └── profile/
├── controllers/
│   ├── dashboard_controller.dart
│   ├── menu_controller.dart
│   ├── order_controller.dart
│   ├── balance_controller.dart
│   └── profile_controller.dart
├── services/
│   ├── api_service.dart
│   └── auth_service.dart
├── utils/
└── main.dart
```

GetX controllers are bound to their respective views and disposed on navigation away, keeping memory usage lean across the app's screen surface.

---

## Technical Highlights

**Multi-Step Order Flow**
The canteen ordering process spans multiple steps - date range selection, recess time, and food category selection. Each step is managed through a single GetX controller that holds the in-progress order state across screen transitions, with validation gates preventing progression until required selections are made.

**Calendar-Based Menu Navigation**
The menu browsing view uses a calendar picker to navigate between days and weeks. Date selection triggers an API fetch for that day's available items, with loading and empty states handled inline to keep the experience smooth.

**Real-Time Balance with Low Balance Alerts**
Account balance is fetched on dashboard load and after every transaction. A threshold-based alert system notifies parents when the balance drops below a configurable minimum, surfacing the alert contextually within the dashboard and order flow.

**Multi-Child Profile Switching**
Profile switching under a single parent account re-initializes the relevant GetX controllers with the selected child's data. Each child's balance, order history, and spending limit are fetched independently to ensure no data bleed between profiles.

**Transaction History View**
The transaction history renders a paginated list of entries with date, transaction type, amount, and running balance per row. Local caching reduces redundant API calls when the user navigates back to previously loaded history pages.

---

## Impact & Summary

Hooray is a live school cafeteria management application deployed on both iOS and Android. I joined the project post-launch, contributing bug fixes, UI updates, code structure improvements, and build management.

Working within an existing MVC codebase required adapting quickly to established patterns, making targeted fixes without disrupting live functionality, and improving code structure incrementally without introducing regressions.

Key contributions:

- Resolved UI and API integration bugs across multiple screens in a live production app
- Delivered new UI updates and screen-level changes consistent with the existing design and architecture
- Improved code structure and maintainability within the existing MVC pattern
- Managed build generation and release uploads to both the App Store and Google Play Store

# Fidelen

> A Flutter-based B2B procurement mobile application that connects businesses with vendors for products and services - enabling discovery, quotation requests, order tracking, and vendor communication at scale.

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

**Fidelen** is a production-deployed B2B procurement mobile application built with Flutter for iOS and Android. It provides businesses with a structured procurement workflow - from product and service discovery across 1200+ offerings, through vendor quotation requests, to order tracking and real-time vendor communication.

The application targets business buyers and procurement teams who need a reliable, efficient alternative to fragmented vendor outreach and manual quotation processes.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

### Live App

-  Apple App Store: [Fidelen](https://apps.apple.com/pk/app/fidelen/id6449617954)

---

## My Role

**Flutter Developer** - joined an existing production application to deliver bug fixes, UI improvements, and new feature implementations on the live codebase.

Responsibilities included:

- Diagnosing and resolving UI and API integration bugs across multiple feature modules
- Implementing new screens aligned with the existing architecture and design system
- Adding the in-app unread message counter to the inbox/chat module
- Integrating new API endpoints into the Flutter client as backend features were extended
- Collaborating with the backend developer on API contracts for new functionality
- Maintaining consistency with the existing BLoC/Cubit state management architecture throughout all changes

> The application was already built and live before my involvement. Backend infrastructure and API development were handled by a dedicated backend developer.

---

## Key Features

### Product & Service Discovery
Users can search across 1200+ products and services with support for 15+ categories including Cleaning & Sanitation, Communications, Furniture, Electronics, and Health Care. Category browsing and keyword search allow quick navigation to relevant offerings.

### Deals & Recommendations
A home feed surfaces weekly deals and personalized recommendations with pricing offers and discounts, giving buyers immediate visibility into relevant opportunities without active searching.

### Quotation System
Users can send quotation requests to multiple vendors simultaneously from a single product or service page. Incoming quotations are presented with full detail - pricing, lead time, and vendor information - enabling side-by-side comparison and informed decision-making.

### Order Management
Orders progress through a defined five-stage timeline: Agreement, Kick-off, Middle, Final, and Receiving. Users can track real-time status, view agreements, and monitor progress without contacting vendors directly.

### In-App Messaging
A dedicated inbox enables direct chat with vendors. An unread message counter provides instant visibility into pending communications, ensuring buyers never miss a vendor response.

### Vendor Directory & Profiles
Vendor profiles display ratings, business tenure, response time, certifications, and company information. Users can follow vendors for quick future access, supporting long-term procurement relationships.

### Product Detail View
Individual product pages include images, descriptions, pricing, reviews, and seller information, providing all context needed to initiate a quotation or evaluate fit before engaging a vendor.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | BLoC / Cubit |
| Navigation | GoRouter |
| Local Storage | SharedPreferences |
| Backend Integration | REST API (Dio) |
| Dependency Injection | GetIt |
| Serialization | json_serializable / Freezed |
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
│   ├── discovery/
│   │   ├── data/
│   │   │   ├── datasources/
│   │   │   ├── models/
│   │   │   └── repositories/
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   ├── repositories/
│   │   │   └── usecases/
│   │   └── presentation/
│   │       ├── bloc/
│   │       ├── pages/
│   │       └── widgets/
│   ├── quotations/
│   ├── orders/
│   ├── messaging/
│   ├── vendors/
│   └── deals/
└── main.dart
```

Each feature is self-contained across three layers: **data**, **domain**, and **presentation**. The domain layer has zero Flutter dependencies, enabling isolated unit testing of all business logic.

---

## Technical Highlights

**Quotation Request Flow**
The quotation system dispatches a single request to multiple vendors concurrently. Responses are normalized and displayed in a unified list view with sortable attributes (price, lead time, rating), decoupling the request dispatch logic from the response rendering layer.

**Order Status Timeline**
Order progress is rendered as a five-stage visual timeline using a custom widget. Each stage maps to a backend status enum, and transitions animate on state update. The timeline component is fully reusable and driven by a single data model.

**In-App Messaging with Unread Counter**
The chat module maintains a local unread count that syncs against the backend on app resume and after each conversation is opened. The counter updates reactively via a dedicated Cubit, keeping the inbox badge accurate without polling.

**Vendor Profile Architecture**
Vendor profiles aggregate data from multiple endpoints (ratings, certifications, response metrics, product listings) into a single unified view. Data is fetched in parallel and rendered progressively as each stream resolves, keeping the UI responsive on slower connections.

**Category & Search Architecture**
The discovery module supports two entry points - category browsing (15+ categories) and keyword search (1200+ items) - both backed by the same repository layer. A unified product entity ensures consistent rendering regardless of how the item was discovered.

**Incremental Feature Delivery**
Post-launch updates introduced new screens and the messaging unread counter while preserving the existing BLoC architecture. New features were implemented as isolated Cubits to avoid side effects on existing state trees.

---

## Impact & Summary

Fidelen is a live B2B procurement application available on both the Google Play Store and Apple App Store. I joined the project post-launch as a Flutter developer, contributing targeted bug fixes and new feature development on an existing production codebase.

Working on a live app required understanding an established architecture quickly, making precise changes without breaking existing functionality, and delivering improvements that integrated cleanly with the existing BLoC/Cubit state management and API layer.

Key contributions:

- Diagnosed and resolved UI and API integration bugs across multiple feature modules in a live production app
- Implemented new screens consistent with the existing architecture and design system
- Built and integrated the real-time unread message counter for the inbox/chat module
- Integrated new API endpoints as backend features were extended post-launch

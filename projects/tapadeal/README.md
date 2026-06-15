# TapADeal

> A Flutter-based TapADeallication enabling users to find nearby places, food trucks, events, and exclusive deals through map-based exploration, category browsing, and calendar-based filtering. Built for iOS, Android, and Web using Flutter with a Firebase backend.

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

**TapADeal** is a full-stack local discovery and deals platform built entirely with Flutter for mobile (iOS & Android) and web, backed by Firebase. It connects users with nearby places, food trucks, local deals, and events through an intuitive map-first interface with calendar filtering, category browsing, and wallet-based transactions.

The project covers the complete product - mobile client, web client, and backend - developed and delivered independently as a solo engineering effort.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

---

### Live Apps

-  Google Play Store: [Tap A Deal](https://play.google.com/store/apps/details?id=org.microprogramers.tapadeal&hl=en)

## My Role

**Full-Stack Flutter Developer** - sole developer responsible for the complete mobile app, web app, and Firebase backend.

Responsibilities included:

- Designing and building all screens and UI components across iOS, Android, and Flutter Web
- Architecting and implementing the Firebase backend including Firestore data modeling, Firebase Auth, Cloud Functions, and Storage
- Building the map-based places discovery system with location-aware distance filtering
- Implementing the Food Trucks module with calendar-based availability browsing
- Developing the deals and offers engine with promotional banner management
- Building the events calendar with weekly view and date-based filtering
- Implementing the wallet and transaction management system
- Integrating real-time location services for map pins and distance calculations
- Managing state across the full application using GetX
- Deploying the mobile app to both the App Store and Google Play Store
- Deploying the web version via Flutter Web

---

## Key Features

### Map-Based Places Discovery
Users can explore nearby places through an interactive map with location pins. Distance filters (100 km to 10,000 km) allow users to control the discovery radius. A list view complements the map, displaying place names, images, and distance.

### Food Trucks Module
A dedicated Food Trucks section lets users browse available trucks by date using a calendar picker. Availability is shown for Today and Tomorrow with operating time slots, helping users plan visits in advance.

### Deals & Offers Engine
A deals section surfaces location-aware exclusive offers across categories including dining, beauty, and activities. Prominent promotional banners highlight top deals on the home screen for immediate visibility.

### Category Browsing & Search
Users can filter discovery results by categories including Shop, Services, Beauty, and Hair. Category filters are accessible from the home screen for quick narrowing of results without entering a full search flow.

### Events Calendar
An events module provides a weekly calendar view for browsing and filtering upcoming events by specific dates. Users can search availability and discover local happenings relevant to their selected date range.

### Wallet & Transactions
An in-app wallet handles payments and tracks transaction history, enabling cashless interaction with deals and services discovered through the platform.

### Feed & Profile
A feed section surfaces content and platform updates. Profile management allows users to maintain their account, preferences, and saved places.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| Platform Targets | iOS, Android, Web (Flutter Web) |
| State Management | GetX |
| Backend | Firebase (Firestore, Auth, Cloud Functions, Storage) |
| Maps & Location | Google Maps Flutter / Geolocator |
| Local Storage | SharedPreferences |
| Serialization | json_serializable |

---

## Architecture

The application follows an **MVC (Model - View - Controller)** pattern organized by type, with GetX controllers managing state and business logic per screen. The same codebase targets iOS, Android, and Web through Flutter's multi-platform build system.

```
lib/
├── models/
│   ├── place_model.dart
│   ├── food_truck_model.dart
│   ├── deal_model.dart
│   ├── event_model.dart
│   └── transaction_model.dart
├── views/
│   ├── home/
│   ├── map/
│   ├── food_trucks/
│   ├── deals/
│   ├── events/
│   ├── wallet/
│   └── profile/
├── controllers/
│   ├── home_controller.dart
│   ├── map_controller.dart
│   ├── food_truck_controller.dart
│   ├── deals_controller.dart
│   ├── events_controller.dart
│   └── wallet_controller.dart
├── services/
│   ├── firebase_service.dart
│   ├── location_service.dart
│   └── auth_service.dart
├── utils/
└── main.dart
```

Firebase services are abstracted behind a service layer, keeping Firestore and Auth calls isolated from controllers and views.

---

## Technical Highlights

**Map-Based Discovery with Distance Filtering**
The map module integrates Google Maps with real-time user location to render nearby place pins. A distance filter slider dynamically adjusts the discovery radius and triggers a Firestore geo-query to reload results within the updated range. List and map views share a single GetX controller to stay in sync without duplicate fetches.

**Food Truck Calendar Availability**
Food truck availability is stored per date slot in Firestore. The calendar picker maps selected dates to availability documents, fetching Today and Tomorrow slots with their operating times. The controller caches fetched date slots to avoid redundant reads on date re-selection.

**Firebase Backend Architecture**
Firestore collections are structured around core entities - places, food trucks, deals, events, and transactions. Cloud Functions handle server-side logic including deal expiry management, wallet balance updates, and push notification triggers. Firebase Auth manages user sessions across mobile and web from a single authentication layer.

**Flutter Web Parity**
The same Flutter codebase compiles to web with platform-aware conditionals handling map rendering and location access differences between mobile and browser environments. Shared controllers and models ensure feature parity across all three platforms without duplicated business logic.

**Wallet & Transaction Flow**
The wallet module reads and writes transaction records to Firestore in real-time. Balance updates are handled through Cloud Functions to ensure atomic writes, preventing race conditions on concurrent transactions. Transaction history is paginated using Firestore cursors to handle large record sets efficiently.

**Deals Engine with Promotional Banners**
Deals are stored in Firestore with category tags, expiry dates, and location coordinates. The home screen banner fetches the highest-priority active deal on load. Category filtering applies client-side to the already-fetched deal set, keeping interaction fast without additional API calls.

---

## Impact & Summary

This project represents a complete full-stack delivery - mobile (iOS & Android), web (Flutter Web), and Firebase backend - built and shipped independently as a solo engineering effort.

It required end-to-end ownership across every layer: data modeling in Firestore, backend logic in Cloud Functions, real-time location and map integration, multi-platform UI, and state management across a broad feature surface.

Key engineering outcomes:

- Sole developer for the complete product across mobile, web, and backend
- Built and deployed to iOS (App Store), Android (Google Play), and Flutter Web
- Implemented real-time map discovery with dynamic geo-based distance filtering
- Designed and built the Firebase backend including Firestore schema, Cloud Functions, Auth, and Storage
- Delivered 7 functional modules under a unified GetX-driven MVC architecture
- Achieved full feature parity across iOS, Android, and Web from a single Flutter codebase

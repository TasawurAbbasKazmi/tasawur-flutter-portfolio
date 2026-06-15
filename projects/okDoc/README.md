# OkDoc

> A Flutter-based offline-first document and file management application with a structured folder hierarchy, full CRUD operations, recycle bin, Firebase authentication, and integrated Google Pay / Apple Pay support. All data is persisted locally using Hive for fast, reliable offline performance.

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

**OkDoc** is a Flutter mobile application that gives users a structured, offline-first environment to organize and manage their files and documents. Users can create nested folder hierarchies, upload multiple file types, perform full CRUD operations, and recover deleted items through a recycle bin system.

The app is designed around local-first principles - all file metadata and folder structure is stored using Hive, ensuring the core functionality works without an internet connection. Firebase Authentication handles secure sign-in, and Google Pay / Apple Pay are integrated for premium feature access.

> Source code is proprietary and not publicly available. This document serves as a technical case study.

---

## My Role

**Flutter Developer** - responsible for the complete mobile client including UI development, feature implementation, local storage architecture, Firebase integration, and payment integration.

Responsibilities included:

- Designing and building all screens and UI components across every feature module
- Architecting and implementing the local-first data layer using Hive for folders, sub-sections, and file metadata
- Building the nested folder and sub-section hierarchy system with full CRUD support
- Implementing the recycle bin with soft delete, restore, and permanent delete flows
- Integrating Firebase Authentication for secure user sign-in and account management
- Integrating Google Pay and Apple Pay for in-app purchases and premium features
- Implementing state management using GetX across the full application
- Structuring the codebase using a feature-first Clean Architecture approach

> App store deployment was handled separately outside of my scope of work.

---

## Key Features

### Folder & Sub-Section Hierarchy
Users can create folders and nested sub-sections to organize files in a structured hierarchy. The system supports multiple levels of nesting, giving users full flexibility over how their content is organized.

### Multi-Type File Management
The app supports uploading and managing multiple file types including documents, images, and PDFs. Files are displayed within their parent folder and can be viewed, edited, or reorganized at any time.

### Full CRUD Operations
Create, read, update, and delete operations are available across folders, sub-sections, and individual files. All operations are performed locally through Hive, ensuring instant feedback without network dependency.

### Recycle Bin
Deleted files and folders are moved to a Recycle Bin rather than being permanently removed. Users can restore items to their original location or permanently delete them from the bin, preventing accidental data loss.

### Firebase Authentication
User sign-in and account management are handled through Firebase Authentication, providing secure access with support for standard auth flows while keeping the core file management layer fully offline.

### Payment Integration
Google Pay and Apple Pay are integrated for in-app purchases, enabling access to premium features or subscription tiers directly from within the app through native payment sheets on both platforms.

### Offline-First Local Storage
All folder structures, sub-sections, and file metadata are persisted locally using Hive. The app is fully functional without an internet connection, with Hive boxes serving as the primary data source for all file management operations.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter (Dart) |
| State Management | GetX |
| Local Storage | Hive |
| Authentication | Firebase Auth |
| Payments | Google Pay / Apple Pay (pay package) |
| File Handling | file_picker / open_file |
| Platform Targets | iOS, Android |

---

## Architecture

The application follows **Clean Architecture** with a **feature-first** directory structure. The local Hive database acts as the single source of truth for all file and folder data, with Firebase and payment integrations isolated in their own service layers.

```
lib/
├── core/
│   ├── error/
│   ├── utils/
│   └── widgets/
├── features/
│   ├── auth/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   │       ├── controllers/
│   │       ├── pages/
│   │       └── widgets/
│   ├── file_manager/
│   │   ├── data/
│   │   │   ├── datasources/     # Hive box operations
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
│   ├── recycle_bin/
│   └── payments/
└── main.dart
```

Hive boxes are accessed exclusively through the data layer, keeping storage operations decoupled from controllers and UI. GetX controllers are scoped per feature and manage reactive state for all CRUD interactions.

---

## Technical Highlights

**Hive-Based Offline-First Architecture**
All folder structures, sub-section hierarchies, and file metadata are stored in typed Hive boxes. Each entity (folder, sub-section, file) has a corresponding HiveObject model with adapters generated via build_runner. Write operations are synchronous and reflected immediately in the UI through GetX reactive state, giving the experience of instant local persistence.

**Nested Folder Hierarchy**
Folders and sub-sections are stored with parent-child references in Hive, enabling arbitrary nesting depth. Navigation through the hierarchy is managed by a stack-based controller that tracks the current path, allowing breadcrumb navigation and accurate back-navigation without rebuilding the full tree on each step.

**Recycle Bin with Soft Delete**
Deleted items are marked with a `deletedAt` timestamp and a boolean flag in their Hive model rather than being removed from storage. The recycle bin reads all flagged items and presents them in a dedicated screen. Restore writes back the original parent reference and clears the deletion flag. Permanent delete removes the entry from the Hive box entirely.

**Google Pay & Apple Pay Integration**
Payment sheets are triggered through the `pay` package with platform-specific configurations for Google Pay and Apple Pay. Payment request parameters (amount, currency, merchant details) are constructed dynamically based on the selected plan. Success and failure callbacks update the user's premium status in Hive and Firebase simultaneously to keep both layers in sync.

**GetX Feature-Scoped Controllers**
Each feature module has its own GetX controller registered lazily on route entry and disposed on exit. File manager state (current folder contents, selected files, loading/error states) is held reactively in `Rx` variables, ensuring the UI rebuilds only on relevant state changes without unnecessary full-tree rebuilds.

**Firebase Auth with Local Session Persistence**
Firebase Authentication handles sign-in flows. On successful auth, the user's UID is stored locally in Hive to associate file metadata with the correct account. Session state is checked on app launch to determine whether to route the user to the auth flow or directly into the file manager.

---

## Impact & Summary

OkDoc is a fully functional offline-first document management application built with a clean feature-first architecture. The project required designing a reliable local data system capable of representing nested hierarchical structures, handling soft deletes, and syncing minimal cloud state (auth, payments) without compromising the offline-first user experience.

Key engineering outcomes:

- Built a complete offline-first file management system using Hive as the sole data persistence layer
- Implemented a nested folder and sub-section hierarchy with stack-based navigation
- Delivered a full recycle bin system with soft delete, restore, and permanent delete flows
- Integrated Firebase Authentication alongside a Hive-based local session layer
- Integrated Google Pay and Apple Pay with dynamic payment request construction and dual-layer state sync
- Structured the full codebase using feature-first Clean Architecture with GetX state management

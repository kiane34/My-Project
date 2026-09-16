# Kent & Paulene — Flutter Portfolio & State Management
### CS 416 - Mobile Computing 2 | BSCS 4th Year

A master compilation Flutter application that serves as the hub for all laboratory activities, demonstrating declarative UI principles, multi-screen navigation, and global state management.

---

## 📋 Project Overview

| Detail          | Value                                  |
|----------------|----------------------------------------|
| **Authors**     | Kent & Paulene                         |
| **Subject**     | CS 416 - Mobile Computing 2            |
| **Framework**   | Flutter 3.41.6 (Dart 3.11.4)          |
| **State Mgmt**  | Provider ^6.1.5                        |
| **Fonts**       | Google Fonts (Inter, Outfit)           |

---

## 🗂️ App Structure

```
lib/
├── main.dart                         # App entry point, MaterialApp, routes, Provider setup
├── providers/
│   └── app_state_provider.dart       # Global state: theme mode, user profile, activity completion
├── services/
│   └── network_service.dart          # Lab 4 stream listener, request queue, & auto-recovery engine
├── screens/
│   ├── home_dashboard_screen.dart    # Master menu dashboard
│   ├── activity1_screen.dart         # Lab 1: Counter & Math Hub (StatefulWidget)
│   ├── activity2_screen.dart         # Lab 2: Task & Notes Planner (StatefulWidget)
│   ├── activity3_screen.dart         # Lab 3: Color & UI Playground (StatefulWidget)
│   ├── network_monitor_screen.dart   # Lab 4: Network Monitor & Request Queue (StatefulWidget)
│   └── settings_screen.dart          # Global settings (Provider theme + user profile)
└── widgets/
    ├── activity_card.dart             # Reusable StatelessWidget lab card
    ├── custom_button.dart             # Reusable StatelessWidget button
    └── stat_summary_card.dart         # Reusable StatelessWidget stat indicator
```

---

## 🎯 Features Implemented

### ✅ Multi-Screen Navigation
- Named routes: `/`, `/activity1`, `/activity2`, `/activity3`, `/network`, `/settings`
- Home Dashboard acts as the master menu with a responsive grid

### ✅ Widget Architecture
- **StatelessWidget** — `ActivityCard`, `CustomButton`, `StatSummaryCard`
- **StatefulWidget** — All activity screens (local, screen-specific state)
- Declarative, immutable UI patterns throughout

### ✅ Real-time Stream Listeners & Network Resiliency
- `connectivity_plus` real-time stream subscription for Wi-Fi, Cellular, and Offline state detection.
- **Request Queuing System**: Catches network loss during long-running data fetches and safely enqueues payloads.
- **Graceful Recovery Engine**: Automatically flushes and retries queued requests upon network connection restoration.

### ✅ Responsive Layout
- `LayoutBuilder` + `GridView.count` adapts to mobile/tablet/desktop
- `Expanded`, `Flexible`, `Column`, and `Row` — no fixed pixel widths
- Overflow-safe text with `maxLines` and `TextOverflow.ellipsis`

### ✅ Global State Management (Provider)
- `AppStateProvider` manages:
  - **Theme Mode** — System / Light / Dark (live toggle)
  - **User Profile** — Name, course, section (live updates on Dashboard)
  - **Activity Completion** — Tracks completed labs globally
- Changing Settings **instantly** reflects across all screens

---

## 🧪 Laboratory Screens

| Screen   | Lab Title                  | Concept Demonstrated          |
|----------|----------------------------|-------------------------------|
| Lab 1    | Counter & Math Hub         | StatefulWidget, local state, history log |
| Lab 2    | Task & Notes Planner       | CRUD, category filters, modal dialogs |
| Lab 3    | Color & UI Playground      | Sliders, color palette, declarative rendering |
| Lab 4    | Network Monitor            | Connectivity streams, request queue, auto-retry recovery |
| Settings | Global App Settings        | Provider, live global state propagation |

---

## 🚀 How to Run

### Prerequisites
- Flutter SDK 3.x installed
- Android device or emulator connected

```bash
# Restore dependencies
flutter pub get

# Run on connected Android device
flutter run

# Run on specific device
flutter run -d <device-id>
```

### Check all devices
```bash
flutter devices
```

---

## 📦 Dependencies

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.1.5       # Global state management
  google_fonts: ^8.2.1   # Inter & Outfit typography
  connectivity_plus: ^7.3.1  # Network state detection
  http: ^1.6.0            # HTTP request handling
  cupertino_icons: ^1.0.8
```

---

## ✅ Quality Checks

```
flutter analyze  → No issues found
flutter test     → All tests passed
```

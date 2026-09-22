# Camba Flutter Portfolio

CS 416 - Mobile Computing 2 | BSCS 4th Year

A Flutter portfolio application that brings the laboratory activities into one responsive dashboard. The project demonstrates local state, CRUD workflows, network resiliency, global Provider state, and a dynamic network-performance throttle.

## Project Details

| Detail | Value |
| --- | --- |
| Authors | Camba & Pamat |
| Framework | Flutter 3.41.6 |
| Language | Dart 3.11.4 |
| State management | Provider 6.1.5+1 |
| Typography | Google Fonts: Inter and Outfit |

## Features

### Master dashboard

- Responsive activity grid for mobile, tablet, and desktop layouts
- Named-route navigation for every activity and settings screen
- Global light/dark theme switching
- Editable profile information and activity completion tracking

### Activity 1: Counter & Math Hub

Demonstrates a `StatefulWidget`, local counter state, mathematical operations, and a history log.

### Activity 2: Network Diagnostic Dashboard

The diagnostic tool periodically measures connection health using a three-stage sequence:

1. **Baseline idle ping** measures latency before a transfer begins.
2. **Download bandwidth and ping** downloads a test payload while measuring latency concurrently.
3. **Upload bandwidth and ping** uploads a test payload while measuring latency concurrently.

The results are classified into operational tiers:

- **Excellent:** more than 10 Mbps
- **Fair:** 2 to 10 Mbps
- **Poor:** below 2 Mbps
- **Degraded:** heavy packet loss, extreme latency, or unavailable probes

The categorized result is published through `AppStateProvider`, allowing the rest of the application to react to current connection health. Activity 3 also demonstrates adaptive UI behavior:

- Excellent and Fair connections use high-resolution media mode.
- Poor and Degraded connections use lightweight placeholder mode.

The dashboard runs automatically every minute and also provides a manual diagnostic button. Probe failures are handled independently with fallback endpoints so one unavailable host does not immediately stop the sequence.

## Project Structure

```text
lib/
├── main.dart
├── providers/
│   └── app_state_provider.dart
├── services/
│   ├── network_diagnostic_service.dart
│   └── network_service.dart
├── screens/
│   ├── home_dashboard_screen.dart
│   ├── activity1_screen.dart
│   ├── activity2_screen.dart
│   ├── activity3_screen.dart
│   ├── network_monitor_screen.dart
│   └── settings_screen.dart
└── widgets/
    ├── activity_card.dart
    ├── custom_button.dart
    └── stat_summary_card.dart
```

## Routes

| Route | Screen |
| --- | --- |
| `/` | Home dashboard |
| `/activity1` | Counter & Math Hub |
| `/activity2` | Task & Notes Planner |
| `/activity3` | Network Diagnostic Dashboard |
| `/network` | Network Monitor |
| `/settings` | Global settings |

## Setup

### Requirements

- Flutter SDK 3.x
- Dart SDK 3.11.4 or compatible
- Android device/emulator, iOS simulator, desktop target, or web browser
- An internet connection for live Activity 3 measurements

### Run the application

```bash
flutter pub get
flutter run
```

To choose a specific target:

```bash
flutter devices
flutter run -d <device-id>
```

Android release builds require network access because Activity 3 performs HTTPS diagnostic requests. The Android manifest includes the `INTERNET` permission.

## Dependencies

```yaml
provider: ^6.1.5+1
google_fonts: ^8.2.1
connectivity_plus: ^7.3.1
http: ^1.6.0
cupertino_icons: ^1.0.8
```

## Validation

```bash
flutter analyze
flutter test
```

`flutter analyze` currently passes with no issues. The network queue test passes. The existing home smoke test needs its assertion updated because the dashboard intentionally displays `Mobile Computing Portfolio` in both the app bar and the hero section.

## Notes

Network measurements depend on DNS, server availability, device permissions, and the active connection. When all probe endpoints are unavailable, the diagnostic completes as **Degraded** instead of crashing, and the dashboard retains the failed-test details for troubleshooting.

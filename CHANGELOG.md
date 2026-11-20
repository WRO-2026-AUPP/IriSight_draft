# Changelog

This file records significant changes between major IriSight robot and
repository milestones. Detailed development history belongs in the Engineering
Journal, while measurements and test evidence belong in `other/testing/`.

## International Final — In progress

### Repository

- Reorganized the software into Jetson, ESP32 and AI-model sections.
- Archived the National Jetson programs under `legacy_national/`.
- Archived the National firmware, CAD and electrical diagrams separately from
  the default International locations.
- Added dedicated locations for the Engineering Journal and testing evidence.

### Firmware

- Added the current tested ESP32 actuator firmware.
- Updated the steering-servo signal from GPIO 17 to GPIO 18.
- Removed ultrasonic-sensor handling from the current firmware.

### Pending documentation

- Mechanical rebuild and updated CAD files
- Final power and wiring architecture
- Current International Jetson programs and dependencies
- Parking test evidence and final challenge results

## National Competition baseline — 2026-11-20

- Preserved the National Competition repository as the migration baseline for
  the International Final update.

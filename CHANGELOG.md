# Changelog

This file records significant changes between major IriSight robot and
repository milestones. Detailed development history belongs in the Engineering
Journal, while measurements and test evidence belong in `other/testing/`.

## International Final — November 2026

### Repository

- Reorganized the software into Jetson, ESP32 and AI-model sections.
- Preserved the complete National repository under
  `other/legacy_national/`, including its original README and folder layout.
- Separated the current International firmware, CAD and electrical
  documentation from the self-contained National archive.
- Added dedicated locations for the Engineering Journal and testing evidence.
- Organized the current mechanical CAD, STL files, drawings and renders by
  subsystem while keeping National assets inside the archive.

### Documentation and evidence

- Documented the International mechanical rebuild, electrical architecture,
  software interfaces and current challenge behavior.
- Added repeatable test procedures, acceptance criteria and a video-evidence
  register.
- Verified the YOLOv8n checkpoint metadata and validation results, exported all
  100 training epochs, and recorded the unavailable original dataset split as
  an evidence boundary.
- Added the first Engineering Journal manuscript covering the complete
  mechanical evolution.
- Added a CAD-derived Ackermann steering calculation sheet, including the
  wheelbase, kingpin spacing, steering-arm angle and convergence error.
- Added engineering drawings (PDF and PNG) for every current printed part,
  generated from the STEP files.
- Added the International power-distribution and signal-wiring diagrams with a
  datasheet-based power budget.
- Added MATLAB models of the steering linkage and the Open Challenge program
  for the MathWorks Modeling Award.

### Firmware

- Added the current tested ESP32 actuator firmware.
- Updated the steering-servo signal from GPIO 17 to GPIO 18.
- Removed ultrasonic-sensor handling from the current firmware.

## National Competition baseline — 2026-11-20

- Preserved the National Competition repository as the migration baseline for
  the International Final update.

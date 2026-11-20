# Robot software

This directory separates the software running on the NVIDIA Jetson Orin Nano,
the firmware running on the custom ESP32 board, and the trained vision model.

> **International update status:** The current Jetson programs still need to be
> copied from the rebuilt robot. The National Competition baseline is archived
> under `main_controller/legacy_national/`. The tested ESP32 actuator firmware
> under `microcontroller/firmware/` is current.

## System boundary

```text
Sensors and camera
        |
        v
Jetson Orin Nano (perception, navigation, lap counting and parking)
        |
        | USB serial at 115200 baud
        v
Custom ESP32 board (motor driver and steering servo)
```

## Directory map

| Path | Purpose | Current status |
| --- | --- | --- |
| [`main_controller/`](main_controller/) | Jetson challenge programs, sensor helpers and configuration | International programs pending; National baseline archived separately |
| [`microcontroller/`](microcontroller/) | ESP32 firmware, flashing information and pin map | Current actuator firmware added |
| [`ai_model/`](ai_model/) | Trained traffic-sign detector and model documentation | Existing model preserved for later verification |

The current International Jetson source, installation requirements and final
run commands will be added after the working files are copied from the robot.
Until then, do not use the National baseline programs to operate the rebuilt
vehicle.

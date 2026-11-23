# Robot software

This directory contains the software for the International robot:

- the Python programs on the NVIDIA Jetson Orin Nano (the main controller);
- the firmware on the custom ESP32 board (the microcontroller);
- the trained traffic-sign model.

The Jetson does all of the sensing and decision-making. It sends short text
commands over USB serial to the ESP32, which drives the motor and steering servo.

> **Status:** The Open Challenge and Obstacle Challenge programs below are the
> current International versions. Some competition features are still missing;
> see [Not implemented yet](#not-implemented-yet). The National Round software is
> archived in [`../other/legacy_national/`](../other/legacy_national/) and must not
> be used on the rebuilt robot.

## Directory map

```text
src/
├── main_controller/                      Jetson programs (Python)
│   ├── open_challenge/
│   │   ├── open_clockwise.py             follows the inner RIGHT wall
│   │   └── open_counter_clockwise.py     follows the inner LEFT wall
│   ├── obstacle_challenge/
│   │   ├── obstacle_clockwise.py         full clockwise run
│   │   └── obstacle_counter_clockwise.py full counter-clockwise run
│   ├── config/                           pillar map files read by the obstacle programs
│   ├── sensors/                          where the sensor code is in each program
│   └── requirements.txt                  Python packages
├── microcontroller/
│   └── firmware/firmware.ino             ESP32 motor and servo firmware
└── ai_model/
    └── traffic_sign_detector.pt                          YOLOv8n traffic-sign (pillar) detector
```

| Path | Purpose |
| --- | --- |
| [`main_controller/`](main_controller/) | Jetson programs, setup, run commands and safety notes |
| [`microcontroller/`](microcontroller/) | ESP32 firmware, pin map and flashing |
| [`ai_model/`](ai_model/) | Trained pillar detector and how it was trained |

## System overview

```text
 Hokuyo UST-30LX LiDAR (Ethernet) ──┐
 BNO055 IMU (I2C bus 7) ────────────┤
 USB camera + YOLOv8n model ────────┼──► Jetson (Python) ── USB serial 115200 ──► ESP32 ──► motor + steering servo
 VL53L0X rear distance (I2C bus 1) ─┘          │
                                               └── web dashboard (port 5000), for testing only
```

| Sensor or device | Role | Used in |
| --- | --- | --- |
| Hokuyo UST-30LX LiDAR (`192.168.0.10:10940`) | Front, side and front-corner distances; wall and corner detection | Both challenges |
| BNO055 IMU (I2C bus 7, address `0x28`) | Heading (yaw), turn completion and lap counting | Both challenges |
| USB camera + YOLOv8n (`traffic_sign_detector.pt`) | Tells red pillars from green pillars | Obstacle Challenge |
| VL53L0X (I2C bus 1, address `0x29`, facing backward) | Rear distance during final parking | Obstacle Challenge |
| ESP32 board (`/dev/ttyUSB0`, 115200 baud) | Carries out the drive commands | Both challenges |

## Jetson to ESP32 commands

Commands are ASCII text lines ending in a newline (`\n`):

| Command | Meaning | Used by |
| --- | --- | --- |
| `DRIVE <steering> <pwm>` | Drive forward. Steering is in degrees from centre (**positive = right, negative = left**); PWM is motor speed, `0–255` | All programs |
| `BACK <steering> <pwm>` | Drive backward with the same steering and speed values | Obstacle programs (parking exit and final parking) |
| `STOP` | Stop the motor and centre the steering | All programs |

The firmware adds the steering value to the servo centre (95°) and limits the
servo to 35°–150°. Details are in [`microcontroller/`](microcontroller/).

## Not implemented yet

These items are needed for competition runs and are not yet in the code:

- **Start button.** The programs start driving as soon as they run and the LiDAR
  gives valid scans. They do not yet wait for the start button (General Rules
  9.10–9.11). The start button on the ESP32 board is not read by the firmware yet.
- **Starting without a laptop.** During testing, the programs are started over SSH
  and stopped with `Ctrl+C`. For competition, the robot must start without any
  wireless connection (rule 11.10).
- **Automatic pillar scan.** The obstacle programs read the pillar colours and
  order from a JSON file that is currently written by hand. A scan that creates
  this file from the camera has not been written yet. See
  [`main_controller/obstacle_challenge/`](main_controller/obstacle_challenge/).
- **ESP32 command timeout.** The programs assume the ESP32 stops the motor when
  commands stop arriving, but the current firmware does not do this yet.

Setup, run commands and safety notes are in
[`main_controller/README.md`](main_controller/README.md).

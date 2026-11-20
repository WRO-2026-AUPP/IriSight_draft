# Jetson main controller

The NVIDIA Jetson Orin Nano performs perception, navigation, lap counting and
parking, then sends steering and speed commands to the custom ESP32 board.

## Migration status

The rebuilt robot uses a Hokuyo UST-30LX LiDAR, a 1 MP USB camera and a rear
VL53L0X sensor. Its tested Jetson programs have not yet been copied into this
repository. The National programs are retained separately under
`legacy_national/` and must not be used to operate the rebuilt robot.

| Path | Contents |
| --- | --- |
| [`open_challenge/`](open_challenge/) | Destination for current International Open Challenge programs |
| [`obstacle_challenge/`](obstacle_challenge/) | Destination for current International Obstacle Challenge programs |
| [`sensors/`](sensors/) | Destination for current International sensor modules |
| [`config/`](config/) | Destination for shared International configuration |
| [`legacy_national/`](legacy_national/) | Archived National controller and sensor code |

`requirements.txt`, installation commands and final run commands will be added
only after the current International source has been imported. This avoids
documenting the legacy RealSense and ultrasonic dependencies as if they were
part of the rebuilt robot.

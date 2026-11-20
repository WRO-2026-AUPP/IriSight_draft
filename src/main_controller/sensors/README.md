# Sensor helpers

This directory will contain the sensor modules actually used by the
International controller:

- Hokuyo UST-30LX LiDAR
- 1 MP USB camera from the Raspbot V2
- rear VL53L0X time-of-flight sensor
- BNO055 orientation sensor

The National BNO055 helper and calibration file are preserved under
[`../legacy_national/sensors/`](../legacy_national/sensors/). No International
sensor module should be documented as reproducible until its working source and
calibration procedure have been copied from the Jetson.

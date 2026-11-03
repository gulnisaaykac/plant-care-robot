# Plant Care and Monitoring Robot

An indoor two-wheel robot. It drives up to a pot, measures soil moisture, and waters for a short time when the safety checks pass. Telemetry and drive commands go through ThingsBoard Cloud.

Losant is a comparison in the report. The robot does not publish to a second platform.

## Pins

| Function | Pin |
| --- | --- |
| Motor direction and speed | GPIO14, GPIO21, GPIO41, GPIO42 |
| Distance sensor I2C | GPIO38, GPIO39 |
| Soil moisture | GPIO1 |
| Servo signal | GPIO40 |
| Pump gate | GPIO47 |
| Future IMU interrupt | GPIO2, leave unused |

Camera pins stay dedicated to the camera. Enable PSRAM in the build, or the camera fails.

## Power

The pack is 3S, 11.1 V nominal. The motor driver takes that rail directly. The ESP32 is powered only from the fixed 5 V regulator. The servo and the pump share a separate regulator set to 6.0 V. All grounds are common. Do not connect the driver board's 5 V pin to the ESP32.

## Keep out of the repository

Do not commit the access token, the Wi-Fi password, or `.env` files.

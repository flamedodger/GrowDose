# Tank Sensor Integration

## Overview

Integrated the A0221A4 tank sensor with the KinCony A6 and updated the GrowDose tank card to display live tank level information.

## Work completed

- Added the A0221A4 to the existing 9600-baud RS485 bus at address 2.
- Retained the SHT20 at address 1.
- Diagnosed communication at the factory address and changed the A0221A4 address.
- Removed temporary sensor setup controls after configuration.
- Set A0221A4 polling to one second.
- Restored SHT20 polling to ten seconds.
- Added `sensor.nft_tank_level` in `/config/packages/nft_tank_level.yaml`.
- Updated the GrowDose tank card to show live percentage and fill level.

## Calibration

The sensor is calibrated using distance from the sensor:

- Empty reference: 150 mm = 0%
- Full reference: 50 mm = 100%
- Conversion: `percentage = (150 - distance_mm)`, clamped to the range 0–100%

This produces a calibrated level percentage. It is not a verified volume percentage unless the tank geometry and calibration have been independently validated.

## Calculation validation

| Distance | Expected percentage |
| ---: | ---: |
| 150 mm | 0% |
| 117 mm | 33% |
| 100 mm | 50% |
| 50 mm | 100% |
| 175 mm | 0% |
| 25 mm | 100% |

Invalid or unavailable distance readings correctly make the percentage unavailable.

## Validation status

- YAML/JSON parsing tests passed.
- Calibration calculation tests passed.
- The live tank card was confirmed working after activation.
- Recovery backups and reusable card YAML were saved in the task directory.
- The 50 mm full point is the specified calibration reference; a separate physical full-tank test was not reported.

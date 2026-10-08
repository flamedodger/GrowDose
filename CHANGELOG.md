# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- Project repository initialized
- Hardware assembly documentation
- ESPHome configuration template
- Pump calibration guide
- Bill of materials

### Added since 0.1.0
- Deployed ESPHome GPIO pulse test controls for all three pumps, with shared driver enable released after each test
- Integrated the A0221A4 tank-level sensor into Home Assistant and the GrowDose tank card
- Installed a Home Assistant nutrient event logger that records meaningful independent tank-level changes across restarts

### In Progress
- Final liquid-path calibration and verified steps-per-ml values
- Production dose controls, priming, and safety limits
- Complete dose/fill event logging, usage totals, and notifications
- Automatic nutrient and pH control

## [0.1.0] - 2026-08-26

### Initial Release

#### Added
- Hardware design based on ESP32-S3, CNC Shield V3, and A4988 drivers
- Support for three independent dosing channels
- Pinout documentation and wiring guide
- Development roadmap

#### Hardware Status
- ✅ ESP32-S3 controller tested and working
- ✅ CNC Shield interface verified
- ✅ All three A4988 drivers operational
- ✅ All pumps tested in forward and reverse rotation
- ✅ Shared motor enable control functional
- ⏳ Pump calibration (pending)

#### Known Limitations at the 0.1.0 release
- No ESPHome firmware yet deployed
- Pump calibration values not established
- Home Assistant integration pending
- Dosing safety limits not yet implemented

---

## Future Roadmap

### Phase 2: Calibration & Control
- Establish accurate steps-per-ml values for each pump
- Implement ESPHome stepper integration
- Test volume-based dosing commands

### Phase 3: Integration
- Develop Home Assistant MQTT/ESPHome bridge
- Create automations for nutrient dosing schedules
- Implement dosing history logging

### Phase 4: Advanced Features
- Dosing safety limits and error detection
- pH adjustment with feedback
- Usage analytics and trend tracking
- Web dashboard for monitoring

---

## Contributing

This is an open-source project. Contributions, bug reports, and feature requests are welcome!

## License

See LICENSE file for details.

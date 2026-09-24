# Pump Calibration Guide

## Overview

Calibration establishes the conversion between pump pulses and delivered volume. GrowDose must use the **density of the liquid being dispensed** when converting a measured mass to millilitres:

```text
volume (ml) = measured mass (g) / liquid density (g/ml)
ml per pulse = measured mass (g) / (pulse count × liquid density (g/ml))
pulses per ml = pulse count × liquid density (g/ml) / measured mass (g)
```

Do not apply a water-based calibration directly to nutrient concentrate or pH-down solution unless its density is known to be the same. Record the liquid, concentration, density source, pulse count, mass, and test date with every calibration.

## Recorded Calibration Results

The following results are measured masses, not final volume settings. All three pumps were tested over **12,000 pulses**:

| Pump | Measured output | Pulse count | Measured mass | Derived mass per pulse | Status |
| --- | ---: | ---: | ---: | ---: | --- |
| A | 20 g | 12,000 | 20 g | 0.0016667 g/pulse | Convert using the density of the dispensed liquid |
| B | 20 g | 12,000 | 20 g | 0.0016667 g/pulse | Convert using the density of the dispensed liquid |
| C | 15 g | 12,000 | 15 g | 0.00125 g/pulse | Recheck with the actual pH-down solution |

For a liquid density of `D` g/ml:

```text
Pump A ml per pulse = 20 / (12000 × D) = 0.0016667 / D
Pump B ml per pulse = 20 / (12000 × D) = 0.0016667 / D
Pump C ml per pulse = 15 / (12000 × D) = 0.00125 / D
```

Equivalent pulses-per-ml values are:

```text
Pump A = 600 × D
Pump B = 600 × D
Pump C = 800 × D
```

The Pump C result must be checked again using the actual pH-down solution before acid dosing is enabled. If the density is unavailable, keep the calibration in grams per pulse and do not label it as a millilitres-per-dose setting.

## Calibration Process

### Prerequisites

- GrowDose hardware fully assembled and tested
- ESP32-S3 flashed with ESPHome firmware
- A scale with suitable resolution and capacity
- A container that can be weighed or tared
- The actual liquid to be dispensed, or its verified density
- The pulse count used for each test
- Distilled water or another non-hazardous liquid for initial pump checks

### Step 1: Prepare the Setup

1. Prime the pump and remove air bubbles from the tubing.
2. Place the collection container on the scale and tare it.
3. Connect to GrowDose via the ESPHome interface.
4. Ensure all pumps are de-energized before starting.
5. Confirm the pulse count, liquid identity, and density to be used for the test.

### Step 2: Run a Gravimetric Test

For each pump (A, B, and C):

1. Send a precisely recorded pulse/step command.
2. Collect the complete output in the tared container.
3. Record the delivered mass in grams.
4. Repeat the test at least three times.
5. Calculate the average mass per pulse.

```text
mass per pulse (g/pulse) = measured mass (g) / pulse count
```

### Step 3: Convert Mass to Volume

Use the verified density of the liquid at the test temperature:

```text
volume (ml) = measured mass (g) / density (g/ml)
ml per pulse = measured mass (g) / (pulse count × density (g/ml))
pulses per ml = 1 / (ml per pulse)
```

If the density is unavailable, keep the calibration in grams per pulse and do not label it as a millilitres-per-dose setting.

### Step 4: Verify Results

1. Run the calibration sequence three times for each pump.
2. Average the conversion factors, preferably using the same liquid and container setup.
3. Record the final value together with the liquid density and test conditions.
4. Test each pump with known doses, such as 5 ml, 10 ml, 20 ml, and 50 ml.
5. Confirm accuracy to within the project’s accepted tolerance before enabling automated dosing.

## pH-Down Acid Dosing

Pump C is intended for pH adjustment, but its calibration must be checked again using the actual pH-down solution before it is placed into service. Acid concentration and density can differ substantially from water or nutrient solution.

Before acid dosing is enabled, verify that every wetted component is compatible with the **specific acid and concentration**:

- Pump tubing
- Feed/inlet tubing
- Outlet/dosing tubing
- Fittings and connectors
- Storage container
- Any valve, check valve, filter, or other component in the liquid path

Check the product’s safety data and technical information, then confirm the materials against the manufacturers’ chemical-compatibility guidance. Do not infer compatibility from appearance or from compatibility with nutrient solution. Replace or isolate any component that is not explicitly suitable.

Use appropriate chemical handling and personal protective equipment, prevent backflow into the reservoir, and keep acid dosing disabled until compatibility, priming, leak checks, and a measured-output test with the actual solution are complete.

## Troubleshooting

**Inconsistent measurements:**
- Check for air bubbles in the pump inlet line.
- Ensure pump priming is complete.
- Verify that the scale is stable and the container is tared.
- Repeat tests using the same pulse count and liquid temperature.

**Values significantly higher or lower than expected:**
- Review motor microstep configuration.
- Check for mechanical binding or occlusion.
- Verify pump direction and tubing installation.
- Confirm that the liquid density and units are correct.

**Pump will not prime:**
- Check that the inlet line is submerged.
- Verify that there is no debris or air leak in the inlet path.
- Ensure motor direction is correct for the pump.
- Check tubing and fittings for leaks or chemical damage.

## Safety Notes

- Always test with water or another non-hazardous liquid before testing an acid.
- Never leave a powered pump unattended.
- Allow the motor to cool between extended test runs.
- Keep acid and nutrient channels clearly identified and separate.
- Do not enable automated pH dosing until the actual solution has been tested and all wetted materials have been verified as compatible.
- Store calibration values and their associated liquid/density information in non-volatile project documentation.

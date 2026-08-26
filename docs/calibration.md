# Pump Calibration Guide

## Overview

Calibration establishes the **steps-per-millilitre (steps/ml)** ratio for each pump. This allows GrowDose to deliver precise volumes based on stepper motor commands rather than timing estimates.

## Calibration Process

### Prerequisites

- GrowDose hardware fully assembled and tested
- ESP32-S3 flashed with ESPHome firmware
- Three calibrated measuring containers (10ml minimum accuracy)
- Distilled water or test liquid

### Step 1: Prepare the Setup

1. Place measuring container under Pump A
2. Connect to GrowDose via ESPHome interface
3. Ensure all three pumps are de-energized before starting

### Step 2: Run Test Pulses

For each pump (A, B, C):

1. Send a step command of exactly 1000 steps
2. Measure the volume dispensed (in millilitres)
3. Record the result

**Formula:**
```
steps/ml = 1000 steps / measured volume (ml)
```

### Step 3: Verify Results

1. Run the calibration sequence 3 times for each pump
2. Average the results to get the final `steps/ml` value
3. Record all values in the ESPHome configuration

### Step 4: Validate

1. Test each pump with a known dose (e.g., 5ml)
2. Calculate required steps: `5ml × steps/ml`
3. Command that number of steps and verify actual output
4. Repeat for 10ml, 20ml, and 50ml doses
5. Confirm accuracy to within ±2% variation

## Expected Results

For typical stepper peristaltic pumps with 1/8 microstepping:
- Pump A steps/ml: ~500-800
- Pump B steps/ml: ~500-800
- Pump C steps/ml: ~400-600

*Actual values depend on specific pump model and configuration*

## Troubleshooting

**Inconsistent measurements:**
- Check for air bubbles in pump inlet line
- Ensure pump priming is complete
- Verify stepper motor connections are secure

**Values significantly higher/lower than expected:**
- Review motor microstep configuration
- Check for mechanical binding or occlusion
- Verify pump impeller orientation and assembly

**Pump won't prime:**
- Check inlet line is submerged
- Verify no debris in pump inlet
- Ensure motor direction is correct for this pump

## Safety Notes

- Always test with water or non-hazardous liquid first
- Never leave powered pump unattended
- Allow motor to cool between extended test runs
- Store calibration values in non-volatile memory

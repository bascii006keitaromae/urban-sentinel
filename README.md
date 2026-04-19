# Urban Sentinel

Urban Sentinel is a low-cost IoT flood monitoring prototype designed for localized urban flooding scenarios such as Thai sois. The system detects rainfall and rising water levels, classifies flood severity, and triggers local warning outputs including LED indicators, buzzer alarms, and relay activation.

## Project Objective

The goal of this project is to provide early warning for small-scale urban flooding using a staged sensing approach:

1. Detect rainfall
2. Detect initial water presence
3. Activate precise water level monitoring
4. Classify flood severity
5. Trigger warning outputs

This project was developed for the **Connected IoT Systems** final project.

---

## Features

- Rain detection using rain sensor (AO + DO)
- Initial water detection using HW-038 water sensor
- Precise level monitoring using JSN-SR04T ultrasonic sensor
- Flood severity classification into multiple warning levels
- Local visual warning using RGB LED
- Audible warning using active buzzer
- Relay output for external emergency action
- Serial Monitor output for live debugging and demonstration

---

## System Workflow

The system operates in stages:

### Stage 1: Rain + Initial Water Monitoring
- The rain sensor continuously checks for rainfall
- The HW-038 sensor continuously checks for initial water contact

### Stage 2: Water Threshold Trigger
- Once the HW-038 reading passes the threshold, the system activates the ultrasonic sensor

### Stage 3: Flood Classification
- The ultrasonic sensor measures distance to the water surface
- Based on calibrated thresholds, the system classifies the situation into flood levels

### Stage 4: Warning Output
- LED color changes according to state
- Buzzer activates at higher danger levels
- Relay turns on during dangerous flood conditions

---

## Flood Levels

- **Level 0**: Water detected, below flood range
- **Level 1**: Potential Flood
- **Level 2**: Warning
- **Level 3**: Warning Evacuate
- **Level 4**: Flood

---

## Hardware Components

### Microcontroller
- ESP32 DevKit V1

### Sensors
- Rain sensor module
- HW-038 water level sensor
- JSN-SR04T waterproof ultrasonic sensor

### Outputs
- RGB LED
- Active buzzer
- 1-channel relay module

---

## Wiring

### Rain Sensor
- AO -> GPIO 34
- DO -> GPIO 27
- VCC -> 3.3V
- GND -> GND

### HW-038 Water Sensor
- S -> GPIO 35
- VCC -> 3.3V
- GND -> GND

### Ultrasonic Sensor
- TRIG -> GPIO 5
- ECHO -> GPIO 18
- VCC -> 5V / VIN
- GND -> GND

### RGB LED
- R -> GPIO 14
- G -> GPIO 12
- B -> GPIO 13
- Common cathode (-) -> GND

### Active Buzzer
- SIG -> GPIO 25

### Relay
- IN -> GPIO 26

---

## Important Notes

- The ESP32 is a **3.3V** device.
- If the ultrasonic sensor ECHO pin outputs **5V**, use a voltage divider or level shifter before connecting it to GPIO 18.
- Sensor thresholds must be calibrated using real readings from the prototype.
- The system currently uses Serial Monitor output for debugging and live demonstration.

---

## Software Requirements

- Arduino IDE
- ESP32 board package installed
- Board selection: **DOIT ESP32 DEVKIT V1**

---

## Main Logic Summary

- If rain sensor AO is below threshold, rain is detected
- If water level sensor value is below threshold, water is detected
- If water is detected, ultrasonic sensor is activated
- Ultrasonic reading determines flood severity level
- Level 3 triggers slow buzzer alert
- Level 4 triggers fast buzzer alert and relay activation

---

## Live Demo Video
https://drive.google.com/file/d/1ahSTD4-SEh3nba5NuTJ95Jg_tVaRBi5V/view?usp=sharing

---

## Example Serial Output

```text
Rain AO: 2400
Rain DO: WET
Rain: POSITIVE
WaterLevel: 1800
Water Trigger: POSITIVE
Ultrasonic Distance (cm): 5.80
Level 3: Warning Evacuate

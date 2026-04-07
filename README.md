# Vehicle-Control-Unit-PCB Overview
The Vehicle Control Unit PCB (VCU) is a 4-layer PCB designed for the 2025-2026 Formula SAE Competition EV car (FS-4) at UC Santa Cruz. This board serves as the central low-voltage control system for the vehicle and integrates multiple critical functions into a single platform. The board was designed using KiCAD and printed through JLC PCB.
The board mainly serves these purposes:
1. Brake System Plausibility Device (BSPD) and Main Shutdown Circuit:
2. Electronic Throttle Control: Motor control using position pedal sensor inputs
3. Inertial Measurement Unit: Improves FS-4's traction control
4. System Fault Indication: Traction System Status Indicator, ETC.

## Top Layer Signal Diagram
<div align="center">
  <img src="Schematic_Images/Signals_In:Out.png" width="90%">
</div>
The top layer of my schematic is dedicated to present all of the signals inputs and outputs from each connector. It represents a "block diagram" view of the schematic, containing where each of the 60+ signals go.

## BSPD and Shutdown Circuit
<div align="center">
  <img src="Schematic_Images/BSPD.png" width="90%">
</div>
The brake system plausibility device is a safety mechanism that detects a high current from the motor and active braking. To detect a high current, the output signal from the HASS-300-S current sensor is each filtered to 8841 Hz and buffered. It is then put through a differential amplifier with a gain of 20 in order to obtain a stable, single ended voltage output, as well as a comparator with a voltage threshold based on the reading of the current sensor at our vehicle's nominal current. Similarly, to detect a hard braking, we filter and buffer signals from a pressure sensor for both the front and rear brake. This is compared to a potentiometer we calibrated based on our driver's voltage reading on the pressure sensor while braking. If both of these requirements are fulfilled, then the circuit will output a high, openning our relay connected to the shutdown circuit. Other cases such as the sensor having a short or open circuit also triggers a fault using a series of comparators and logic gates.

## STM32 Microcontroller
<div align="center">
  <img src="Schematic_Images/MCU.png" width="90%">
</div>

## Final PCB
<div align="center">
  <img src="VCU_PCB.jpg" width="55%">
</div>
One of the hardest parts of the process was soldering and debugging the board. 

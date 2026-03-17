
# LightRail Gen3 – Versal Accelerator Board Architecture (Upgrade Plan)

Target device:
AMD Versal Adaptive SoC

Recommended configuration:
• 1 × 400G QSFP-DD optical interface
• PCIe x16 accelerator card
• 20-layer PCB stackup

-----------------------------------
Compute Engine
-----------------------------------

Main device:
U1  AMD Versal ACAP

Required support:
U2  QSPI Boot Flash
U3  I2C EEPROM
U4  DDR4 / DDR5 memory
J1  JTAG Header
U5  System monitor

Power rails required:

VCCINT   0.85V
VCC_RAM  0.90V
VCCIO    1.8V / 3.3V
VCCAUX   1.8V
MGTAVCC  0.9V
MGTAVTT  1.2V

-----------------------------------
PCIe Interface
-----------------------------------

Connector:
PCIe x16 edge connector

Clock:
100 MHz differential reference clock

Required components:

PCIe clock buffer
Reset supervisor
I2C EEPROM

-----------------------------------
Optical Interface
-----------------------------------

Connector:
QSFP-DD 400G module

Signals:

TX0±
TX1±
TX2±
TX3±

RX0±
RX1±
RX2±
RX3±

Control:

MODSEL
RESET
INT
SCL
SDA

-----------------------------------
Clock System
-----------------------------------

Recommended clock generator:

Si5341 jitter-cleaning clock generator

Outputs:

100 MHz PCIe
156.25 MHz Ethernet
322 MHz SerDes
25 MHz management

-----------------------------------
Power Tree
-----------------------------------

Input:

12V from PCIe slot

Generate rails:

0.85V  FPGA core
0.9V   transceivers
1.2V   logic
1.8V   IO
3.3V   management

Use multiphase buck regulators for core rails.

-----------------------------------
PCB Stackup (20 Layers)

L1  Signal
L2  GND
L3  PCIe
L4  GND
L5  Power
L6  Signal
L7  SerDes
L8  GND
L9  Power
L10 Signal
L11 Signal
L12 Power
L13 GND
L14 SerDes
L15 Signal
L16 Power
L17 GND
L18 Signal
L19 GND
L20 Signal

-----------------------------------
Routing Constraints

PCIe lanes:
85Ω differential impedance
skew < 5 mil

SerDes lanes:
100Ω differential
length mismatch < 1 mil

Clock nets:
50Ω single ended
100Ω differential

-----------------------------------

Next recommended steps:

1. Fix ERC violations in schematics
2. Populate FPGA support circuits
3. Implement power sequencing
4. Define differential pair constraints in KiCad
5. Perform signal integrity simulation before fabrication

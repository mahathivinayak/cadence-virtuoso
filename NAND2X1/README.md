# NAND2X1 — 2-Input CMOS NAND Gate (1X Drive Strength)

A 2-input NAND gate designed in **Cadence Virtuoso**, taken through the full custom design flow: schematic → symbol → simulation → layout → DRC → LVS.

**Function:** `Y = NOT (A AND B)`

| A | B | Y |
|:-:|:-:|:-:|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

## 1. Schematic
- **Pull-down network:** two NMOS transistors in **series**. The output is pulled to GND only when both A and B are high.
- **Pull-up network:** two PMOS transistors in **parallel**. The output is pulled to VDD when either input is low.

![Schematic](Schematic.png)

## 2. Symbol
The schematic is wrapped into a symbol with pins A, B, Y, VDD and GND for reuse in larger designs.

![Symbol](Symbol.png)

## 3. Testbench
Pulse sources with different periods drive A and B so that all four input combinations are covered, with a load capacitor on the output.

![Testbench](Testbench.png)

## 4. Sizing
The two series NMOS transistors act like one transistor of double length, so each is made about twice as wide as in the inverter to keep the pull-down strength the same. The parallel PMOS transistors keep inverter sizing, since one PMOS alone has to be able to pull the output up.

![Symmetric Values](Symmetric%20Values.png)

## 5. Output Waveforms
The output goes low only while both inputs are high, which matches the NAND truth table.

![Output Waveforms](Output%20Waveforms.png)

## 6. Layout
The PMOS pair sits in the N-well at the top and the NMOS pair at the bottom, with shared poly gates for A and B and VDD/GND rails.

![Layout](Layout.png)

## 7. DRC — Design Rule Check
Checks the layout against the foundry's minimum width, spacing and enclosure rules.

**Result: no DRC violations.**

![DRC](DRC.png)

## 8. LVS — Layout vs Schematic
Extracts the circuit from the layout and confirms it matches the schematic netlist.

**Result: the layout matches the schematic.**

![LVS](LVS.png)

---

## Tools
Cadence Virtuoso (Schematic, Layout), ADE with Spectre, physical verification for DRC/LVS

# Procedure · Panel signal wiring (landing strips → DAQ)

The schematic is the wiring authority - this is the bench procedure distilled from it.
**Wire the DAQ by terminal NUMBER.** The USB-1608G silkscreen shows single-ended names; in
differential mode the same screws become H/L pairs.

## Wire colors (as built)

| Family | HI wire | LO wire |
|---|---|---|
| Wave gauges + pressure | **white** | **blue** |
| Load cells | **yellow** | **green** |

Twist each HI wire with its LO partner the whole way, landing strip → DAQ.

## Per-channel hookup

| Channel | Sensor | From landing | HI → DAQ pin | LO → DAQ pin |
|---|---|---|---|---|
| CH0 | WG1 | TB-J1: term 3 / term 4 | white → **1** | blue → **2** |
| CH1 | WG2 | TB-J2: term 3 / term 4 | white → **4** | blue → **5** |
| CH2 | WG3 | TB-J3: term 3 / term 4 | white → **7** | blue → **8** |
| CH3 | WG4 | TB-J4: term 3 / term 4 | white → **10** | blue → **11** |
| CH4 | F1 (IAA-1) | TB-J5: term 5 / term 4 | yellow → **38** | green → **37** |
| CH5 | F2 (IAA-2) | TB-J6: term 5 / term 4 | yellow → **35** | green → **34** |
| CH6 | F3 (IAA-3) | TB-J7: term 5 / term 4 | yellow → **32** | green → **31** |
| CH7 | PS1 Setra | TB-J8: term 3 / term 4 | white → **29** | blue → **28** |

## Ground references - each power island touches AGND exactly ONCE

| GND bus position | Connection |
|---|---|
| G1–G4 | Gauge shields in (TB-J1..J4 term 5, black wire) |
| G5 | Setra −Out tie (TB-J8 term 4 **also** runs a black wire here - keep both its wires) |
| G6 | GND_24 reference jumper from block A6 (force island's only path to AGND) |
| back sides | 2 drops out → DAQ pins **12** and **39** |

## Rules

- Gauge/amp signal-low wires go ONLY to their CHxL pins - never to the GND bus.
- Yellow blocks (GND_24ISO / Setra excitation) never connect to anything outside the island.
- Never land a supply wire on a DAQ terminal - absolute max input is ±25 V to AGND.
- Terminals marked X on the schematic stay empty (incl. DAQ pins 13, 15, 27, 47, 48 - true no-connects).
- Shunt-cal lines park on TB-J5..J7 term 3, back side empty - see `shunt-calibration.md`.
- Ferrule every stranded conductor into a screw clamp.

# Procedure · Panel signal wiring (landing strips → DAQ)

The schematic is the wiring authority - this is the bench procedure distilled from it, updated
to the **as-built** panel (2026-10). **Wire the DAQ by terminal NUMBER.** The USB-1608G
silkscreen shows single-ended names; in differential mode the same screws become H/L pairs.

## Landing strip map - same 5-terminal pattern on every strip

Every bulkhead receptacle pigtail uses the same conductor colors (TE insert):

| Term | Pigtail wire | Function |
|---|---|---|
| 1 | **brown** | Power + (12 V for WG, 24 V for LC, 24 V-ISO for PT) |
| 2 | **white** | Signal HI → DAQ CHxH |
| 3 | **blue** | Signal LO / analog reference → DAQ CHxL |
| 4 | **black** | Power return (GND_12 / GND_24 / GND-ISO) |
| 5 | **gray** | Shield (WG, PT) - **but SHUNT on LC strips** (see warning) |

> **Warning - LC term 5 is NOT a shield.** On LC1-LC3 the gray conductor carries the IAA100
> **remote shunt** line (orange wire at the amp, FI1573 pin 3). The printed strip label
> "5-GRY-SHLD" is wrong on the LC strips - relabel as SHUNT. Load cell shields terminate at
> the amp's CHASSIS screw at the flume and never enter the panel.

## Internal hookup wire colors (strip → buses / DAQ), as built

| Color | Use |
|---|---|
| yellow | +12 V feeds (12 V bus → WG term 1) |
| red | +24 V feeds (24 V bus → LC term 1) |
| orange | Setra isolated island (24V-ISO → PT term 1) |
| black | power returns (term 4 → ground buses) |
| blue | AGND / analog reference distribution |
| white + blue twisted | WG + PT signal pairs to DAQ (white = HI) |
| yellow + green twisted | LC signal pairs to DAQ (yellow = HI) |

Twist each HI wire with its LO partner the whole way, landing strip → DAQ.

## Per-channel hookup

| Channel | Sensor | From landing | HI → DAQ pin | LO → DAQ pin |
|---|---|---|---|---|
| CH0 | WG1 | TB-J1: term 2 / term 3 | white → **1** | blue → **2** |
| CH1 | WG2 | TB-J2: term 2 / term 3 | white → **4** | blue → **5** |
| CH2 | WG3 | TB-J3: term 2 / term 3 | white → **7** | blue → **8** |
| CH3 | WG4 | TB-J4: term 2 / term 3 | white → **10** | blue → **11** |
| CH4 | LC1 (IAA-1) | TB-J5: term 2 / term 3 | yellow → **38** | green → **37** |
| CH5 | LC2 (IAA-2) | TB-J6: term 2 / term 3 | yellow → **35** | green → **34** |
| CH6 | LC3 (IAA-3) | TB-J7: term 2 / term 3 | yellow → **32** | green → **31** |
| CH7 | PT1 Setra | TB-J8: term 2 / term 3 | white → **29** | blue → **28** |

## Cable (plug) side, as built

| Family | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| WG (gauge pins F/B/C/E/D) | red = PWR_HI | green = SIG_HI | white = SIG_LO | black = PWR_LO | shield drain |
| LC (IAA100 power/output) | red = +VIN | white = VOUT | blue = OUT_GND | black = PWR_GND | orange = SHUNT |
| PT (Setra 239, code 02/10/25) | red = +Exc | green = +Out | white = −Out | black = −Exc | shield = case |

## Ground references - each power island touches AGND exactly ONCE

| GND bus position | Connection |
|---|---|
| G1-G4 | Gauge shields in (TB-J1..J4 term 5, gray wire) |
| G5 | Setra −Out tie (TB-J8 term 3 **also** runs a wire here - keep both its wires) |
| G6 | GND_24 reference jumper from block A6 (force island's only path to AGND) |
| back sides | 2 drops out → DAQ pins **12** and **39** |

## Rules

- Gauge/amp signal-low wires go ONLY to their CHxL pins - never to the GND bus.
- The Setra excitation island (orange 24V-ISO / GND-ISO blocks) never connects to anything
  outside the island.
- Never land a supply wire on a DAQ terminal - absolute max input is ±25 V to AGND.
- Terminals marked X on the schematic stay empty (incl. DAQ pins 13, 15, 27, 47, 48 - true no-connects).
- Shunt-cal lines park on TB-J5..J7 **term 5** (front = gray pigtail, back side empty) - see
  `shunt-calibration.md`.
- Ferrule every stranded conductor into a screw clamp.

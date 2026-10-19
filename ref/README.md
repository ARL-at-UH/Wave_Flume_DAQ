# ref/ - Reference documents

Primary sources for the wave flume DAQ panel. The design documents (ICD, schematic, BOM) cite these.

| File | What it is | Used for |
|---|---|---|
| `AWP-24-3_Users_Guide.pdf` | Akamina AWP-24-3 wave gauge user's guide | Gauge pinout, 8–24 V supply range, single-point grounding rule, operating-frequency selection |
| `iaa100-drawing-fi1573.pdf` | FUTEK IAA100 spec drawing FI1573 | Supply 12–30 VDC, 1.2 A inrush (time-delay fuse), power/output pin colors, shield-to-CHASSIS rule |
| `iaa100-product-manual.pdf` | FUTEK IAA100 product manual | DIP switch settings (10 V excitation, 2 mV/V gain), shunt cal |
| `lsb210-drawing.pdf` | FUTEK LSB210 load cell drawing | Wiring code WC1 (Red +Exc / Black −Exc / Green +Sig / White −Sig), 2 mV/V |
| `239-Operating-Instructions.pdf` | Setra 204/239 operating instructions (SS0461 Rev. I) | 4-terminal rule (−Exc never to −Out), termination color codes, multi-hookup options |
| `digilent-usb-1608g-manual.pdf` | MCC USB-1608G user's guide (Digilent, Jan 2019 Rev 2) | Differential pinout (Fig. 5), floating-source 100 kΩ rule, ±10.2 V common-mode window, specs |
| `hdr-15-spec.pdf` | Mean Well HDR-15 series datasheet | Class II floating output, adjustment ranges, derating |
| `DAQ_Sketch.pdf` | Original hand sketch of the system | Historical - source of the channel assignments (force CH0–2, pressure CH3, gauges CH4–7) |

Unit label (recorded, no PDF): Setra **2391-015WB1F23259NN** - ±15 inWC, excitation 22–30 VDC single supply, output ±2.5 VDC bipolar (standard 4-wire).

# Wave Flume DAQ Panel

Student-built data acquisition panel for a laboratory wave flume: 4× Akamina AWP-24-3 wave-height
gauges, 3× FUTEK LSB210 load cells (through IAA100 amplifiers at the flume), and a Setra 239
differential pressure transducer — all eight channels **differential** into an MCC **USB-1608G**
(16-bit), with three isolated power islands and M12 bulkhead connectors on a DIN-rail panel.

## Schematic

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/schematic-dark.svg">
  <img alt="Wave flume DAQ interconnect schematic" src="docs/schematic.svg">
</picture>

*Zoom in — it's vector. Printable copy: [`docs/wave_flume_daq_schematic.pdf`](docs/wave_flume_daq_schematic.pdf)
(A2 sheet — print poster-tiled at 100% or large-format).*

**Interactive viewer:** open the schematic in [KiCanvas](https://kicanvas.org) by pasting this repo's
URL (or a direct link to `kicad_schematic/wave_flume_daq.kicad_sch`) — pan, zoom, and click nets in
the browser, nothing to install.

## Repo map

| Path | Contents |
|---|---|
| [`docs/`](docs/) | Build & operations documents: schematic PDF/SVG, as-ordered BOM, noise-debugging checklist |
| [`ref/`](ref/) | Primary sources: sensor/DAQ manufacturer manuals and drawings (indexed in its README) |
| [`kicad_schematic/`](kicad_schematic/) | KiCad 9/10 project — schematic, project symbol library |

## Design rules worth knowing before touching anything

- **Three power islands, each referenced to analog ground exactly once:** `GND_24` (force amps,
  via the A6 jumper), `GND_12` (gauges, via their shields), `GND_24ISO` (Setra island, via −Out).
  Never add a second path; never let yellow (`GND_24ISO`) blocks touch anything.
- **Every channel is a twisted HI+LO pair:** gauges + pressure = **white (HI) / blue (LO)**;
  load cells = **yellow (HI) / green (LO)**. Channels as installed: gauges CH0–CH3, force CH4–CH6,
  pressure CH7. Wire the DAQ by **terminal number** — the USB-1608G silkscreen shows single-ended
  names; the schematic's hookup block gives the numbers.
- **Block color = wire color** on the DIN rails. No green/yellow PE blocks anywhere (they bond to
  the rail and would earth the floating grounds).
- M12 **B-code** (gauges, J1–J4) physically cannot mate **A-code** (amps + pressure, J5–J8) —
  that keying separates the 12 V and 24 V domains. J5–J8 are identical to each other: read the labels.

The full interface control document (pinouts, cable schedule, terminal maps, grounding rationale)
is maintained as a living web document — ask the maintainer for the current link.

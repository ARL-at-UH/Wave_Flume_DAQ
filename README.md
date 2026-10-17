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
| [`docs/`](docs/) | Hosted ICD (`index.html`), step-by-step [`procedures/`](docs/procedures/), [`debug/`](docs/debug/) guides, schematic PDF, as-ordered BOM |
| [`ref/`](ref/) | Primary sources: sensor/DAQ manufacturer manuals and drawings (indexed in its README) |
| [`kicad_schematic/`](kicad_schematic/) | KiCad 9/10 project — schematic, project symbol library |

## Project site

The full **Interface Control Document** (pinouts, cable schedule, terminal maps, grounding
rationale) ships as [`docs/index.html`](docs/index.html). Enable **GitHub Pages**
(Settings → Pages → Deploy from a branch → `main`, folder `/docs`) and it is served as the
project's website — no build step, it's one self-contained page.

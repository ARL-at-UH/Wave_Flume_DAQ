# docs/ — Build & operations documents

| File | What it is |
|---|---|
| `wave_flume_daq_schematic.pdf` | Full interconnect schematic (A2) — print at 100% tiled, or large-format. Regenerated from `../kicad_schematic/` with kicad-cli |
| `BOM.csv` | Master parts record, as-ordered (equipment in hand + purchased items with part numbers) |
| `noise_debug_checklist.md` | Ordered noise-diagnosis procedure (characterize → toggles → ground-loop checks → per-sensor → software) |

Per-channel DAQ wiring lives in the schematic's DAQ hookup block and the ICD's IF-F table — the schematic is the wiring authority.

The living Interface Control Document (Rev C) is the published web version — ask Matthew for the link.
Primary manufacturer sources live in `../ref/`.

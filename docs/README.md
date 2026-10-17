# docs/ — Build & operations documentation

## Interface Control Document (hosted)

`index.html` is the full ICD — pinouts, cable schedule, terminal maps, grounding rationale.
With GitHub Pages enabled (repo **Settings → Pages → Deploy from a branch → `main` / `/docs`**)
it is served at `https://<user>.github.io/<repo>/`. It is a self-contained page; no build step.

## Procedures

| File | Purpose |
|---|---|
| [`procedures/panel-wiring.md`](procedures/panel-wiring.md) | Landing-strip → DAQ hookup by terminal number, as-built wire colors, ground references |
| [`procedures/software-setup.md`](procedures/software-setup.md) | InstaCal differential mode, per-channel ranges, acquisition settings, first-signal checks |
| [`procedures/shunt-calibration.md`](procedures/shunt-calibration.md) | Verifying each force chain with the IAA100 internal shunt |

## Debug

| File | Purpose |
|---|---|
| [`debug/noise-debugging.md`](debug/noise-debugging.md) | Ordered noise diagnosis: characterize → toggles → ground-loop checks → per-sensor → software |

## Reference artifacts

| File | Purpose |
|---|---|
| `wave_flume_daq_schematic.pdf` | Full interconnect schematic (A2) — print poster-tiled at 100%, or large-format. Regenerated from `../kicad_schematic/` |
| `BOM.csv` | Master parts record, as ordered |

Primary manufacturer manuals live in [`../ref/`](../ref/). The KiCad schematic is the wiring
authority; procedures here restate it for the bench — if they ever disagree, the schematic wins
and the procedure gets fixed.

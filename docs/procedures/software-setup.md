# Procedure · DAQ software setup (USB-1608G)

## 1 · InstaCal (once per PC)

1. Connect the panel's exterior USB-B jack to the PC; the DAQ's Status LED lights.
2. Open **InstaCal** - the USB-1608G appears as board 0.
3. Open the board's configuration and set **Analog Input Mode = Differential**.
   Until this is set, the terminal numbering means different things - do not trust any reading.

## 2 · Channel configuration (DAQami or Python)

| Channels | Source | Range |
|---|---|---|
| CH0–CH3 | Wave gauges WG1–4 | ±10 V |
| CH4–CH6 | Load cells LC1–3 (via IAA100) | ±10 V |
| CH7 | Setra 239 pressure | **±5 V** (output is ±2.5 V = ±15 inWC) |

The 1608G supports per-channel ranges (channel-gain queue) - DAQami handles this natively.

## 3 · Acquisition settings that fight noise for free

- **Hardware-paced** scans, not software-paced (software pacing adds USB timing jitter).
- Sample at an **integer multiple of 60 Hz** (600 or 1200 S/s) and average whole 1/60-s
  windows - this notches mains hum almost perfectly. Wave phenomena live below ~10 Hz,
  so nothing of interest is lost.
- Allow the module's **15-minute warm-up** before calibration-grade readings.

## 4 · First-signal sanity checks

1. With everything powered and sensors connected, each channel should sit at a steady,
   plausible value (gauges mid-range in still water, force near zero unloaded, pressure near
   zero at equal port pressures).
2. A channel pegged at full scale usually means its H/L pair is on the wrong terminals -
   recheck against `panel-wiring.md` by terminal number.
3. A channel reading inverted (goes down when it should go up) means H and L are swapped
   at the landing strip or the DAQ.
4. Laptop-on-battery vs. mains is the 30-second USB-ground-loop test - see
   `../debug/noise-debugging.md`.

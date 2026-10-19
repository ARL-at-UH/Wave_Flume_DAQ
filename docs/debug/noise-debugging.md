# Wave Flume DAQ - Noise Debugging Checklist

System: 8 sensors differential into MCC USB-1608G · three power islands (GND_24 force / GND_12 gauges / GND_24ISO Setra) · single-point references to AGND.
Work top-down. **What the noise looks like tells you which branch to walk.**

---

## 0 · Characterize before touching anything

- [ ] **Measure the floor.** Jumper a spare differential channel's H + L together and to AGND at the DAQ. Record a few seconds. This is the best the system can ever do (~1–2 LSB).
  - Noisy even here → the problem is the DAQ's USB/PC environment, not the wiring. Stop and fix that first.
- [ ] **Look at the shape** of the noise on a real channel (strip chart or FFT):

| Noise signature | Likely cause | Go to |
|---|---|---|
| Clean 60 Hz (+ 120/180 Hz harmonics) | Mains coupling or ground loop | §2 |
| Slow wandering beats, a few Hz | Gauge-oscillator interference | §4 gauges |
| Broadband hash / fuzz | Switching-supply EMI or aliasing | §1 + §5 |
| Discrete spikes / bursts | Something switching nearby (paddle drive, pump, solenoid) | §1 toggles |

- [ ] **Note which channels** are noisy:
  - All eight → common cause (power, USB, DAQ)
  - One sensor family → that island
  - One channel → that wire / that sensor

---

## 1 · Five-minute toggles (in order; record the result of each)

| # | Toggle | If the noise drops, the culprit is |
|---|---|---|
| 1 | Laptop on battery, charger unplugged | USB ground loop through the PC supply. Fix: powered isolated USB hub, or run on battery |
| 2 | One sensor powered at a time (pull orange/red feeds at the bus) | Inter-sensor interference - almost always the gauges (§4) |
| 3 | Wave paddle / pumps / VFD off | Drive electronics EMI. Reroute field bundles away from motor cables; add ferrites |
| 4 | Room lights off (esp. fluorescent/LED banks over the flume) | Radiated pickup - field bundle routing/twisting |
| 5 | Swap the HDR supply for the bench BK 1672 (one rail at a time, current-limited) | HDR switching noise. Add 100 µF + 0.1 µF across that rail at the bus, or move the supply away from the signal duct |

---

## 2 · Ground-loop verification (ohmmeter; everything powered OFF, USB unplugged)

Confirm the single-reference design actually got built:

- [ ] **GND_24ISO (X2 / yellow) to AGND: OPEN** (>1 MΩ). Continuity = someone jumpered yellow - suspect #1.
- [ ] **AGND to earth stud / steel box: OPEN.** Continuity = a shield shell got terminated, a supply output touches earth, or a duct screw pinched a wire.
- [ ] **GND_12 (B-row) to AGND:** reads through the gauges only - unplug J1–J4 and it must go OPEN.
- [ ] **GND_24 to AGND:** exactly one path - lift the A6 jumper and it must go OPEN.
- [ ] **Flume water to panel AGND** (voltmeter, AC range, powered ON): the gauges stand in water that touches pumps and building plumbing - labs see volts of 60 Hz here. If large, the fix is a deliberate bonding strategy at the flume, not panel wiring.

---

## 3 · Wiring craft (visual + tug test)

- [ ] Every H wire **twisted with its L partner** the whole way, landing strip → DAQ - not two loose wires on different routes.
- [ ] Field bundles: white twisted with its black; bundle **not parallel** to the mains cord or paddle motor cables (90° crossings fine).
- [ ] Mains inside the box (C14 → TB14 → supplies) routed along one edge, away from the signal duct.
- [ ] Shield continuity end-to-end: gauge pin D → M12 contact 5 → landing term 5 → G1–G4 (beep it).
- [ ] Ferrules fully seated - a strand-or-two connection is a noise generator.

---

## 4 · Sensor-specific

**Wave gauges (the usual winner):**
- [ ] If one-at-a-time (§1 #2) was quiet but together is noisy → the AWP-24 oscillators are beating. Set each gauge to a **different operating frequency** (frequency-select in the AWP-24-3 manual, `../ref/`).
- [ ] Check Akamina's "Acquiring Minimum Noise Data" app note for probe spacing.

**Load cell amps (IAA100):**
- [ ] Each cable shield on the **CHASSIS screw**, with the short bond to out-gnd (one point only).
- [ ] Amps mounted away from paddle drives.
- [ ] DIP switches: 10 V excitation / 2 mV/V range.

**Setra 239:**
- [ ] If its cable was extended: long cables can make the output **oscillate** - fix is 100 Ω in series with each output lead (per the manual).
- [ ] Vent cable not pinched or sealed.

---

## 5 · Software (free fixes - do these regardless)

- [ ] **Sample fast and average:** sample at an integer multiple of 60 Hz (600 or 1200 S/s) and average whole 1/60-s windows - notches line hum almost perfectly; wave phenomena are <10 Hz so nothing is lost.
- [ ] Hardware-paced scans, not software-paced (software pacing adds USB timing jitter).
- [ ] Tightest range that fits: CH7 ±5 V (Setra); gauges (CH0–CH3) ±5 V too if their calibrated span allows.
- [ ] 15-minute warm-up before judging anything.

---

*If you reach the end without a verdict: record amplitude, spectrum, affected channels, and which toggles changed it - then diagnose from data.*

# Procedure · Load cell shunt calibration (IAA100)

Verifies the whole force chain — cell, cable, amplifier gain, DAQ — without applying a load.
Per the IAA100 manual (`../../ref/iaa100-product-manual.pdf`): applying **5–26 VDC to the shunt
pin** switches the amp's internal shunt resistor (60.4 kΩ default) across the bridge, exactly
like pressing the front-panel button. Removing the voltage ends it. The pin floats when idle —
it is **never tied to ground**.

## Steps (per channel)

1. Start acquisition on the force channel (CH4 = F1, CH5 = F2, CH6 = F3) with the cell
   **unloaded**. Note the zero reading.
2. Take a short jumper wire with ferruled ends.
3. At the panel: touch one end to any **red +24 V block** and the other to the parked shunt
   terminal — **TB-J5 term 3** (F1), **TB-J6 term 3** (F2), **TB-J7 term 3** (F3). Front side;
   the back side is intentionally empty.
4. The channel steps to its shunt value. Hold a few seconds, record, remove the jumper.
5. Compare the step against the **FUTEK calibration certificate** for that cell/amp pair
   (the expected shunt output in volts). Within tolerance → the chain is verified.

## Notes

- A step appears but is the wrong size → amp gain DIP switches (should be 10 V excitation,
  ±2 mV/V range — see the manual's switch tables) or wrong cell certificate.
- No step → check the shunt wire chain: amp pin 3 → M12 contact 3 → TB-J5..7 term 3.
- Touching the jumper to anything other than +24 V red blocks does nothing useful; touching
  it to the blue/yellow blocks violates the grounding scheme — don't.
- A future upgrade for software-triggered shunt cal (DAQ DIO → opto-isolated relay) is
  designed but not installed; the parked terminals are where it would connect.

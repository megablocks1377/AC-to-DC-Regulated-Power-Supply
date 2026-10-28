# LTspice files - 12 V AC to 5 V DC power supply

## Open the editable schematic

1. Extract this ZIP into a single folder. **Keep `.asc`, `.asy`, and `.lib` files together.**
2. Open `AC_DC_5V_Power_Supply.asc` with LTspice.
3. The circuit already contains a 60 Hz, 11.9 Vrms sine source, four-diode full-wave bridge, 1000 uF reservoir capacitor, 4.7k bleeder resistor, 0.33 uF input bypass, behavioral 7805 regulator, 0.1 uF output bypass, and 1k load.
4. Click **Run**. Probe the nodes `VRAW` and `VOUT` to see filtered DC and regulated DC. The voltage source and bridge let you inspect the AC and rectified stages too.
5. To test load regulation, edit `.param RL=1k` to `RL=470`, `RL=220`, or `RL=100`, then re-run. Keep safe power ratings in mind if constructing a physical circuit.
6. Open **View > SPICE Error Log** (or `Ctrl+L` on Windows) to read the `.meas` averages and ripple.

## Text-only simulation

Open `AC_DC_5V_Power_Supply.cir` in LTspice and run it. It uses the same model library but does **not** display a graphical schematic; use the `.asc` file for the editable visual design.

## Critical model limitations

`LM7805_EDU.lib` is an **educational behavioral model** that approximates 5 V regulation above roughly 7 V input, a typical 5 mA quiescent input current around 15.3 V and nominal output current draw. It is NOT a real LM7805 manufacturer SPICE model. It does NOT accurately simulate thermal shutdown, short circuit behavior, current limiting, minimum/maximum dropout across temperature, loop stability, line/load-transient response, or ripple-rejection bandwidth. The diode `.model` is also illustrative, not a characterized sample of your exact diodes.

**Do not present simulated figures as measured results.** Your real lab values were approximately 11.9 Vrms AC, 10 V unfiltered average, 15.2 V filtered DC, 4.99 V output at 1k, ~27 mV peak-to-peak ripple with a light load, and ~55 mA input current into the 7805 at a 100-ohm load. These are separate from LTspice predictions.

## Model and physical circuit

- Physical input: safely isolated 12 V AC low-voltage source; 120 V wall power must NOT connect to this breadboard.
- Electrolytic filter capacitor must be rated **35 V or higher** and be correctly polarized. The schematic capacitor value shows capacitance only.
- Include a suitable 100-ohm high-power load resistor and evaluate regulator heat when testing 50 mA physically.
- Overall AC-to-DC efficiency requires **real input power** measurement, not just DC regulator efficiency.

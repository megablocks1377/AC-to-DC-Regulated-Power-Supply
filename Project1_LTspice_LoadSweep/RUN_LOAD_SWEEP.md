# Project 1 — Automated LTspice load sweep

Open `AC_DC_5V_Power_Supply.asc` in LTspice from this extracted folder and press **Run**.

The `.step param RL list 1k 470 220 100` directive runs four load-resistor cases automatically.

Press **Ctrl+L** (SPICE Error Log) to inspect the measured values for each step:

- `VRAW_AVG`: filtered rectifier DC input to regulator, V
- `VOUT_AVG`: regulated output, V
- `ILOAD_AVG`: load current through R_LOAD, A (multiply by 1000 for mA)
- `VRAW_RIPPLE`: peak-to-peak ripple at the regulator input, V
- `VOUT_RIPPLE`: peak-to-peak ripple at the regulated output, V

The measurements are taken from **200 ms to 250 ms**, after startup.

| Load (ohms) | LTspice VRAW avg (V) | LTspice VOUT avg (V) | LTspice load current (mA) | LTspice VRAW ripple (mV p-p) | Bench VOUT (V) |
|---:|---:|---:|---:|---:|---:|
| 1000 |  |  |  |  | 4.99 |
| 470 |  |  |  |  | *record exact value* |
| 220 |  |  |  |  | *record exact value* |
| 100 |  |  |  |  | *record exact value* |

**Important:** The previously observed roughly 27 mV p-p ripple was measured at an earlier stage with only the 4.7 kohm rectifier-side load. Do not compare it directly to this simulation with an added 7805 and different loads, which place extra demand on the reservoir capacitor.

**Model limitation:** `LM7805_EDU.lib` is a simplified behavioral teaching model, not a manufacturer 7805 model; do not claim simulated transient behavior or thermal protection validate a real regulator.

**Safety when repeating physical tests:** 100 ohm at 5 V dissipates 0.25 W: use a 1 W resistor for sustained tests. The regulator dissipates ~0.59 W at the observed 100-ohm load and should be thermally checked. Use only an isolated 12 V AC supply.

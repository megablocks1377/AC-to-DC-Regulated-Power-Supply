# Project 1 — Portfolio Results Package

This package is a **results add-on** to the existing AC-to-DC LTspice project, not a replacement for the existing `.asc` schematic and `.lib` model files.

- `results/ltspice_load_sweep.csv`: numeric results transcribed from LTspice 24.1.10 Error Log (`.meas` window: 200–250 ms)
- `results/RESULTS.md`: calculations, validation discussion, bench-vs-simulation caveats and embedded charts
- `charts/load_regulation.png`: simulated output-voltage-versus-current graph
- `charts/input_ripple.png`: simulated filtered DC ripple-versus-current graph
- `charts/input_voltage.png`: simulated filtered DC average-versus-current graph
- `PORTFOLIO_COPY.md`: ready-to-edit portfolio write-up

To publish, copy these files into your GitHub repository and keep your original LTspice simulation files under `simulation/`.

No hardware photos are needed. Do not represent simulated output ripple, simulated values for unrecorded bench loads, or idealized regulator behavior as physical measurements.

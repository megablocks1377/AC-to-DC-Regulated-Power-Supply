# AC-to-DC Regulated Power Supply

A low-voltage power electronics project designed to convert a nominal **12 V AC input into a regulated 5 V DC output** using full-wave bridge rectification, capacitive filtering, and an LM7805 linear voltage regulator.

The project was designed and analyzed using **LTspice**, including a multi-load sweep to evaluate rectified voltage, ripple, output regulation, and circuit behavior as load current increased.

---

## Project Overview

The goal of this project was to design and evaluate a complete AC-to-DC power conversion system.

The conversion chain is:

```text
12 V AC Input
      ↓
Full-Wave Bridge Rectifier
      ↓
Pulsating DC
      ↓
Capacitive Filter
      ↓
Smoothed DC
      ↓
LM7805 Linear Regulator
      ↓
Regulated 5 V DC Output
```

The project demonstrates several fundamental concepts in power electronics:

- AC-to-DC conversion
- Full-wave bridge rectification
- Diode voltage drops
- Capacitive filtering
- Ripple voltage
- Linear voltage regulation
- Load regulation
- Power dissipation
- Efficiency
- Circuit simulation
- Electrical testing

---

# Circuit Architecture

The power supply consists of the following major stages:

## 1. AC Input

The circuit begins with a nominal:

```text
12 V RMS AC
```

source.

For a sinusoidal waveform, the theoretical peak voltage is:

```text
Vpeak = Vrms × √2
```

Therefore:

```text
Vpeak = 12 × 1.414
Vpeak ≈ 16.97 V
```

---

## 2. Full-Wave Bridge Rectifier

Four rectifier diodes are arranged as a full-wave bridge.

During each half-cycle, two diodes conduct.

Assuming approximately:

```text
0.7 V
```

of forward voltage drop per diode:

```text
Vrectified_peak ≈ Vpeak - 2Vd
```

```text
Vrectified_peak ≈ 16.97 - 1.4
```

```text
Vrectified_peak ≈ 15.57 V
```

The bridge rectifier converts both halves of the AC waveform into positive-going pulses.

---

## 3. Capacitive Filtering

A large electrolytic capacitor is connected after the bridge rectifier.

The filter capacitor:

- Charges near the peak of the rectified waveform
- Supplies current to the load between peaks
- Reduces voltage ripple
- Produces a smoother DC voltage for the regulator

The design uses approximately:

```text
1000 µF
```

of bulk filtering.

Ripple voltage can be approximated using:

```text
Vripple ≈ Iload / (fripple × C)
```

For full-wave rectification from a 60 Hz source:

```text
fripple = 120 Hz
```

As load current increases, the capacitor discharges more between charging peaks, increasing ripple.

---

## 4. LM7805 Voltage Regulation

The filtered DC voltage is supplied to an **LM7805 linear voltage regulator**.

The LM7805 produces a regulated output near:

```text
5 V DC
```

The regulator requires sufficient input voltage above 5 V to remain in regulation.

Because the rectified and filtered voltage is substantially greater than 5 V, the regulator has enough voltage headroom throughout the tested operating range.

---

# LTspice Simulation

The circuit was modeled and simulated using **LTspice**.

Two main simulation configurations were created.

---

## Main Power Supply Simulation

Located in:

```text
AC_DC_5V_LTspice/
```

This directory contains the main AC-to-DC regulated power supply simulation.

The model includes:

- AC source
- Bridge rectifier
- Rectifier diodes
- Filter capacitor
- LM7805 regulator model
- Output load
- Supporting components

---

## Load Sweep Simulation

Located in:

```text
Project1_LTspice_LoadSweep/
```

A stepped-load simulation was performed to evaluate how the circuit responds to increasing output current.

The following resistive loads were tested:

| Load Resistance | Approximate Output Current at 5 V |
|---:|---:|
| 1 kΩ | 5 mA |
| 470 Ω | 10.6 mA |
| 220 Ω | 22.7 mA |
| 100 Ω | 50 mA |

The LTspice sweep was configured using:

```text
.step param RL list 100 220 470 1000
```

This allows the same circuit to be automatically simulated under several output load conditions.

---

# Load Sweep Results

The average unregulated DC voltage decreased as load current increased.

Measured LTspice results included:

| Load Resistance | Average Raw DC Voltage |
|---:|---:|
| 100 Ω | 14.402 V |
| 220 Ω | 14.658 V |
| 470 Ω | 14.805 V |
| 1 kΩ | 14.890 V |

This behavior is expected because heavier loads draw more current from the filter capacitor between rectifier charging peaks.

As load current increases:

```text
Load Resistance ↓
        ↓
Load Current ↑
        ↓
Capacitor Discharge ↑
        ↓
Ripple ↑
        ↓
Average Raw DC Voltage ↓
```

The regulated output remains near the target **5 V DC** as long as the LM7805 input voltage remains above its required operating voltage.

---

# Example LTspice Measurement

One of the automated LTspice measurements used in the project was:

```text
Measurement: vraw_avg

step    AVG(V(VRAW))
1       14.4021033832
2       14.658059293
3       ~14.805
4       ~14.890
```

The corresponding stepped loads were:

```text
.step RL=100
.step RL=220
.step RL=470
.step RL=1000
```

This demonstrates the effect of load current on the unregulated DC bus.

---

# Expected Waveforms

## AC Input

Before rectification:

```text
      / \      / \      / \
     /   \    /   \    /   \
----/-----\--/-----\--/-----\----
   /       \/       \/       \
```

The voltage alternates between positive and negative polarity.

---

## Full-Wave Rectified Output

After the bridge rectifier:

```text
      / \      / \      / \
     /   \    /   \    /   \
----/-----\--/-----\--/-----\----
```

Both halves of the AC waveform are converted to positive polarity.

The ripple frequency becomes twice the input frequency.

For a 60 Hz source:

```text
Ripple Frequency = 120 Hz
```

---

## Filtered DC

After the smoothing capacitor:

```text
────────\____────────\____────────
```

The capacitor charges near each waveform peak and slowly discharges into the load between peaks.

This creates a mostly DC waveform with a small ripple component.

---

## Regulated Output

After the LM7805:

```text
──────────────────────────────────
             ≈ 5 V
```

The regulator removes most of the remaining voltage variation and maintains approximately 5 V DC.

---

# Load Current Calculations

Using Ohm's Law:

```text
I = V / R
```

For a 5 V output:

### 1 kΩ Load

```text
I = 5 / 1000
I = 0.005 A
I = 5 mA
```

### 470 Ω Load

```text
I = 5 / 470
I ≈ 10.64 mA
```

### 220 Ω Load

```text
I = 5 / 220
I ≈ 22.73 mA
```

### 100 Ω Load

```text
I = 5 / 100
I = 50 mA
```

Therefore, the load sweep evaluates the regulator from approximately:

```text
5 mA → 50 mA
```

---

# Linear Regulator Power Dissipation

One disadvantage of a linear regulator is that excess voltage is dissipated as heat.

Regulator power loss can be approximated using:

```text
Ploss = (Vin - Vout) × Iout
```

For example, if:

```text
Vin ≈ 14.4 V
Vout ≈ 5 V
Iout ≈ 50 mA
```

then:

```text
Ploss = (14.4 - 5) × 0.05
```

```text
Ploss ≈ 0.47 W
```

This illustrates an important tradeoff of linear regulators:

### Advantages

- Simple circuit
- Low component count
- Stable output
- Low output noise
- Easy implementation

### Disadvantages

- Lower efficiency
- Power dissipated as heat
- Efficiency decreases as the input-to-output voltage difference increases

---

# Engineering Observations

## Increasing Load Increases Ripple

Higher output current causes the filter capacitor to discharge more quickly between rectifier charging peaks.

Therefore:

```text
Higher Current → Greater Ripple
```

---

## Increasing Load Reduces Raw DC Voltage

The LTspice results demonstrate that the average raw DC voltage decreases as the load becomes heavier.

For example:

```text
1 kΩ load  → approximately 14.89 V
100 Ω load → approximately 14.40 V
```

---

## Voltage Regulation Remains Stable

Although the unregulated DC bus changes with load, the LM7805 maintains an output near:

```text
5 V
```

provided its input voltage remains sufficiently above the regulated output voltage.

---

## Rectification Creates a Higher DC Voltage Than 12 V

Although the source is specified as:

```text
12 V AC RMS
```

the capacitor charges close to the **peak** of the sinusoidal waveform rather than the RMS value.

Since:

```text
12 Vrms × √2 ≈ 16.97 Vpeak
```

the filtered DC voltage can be significantly greater than 12 V.

---

# Project Files

The repository is organized into three main directories:

```text
AC-to-DC-Regulated-Power-Supply/
│
├── AC_DC_5V_LTspice/
│   └── Main LTspice power supply design
│
├── Project1_LTspice_LoadSweep/
│   └── Stepped-load LTspice simulation
│
├── Project1_Results/
│   └── Simulation results and analysis
│
└── README.md
```

---

# Tools and Equipment

## Simulation

- LTspice

## Laboratory Equipment

The project is designed for validation using equipment including:

- Keysight oscilloscope
- Digital multimeter
- Keysight function generator
- Laboratory DC power supply
- BNC test leads
- Breadboard and jumper wiring

---

# Components

Major components used in the design include:

- Rectifier diodes
- Full-wave bridge configuration
- 1000 µF electrolytic capacitor
- LM7805 5 V linear regulator
- Output capacitors
- Resistive loads
- Breadboard
- Jumper wires

---

# Skills Demonstrated

This project demonstrates experience with:

- Power electronics
- AC-to-DC conversion
- Full-wave bridge rectifiers
- Diode circuits
- Capacitive filtering
- Linear voltage regulators
- LM7805 operation
- Ripple analysis
- Load regulation
- Ohm's Law
- Power calculations
- Efficiency analysis
- LTspice
- Parameter sweeps
- Circuit simulation
- Oscilloscope measurements
- Digital multimeter measurements
- Electrical troubleshooting
- Hardware validation

---

# Future Improvements

Potential extensions of the project include:

- Compare the LM7805 with a switching buck converter
- Measure efficiency over a larger load range
- Measure LM7805 temperature under heavier loads
- Compare multiple filter capacitor sizes
- Add overcurrent protection
- Add input/output protection
- Add a power indicator LED
- Design a PCB version of the circuit
- Evaluate regulator dropout behavior
- Compare simulated and measured ripple values
- Add thermal analysis

---

# Why This Project Matters

This project demonstrates the complete process of converting an AC source into a usable regulated DC supply.

Rather than treating rectification, filtering, and regulation as separate concepts, the project combines them into a complete power conversion system.

The project also demonstrates the relationship between:

```text
Load Current
     ↓
Capacitor Discharge
     ↓
Ripple Voltage
     ↓
Raw DC Voltage
     ↓
Regulator Performance
```

This provides practical experience with the fundamental principles used in power supplies and power electronics systems.

---

# Author

**Alan Davila**  
Computer Engineering  


### GitHub

[github.com/megablocks1377](https://github.com/megablocks1377)

### LinkedIn

[Alan Amadeus Davila](https://www.linkedin.com/in/alan-amadeus-davila-268542233/)

### Email

[alanamadeus1377@gmail.com](mailto:alanamadeus1377@gmail.com)

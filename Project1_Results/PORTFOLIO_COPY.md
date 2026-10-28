# AC-to-DC Regulated Power Supply — Portfolio Copy

**Power Electronics · Circuit Design · LTspice · Bench Validation**

Designed and tested a low-voltage AC-to-DC power supply using a four-diode full-wave bridge, 1,000 µF filter capacitor, and 7805 linear regulator. Converted a measured 11.9 V RMS AC input into a regulated 4.99 V DC output and verified operation across multiple resistive loads.

**Selected outcomes**
- Recorded a 15.2–15.3 V DC rectifier/filter voltage prior to linear regulation.
- Simulated 100 Ω, 220 Ω, 470 Ω, and 1 kΩ output loads in LTspice; output stayed between 4.9960 and 4.9996 V in the simplified 7805 model.
- Quantified increasing input ripple as load rises (91.6 to 385.4 mV peak-to-peak across the simulated test range).
- Measured approximately 29.6% **7805-stage DC efficiency** at the 100 Ω operating point, with about 0.592 W lost in the regulator stage.

**Design tradeoff:** Linear regulation is simple and delivers stable output voltage, but dropping about 15.3 V to 5 V at 50 mA converts substantial input power into heat. This motivates a future comparison with a buck converter.

**Validation note:** Bench ripple was reported as close to 27 mV pp but was not precisely captured; it is not directly matched to the simulated ripple. The LTspice LM7805_EDU is a simplified educational model.

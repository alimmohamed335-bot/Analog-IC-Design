# Self-Biased Sub-1V Bandgap Reference (BGR)

## Design Overview
A sub-1V Bandgap Reference designed and characterized in a 65 nm CMOS process running on a 1.2 V supply rail. The circuit produces a nominal temperature-compensated reference of $V_{OUT} \approx 800\text{ mV}$ while consuming $< 10\,\mu\text{A}$ across industrial temperatures ($-40^\circ\text{C}$ to $125^\circ\text{C}$) and full process corners (TT, SS, FF, SF, FS).

The design integrates a current-mode summing topology, a self-biased OTA, a leak-free dynamic startup circuit, and full verification with foundry PDK unsalicided P-poly resistors and substrate PNPs.

---

## Target Specifications vs. Simulated Results

| Metric | Target Specification | Hand Calculation | Spectre Simulation | Status |
| :--- | :---: | :---: | :---: | :---: |
| Technology Node | 65 nm CMOS | 65 nm | 65 nm | Compliant |
| Supply Voltage ($V_{DD}$) | 1.20 V | 1.20 V | 1.20 V | Pass |
| Reference Output ($V_{OUT}$) | 800.0 mV | 800.0 mV | 801.3 mV (Ideal) / 801.3 mV (OTA) | Pass |
| Total Bias Current ($I_{total}$) | $< 10.0\,\mu\text{A}$ | Core $\approx 3.0\,\mu\text{A}$ | $3.19\,\mu\text{A}$ (Core) / $4.15\,\mu\text{A}$ (w/ OTA) | Pass |
| Loop Phase Margin (STB) | $> 60.0^\circ$ | — | $86.71^\circ$ ($C_c = 5.0\text{ pF}$) | Pass |
| Nominal Temp Drift (TT) | Low | First-order cancel | $\Delta V_{OUT} \approx 1.052\text{ mV}$ ($-40^\circ\text{C}$ to $+130^\circ\text{C}$) | Pass |
| Corner Spread (PDK Passives) | Minimal | — | 800.1 mV to 801.6 mV ($\Delta \le 1.5\text{ mV}$) | Pass |
| Startup Settling Time | Fast / Clean | — | Settles to 801.37 mV at $t = 1.55\text{ ms}$ | Pass |
| Startup Leakage Current | Zero quiescent impact | 0 A | $< 26\text{ pA}$ in normal operation | Pass |

---

## Technical Highlights & Circuit Sizing

* **Current-Summing Architecture:** Sinks PTAT and CTAT currents into an output resistor $R_3$ to bypass the conventional $\approx 1.25\text{ V}$ bandgap constraint:
  $$V_{OUT} = R_3 \left( \frac{V_{BE}}{R_1} + \frac{\Delta V_{BE}}{R_2} \right)$$
  Resistor ratios were derived using $R_1/R_2 = 6.39$, with swept values establishing zero-TC compensation at $R_{PTAT} = 175\text{ k}\Omega$ and $R_{out} = 780\text{ k}\Omega$ ($\Delta V_{OUT} \approx 1.05\text{ mV}$).
* **Self-Biased OTA:** Replacing the behavioral amplifier with a self-biased OTA ($W/L = 5\,\mu\text{m}/2\,\mu\text{m}$ NMOS input pair) required retuning passives to $R_{PTAT} = 165\text{ k}\Omega$ and $R_{out} = 770\text{ k}\Omega$ to correct for finite gain and systemic offset. An output capacitor ($C_c = 5\text{ pF}$) sets loop stability at $86.71^\circ$.
* **Leak-Free Dynamic Startup:** A startup circuit dislodges the bandgap from the zero-current state during a 1 ms supply ramp, settling cleanly at $1.55\text{ ms}$. In steady-state operation, the startup devices shut down, drawing $< 26\text{ pA}$ leakage.
* **Foundry PDK Passive Verification:** Replaced ideal elements with actual foundry models: unsalicided P-poly resistors (`rppolywo_mx`, $W=400\text{ nm}, R \approx 1.278\text{ M}\Omega$) and substrate PNP transistors (`pnp5`). Full PVT corner simulations confirmed output variation within $800.1\text{ mV} - 801.6\text{ mV}$ ($\le 1.5\text{ mV}$ total window).

---

## Documentation
* [View Technical Report (PDF)](./Design_challenge%20(1).pdf)

# Two-Stage CMOS Miller Operational Transconductance Amplifier (OTA)

## Design Overview
A systematic design, sizing, and characterization of an unbuffered two-stage Miller-compensated OTA driving a heavy capacitive load ($C_L = 5\text{ pF}$) under a 1.8 V supply rail in a 0.18 µm CMOS process. Sized via the $g_m/I_D$ methodology using the Analog Designer's Toolbox (ADT), the amplifier satisfies strict static gain error ($\le 0.05\%$), CMRR ($\ge 74\text{ dB}$), slew rate ($\ge 5\text{ V}/\mu\text{s}$), and input common-mode range constraints.

A Johns & Martin dynamic lead compensation tracking network was implemented to replace the conventional fixed nulling resistor, locking the phase margin across varying temperature and process corners.

---

## Target Specifications vs. Simulated Results

| Metric | Target Specification | Hand Calculation | Spectre Simulation | Status |
| :--- | :---: | :---: | :---: | :---: |
| Technology Node | 0.18 µm CMOS | 0.18 µm | 0.18 µm | Compliant |
| Supply Voltage ($V_{DD}$) | 1.8 V | 1.8 V | 1.8 V | Pass |
| Total Core Current | $\le 60\,\mu\text{A}$ | $50.0\,\mu\text{A}$ | $49.60\,\mu\text{A}$ | Pass |
| Open-Loop DC Gain ($A_{ol}$) | $\ge 66.02\text{ dB}$ | 68.55 dB (2677 V/V) | 68.53 dB (2671 V/V) | Pass |
| Static Closed-Loop Error | $\le 0.05\%$ | 0.037% | 0.037% | Pass |
| Unity-Gain Frequency ($f_u$) | $\approx 5.0\text{ MHz}$ | 5.26 MHz | 4.87 MHz (5.67 MHz comp.) | Pass |
| Phase Margin (PM) | $\ge 70^\circ$ | $72.0^\circ$ | $71.3^\circ$ ($C_c = 1.7\text{ pF}$) | Pass |
| CMRR @ DC | $\ge 74\text{ dB}$ | 80.58 dB | 80.74 dB | Pass |
| Slew Rate (SR) | $\ge 5.0\text{ V}/\mu\text{s}$ | $5.67\text{ V}/\mu\text{s}$ | $5.02\text{ V}/\mu\text{s}$ | Pass |
| Small-Signal Rise Time ($t_{rise}$) | $< 70\text{ ns}$ | 61.64 ns (1st-order) | 43.87 ns (2nd-order) | Pass |
| CMIR Low / High | $\le 0.2\text{ V}$ / $\ge 0.8\text{ V}$ | 0.00 V / 0.80 V | 9.4 mV / 835 mV | Pass |
| Quiescent Output DC Voltage | $V_{DD}/2 = 0.9\text{ V}$ | 0.90 V | 900.4 mV | Pass |

---

## Technical Highlights & Circuit Sizing

* **Input Stage & CMIR:** PMOS differential input pair ($W=7.1\,\mu\text{m}, L=430\text{ nm}, g_m/I_D = 13\text{ V}^{-1}$) enables the common-mode input range to reach down to ground ($V_{ICM,min} \approx 9.4\text{ mV}$) while leveraging lower flicker noise.
* **Systematic DC Offset Cancellation:** To compensate for quiescent shifts introduced by the second-stage NMOS driver ($W=12.3\,\mu\text{m}, L=320\text{ nm}$), the first-stage NMOS load was resized to $W=5.4\,\mu\text{m}$, balancing the internal node at $731.8\text{ mV}$ and centering the open-loop DC output at $900.4\text{ mV}$ ($V_{DD}/2$).
* **Tracking Lead Compensation:** Replaced the ideal nulling resistor with a deep-triode NMOS transistor biased via a dedicated tracking stack. This fixes $R_z g_{m7} = 1$ based strictly on aspect ratios:
  $$\frac{R_z}{1/g_{m7}} = \frac{(W/L)_{M7}}{(W/L)_{triode}}\sqrt{\frac{(W/L)_{top}}{(W/L)_{bottom}}} = 1$$
* **Slew-Rate Retuning:** Decreasing $C_c$ from $2.0\text{ pF}$ to $1.7\text{ pF}$ boosted the slew rate to $5.02\text{ V}/\mu\text{s}$ while achieving an underdamped settling rise time of $43.87\text{ ns}$.

---

## Documentation
* [View Technical Report (PDF)](./Mini_project1.pdf)

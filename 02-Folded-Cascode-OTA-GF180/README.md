# Fully-Differential Folded Cascode OTA with Continuous-Time CMFB

## Design Overview
A fully-differential folded cascode Operational Transconductance Amplifier driving a $C_L = 500\text{ fF}$ load in the GF180MCU 2.5 V process node. Designed using the $g_m/I_D$ methodology, the circuit satisfies stringent high-speed settling targets ($\le 100\text{ ns}$ to 1%), open-loop DC gain ($\ge 60\text{ dB}$), and full-scale differential output swing ($1.2\text{ V}_{p-p}$).

A continuous-time CMFB circuit featuring PMOS source-follower sensing and an auxiliary dummy tracking branch stabilizes the output common-mode voltage at an optimized $925\text{ mV}$, maximizing symmetrical dynamic range.

---

## Target Specifications vs. Simulated Results

| Metric | Target Specification | Hand Calculation | Spectre Simulation | Status |
| :--- | :---: | :---: | :---: | :---: |
| Process Node | GF180MCU (2.5 V) | 2.5 V | 2.5 V | Compliant |
| Closed-Loop Gain ($A_{cl}$) | 2.0 V/V (6.0 dB) | 2.0 V/V | 1.998 V/V (AC) / 1.997 V/V (Tran) | Pass |
| Open-Loop DC Gain ($A_{ol}$) | $\ge 60.0\text{ dB}$ | 69.79 dB (3088 V/V) | 69.27 dB (2906 V/V loaded) | Pass |
| Open-Loop GBW ($C_L = 500\text{ fF}$) | — | 58.00 MHz | 53.01 MHz | Pass |
| Differential Phase Margin | $\ge 70.0^\circ$ | $\approx 85^\circ - 88^\circ$ | $89.15^\circ$ (STB) | Pass |
| Common-Mode Phase Margin | $\ge 70.0^\circ$ | — | $70.72^\circ$ (STB) | Pass |
| 1% Settling Time ($t_s$) | $\le 100\text{ ns}$ | 21.7 ns ($\tau$) | 98.09 ns (ADE Calculator) | Pass |
| Differential Output Swing | $1.2\text{ V}_{p-p}$ | $1.2\text{ V}_{p-p}$ | $1.198\text{ V}_{p-p}$ (unclipped) | Pass |
| Output CM Voltage ($V_{OCM}$) | Nominal $V_{DD}/2$ | 925 mV (optimized) | 926.2 mV (open) / 927.5 mV (closed) | Pass |
| Core / CMFB Current | — | $50.0\,\mu\text{A}$ / $23.0\,\mu\text{A}$ | $59.4\,\mu\text{A}$ / $29.1\,\mu\text{A}$ ($I_{tot} = 88.5\,\mu\text{A}$) | Pass |
| Total Power Dissipation | — | — | $221.3\,\mu\text{W}$ at 2.5 V | Pass |
| Active Transistor Area | — | — | $318.9\,\mu\text{m}^2$ (OTA: 118.7, CMFB: 200.2) | Pass |

---

## Technical Highlights & Circuit Sizing

* **Cascode Output Impedance Enhancement:** Increasing the channel length of all cascode devices (M1, M7, M9, M11) from $350\text{ nm}$ to $400\text{ nm}$ raised the output impedance to $R_{out} \approx 16.95\text{ M}\Omega$, boosting open-loop DC gain to $69.84\text{ dB}$ ($69.27\text{ dB}$ loaded).
* **High-Speed Settling:** Sizing the PMOS input pair into weak-to-moderate inversion ($g_m/I_D = 18\text{ V}^{-1}, g_m = 180\,\mu\text{S}, W=35.34\,\mu\text{m}, L=320\text{ nm}$) maximized transconductance efficiency and closed-loop bandwidth, achieving a 1% settling time of $98.09\text{ ns}$ for a 100 mV input step.
* **Symmetrical Swing CMFB:** Midpoint voltage boundaries between top PMOS sources ($1.45\text{ V}$) and bottom NMOS sources ($0.40\text{ V}$) established an optimal reference point:
  $$V_{REF(opt)} = \frac{1.45\text{ V} + 0.40\text{ V}}{2} = 925\text{ mV}$$
  A dummy source-follower branch matches the $V_{GS}$ drop of the resistive sensing buffers, eliminating systematic common-mode offset at the error amplifier.
* **Loop Stability:** Stability analysis verified $89.15^\circ$ differential PM and $70.72^\circ$ common-mode PM, demonstrating robust damping during common-mode transients with zero cross-mode interference.

---

## Documentation
* [View Technical Report (PDF)](./Mini_project2.pdf)

# Analog IC Design Portfolio

This repository contains transistor-level analog integrated circuit designs executed using the $g_m/I_D$ methodology and verified using Cadence Virtuoso and Spectre.

## Projects Overview

| # | Project Name | Architecture | Technology Node | Supply Voltage | Key Highlights |
| :---: | :--- | :--- | :---: | :---: | :--- |
| **01** | [Two-Stage Miller OTA](./01-Two-Stage-Miller-OTA/) | PMOS Input, Unbuffered Two-Stage Miller | 0.18 µm CMOS | 1.8 V | Johns & Martin lead tracking compensation, $A_{ol} = 68.53\text{ dB}$, $PM = 71.3^\circ$ |
| **02** | [Folded Cascode OTA](./02-Folded-Cascode-OTA-GF180/) | Fully-Differential Folded Cascode | GF180MCU | 2.5 V | Continuous-Time CMFB, $t_s = 98.09\text{ ns}$ (1%), $1.2\text{ V}_{p-p}$ swing |
| **03** | [Sub-1V Bandgap Reference](./03-Sub1V-Bandgap-Reference-TSMC65/) | Self-Biased Current-Summing BGR | 65 nm CMOS | 1.2 V | $V_{REF} = 801.3\text{ mV}$, $I_{tot} = 4.15\,\mu\text{A}$, PDK poly resistor verification |

---

## Directory Structure
- **`01-Two-Stage-Miller-OTA/`**: Design, small-signal characterization, Johns & Martin tracking lead compensation, and transient step analysis for an unbuffered two-stage Miller OTA.
- **`02-Folded-Cascode-OTA-GF180/`**: Sizing, swing optimization, dummy level-shifting CMFB design, and full-scale settling transient verification in GF180MCU.
- **`03-Sub1V-Bandgap-Reference-TSMC65/`**: Sub-1V current-mode BGR core design, startup circuit, integrated self-biased OTA, and Monte Carlo/PVT corner sweeps with foundry passives.

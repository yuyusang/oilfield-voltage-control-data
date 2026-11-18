# Two-Timescale Voltage Control for Oilfield Distribution Networks

Supplementary data and reinforcement learning settings for the DDQN and GCN-TC-SAC voltage control study.

## Files

[Download data.zip](data.zip) and extract it to access the following files.

| File | Content |
| --- | --- |
| `pv_profiles_14_days.csv` | Active power profiles for PV1, PV2 and PV3 and their sum, for all 14 test days. |
| `residential_load_example.csv` | One day of aggregate residential (other) active load used by the case-study model, for `EMSX_2014-08-13`. |
| `rl_parameters.json` | Training schedule, learning and exploration settings, and network sizes for the reference DDQN and GCN-TC-SAC configuration. |

Each day contains 96 consecutive 15-minute intervals. `step` runs from 0 to 95, and `interval_start_h` runs from 0.00 to 23.75 h. All power values are in kW. The PV columns represent available active power inputs in the simulated network. The PV1, PV2 and PV3 ratings are 550, 600 and 650 kW, respectively.

## Training settings at a glance

| Setting | Value |
| --- | --- |
| Fast and slow decision intervals | 15 min and 60 min |
| Training episodes | 3,000 (800 fast-controller pretraining and 2,200 joint training) |
| Fast and slow discount factors | 0.995 and 0.980149500625 |
| Fast-controller learning rate | 0.00005 |
| Entropy-temperature learning rate | 0.00005 |
| DDQN learning rate | 0.00005 |
| Fast and slow batch sizes | 512 and 128 |
| Training seeds used in the evaluation | 42, 123 and 2026 |

During pretraining, OLTC actions are sampled uniformly from the admissible set. The fast and slow controllers are subsequently trained jointly.

## Profile provenance

The CSVs contain the profiles as used in the oilfield simulation. They are derived from [the EMSx dataset](https://doi.org/10.5281/zenodo.5510400) by Adrien Le Franc and Marc Ittel, which includes historical PV and load series from Schneider Electric. In the simulation, the PV profile is scaled to the three PV ratings, and the historical industrial demand profile is scaled and allocated to the modeled non-production loads. The aggregate `residential_load_kw` series is therefore a **proxy used in the case study**, rather than a measurement from residential meters.

The EMSx-derived CSVs are provided under the [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/). When using these profiles, please cite [the EMSx dataset](https://doi.org/10.5281/zenodo.5510400) and its [companion article](https://doi.org/10.1007/s12667-020-00417-5).

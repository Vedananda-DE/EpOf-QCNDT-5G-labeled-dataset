# Labeled 5G handover dataset

Labeled traces for handover prediction on the public 5G production dataset (Raca et al., MMSys 2020). The original measurement files are not in this repository.

Each kept sample has one handover decision:

| Label | Decision | Rule |
|---|---|---|
| 0 | Maintain current link | RSRP is at least -100 dBm, SNR is at least -5 dB, and delta RSRP is greater than -2 dB |
| 1 | Handover to a macro cell | The maintain test fails and speed is at least 30 km/h |
| 2 | Handover to a small cell | The maintain test fails and speed is below 30 km/h |

`delta_RSRP` is the change in logged serving RSRP from the previous sample in the same session. A new decision is held for 2 seconds. Rows with an empty RSRP marker or no usable SNR were removed. 172,001 of 188,711 samples remain.

Sessions are split 70/15/15 inside each mobility and application group. The `split` column is `train`, `val`, or `test`.

## Files

- `labeled_traces.csv` — labeled samples, including RSRP, delta RSRP, SNR, Speed, and `HO_label`
- `labeled_traces.mat` — the same labels and the four selected features for MATLAB
- `session_split.csv` — session-level split
- `cell_layout.csv` — synthetic macro, BS, and femto sites for later network simulation
- `feature_scaling.csv` — training min/max for RSRP, delta RSRP, SNR, and Speed
- `dataset_summary.csv` — class counts by mobility and application
- `feature_ranking.csv` — depth-5 Gini ranking on the training sessions
- `dataset_analysis.txt` — labeling notes and counts

The four model features are RSRP, delta RSRP, SNR, and Speed.

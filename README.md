# make inverse operator

Brainlife.io app to compute the MNE inverse operator for MEG/EEG source reconstruction.

Combines a forward solution and a noise covariance matrix to produce an inverse operator (`inv.fif`), consumed by `app-source-estimate-v2`.

## Inputs

| Input | Description |
|-------|-------------|
| `forward` | Forward solution file (`fwd.fif`) from app-forward-v2 |
| `noise_cov` | Noise covariance file (`noise-cov.fif`) from app-noise-covariance-v2 |
| `epo` | Epochs FIF file (for sensor info) |
| `evoked` | Evoked FIF file (alternative to epochs for sensor info) |

## Outputs

| Output | Description |
|--------|-------------|
| `out_dir/inv.fif` | Inverse operator |
| `out_report/report.html` | HTML report |

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `loose` | `0.2` | Loose orientation constraint (0 = fixed, 1 = free, `auto` = automatic) |
| `depth` | `0.8` | Depth weighting (0–1, or `None` to disable) |
| `rank` | `None` | Rank of the noise covariance (`None` = auto, `info`, `full`) |

## Pipeline position


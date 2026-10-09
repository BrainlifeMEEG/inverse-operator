# Make Inverse Operator

[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.905-blue.svg)](https://doi.org/10.25663/brainlife.app.905)

## Description

Computes the MNE inverse operator for MEG/EEG source reconstruction using
`mne.minimum_norm.make_inverse_operator`. It combines a pre-computed forward solution and a noise
covariance matrix; sensor info (channel layout, projectors) needed to build the operator is taken
from an epochs or evoked file.

The app generates:
- The inverse operator (`inv.fif`), consumed by `app-source-estimate-v2`
- An HTML report
- A `product.json` with status/diagnostic messages

## Inputs

- **`forward`** (`neuro/meeg/mne/forward-inverse`): Forward solution file (`fwd.fif`) from app-forward-v2 (required)
- **`noise_cov`** (`neuro/meeg/mne/covariance`): Noise covariance file (`cov.fif`/`noise-cov.fif`) from app-noise-covariance-v2 (also accepted under the legacy key `cov`) (required)
- **`epo`** (`neuro/meeg/mne/epochs`): Epoched data, used only for sensor info (channel layout, projectors) (one of `epo`/`evoked` required)
- **`evoked`** (`neuro/meeg/mne/evoked`): Evoked data, used only for sensor info, as an alternative to `epo` (one of `epo`/`evoked` required)

## Outputs

- **`out_dir/inv.fif`** (`neuro/meeg/mne/forward-inverse`): the inverse operator
- **`out_report/report.html`**: HTML report
- **`product.json`**: Brainlife.io metadata — status/diagnostic messages (source/covariance/sensor info summaries, or a fatal error message)

## Configuration Parameters

| key | type | default | description |
|---|---|---|---|
| `loose` | string | `auto` | Loose orientation constraint passed to `mne.minimum_norm.make_inverse_operator` (`0` = fixed orientation, `1` = free orientation, `auto` = automatic, based on the source space type). |
| `depth` | string | `0.8` | Depth weighting exponent (0–1) passed to `make_inverse_operator`; `None`/`none` disables depth weighting. |
| `rank` | string | `None` | Rank of the noise covariance: `None`/empty = auto-detect, `info` = from measurement info, `full` = assume full rank. |

## Usage

### Running on Brainlife.io

1. Select the forward solution (`forward`), noise covariance (`noise_cov`), and epochs or evoked data (`epo`/`evoked`) as inputs.
2. Set `loose`, `depth`, and `rank` if the defaults are not appropriate.
3. Submit the process.
4. Review `out_dir/inv.fif` and the HTML report in the output viewer.

### Local Testing

```bash
# Edit config.json to point "forward", "noise_cov" and "epo" (or "evoked") at real files, then:
python main.py
```

## Pipeline Position

This app is step 3 of the source reconstruction pipeline:

```
[Forward Model] --> [Noise Covariance] --> [Inverse Operator] --> [Source Estimate]
```

## Authors

- [Guiomar Niso](https://github.com/guiomar)
- [Antonio Caulín](https://github.com/AntonioCauAt)
- [Maximilien Chaumon](https://github.com/dnacombo)
- [obVdo](https://github.com/obVdo)

## Citations

1. Hayashi, S., Caron, B.A., Heinsfeld, A.S. et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. Nat Methods 21, 809–813 (2024). https://doi.org/10.1038/s41592-024-02237-2
2. Gramfort, A., Luessi, M., Larson, E., et al. MEG and EEG data analysis with MNE-Python. Front. Neurosci. 7, 267 (2013). https://doi.org/10.3389/fnins.2013.00267

## Funding Acknowledgement

brainlife.io is publicly funded and for the sustainability of the project it is helpful to acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your code and publications.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://grantome.com/grant/NIH/R01-EB030896-01)

## License

Copyright (c) 2026 MEEG Brainlife team. Licensed under AGPL-3.0, see [license.txt](license.txt).

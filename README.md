<h1 align="center">Make Inverse Operator</h1>

<p align="center">
  Computes an MNE minimum-norm inverse operator for MEG/EEG source reconstruction from a forward solution, a noise covariance and sensor info from epochs, using MNE-Python.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.905"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.905-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Computes an MNE minimum-norm inverse operator for MEG/EEG source reconstruction from a forward solution, a noise covariance and sensor info from epochs, using MNE-Python.**

Combines a precomputed forward solution and a noise covariance with the channel layout and projectors of an epochs (or evoked) file in mne.minimum_norm.make_inverse_operator, and saves inv.fif with an HTML report. Use it between the forward/covariance Apps and source estimation. loose, depth and rank are passed to make_inverse_operator.

| | |
|---|---|
| **Inputs** | `neuro/meeg/mne/forward-inverse` · `neuro/meeg/mne/covariance` · `neuro/meeg/mne/epochs` |
| **Outputs** | `neuro/meeg/mne/forward-inverse` |
| **Container** | `brainlifemeeg/mne:1.12.1` |
| **Resources** | 1 CPUs · 20 GB memory · 1 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.905](https://doi.org/10.25663/brainlife.app.905) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `forward` | `neuro/meeg/mne/forward-inverse` | yes | Forward solution (fwd.fif). |
| `noise_cov` | `neuro/meeg/mne/covariance` | yes | Noise covariance matrix (cov.fif). |
| `epo` | `neuro/meeg/mne/epochs` | yes | Epoched data used only for sensor information (channels, projectors). |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `out_dir` | `neuro/meeg/mne/forward-inverse` | Inverse operator (inv.fif). |

<details>
<summary><b>Parameters</b> (3)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `loose` | string | `auto` | Loose orientation constraint passed to make_inverse_operator ('auto' or a value from 0 to 1). |
| `depth` | string | `0.8` | Depth weighting exponent passed to make_inverse_operator. |
| `rank` | string | `None` | Data rank passed to make_inverse_operator (None estimates it). |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.905](https://doi.org/10.25663/brainlife.app.905), choose `neuro/meeg/mne/forward-inverse`, `neuro/meeg/mne/covariance`, `neuro/meeg/mne/epochs` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/meeg/mne/forward-inverse`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlifemeeg/mne:1.12.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "forward": "/path/to/forward/forward",
       "inverse": "/path/to/forward/inverse",
       "cov": "/path/to/noise_cov/cov",
       "epo": "/path/to/epo/epo",
       "loose": "auto",
       "depth": "0.8",
       "rank": "None"
   }
   ```

3. Run `./main`.

## Configuration Parameters

| key | type | default | description |
|---|---|---|---|
| `loose` | string | `auto` | Loose orientation constraint passed to `mne.minimum_norm.make_inverse_operator` (`0` = fixed orientation, `1` = free orientation, `auto` = automatic, based on the source space type). |
| `depth` | string | `0.8` | Depth weighting exponent (0–1) passed to `make_inverse_operator`; `None`/`none` disables depth weighting. |
| `rank` | string | `None` | Rank of the noise covariance: `None`/empty = auto-detect, `info` = from measurement info, `full` = assume full rank. |

## Local Testing

```bash
# Edit config.json to point "forward", "noise_cov" and "epo" (or "evoked") at real files, then:
python main.py
```

## Pipeline Position

This app is step 3 of the source reconstruction pipeline:

```
[Forward Model] --> [Noise Covariance] --> [Inverse Operator] --> [Source Estimate]
```

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Make Inverse Operator. brainlife.io App. [doi:10.25663/brainlife.app.905](https://doi.org/10.25663/brainlife.app.905)
- Gramfort A, et al. MEG and EEG data analysis with MNE-Python. Front Neurosci 7(267):1-13 (2013). [doi:10.3389/fnins.2013.00267](https://doi.org/10.3389/fnins.2013.00267)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- [Guiomar Niso](https://github.com/guiomar)
- [Antonio Caulín](https://github.com/AntonioCauAt)
- [Maximilien Chaumon](https://github.com/dnacombo)
- [obVdo](https://github.com/obVdo)

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).

<h1 align="center">app-tractoflow</h1>

<p align="center">
  Runs the TractoFlow Nextflow pipeline (scilus 1.6.0 container) on a DWI and T1w image to produce preprocessed DWI, a resampled T1 and a particle-filtering (PFT) tractogram.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.868"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.868-blue.svg" alt="Run on brainlife.io"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Runs the TractoFlow Nextflow pipeline (scilus 1.6.0 container) on a DWI and T1w image to produce preprocessed DWI, a resampled T1 and a particle-filtering (PFT) tractogram.**

Arranges the inputs as a single-subject TractoFlow input folder, installs Miniconda and Nextflow 21.10.6 at run time, clones the scilus/tractoflow repository and runs it with the scilus 1.6.0 Singularity image. TractoFlow performs DWI preprocessing (denoising, eddy/topup, registration, resampling), tensor and fODF fitting and PFT tracking. It needs internet access on the compute node and about four hours on 16 cores.

| | |
|---|---|
| **Inputs** | `neuro/dwi` · `neuro/anat/t1w` |
| **Outputs** | `neuro/dwi` · `neuro/anat/t1w` · `neuro/track/trk` |
| **Container** | `scilus/scilus:1.6.0` |
| **Resources** | 16 CPUs · 4 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.868](https://doi.org/10.25663/brainlife.app.868) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `dwi` | `neuro/dwi` | yes | Raw DWI (NIfTI) with bvals and bvecs. |
| `t1w` | `neuro/anat/t1w` (acpc_aligned) | yes | ACPC-aligned T1-weighted image of the same subject. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `Resample_DWI` | `neuro/dwi` | Preprocessed, resampled DWI from TractoFlow with the bvals/bvecs of the fODF shell. |
| `Resample_T1` | `neuro/anat/t1w` | Preprocessed, resampled T1 from TractoFlow. |
| `PFT_Tracking` | `neuro/track/trk` | Probabilistic particle-filtering tractogram seeded in white matter (.trk). |

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.868](https://doi.org/10.25663/brainlife.app.868), choose `neuro/dwi`, `neuro/anat/t1w` from your project and press **Execute**. The results are saved to your project as `neuro/dwi`, `neuro/anat/t1w`, `neuro/track/trk`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `scilus/scilus:1.6.0`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "dwi": "/path/to/dwi/dwi",
       "bvecs": "/path/to/dwi/bvecs",
       "bvals": "/path/to/dwi/bvals",
       "t1": "/path/to/t1w/t1"
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- app-tractoflow. brainlife.io App. [doi:10.25663/brainlife.app.868](https://doi.org/10.25663/brainlife.app.868)
- Theaud, G., Houde, J. C., Boré, A., Rheault, F., Morency, F., & Descoteaux, M. (2020). TractoFlow: A robust, efficient and reproducible diffusion MRI pipeline leveraging Nextflow & Singularity. Neuroimage, 218, 116889.
- Hayashi, S., Caron, B. A., Heinsfeld, A. S., ... & Pestilli, F. (2024). brainlife. io: a decentralized and open-source cloud platform to support neuroscience research. Nature methods, 21(5), 809-813. ---
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

**Sydney Fulton**
(email: [](mailto:)

**Gabriele Amorosino**
(email: [](mailto:)

---

# FoldColabFlow Installation and Dependency Inventory

This document describes the software dependencies and installation procedures used by **FoldColabFlow**, a Google Colab-based workflow for protein sequence analysis, physicochemical profiling, structure prediction, structural assessment, functional annotation, and structural comparison.

The installation inventory was extracted from all 19 cells (numbered 0–18) of the FoldColabFlow notebook.

The notebook already contains its own installation procedures. Therefore, users running FoldColabFlow in Google Colab generally do not need to install the dependencies separately.

**Important:** This document records the installation commands implemented in the notebook. It does not independently verify that all dependencies can be installed successfully in every runtime environment.

## 1. Recommended Execution Environment

FoldColabFlow is primarily designed for Google Colab.

Recommended environment:

- Platform: Google Colab
- Runtime: Python 3
- Hardware accelerator: GPU recommended for protein structure prediction
- Internet connection: Required for downloading software dependencies, model parameters, and sequence databases
- Google Drive: Optional for persistent storage of output files

### Running FoldColabFlow

1. Open `FoldColabFlow.ipynb` in Google Colab.
2. Select a suitable runtime under Runtime → Change runtime type.
3. Enable GPU acceleration when performing structure prediction.
4. Execute the notebook cells in their intended order.
5. Follow the interactive instructions for sequence input and analysis.

The notebook installs required dependencies through its own installation cells.

**Users should not additionally execute `pip install -r requirements.txt` before running the notebook unless they are deliberately configuring a separate environment.** Performing both installations may be redundant and could cause version conflicts.

## 2. Python Dependencies

The following Python packages are explicitly installed by the notebook.

| Package | Installation method | Purpose |
|---|---|---|
| biopython | pip | Sequence alignment, physicochemical analysis, PDB parsing |
| pandas | pip | Data processing and tabular outputs |
| matplotlib | pip, conditional | Plotting and visualization |
| plotly | pip, conditional | Interactive visualizations |
| kaleido | pip, conditional | Plotly image export |
| colabfold | pip from GitHub | Protein structure prediction |
| dm-haiku | pip, conditional | JAX-related dependency |
| jax / jaxlib | pip, conditional | Computational backend |
| ramachandraw | pip | Ramachandran plot generation |
| protein-sequence-annotation | pip | PSALM functional domain annotation |

### Explicitly Specified Versions

The notebook specifies the following versions in its installation commands:

- `kaleido==0.2.1`
- `protein-sequence-annotation==2.1.12`
- `dm-haiku==0.0.10`, in a conditional installation path
- `jax[cuda12_pip]==0.3.25`, in a conditional installation path

Other Python packages are installed without fixed version numbers in the notebook.

## 3. Installation Commands Implemented in the Notebook

### 3.1. Sequence Alignment

Cell 3 installs Biopython and pandas:

```bash
python -m pip install -q biopython pandas
```

MAFFT is installed if multiple sequence alignment is requested and the executable is not already available:

```bash
apt-get -qq update
apt-get -qq install -y mafft
```

MAFFT is used for multiple sequence alignment.

### 3.2. Physicochemical Analysis

Cell 4 installs the core analysis packages:

```bash
python -m pip install -q biopython pandas
```

When the relevant plotting options are enabled, additional packages are installed:

```bash
python -m pip install -q matplotlib plotly kaleido==0.2.1
```

These libraries support physicochemical descriptor calculations, visualizations, and exported plots.

### 3.3. ColabFold Installation

Cell 7 installs ColabFold when the notebook's installation-ready flag is absent:

```bash
pip install -q --no-warn-conflicts 'colabfold[alphafold-minus-jax] @ git+https://github.com/sokrypton/ColabFold'
```

Cell 9 also contains the following installation command:

```bash
pip install -q --no-cache-dir "colabfold[alphafold-minus-jax] @ git+https://github.com/sokrypton/ColabFold"
```

Cell 11 contains a fallback installation command that is executed if the initial ColabFold import fails:

```bash
pip install -q --no-cache-dir --force-reinstall 'colabfold[alphafold-minus-jax] @ git+https://github.com/sokrypton/ColabFold'
```

These commands install ColabFold from its GitHub repository.

Because the installation URL does not specify a fixed commit, the precise installed source revision may depend on when the installation is performed.

The installation commands are documented here without modifying the original notebook.

### 3.4. Conditional JAX Installation

When the notebook detects the relevant TPU-specific environment condition during its initial ColabFold setup, it includes:

```bash
pip uninstall -y jax jaxlib
```

Followed by:

```bash
pip install --no-warn-conflicts --upgrade dm-haiku==0.0.10 'jax[cuda12_pip]'==0.3.25 -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
```

This is a conditional path reproduced from the existing notebook, not a universally recommended installation command.

### 3.5. Conditional Miniforge and Conda Dependencies

When template-based prediction or Amber refinement is enabled, the notebook can download and install Miniforge using the `Miniforge3-Linux-x86_64.sh` installer from the latest Miniforge release.

Depending on enabled options, the following external packages may be installed.

**When both template support and Amber refinement are enabled:**

```bash
mamba install -y -c conda-forge -c bioconda kalign2=2.04 hhsuite=3.3.0 openmm=8.2.0 python="${PYTHON_VERSION}" pdbfixer
```

**When template support alone is enabled:**

```bash
mamba install -y -c conda-forge -c bioconda kalign2=2.04 hhsuite=3.3.0 python="${PYTHON_VERSION}"
```

**When Amber refinement alone is enabled:**

```bash
mamba install -y -c conda-forge openmm=8.2.0 python="${PYTHON_VERSION}" pdbfixer
```

These packages are not necessarily installed during every execution. Their installation depends on the selected ColabFold options and existing environment state.

### 3.6. AlphaFold Model Parameters

The structure-prediction module invokes:

```python
download_alphafold_params(model_type, Path("."))
```

This retrieves AlphaFold model parameters required for the selected prediction configuration.

These model parameters are separate from Python package dependencies.

### 3.7. Ramachandran Analysis

Cell 15 installs:

```bash
pip -q install ramachandraw biopython
```

The `ramachandraw` package is used to generate Ramachandran plots from predicted protein structures.

### 3.8. PSALM Functional Annotation

Cell 17 installs:

```bash
pip -q install biopython pandas protein-sequence-annotation==2.1.12
```

The `protein-sequence-annotation` package provides the PSALM functionality used for sequence-based protein domain annotation.

### 3.9. TM-align Installation

Cell 18 downloads the TM-align C++ source code:

```bash
wget -q https://zhanggroup.org/TM-align/TMalign.cpp
```

It then compiles the source into an executable:

```bash
g++ -O3 -ffast-math -o TMalign TMalign.cpp
```

The resulting `TMalign` executable is used for structural comparisons and calculation of TM-score and RMSD.

A working C++ compiler is therefore required for this installation procedure.

## 4. Repeated Installation Commands

Some dependencies are installed in more than one notebook cell.

For example:

- Biopython is installed in multiple analysis modules.
- pandas is installed in multiple modules.
- ColabFold installation occurs in more than one cell, including a conditional fallback.

These commands remain part of the original implementation.

Repeated installation can be redundant and may affect dependency resolution. However, this document describes the existing implementation rather than proposing changes to the working notebook.

## 5. requirements.txt

A separate `requirements.txt` file may be provided as a reference inventory of the direct Python dependencies.

For a manually configured Python environment, it can be installed using:

```bash
python -m pip install -r requirements.txt
```

However, the requirements file alone is not sufficient to configure every external dependency used by FoldColabFlow.

MAFFT, TM-align, conditional Conda packages, ColabFold model parameters, and GPU-related computational components may require additional installation or configuration.

For the standard Google Colab workflow, users should follow the notebook's built-in installation procedures rather than installing the same dependencies twice.

## 6. Software Version and Environment Reproducibility

Some dependency versions are explicitly specified in the notebook, while others are not.

For scientific reproducibility, a successful execution should record:

- Python version
- Operating system and Google Colab runtime environment
- GPU model and CUDA-related environment information
- Installed Python package versions
- ColabFold version and installed Git revision
- MAFFT version
- TM-align executable version or source revision
- AlphaFold model configuration and parameters
- Analysis inputs and relevant execution settings

The exact resolved software environment cannot be fully determined from notebook source code alone.

Accordingly, this installation document is a record of the existing installation procedures, not a complete lockfile or proof of successful reproduction in a fresh environment.

## 7. Summary

FoldColabFlow integrates the installation of its principal dependencies within the Google Colab notebook.

The workflow uses Python libraries, external alignment and structure-comparison tools, ColabFold prediction components, and optional Conda-based tools for particular prediction settings.

The original notebook installation procedures are retained, while this document provides a centralized description of software requirements for users and researchers seeking to inspect or reproduce the computational workflow.
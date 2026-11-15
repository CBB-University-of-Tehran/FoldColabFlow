# Third-party software, models, and resources

This document identifies third-party components invoked, installed, downloaded, or used by **FoldColabFlow**, based on inspection of `FoldColabFlow(4).ipynb` supplied for the licensing review (15 November 2026). It supplements, but does not replace, the repository's `LICENSE` and `NOTICE` files.

**Scope.** FoldColabFlow's original contributions are released under Apache License 2.0 as described in `LICENSE`. Third-party components retain their own licenses and notices. Listing a package here does **not** mean its source code, pretrained models, datasets, or binaries are included in this repository or relicensed under Apache-2.0. The notebook installs or downloads some components at runtime; upstream terms may therefore apply when they are obtained or redistributed. Scientific citation and software-license obligations are distinct.

## A. Directly used software and major model resources

| Component | How it is used | Upstream license / relevant terms | Official source or license |
|---|---|---|---|
| **ColabFold** | Installed from its GitHub repository and used for AlphaFold-based structure prediction and related setup. Some notebook setup logic may be adapted from ColabFold; see `NOTICE`. | **MIT** for ColabFold code; pretrained weights have separate terms. Copyright notice: **Copyright (c) 2021 Sergey Ovchinnikov**. | [ColabFold source](https://github.com/sokrypton/ColabFold); [MIT license](https://github.com/sokrypton/ColabFold/blob/main/LICENSE) |
| **AlphaFold 2** | Structure-prediction implementation accessed through the ColabFold environment. | **Apache-2.0** for AlphaFold code. **CC BY 4.0** for AlphaFold model parameters; these are distinct from the code license. | [Official AlphaFold repository and model licensing](https://github.com/google-deepmind/alphafold#model-parameters) |
| **Biopython** | Sequence alignment and physicochemical analysis; PDB parsing and structural data processing. | **Biopython License Agreement**; parts may have additional or dual-license notices. | [Biopython license](https://github.com/biopython/biopython/blob/master/LICENSE.rst) |
| **MAFFT** | Multiple sequence alignment, installed via the system package manager when needed. | **BSD-style** license for core code; optional extensions may have additional terms. | [MAFFT license](https://github.com/GSLBiotech/mafft/blob/master/license); [extensions license](https://github.com/GSLBiotech/mafft/blob/master/license.extensions) |
| **TM-align** | `TMalign.cpp` is downloaded from the Zhang Group website and compiled locally at notebook runtime. | **Project-specific source notice / conditions: verify against the header of the exact downloaded `TMalign.cpp` and accompanying README.** Do not assume MIT/BSD/Apache from the download availability alone. Retain all upstream notices and attribution. | [Official TM-align download page](https://zhanggroup.org/TM-align/); [downloaded source](https://zhanggroup.org/TM-align/TMalign.cpp) |
| **PSALM** (`protein-sequence-annotation`, **2.1.12**) | Protein-domain annotation via the `psalm-scan` command. | **CC BY 4.0**, as declared in the PyPI metadata for version 2.1.12. Model weights and underlying resources may have separate terms; check their original distribution pages. | [Exact PyPI release and declared license](https://pypi.org/project/protein-sequence-annotation/2.1.12/); [PSALM project](https://github.com/Protein-Sequence-Annotation/PSALM) |
| **ramachandraw** | Ramachandran plot generation. | **MIT**, subject to the installed distribution's license notice. | [Project/PyPI](https://pypi.org/project/ramachandraw/); [source](https://github.com/alexarnimueller/ramachandraw) |
| **py3Dmol / 3Dmol.js** | Interactive protein-structure visualization in the notebook. | **BSD-style**, with separate third-party notices for embedded JavaScript dependencies. | [py3Dmol distribution](https://pypi.org/project/py3Dmol/); [3Dmol.js license/source](https://github.com/3dmol/3Dmol.js); [historical py3dmol notices](https://github.com/avirshup/py3dmol/blob/master/3dmol.js.licenses) |
| **pandas** | Tabular processing and results export. | **BSD-3-Clause**. | [License](https://github.com/pandas-dev/pandas/blob/main/LICENSE) |
| **matplotlib** | Scientific plotting. | **Matplotlib License** (PSF-derived, BSD-compatible). | [Official license](https://matplotlib.org/stable/project/license.html) |
| **Plotly.py** | Interactive graphs and visualizations. | **MIT** for Plotly.py; any separately loaded assets can have their own terms. | [Plotly.py license](https://github.com/plotly/plotly.py/blob/main/LICENSE.txt) |
| **IPython** | Rich notebook outputs and interactive displays. | **BSD-3-Clause**. | [IPython license](https://github.com/ipython/ipython/blob/main/LICENSE) |

## B. Supporting services and resources

| Component | Relationship to FoldColabFlow | License / notes | Source |
|---|---|---|---|
| **MMseqs2 and ColabFold MSA services** | Used indirectly in the ColabFold sequence-search / MSA workflow. | **MIT** for the MMseqs2 software. Remote services and any databases accessed through them have their own policies and attribution requirements. | [MMseqs2 repository](https://github.com/soedinglab/MMseqs2); [ColabFold documentation](https://github.com/sokrypton/ColabFold) |
| **AlphaFold pretrained model parameters** | Downloaded/used by ColabFold during prediction. | **CC BY 4.0**; not covered by the Apache-2.0 license of FoldColabFlow or AlphaFold code. | [AlphaFold model parameter terms](https://github.com/google-deepmind/alphafold#model-parameters) |
| **PSALM model and associated annotation resources** | Downloaded or accessed as required by PSALM. | **Check the precise model repository, model card, version, and applicable Pfam/database terms before redistributing weights or data.** The Python package's CC BY 4.0 metadata alone does not establish rights for every external resource. | [PSALM package](https://pypi.org/project/protein-sequence-annotation/2.1.12/); [PSALM models](https://huggingface.co/ProteinSequenceAnnotation) |
| **NumPy** | Common transitive dependency of scientific Python packages; not identified as a direct import in the reviewed notebook. | **BSD-3-Clause**, with bundled-component notices potentially applicable to binary distributions. | [NumPy license](https://github.com/numpy/numpy/blob/main/LICENSE.txt) |

## C. Conditionally installed dependencies

The reviewed notebook includes installation logic for certain hardware or optional prediction configurations. **Presence of an installation command does not establish that the component was used in the reported analyses.**

| Component | Condition or role | License / terms | Official source |
|---|---|---|---|
| **Miniforge** | Optional environment/bootstrap installer. | **BSD-3-Clause** for the installer project; packages in the distribution have their own licenses. | [Miniforge license](https://github.com/conda-forge/miniforge/blob/main/LICENSE) |
| **HH-suite** (`hhsuite=3.3.0`) | Optional structure-prediction/template-related dependency. | **Verify license and notices in the exact 3.3.0 package/source** before shipping a copy. | [HH-suite source](https://github.com/soedinglab/hh-suite) |
| **Kalign2** (`kalign2=2.04`) | Optional alignment dependency. | **Version-specific license requires verification**; do not substitute the license of modern Kalign releases without checking the legacy 2.04 source/package. | [Kalign project](https://github.com/TimoLassmann/kalign); [Bioconda package](https://bioconda.github.io/recipes/kalign2/README.html) |
| **OpenMM** (`openmm=8.2.0`) | Optional molecular modeling/relaxation support. | **Multiple licenses**, including MIT and LGPL for different parts; consult bundled license files. | [OpenMM license details](https://github.com/openmm/openmm/blob/master/docs-source/licenses/Licenses.txt) |
| **PDBFixer** | Optional structure preparation. | **Check the license packaged with the installed version**. | [PDBFixer repository](https://github.com/openmm/pdbfixer) |
| **JAX / jaxlib** | Hardware-specific numerical backend setup. | **Apache-2.0** for JAX project code; binary builds and bundled third-party components may have additional notices. | [JAX source/license](https://github.com/jax-ml/jax/blob/main/LICENSE) |
| **dm-haiku** (`0.0.10`) | Optional dependency installed with an alternate JAX setup. | **Apache-2.0**. | [Haiku repository/license](https://github.com/google-deepmind/dm-haiku) |
| **Kaleido** (`0.2.1`) | Installed for static Plotly image export where enabled. | **Check the exact package version and bundled browser components** before redistributing the package or binaries. | [Kaleido repository](https://github.com/plotly/Kaleido); [PyPI](https://pypi.org/project/kaleido/0.2.1/) |

## D. Redistributing code versus installing software

1. **Code included or adapted in this repository:** retain the original copyright and permission notices in accordance with the applicable upstream license. For ColabFold-derived code, see the MIT notice reproduced in `NOTICE` and identify adapted sections accurately in the notebook where practical.
2. **Dependencies installed at runtime:** FoldColabFlow does not claim ownership of them. Installing software and redistributing its code or binaries are different activities. If a release later bundles any dependency or executable, review that distributed artifact's exact license and bundled notices.
3. **TM-align source:** the notebook downloads and compiles `TMalign.cpp` during execution. Keep its original header and documentation; verify the exact upstream redistribution conditions before uploading that source or the resulting binary as a release asset.
4. **Models and databases:** cite and comply with their separate conditions. In particular, the AlphaFold parameter license is not the same as the AlphaFold or ColabFold code license.
5. **Scientific citations:** publications using these methods should also cite the relevant scientific papers, independently of the legal license notices.
6. **No blanket license transfer:** the repository's Apache-2.0 terms apply only to original contributions and any other material for which the contributors possess the rights to apply that license.

## E. Pre-release verification items

- [ ] Confirm that the code segments attributed to ColabFold are actually adapted, and retain the correct upstream MIT notice.
- [ ] Inspect the copyright/license header in the exact version of `TMalign.cpp` fetched by the notebook.
- [ ] Verify licenses of the exact **Kalign2 2.04**, **HH-suite 3.3.0**, **PDBFixer**, and **Kaleido 0.2.1** distributions if redistributing their code or binaries.
- [ ] Check the specific **PSALM model card** and any downloaded Pfam-related resources before distributing model weights or datasets.
- [ ] Review notebook-embedded images, logos, figures, example structures, and other non-code assets for provenance and reuse permissions.
- [ ] Record software versions or commit hashes used for the published results, where available; a dependency installed from a moving Git branch may change between runs.
- [ ] Keep the top-level `LICENSE`, `NOTICE`, and this file synchronized whenever the repository's contents change.

*This inventory is a best-effort technical documentation aid based on the supplied notebook, not a legal opinion or a certification that every possible downstream dependency has been audited.*

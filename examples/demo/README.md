# FoldColabFlow demonstration outputs

This directory contains the representative outputs supplied with the current
FoldColabFlow demonstration package.

## Demo inputs

| Demo name | Protein identifier supplied for the project | Length |
|---|---|---:|
| `Seq_1` | `P01308 · INS_HUMAN` | 110 aa |
| `Seq_2` | `A0A1B0GVQ0 · SPAR_HUMAN` | 90 aa |

## Included files

| File | Contents |
|---|---|
| `alignment_outputs.zip` | Pairwise alignment tables, identity/similarity/gap matrices, MAFFT MSA, settings, software versions, and HTML report |
| `physicochemical_outputs.zip` | Descriptor tables, composition tables, statistics, warnings, Plotly HTML, high-resolution PNG/SVG figures, and HTML report |
| `Example_c1402_results.zip` | ColabFold prediction directories for `Seq_1` and `Seq_2`, PDB files, A3M files, score JSON, PAE/pLDDT/coverage plots, configuration files, and upstream `cite.bibtex` files |
| `Seq_1_ramachandran.png` | Example Ramachandran/backbone geometry output |

## Reproducibility notes

The archived alignment software-version file records Python 3.12.13,
Biopython 1.88, pandas 2.2.2, and MAFFT v7.490.

The ColabFold `config.json` files record ColabFold 1.6.2 at commit
`f41090fe3da60283e682f1f284d2c2a1952c519d`, using `alphafold2_ptm`,
five models, three recycles, MMseqs2 MSA mode, no templates, no relaxation,
ranking by pLDDT, and random seed 0.

These files are demonstration artifacts, not experimental validation.

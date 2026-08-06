# Spectral Persistence and the Laplacian Pseudoinverse: A Systematic Empirical Audit

**Author:** Edher Alan Arteaga Marroquín — [ORCID 0009-0004-7333-1975](https://orcid.org/0009-0004-7333-1975)
**Status:** Paused / at rest. Version 5.0. Not peer reviewed.

## What this is

This repository is a reproducible, honest record of a two-week empirical
investigation into a spectral graph observable, V_i = Σ_{k≥2} v_k(i)²/λ_k —
which turned out to be exactly the diagonal of the Laplacian pseudoinverse,
L⁺_ii, already known in the literature (Van Mieghem, Devriendt & Cetinay,
*Phys. Rev. E* 96, 032311, 2017).

**This is not a paper claiming a discovery.** It is a systematic audit: a set
of working conjectures were proposed, tested one at a time under
progressively stricter controls, and reported regardless of whether they
survived. Most did not. The ones that did are modest and clearly labeled as
such. The full account — including bugs found and corrected mid-analysis — is
in the paper.

## Start here

Read **[`paper/SPG_final_v9.docx`](paper/SPG_final_v9.docx)** first. It is the
single authoritative document. Everything else in this repo is supporting
code.

The central result of the paper is a table (Section 3) listing every
conjecture tested and its verdict — refuted, survived, or left open. That
table is the fastest way to understand what this project actually found.

## Central finding, in one paragraph

The strong anti-correlation between node degree and V (Spearman ≈ −0.96 to
−1.00 across 30+ real networks, biological and non-biological) is real,
reproducible, and robust to the choice of connectome atlas — but it is
**not** a property of network topology alone. It depends critically on the
diffusion operator used: it collapses (toward Spearman ≈ 0) when the
combinatorial Laplacian is replaced by its symmetric normalized version. This
operator-dependence, verified with an independently-checked identity, is the
most solid result in this work.

## Repository structure

```
paper/
  SPG_final_v9.docx        <- the single authoritative document, read this first

notebooks/
  01_verificacion_identidad_celegans.ipynb   verifies V = L⁺_ii exactly
  02_tau_vs_V_vs_literatura.ipynb            tests whether τ̃ adds information beyond V (it does not)
  03_budapest_robustez_atlas.ipynb           replicates the human-connectome result on an independent atlas
  04_redes_bio_y_no_bio.ipynb                multidomain sweep: biological vs. non-biological networks
  05_jazz_hallazgo_no_biologico.ipynb        confirms the effect in a social (non-biological) network
  06_bitcoin_powergrid_falsacion.ipynb       deliberate falsification attempt using near-regular networks
```

Each notebook opens with a markdown cell stating the question tested, the
verdict, and a pointer to the relevant section of the paper.

## Data

All networks were downloaded from [Netzschleuder](https://networks.skewed.de/),
using the edge-list (`edges`) CSV files for each dataset. Data files are not
included in this repository; each notebook lists the exact dataset name and
Netzschleuder URL used, so it can be re-downloaded directly.

The core analysis (the `SPG` class computing V and τ̃ from the graph
Laplacian) is **domain-agnostic**: it takes any undirected graph as an
adjacency matrix and works identically regardless of what the network
represents. It was tested here on connectomes, metabolic networks, protein
interactomes, food webs, gene-regulatory networks, financial transaction
networks, and social collaboration networks specifically to confirm this —
see the multidomain sweep (notebook 04) and Section 5.2 of the paper.

Datasets referenced during the broader investigation but without a dedicated
notebook in this repository: `interactome_figeys`, `collins_yeast`,
`celegans_2019` (all also on Netzschleuder, same edge-list format).

The human connectome analyses use:
- **AAL-116 atlas:** BNU1 dataset (Roncal et al., 2013) — see `human_brains` on Netzschleuder
- **HCP atlas:** Budapest Reference Connectome 3.0 (Szalkai et al.,
  *Neurosci. Lett.* 595, 2015)

## Reproducing

Notebooks were run in Google Colab; cells that mount Google Drive
(`drive.mount(...)`) and reference a personal folder path can be skipped or
replaced with a local path to a folder containing the downloaded CSV files.
The core analysis class (`SPG`) has no external dependencies beyond `numpy`,
`scipy`, `networkx`, and `pandas`.

## Why this is public despite mostly negative results

Refuted conjectures are reported alongside surviving ones because that is
the actual record of the investigation, and because negative results —
including two mid-analysis bugs that were caught and corrected — are rarely
published but are exactly the kind of detail that makes a result trustworthy.
See Section 10 ("Lessons from Refuted Conjectures and Methodological Errors")
of the paper for the full account.

## Citation

If you reference this work, please cite via ORCID 0009-0004-7333-1975 and
the Zenodo DOI (to be added once deposited).

## License

Code: MIT License. Paper text: CC BY 4.0.

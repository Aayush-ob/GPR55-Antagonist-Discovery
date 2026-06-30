# Introduction

## The target: GPR55

**GPR55** is an atypical, "non-canonical cannabinoid" G-protein-coupled receptor activated by the endogenous lysophospholipid **L-α-lysophosphatidylinositol (LPI)**. It signals preferentially through the **pro-oncogenic Gα12/13 → RhoA/ROCK** and **PI3K/AKT** cascades.

## Why it is a drug target

GPR55 is **overexpressed across multiple human malignancies** — pancreatic ductal adenocarcinoma, breast, colorectal, ovarian cancer, and glioblastoma — with elevated expression correlating with poor survival. Functional-genomics evidence (including CRISPR knockout in the KPC pancreatic-cancer model) shows GPR55 loss-of-function prolongs survival, marking it as a **causal driver** of tumour progression rather than a bystander. This makes a **GPR55 antagonist** a rational anticancer strategy.

## Why a new structure-based effort

Earlier GPR55 drug discovery relied on homology models built against distant GPCR templates (<15 % transmembrane identity), producing unreliable binding-site geometry. This project instead uses the **experimentally determined cryo-EM structure (RCSB PDB 9IYA, 3.04 Å, 2025)** of human GPR55 in its active, G13-coupled state — the functionally relevant conformation for oncogenic signalling.

## Strategy: three binding sites

Rather than a single pocket, three pharmacologically distinct sites were screened in parallel:

- **Orthosteric (P0)** — the deep transmembrane LPI pocket; compounds act as **competitive antagonists**.
- **Allosteric (P3)** — a secondary extracellular cavity; **non-competitive modulators** offering potential selectivity and reduced on-target toxicity.
- **Protein–protein interface** — the GPR55–Gα12/13 coupling surface; compounds here would block signal transduction at the effector step (**insurmountable antagonism**).

The reference antagonist **AM251** is used throughout as a positive control and benchmark.

See [METHODOLOGY.md](./METHODOLOGY.md) for the full computational pipeline and [RESULTS.md](./RESULTS.md) for outcomes.

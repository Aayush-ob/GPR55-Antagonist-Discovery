# Methodology

End-to-end structure-based pipeline for discovering GPR55 antagonists, from a multi-thousand-compound library to MD- and free-energy-validated leads across three binding sites.

## 1. Computational environment
- **Local:** preprocessing, docking grid setup, ADMET, trajectory analysis, DFT; MD for the orthosteric (P0) and allosteric (P3) systems on an NVIDIA RTX 3050.
- **Cloud:** high-throughput screening on a Google Cloud Compute Engine instance (e2-standard-8); the larger protein–protein-interface MD systems on NVIDIA T4 GPUs via Kaggle.
- **Key software:** AutoDock Vina 1.2.5, AutoDock Tools, RDKit, CHARMM-GUI, ACPYPE/AmberTools, GROMACS 2025, gmx_MMPBSA 1.6.1, ORCA 5.0, SwissADME, ADMET-AI, ProTox-II, PyMOL.

## 2. Target preparation
- Structure: human GPR55 cryo-EM complex, **RCSB PDB 9IYA** (3.04 Å, released Jan 2025), in its active G13-coupled state.
- Chain R (receptor) isolated via CHARMM-GUI PDB Reader; HETATMs, waters, and antibody fragments removed; missing loops modeled; protonation set at pH 7.4 (PROPKA).

## 3. Binding sites (three targeted simultaneously)
| Site | Type | Grid centre (Å) | Box |
|------|------|-----------------|-----|
| **P0** | Orthosteric (competitive) | 110.02, 111.68, 81.10 | 22 Å |
| **P3** | Allosteric (non-competitive) | 105.58, 102.05, 107.35 | 20 Å |
| **Interface** | GPR55–Gα12/13 PPI (signal block) | 112.678, 92.605, 112.545 | 25 Å |

## 4. Library and ligand preparation
- ~34,660 raw compounds (ChEMBL + PubChem) → **Lipinski Rule of Five** filter → **10,940** drug-like candidates.
- 3D conformers via RDKit ETKDGv3 + MMFF94 minimisation; converted to PDBQT (Gasteiger charges). AM251 included as the reference antagonist/positive control.

## 5. High-throughput virtual screening (3-stage funnel)
| Stage | Exhaustiveness | Modes | Result |
|-------|----------------|-------|--------|
| 1 — coarse HTVS | 8 | 1 | ~750/site advance |
| 2 — focused re-dock | 16 | 5 | top-25/site retained |
| 3 — precision | 64 | 15 | **373 validated hits** |
Top 25/site → ADMET filtering → **9 candidates (3/site) + AM251** taken to MD.

## 6. ADMET profiling
SwissADME (physicochemical + pharmacokinetics) and ADMET-AI/ProTox-II (toxicity). A "fatal-flaw" filter removed compounds with high AMES mutagenicity or hERG cardiotoxicity probability; secondary, optimisable liabilities (e.g. DILI) were permitted.

## 7. Ligand topology
Custom parameters for all 10 ligands via **ACPYPE** — **GAFF2** force field with **AM1-BCC** partial charges — producing GROMACS-compatible topologies.

## 8. Membrane system construction
- **CHARMM-GUI Membrane Builder**: POPC bilayer, **OPM/PPM** orientation, TIP3P water, 0.15 M NaCl, **CHARMM36m** force field.
- System sizes: ~62k–63k atoms (P0/P3, receptor alone) to ~225k atoms (Interface, full receptor–G-protein complex).
- A custom **Kabsch-superposition pipeline** re-injected each ligand into its pocket after the OPM rigid-body transformation (which otherwise strips/displaces the ligand), validated by ligand centre-of-mass placement.

## 9. Molecular dynamics
- Steepest-descent minimisation → six-stage NVT/NPT equilibration (position restraints stepped down) → **100 ns unrestrained production** per system (12 systems, ~1.2 µs aggregate).
- 303.15 K (V-rescale thermostat), 1 bar (C-rescale barostat, semi-isotropic), PME electrostatics, LINCS constraints; 2 fs timestep (4 fs with HMR for AM251).

## 10. Trajectory analysis
RMSD, RMSF, radius of gyration, SASA, hydrogen bonds, minimum distance, intermolecular contacts (GROMACS + MDAnalysis); PLIP-style residue-level interaction profiling; PCA/FEL and DCCM for collective motion.

## 11. Binding free energy
**MM-GBSA** via gmx_MMPBSA (GB-OBC2, igb=5, 0.15 M salt) over 51 frames spanning each 100 ns trajectory; single-trajectory, no normal-mode entropy (relative ranking of analogous compounds).

## 12. DFT analysis
The four MD-validated leads (AM251, compound_11569386, compound_76358219, compound_2961621) optimised at **B3LYP/6-31G\*** (ORCA 5.0); HOMO-LUMO energies and gap, derived global reactivity descriptors (hardness, softness, electrophilicity), and MEP surfaces.

See [RESULTS.md](./RESULTS.md) for outcomes and [TARGET_COORDINATES.md](./TARGET_COORDINATES.md) for full grid definitions.

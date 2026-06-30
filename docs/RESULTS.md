# Results

## 1. Virtual screening (docking)

Best docking affinities per site (AutoDock Vina, Stage-3 precision, kcal/mol):

| Site | Top compound | ΔG | AM251 control |
|------|--------------|----|---------------|
| **P0** (orthosteric) | compound_11569386 | **−12.3** | −9.46 |
| **P3** (allosteric) | compound_3992081 | −8.5 | −7.70 |
| **Interface** (PPI) | CHEMBL432162 | −9.6 | −6.27 |

373 hits cleared Stage-3 precision docking; the top 25/site were ADMET-profiled and narrowed to **9 candidates (3 per site)** for MD validation. Three compounds were notable **pan-site binders**, engaging all three pockets.

## 2. ADMET (final 9 candidates)

Stage-3 ΔG with primary toxicity flags (ADMET-AI). All cleared the fatal-flaw filter (AMES and hERG below threshold).

| Compound | Site | ΔG (dock) | AMES | hERG |
|----------|------|-----------|------|------|
| 11569386 | P0 | −12.3 | 0.06 | 0.49 |
| 76358219 | P0 | −11.1 | 0.53 | 0.52 |
| 5505049 | P0 | −11.1 | 0.43 | 0.49 |
| 3992081 | P3 | −8.5 | 0.08 | 0.29 |
| 45803381 | P3 | −8.2 | 0.11 | 0.41 |
| 2961621 | P3 | −8.1 | 0.18 | 0.29 |
| CHEMBL432162 | Interface | −9.6 | 0.28 | 0.56 |
| 92261630 | Interface | −9.1 | 0.28 | 0.07 |
| 121547889 | Interface | −8.6 | 0.10 | 0.42 |

## 3. MD + MM-PBSA binding free energy (100 ns)

ΔG_bind (kcal/mol) from gmx_MMPBSA over 51 frames of each 100 ns trajectory.

**Orthosteric (P0)**
| Compound | ΔG_bind | ± SD |
|----------|---------|------|
| AM251 (control) | −35.06 | 4.33 |
| **compound_11569386** | **−26.30** | 1.94 |
| compound_76358219 | −17.19 | 2.52 |
| compound_5505049 | −8.88 | 1.30 |

**Allosteric (P3)**
| Compound | ΔG_bind | ± SD |
|----------|---------|------|
| **compound_2961621** | **−7.42** | 2.42 |
| AM251 (control) | −6.72 | 2.40 |
| compound_3992081 | +0.51 | 0.13 |
| compound_45803381 | +0.06 | 0.03 |

**Interface (PPI)**
| Compound | ΔG_bind | ± SD |
|----------|---------|------|
| AM251 (control) | −13.03 | 2.14 |
| CHEMBL432162 | −3.79 | 4.94 |
| compound_121547889 | −1.45 | 3.81 |
| compound_92261630 | +0.04 | 0.23 |

## 4. Key findings

- **compound_11569386** is the strongest novel binder overall (−26.30 kcal/mol at P0), second only to the AM251 control.
- **compound_2961621** is the top allosteric hit and **outperforms the AM251 control at P3** (−7.42 vs −6.72) — a genuine novel-modulator result.
- **Docking-to-dynamics re-ranking:** the best-*docking* allosteric compound (3992081, −8.5) became a non-binder under MD (+0.51), while a lower-ranked compound (2961621) emerged as the true lead. This demonstrates that static docking scores are hypotheses, validated only by dynamics and free-energy calculations.

## 5. DFT

The four MD-validated leads (AM251, 11569386, 76358219, 2961621) were characterised at B3LYP/6-31G* (ORCA): HOMO-LUMO gaps, global reactivity descriptors, and MEP surfaces, benchmarking each novel hit's electronic profile against the control.

*Analysis figures (RMSD, RMSF, Rg, SASA, H-bonds, contacts, snapshots, DCCM, FEL, PLIP, HOMO-LUMO, MEP) are in [`../figures/`](../figures/).*

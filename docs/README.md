# GPR55 Antagonist Discovery — Documentation

> Discovery of novel antagonists for the atypical cannabinoid receptor **GPR55** (anticancer target, PDB 9IYA), across three binding sites — completed end-to-end pipeline (thesis defended; manuscript in preparation).

## 📁 Documentation Index

| File | Description |
|------|-------------|
| [INTRODUCTION.md](./INTRODUCTION.md) | Target background, rationale, and three-site strategy |
| [METHODOLOGY.md](./METHODOLOGY.md) | Full computational pipeline (HTVS → ADMET → MD → MM-PBSA → DFT) |
| [RESULTS.md](./RESULTS.md) | Docking, ADMET, MM-PBSA binding energies, and DFT outcomes |
| [TARGET_COORDINATES.md](./TARGET_COORDINATES.md) | Docking grid coordinates for all three sites |
| [REFERENCES.md](./REFERENCES.md) | Key literature references |

## ✅ Status

| Phase | Status |
|-------|--------|
| Target identification & protocol validation (AM251 control) | ✅ Complete |
| Library prep & 3-stage HTVS (10,940 compounds) | ✅ Complete |
| Hit selection & ADMET profiling | ✅ Complete |
| Molecular dynamics (100 ns × 12, ~1.2 µs) | ✅ Complete |
| MM-PBSA binding free energy | ✅ Complete |
| DFT (HOMO-LUMO / MEP) | ✅ Complete |
| Manuscript | 📝 In preparation |

## 📊 Key Results

- Top novel binder: **compound_11569386** (orthosteric), MM-PBSA ΔG_bind **−26.30 kcal/mol**
- Top allosteric hit: **compound_2961621**, **−7.42 kcal/mol** — outperforms the AM251 control (−6.72)
- MD + MM-PBSA **re-ranked** several top docking hits, demonstrating the limits of static scoring

See [RESULTS_BINDING_ENERGIES.md](./RESULTS_BINDING_ENERGIES.md) for the full ranking and `../figures/` for analysis plots.

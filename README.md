# PRC2 Rejuvenation Benchmark — Reproducibility Package

Companion data for: "Transcriptomic Signatures of Partial Reprogramming Are Confounder-Dominated: A PRC2 Fidelity Benchmark with MSigDB Hallmark Validation" (clawRxiv 2604.00847).

## Contents

- `all_signature_rows.tsv` — 28 curated signatures (20 primary + 8 within-family holdouts) with gene symbols, directions, and weights
- `all_module_rows.tsv` — Scoring modules: 5-gene PRC2 (EZH2, SUZ12, EED, JARID2, EPOP) + 4 confounder modules (6 genes each)
- `canonical_prc2.yaml` — Benchmark configuration
- `strict_13_gsea_results.json` — GSEA results for strict 13-gene PRC2 set with permutation 95% CIs, LOGO results, gene set variants, and mouse MSigDB sensitivity
- `chipseq_validation.json` — H3K27me3 ChIP-seq validation (Camacho et al. 2026, GSE288574): Old/Young ratios at PRC2 subunit promoters
- `corrected_prc2_gsea.json` — Full GSEA results for all PRC2 gene set variants
- `ranked_lists/` — Exact .rnk files for all 4 datasets (gene symbol + ranking metric)

## Gene Set Definitions

**Strict 13-gene PRC2 (GSEA primary):** EZH2, EZH1, SUZ12, EED, RBBP4, RBBP7, JARID2, AEBP2, PHF1, MTF2, PHF19, EPOP, PALI1

Per Margueron & Reinberg (2011) and Hauri et al. (2016, doi:10.1016/j.celrep.2016.08.096). Excludes: PRC1 CBXs, KDM6A/B demethylases, DNMT3A/B methyltransferases.

**5-gene PRC2 Scoring Module (benchmark):** EZH2 (w=1.2), SUZ12 (w=1.1), EED (w=1.0), JARID2 (w=0.9), EPOP (w=0.8)

**Confounder Modules (6 genes each, w=1.2-0.7):**
- AP-1: JUN, FOS, FOSL2, ATF3, JUND, CEBPB
- Proliferation: MKI67, PCNA, MCM2, TOP2A, TYMS, CDK1
- Interferon: STAT1, IFIT1, IFIT3, ISG15, MX1, OAS1
- DNA Damage: CDKN1A, GADD45A, DDIT3, BBC3, MDM2, TP53I3

## Reproducing the Benchmark

```bash
git clone https://github.com/scottdhughes/prc2-rejuvenation-benchmark.git
cd prc2-rejuvenation-benchmark
# All 28 signatures, ranked lists, and results are in this repo
# The full pipeline CLI requires the main skill repository:
# uv sync --frozen && uv run prc2-rejuvenation-benchmark run --config canonical_prc2.yaml --out outputs/canonical
```

## Key Results

- PRC2 subunits (strict 13): non-significant in all 4 datasets (p = 0.16-0.36; all permutation 95% CIs contain zero)
- H3K27me3 at PRC2 promoters: stable between young and old (mean Old/Young = 0.95)
- Benchmark: 18/20 primary (Wilson CI: 0.70-0.97), 8/8 within-family holdouts (CI: 0.68-1.00)

## License

CC-BY 4.0

## Deposited Analysis Outputs

All key analytical outputs are pre-computed and deposited in this repository:
- `strict_13_gsea_results.json` — GSEA NES/p-values, permutation 95% CIs, LOGO delta-ES, gene set variants, mouse MSigDB sensitivity
- `chipseq_validation.json` — H3K27me3 Old/Young ratios at 13 PRC2 promoters + 5 targets + 3 controls
- `ssgsea_regression.json` — Per-sample ssGSEA scores and confounder regression (R², coefficients, residual p-values)
- `corrected_prc2_gsea.json` — Full GSEA for all PRC2 gene set variants (original 22, strict 13, ±EZH2, ±CBXs, ±DNMTs)

These allow full verification of all paper claims without running the CLI pipeline.

## Note on Self-Containment

This repository is a companion reproducibility package. The full CLI tool (`prc2-rejuvenation-benchmark`) is distributed as a Python package in the main skill repository. However, all numerical claims in the paper can be verified from the pre-computed JSON outputs deposited here. The `.rnk` files allow independent GSEA verification with any standard tool (e.g., GSEA desktop, gseapy).

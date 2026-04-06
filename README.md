# PRC2 Rejuvenation Benchmark — Reproducibility Package

Companion data for: "Transcriptomic Signatures of Partial Reprogramming Are Confounder-Dominated: A PRC2 Fidelity Benchmark with MSigDB Hallmark Validation" (clawRxiv 2604.00847).

## Contents

- `all_signature_rows.tsv` — 28 curated signatures (20 primary + 8 within-family holdouts) with gene symbols, directions, and weights
- `all_module_rows.tsv` — Scoring modules (PRC2 restoration/loss core + 4 confounder modules) with gene symbols, directions, and weights
- `canonical_prc2.yaml` — Benchmark configuration
- `corrected_prc2_gsea.json` — Full GSEA results for PRC2 gene set variants (original 22, strict 13, minus EZH2, etc.)
- `ranked_lists/` — Exact .rnk files for all 4 datasets (gene symbol + ranking metric)

## Reproducing the 90% / 8-of-8 Benchmark

```bash
git clone https://github.com/scottdhughes/prc2-rejuvenation-benchmark.git
cd prc2-rejuvenation-benchmark
uv sync --frozen
uv run prc2-rejuvenation-benchmark run --config config/canonical_prc2.yaml --out outputs/canonical
uv run prc2-rejuvenation-benchmark verify --config config/canonical_prc2.yaml --run-dir outputs/canonical
```

## Gene Set Definitions

**Strict 13-gene PRC2 (GSEA primary):** EZH2, EZH1, SUZ12, EED, RBBP4, RBBP7, JARID2, AEBP2, PHF1, MTF2, PHF19, EPOP, PALI1

**5-gene PRC2 Scoring Module (benchmark):** EZH2 (w=1.2), SUZ12 (w=1.1), EED (w=1.0), JARID2 (w=0.9), CBX7 (w=0.8), DNMT3A (w=0.7)

**Confounder Modules (6 genes each):**
- AP-1: JUN (1.2), FOS (1.1), FOSL2 (1.0), ATF3 (0.9), JUND (0.8), CEBPB (0.7)
- Proliferation: MKI67 (1.2), PCNA (1.1), MCM2 (1.0), TOP2A (0.9), TYMS (0.8), CDK1 (0.7)
- Interferon: STAT1 (1.2), IFIT1 (1.1), IFIT3 (1.0), ISG15 (0.9), MX1 (0.8), OAS1 (0.7)
- DNA Damage: CDKN1A (1.2), GADD45A (1.1), DDIT3 (1.0), BBC3 (0.9), MDM2 (0.8), TP53I3 (0.7)

## License

CC-BY 4.0

# HLT diphoton trigger efficiency — 2023 results

Tag-and-probe measurements of the CMS diphoton HLT leg efficiencies on 2023 data. Companion to
[HLT-diphoton-efficiency-2024-results](https://github.com/santanumahata/HLT-diphoton-efficiency-2024-results).

## ▶ Interactive comparison tool

Overlay and compare any **2023 and 2024** curves on one plot (drag or click to add; built-in
glossary decodes every label):
**https://santanumahata.github.io/HLT-diphoton-efficiency-2024-results/**

## What the labels mean

**Two data-taking eras** (2023 is split at the BPix pixel-detector boundary):
- `preBPix` — the earlier 2023 era.
- `postBPix` — the later 2023 era.

**Two trigger selections:**
- **standard** — the top-level `csvs/`, `efficiency_plots/`, `fit_plots/`, `jsons/`; the
  track-isolation selection.
- **fullPath** — everything under `fullPath/`; adds the full HLT-path requirement on top of the
  standard selection.

**Legs:** `seed` = seeded (lead) leg; `unseed` = unseeded (sublead) leg (requires the tag to have
fired the seeded leg).

**ECAL region / shower shape:** `EB` = barrel (|η| < 1.44), `EE` = endcap (1.57 < |η| < 2.5).
`R9` = E₃ₓ₃ / E_RAW (shower containment). Categories: EB R9 0.50–0.55 / 0.55–0.85 / > 0.85;
EE R9 0.90–0.93 / > 0.93.

**Fit model:** signal = Breit–Wigner ⊗ double-sided Crystal Ball; background = RooCMSShape
(nominal, `bwDscbCms`) or Exponential (alternate, `bwDscbExp`). Efficiency = fitted pass fraction.

## Layout

- `csvs/hlt_2023_trigger_efficiency_asym_errors.csv` — consolidated efficiencies + asymmetric
  uncertainties (standard selection).
- `efficiency_plots/` — efficiency vs probe pT, one panel per (era, leg).
- `fit_plots/{preBPix,postBPix}/…` — the individual tag-and-probe mass-fit plots.
- `jsons/2023{preBPix,postBPix}/TriggerSF_*.json` — HiggsDNA `TriggerSF` correctionlib JSONs
  (SCEta × r9 × pt multibinning, nominal / up / down; lead ↔ seed, sublead ↔ unseed).
- `fullPath/` — the same four subtrees for the fullPath selection.

## Correspondence to the 2024 repo

The 2024 repo uses labels `etaR9rw_{noPresel,withPresel}[_fullPath]`. The `_fullPath` suffix there
means the **same** full-HLT-path requirement as this repo's `fullPath/` subtree. The differing axis:
2023 splits on data-taking era (preBPix / postBPix), whereas 2024 splits on how the η–R9 reweighting
was derived (noPresel / withPresel).

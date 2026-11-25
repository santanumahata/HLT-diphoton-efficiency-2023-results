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

## Update (2026-11-25): Cone-based H/E preselection fix (`probe_hoe_bc < 0.08`)

The standard selection (`csvs/`, `efficiency_plots/`, `fit_plots/`, and `jsons/`) has been updated
after fixing the MiniAOD TnP ntuplizer H/E branch swap: switching the offline probe cut from
single-tower `probe_hoe < 0.08` (`hadTowOverEm()`) to cone-based `probe_hoe_bc < 0.08`
(`hadronicOverEm()`, matching both Run 3 NanoAOD `Photon_hoe` and online HLT
`EgammaHLTHcalVarProducerFromRecHit`, `useSingleTower=False, outerCone=0.14`).

- **Fitter:** Re-run with the latest `cms-egamma/egm_tnp_analysis` (`CMSSW_11_2_0`) + custom
  `BW×DSCB` and asymmetric Minos error patches (cross-checked against `CMSSW_10_6_8` to
  `median |Δ| = 0.015 pp`; 5 bins where `CMSSW_11_2_0` hit HESSE status `-1` use the matching
  converged `CMSSW_10_6_8` fit and plot).
- **Uncertainties & binning:** All pT bins (including `[0, 35]` seeded and `[0, 21]` unseeded)
  are plotted at each bin's right edge in `efficiency_plots/` (overflow `[90, ∞)` capped at 120 GeV),
  with total uncertainty `stat (Minos fit) ⊕ |eff_CMS − eff_Exp|` strictly capped at `[0, 1.0]`.
- **JSON R9 boundary fix:** Sublead (`unseed`) `TriggerSF` JSON `r9` edges are now corrected from
  `[0.0, 0.56, 0.85, 0.90, 999.0]` to `[0.0, 0.55, 0.85, 0.93, 999.0]` to match the fitter bins.
- **Note:** `fullPath/` remains from the previous production and has not been re-run yet.

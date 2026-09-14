# exocomet-hunter-data

Generated training data and model artifacts for [exocomet-hunter](https://github.com/AJpro-merc/exocomet-hunter).

**Not a scientific product on its own.** Every row here is either synthetic (a fake comet/flare/starspot/etc.
shape injected into a real light curve) or a plain detection on unmodified real photometry, produced by the
code in the main repo. See that repo for what generated this and why.

Source photometry: NASA Kepler and TESS archives via MAST (mast.stsci.edu). This repo stores only small,
derived measurements (feature rows, model files) -- never raw light curves.

## Layout

- `training/labels_kepler.parquet` -- labelled feature rows, Kepler track. Safe, no open correctness bugs.
- `training/labels_tess.parquet` -- labelled feature rows, TESS track. Only exists post-A2-fix; see the
  main repo's `docs/NEXT_STEPS.md` for what A2 was.
- `models/*.joblib` -- trained classifier(s), overwritten weekly (no dated snapshots kept; the manifest
  below has the full history of what each version was trained on).
- `models/manifest_*.jsonl` -- one line per training run: row count, class balance, host stars, date,
  package versions, training-set hash, and backtest results. This is the "how much was it trained on"
  record.
- `models/last_compare.json` -- most recent training run's backtest scores vs. the previous run's, for
  spotting a regression (the model still gets committed either way -- this is visibility, not a gate).
- `models/threshold_*.json` -- the probability cutoff chosen for each model from calibration.

Append-only by convention: manifests never get rewritten, only appended to. Nothing here is force-pushed.

Generated automatically by `.github/workflows/train.yml` in the main repo, on a schedule, unattended.

---



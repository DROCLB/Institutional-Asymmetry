# Monte Carlo Code for Institutional Asymmetry

This directory contains the current Monte Carlo notebooks for *Institutional Asymmetry, Endogenous Fragility, and Economic Growth*. They are self-contained, run independently, require no external data or project-specific paths, and implement the exercises reported in Online Appendix B.

## Current Notebooks

| Notebook | Online appendix | Numerical exercise | Reported run |
|---|---|---|---|
| `mc_block1_micro_drag_pricing_spillovers.ipynb` | B.1 | Micro-to-drag mechanics, fiscal feasibility, pricing, wedge, and spillover diagnostics | `260811_1431` |
| `mc_block2_threshold_dynamics.ipynb` | B.2 | Finite-horizon realization of static threshold geometry under baseline-prior and threshold-targeted designs | `260812_1353` |
| `mc_block3_intervention_hysteresis.ipynb` | B.3 | Conditional hysteresis, stimulus attenuation, and repeated-reform escape | `260812_0217` |

All final notebooks enforce the global second-order-condition screen documented in Online Appendix B: 4,001 risk-grid points, bounded local refinement of the three lowest values, and a refined-margin tolerance of `1e-6`.

## Requirements

The notebooks require Python 3.9 or later, NumPy, pandas, Matplotlib, SciPy, and Jupyter Notebook:

```bash
python -m pip install numpy pandas matplotlib scipy notebook
```

## Running the Code

Launch Jupyter from the directory where outputs should be stored:

```bash
jupyter notebook
```

Open a notebook and run its single code cell. Each run writes to `results/<MC_NAME>_<YYMMDD_HHMM>/` under the process's current working directory. Blocks 2 and 3 are long production runs and impose no wall-clock timeout.

## Production Settings and Seeds

| Block | Principal production settings | Random stream(s) |
|---|---|---|
| Block 1 | 1,000 admissible primitive draws; 200-point institutional-state grid | `20260609` |
| Block 2 | 250 accepted structural countries; 200-point institutional-state grid; 21 initial institutional states; horizon `T=200`; step `dt=0.05` | Structural primitives: `20260609`; dynamic parameters: `20260619`; threshold targeting: `20261609` |
| Block 3 | 1,000 accepted bistable economies; horizon `T=60`; step `dt=0.05`; robustness grids for threshold location, bisection, sample size, and initial-condition buffer | `20260312` |

Changing seeds, sample sizes, grids, horizons, or tolerances changes the outputs. Reduced settings are suitable for smoke tests but do not reproduce the reported values.

## Outputs

| Block | Saved materials |
|---|---|
| Block 1 | CSV diagnostic and audit results; pricing, wedge, and spillover results; summary figure in PNG and PDF |
| Block 2 | CSV audit ledger, trajectories, and treatment summaries; diagnostic figures in PNG and PDF; `config_dump.json` |
| Block 3 | CSV candidate, threshold, hysteresis, stimulus, and reform results; figures under `figures/`; `config_dump.json` |

The Block 2 threshold-targeted design is an auxiliary diagnostic conditional on an interior political threshold; it does not estimate the unconditional distribution of economies. Block 3 conditions on structurally admissible economies inside the bistable threshold domain; its escape rates are unweighted reform-grid-cell outcomes within that experiment, not unconditional policy-success probabilities.

The notebooks are independent and no block consumes another block's output. Configuration dumps record package versions and run parameters for Blocks 2 and 3.

## Citation

Please cite:

Cayirli, Omer. *Institutional Asymmetry, Endogenous Fragility, and Economic Growth*. Working paper.

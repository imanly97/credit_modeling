# Cash-advance underwriting simulator

A self-contained, executable credit-science notebook on **fully synthetic data**: simulate bank cash flow and short-term advances, then model, explain, price, and monitor the credit decision.

## Run it
```bash
pip install -r requirements.txt
jupyter notebook credit_underwriting_simulator.ipynb     # Run All; about 1.5 minutes
```
The shipped notebook already contains outputs from a full run. Everything is seeded.

## What's inside
1. **Simulator**: members with hidden fragility, pay cycles, bills, spending, shocks, overdrafts (20,000 members x 360 days, ~127k advance applications).
2. **Outcomes**: default drawn from a hidden, nonlinear, noisy probability; labels mature 14 days after the due date.
3. **Point-in-time features** plus a **leakage test that is shown to fail** on a deliberately leaky version.
4. **Models**: binned-logistic scorecard vs monotone-constrained LightGBM; time-based **out-of-time** and **out-of-member** evaluation; Platt calibration; KS, Brier, ECE; compared against the **oracle** (true hidden probability).
5. **SHAP**: additivity check, global importance, dependence plots, local waterfalls.
6. **Policy layer**: approve/decline *and* advance amount by expected profit with guardrails, graded against the true probabilities.
7. **Reason codes**: grouped SHAP reasons with a perturbation test.
8. **Selection bias**: approved-only training vs random exploration + inverse-propensity weighting.
9. **Monitoring**: PSI, calibration, early read on fast-resolving loans, and a macro stress period.
10. **Robustness**: reruns under different generator assumptions.

## Read this before quoting any number
All data is synthetic and the default process is a formula written for this project. Absolute AUCs and profits say nothing about a real lender. Fees, recovery and base default rate are illustrative assumptions. What transfers is the methodology and the relative comparisons. The notebook's final cell lists limitations and natural extensions.

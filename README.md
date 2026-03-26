# Actuarial Survival Models in PyMC (GSoC 2026)

Welcome! This repository contains the proof-of-concept notebook for my Google Summer of Code (GSoC) 2026 proposal for **PyMC**. 

My name is Shuo Zhang, an MSc grad in Financial & Insurance Mathematics at Charles University and an Actuary Candidate.

## 📌 Project Focus
In Life/Health Insurance pricing, dealing with highly censored and truncated data is the daily reality. While right-censoring is elegantly handled by PyMC, **Left-Truncation** (Immortal Time Bias) currently requires actuaries to manually construct complex, numerically sensitive tensor graphs.

This notebook demonstrates:
1. **Simulation-Based Calibration**: Generating actuarial data with $7.4\%$ percent left-truncation (pre-entry mortality) and $48\%$ percent right-censoring (administrative censoring & lapses).
2. **Numerically Stable Tensor Math**: Implementing closed-form Weibull log-likelihoods via `pm.Potential`.
3. **Log-Link AFT Architecture**: Ensuring strict positivity of the scale parameter to avoid MCMC divergence.
4. **Parameter Recovery**: Successfully recovering the true ground parameters despite heavily masked data.

## 🚀 The GSoC Vision (Formula API)
My ultimate goal for GSoC is to abstract this complex tensor math into an elegant, declarative Formula API inspired by R's `survival` package, making PyMC the ultimate tool for actuaries:

```python
import pymc_survival as pms

model = pms.SurvivalModel(
    formula="exit_age | truncate(entry_age, type='left') ~ smoker_status",
    data=df_actuarial,
    distribution="Weibull"
)

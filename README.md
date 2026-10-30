# Tambura Oil Field: Which Power Option Deserves the Capital?

**Case Study #9 in *The Feasibility Stress Test*. Primary lens: Capital Budgeting.**

An open-source Python reconstruction and browser simulator of a published capital-rationing study: three mutually exclusive ways to power a progressive-cavity pump (PCP) insert in an Indonesian oil field. One option has the highest NPV. A different option is the one the authors recommend. This repo shows why.

## The case

Tambura LLP, Makamah Block (PSC cost-recovery scheme). One well, about 0.4 MMbbl of reserves, peak output near 180 BOPD, project life 2023-2030, hurdle rate 10.45%. Three ways to power the pump:

1. **Option-1, cable laying:** highest capex, lowest opex.
2. **Option-2, own genset on platform:** middle on both.
3. **Option-3, rental genset:** lowest capex, highest opex.

## Citation

Jamal, M.N. & Sudrajat, O.Y. (2022). *Project Capital Rationing using Discounted Cash Flow Method, Sensitivity Analysis and Monte Carlo Simulation: Case Study Tambura Oil Development.* European Journal of Business and Management Research, 7(6), 287-296. https://doi.org/10.24018/ejbmr.2022.7.6.1760 (open access, CC BY-NC 4.0).

## Confirmed findings (paper's own tables)

| Metric (US$M unless noted) | Option-1 Cable | Option-2 Genset | Option-3 Rental |
|---|---|---|---|
| Capex | 2.39 | 1.89 | 0.39 |
| Life-of-project opex | 1.38 | 3.25 | 5.46 |
| NPV @ 10.45% | **1.44** | 1.33 | 1.41 |
| IRR | 36% | 41% | 176% |
| Payback (years) | 1.79 | 1.58 | 0.48 |
| Profitability index | 2.02 | 2.11 | 5.44 |

- NPV ranks Option-1 first, Option-3 second, by US$0.03M (2.1%).
- Option-3 needs US$2.00M less capital (83.7% less). Own arithmetic: NPV per US$ of capex is 0.60 for Option-1 and 3.62 for Option-3.
- Break-even (own arithmetic): the freed US$2.00M only has to earn NPV of US$0.03M elsewhere for Option-3 plus redeployment to beat Option-1.
- The paper reports a collective 10-30% probability of NPV below zero from 1,000 Monte Carlo iterations, and a scenario NPV range from about -US$1.09M to +US$2.62M. Per-option values are not tabulated in the text I could extract.
- Recommendation: Option-3. The paper reports no post-decision outcome. It is a prospective study.

## Reconstruction results (ILLUSTRATIVE, not the authors' numbers)

10,000 paired trials, triangular distributions on the paper's scenario ranges, one assumed price-inflation correlation of 0.4 (Cholesky Gaussian copula):

| Option | Mean NPV | SD | P5 | P(NPV<0) | Mean NPV per $ capex |
|---|---|---|---|---|---|
| Option-1 Cable | 2.05 | 0.86 | 0.82 | 0.0% | 0.86 |
| Option-2 Own genset | 1.90 | 0.80 | 0.75 | 0.0% | 1.00 |
| Option-3 Rental | 1.88 | 0.68 | 0.92 | 0.0% | 4.83 |

Option-3 beats Option-1 in 19.8% of paired trials in this reconstruction, and Option-1's mean NPV is higher by about US$0.17M. Option-3 has the lowest dispersion and the best fifth-percentile outcome.

## Honesty disclosure

- **Full text was read through automated extraction** of the open-access PDF, not manually. Check any number against the published paper before reuse.
- The paper does **not** publish its PSC split, oil price, annual cash flows, or the distribution shapes in its Monte Carlo. Oil price (US$70/bbl), the per-option contractor share, triangular shapes, the production range reading (-40%/+120%) and the price-inflation correlation are **my disclosed assumptions**.
- Each option's contractor share is **calibrated** so reconstructed NPV equals the paper's NPV. The three calibrated shares differ (0.124, 0.116, 0.098), which signals missing PSC mechanics in the simplified model.
- **The reconstruction does not reproduce the paper's downside.** It shows 0% probability of negative NPV against the paper's 10-30%, and its all-worst corner stays near zero or positive while the paper's scenario range reaches about -US$1.09M. Its all-best corner (up to US$5.6M) overshoots the paper's US$2.62M. Treat reconstruction risk figures as a demonstration of method, not as evidence about Tambura.
- Reconstructed IRR and payback differ from the paper's, most for Option-3.

## Run it

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebook.ipynb
```

Or open `docs/index.html` in a browser for the interactive simulator (no build step). Enable GitHub Pages on the `docs/` folder to host it.

## License

MIT, copyright 2026 Eka Krisna Santoso. See `LICENSE`. The source paper is CC BY-NC 4.0 and remains the authors' work.

---
Part of **The Feasibility Stress Test**: real Monte Carlo and financial-engineering case studies for capex decisions.

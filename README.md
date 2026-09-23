# Pricing Bermudan Options by Least-Squares Monte Carlo

### The In-Sample Bias, a Comparison of Regression Methods, and a Dual Upper Bound

Chan Tsz Him Chris — July 23, 2026

This repository holds the paper and the full analysis notebook for a short study of the Longstaff–Schwartz least-squares Monte Carlo (LSM) algorithm for pricing Bermudan options: why the naive in-sample estimate is biased, how much the choice of regression basis for the continuation value actually matters, and how far a cheap fitted policy sits from the true optimal price.

**Results:**
- Evaluating an exercise policy on the same paths used to fit it is optimistic by construction (a look-ahead bias); fitting on one path set and pricing on an independent set fixes this and gives a valid lower bound regardless of how good the policy is.
- Four very different regression bases for the continuation value — a degree-7 polynomial, a piecewise-linear basis, Nadaraya–Watson kernel regression, and a two-parameter Black–Scholes-price basis — produce out-of-sample lower bounds that agree to within statistical noise (\$4.109–\$4.147), despite a ~750× difference in compute time.
- An Andersen–Broadie dual upper bound built from the same fitted policy gives \$4.339 (±\$0.082), bracketing the true price to within about \$0.23 of the lower bound — evidence that even the cheapest regression choices tested are already close to optimal for this problem.

Read the paper: [`paper/Pricing Bermudan Options by Least-Squares Monte Carlo.pdf`](paper/Pricing%20Bermudan%20Options%20by%20Least-Squares%20Monte%20Carlo.pdf)

## Contents

```
.
├── bermudan_lsm.ipynb   # the single notebook — full analysis, start to finish
├── paper/
│   ├── *.pdf              # the compiled paper
│   └── main.tex           # LaTeX source
├── requirements.txt
└── README.md
```

## Running it

```bash
pip install -r requirements.txt
jupyter notebook bermudan_lsm.ipynb
```

Fully self-contained: everything is simulated (Black–Scholes Monte Carlo), no external data or credentials needed. Most cells run in well under a second; the Nadaraya–Watson kernel-regression cell takes roughly two minutes.

## Structure

The notebook mirrors the paper's own structure section by section: setup and the Longstaff–Schwartz algorithm, the in-sample bias (reproducing the source demonstration's numbers, including a flagged maturity/discounting inconsistency in that demonstration that we do not correct or rely on), the out-of-sample lower-bound proposition and its proof, a comparison of four regression methods, results, the Andersen–Broadie dual upper bound construction, and discussion/limitations.

## References

- Andersen, L., & Broadie, M. (2004). Primal-dual simulation algorithm for pricing multidimensional American options. *Management Science*, 50(9), 1222–1234.
- Broadie, M., & Glasserman, P. (1997). Pricing American-style securities using simulation. *Journal of Economic Dynamics and Control*, 21(8–9), 1323–1352.
- Carriere, J. F. (1996). Valuation of the early-exercise price for options using simulations and nonparametric regression. *Insurance: Mathematics and Economics*, 19(1), 19–30.
- Haugh, M. B., & Kogan, L. (2004). Pricing American options: a duality approach. *Operations Research*, 52(2), 258–270.
- Longstaff, F. A., & Schwartz, E. S. (2001). Valuing American options by simulation: a simple least-squares approach. *The Review of Financial Studies*, 14(1), 113–147.
- Moreno, M., & Navas, J. F. (2003). On the robustness of least-squares Monte Carlo (LSM) for pricing American derivatives. *Review of Derivatives Research*, 6(2), 107–127.
- Rogers, L. C. G. (2002). Monte Carlo valuation of American options. *Mathematical Finance*, 12(3), 271–286.
- Tsitsiklis, J. N., & Van Roy, B. (2001). Regression methods for pricing complex American-style options. *IEEE Transactions on Neural Networks*, 12(4), 694–703.

# Odds-Ratio Stats Converter

A single-file, dependency-free web tool for converting between the quantities you meet when reading genetic-epidemiology and GWAS results.

**Live:** https://lexiyao.github.io/or-stats-converter/

## What it does

Enter any *sufficient* combination and everything else recomputes live from the canonical log-odds (β) and its standard error:

- **OR ↔ log-OR (β)**
- **CI ↔ SE** (95% by default; 90 / 99 / custom supported)
- **SE / β ↔ two-sided p-value** (Wald z)
- **Paste a reported string** — e.g. `OR 2.00 (95% CI 1.25–3.20)` — and it fills OR + CI for you

Outputs: OR, log-OR (β), SE, Wald z, two-sided p, and the confidence interval at the chosen level.

## Method notes

- Confidence intervals use the **Wald (log-normal)** approximation: symmetric on the log scale, `CI = exp(β ± z_crit · SE)`. Derived SE/CI are approximate reconstructions and will **not** exactly match profile-penalised-likelihood or exact intervals (e.g. Firth / `logistf`).
- Normal CDF via Abramowitz–Stegun 7.1.26; inverse normal via Acklam's algorithm. Accuracy ≈ 1e-7.

## Development

Everything lives in `index.html` — HTML, CSS, and JavaScript, no build step and no external dependencies. Open it in any browser.

The math core and input-resolution logic were unit-tested (34 assertions against known reference values: `z_crit(95%) = 1.959964`, two-sided p for z = 1.96 ≈ 0.04998, CI↔SE round-trips, parser formats) before being embedded.

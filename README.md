# Monetary and Exchange Rate Stability in Armenia, 1994–2024

An empirical study of whether Armenia's disinflation was matched by stability in its
exchange rate — and a worked example of a correlation that was wrong, how I found out,
and what it taught me.

Written in Python (pandas, matplotlib) as a first-year master's project in economics.

---

## The question

Armenia went from 3,374% inflation in 1994 to low single digits today. That much is well
known. The question here is narrower: **did external stability follow internal stability?**

A central bank can deliver low domestic inflation and still preside over a currency that
moves with every external shock. The two are different achievements, and conflating them
is easy, because the headline inflation number improves in both cases.

## What the notebook does

1. Loads annual Armenian inflation and exchange rate data (World Bank).
2. Computes the rate of depreciation of the dram, so that it can be compared with a rate
   of inflation.
3. Describes both series over the full sample and over the post-stabilisation sample.
4. Measures the *volatility* of each series with rolling five-year standard deviations,
   rather than its level.
5. Exports a summary table of volatility by period.

## Findings

**Internal stability was achieved and held.** Inflation volatility falls from the hundreds
to roughly 3 by the 2000s, and never returns.

**External stability was not, in the same sense.** The volatility of the depreciation rate
falls from about 16 to about 6, then rises again to about 8 during the 2010s. It is not a
steady convergence.

This matters because every post-Soviet economy disinflated after the 1990s. The fall in
inflation alone says little that is specific to Armenia; the divergence between the two
kinds of stability does.

**On the link between the two:** the correlation between depreciation and inflation is
clear only in the hyperinflation years. After stabilisation, annual data show almost no
relationship. With 31 annual observations and no identification strategy, this project
cannot distinguish genuinely weak exchange rate pass-through from the limits of annual
averages — and does not claim to.

---

## The methodological correction

The first version of this analysis correlated the **inflation rate** with the
**exchange rate level**, in drams per dollar. The result was **−0.40**: a weaker currency
apparently came with lower inflation. For an economy that imports most of what it consumes,
that is not plausible.

The error was comparing a rate of change with a level. The exchange rate rose from 289 to
579 drams per dollar over the period — a trending series. Any trending level will correlate
mechanically with a declining rate, whatever the underlying economics. The number was real;
it just measured the meeting of two trends.

Expressing both variables as rates of change gives **+0.66** — the expected sign, since
depreciation raises import prices.

The sign flipped because the specification changed, not because the data did. I have kept
this prominent rather than quietly fixing it, because the diagnosis is the part of this
project I would defend.

A second correction concerns the inflation chart. A linear axis is unusable here: the 1994
value of 3,374% flattens every other year into a line at zero. A plain logarithmic axis
cannot be used either, because it has no room for zero or negative values, and Armenia had
deflation in 2000 (−0.8%) and 2016 (−1.4%) — a log scale drops those two years silently.
The chart therefore uses a symmetric log scale, linear between −1 and +1 and logarithmic
beyond, with a line marking zero so deflation years stay visible.

---

## Running it

```
pip install pandas matplotlib
jupyter notebook monetary_stability_armenia.ipynb
```

Run the cells in order. The data files are in the repository, so no download is needed.

## Contents

| File | |
|---|---|
| `monetary_stability_armenia.ipynb` | The analysis |
| `inflation.csv` | Annual inflation, World Bank |
| `exchange.csv` | Annual exchange rate, drams per US dollar, World Bank |
| `volatility_by_period.csv` | Produced by the notebook |

## Limitations

- 31 annual observations. Too few for anything beyond description.
- No identification strategy: nothing here establishes causality in either direction.
- Annual averages are coarse for exchange rate pass-through, which operates over months.
- A proper study would need monthly or quarterly data, an identified monetary policy shock,
  and a comparison group such as Georgia or Moldova.

## Context

First-year master's coursework, Economics and Finance, Université Lyon 2. A follow-up
project extends this question to a panel of eight post-communist economies, estimated with
country-level vector autoregressions.

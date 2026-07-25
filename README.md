# Perpify — Gap Risk Methodology

Public artifacts behind [gap.perpify.trade](https://gap.perpify.trade): the reopen-gap
statistics and calibration data for [Perpify](https://www.perpify.trade), an onchain
perpetual futures exchange for assets that stop trading — starting with the S&P 500.

**Markets close. Risk doesn't.** Over 31 years of SPY data (7,936 sessions, 1995–2026):

- **28.5%** of sessions open with a gap larger than 0.5% — more than 1 in 4
- **1 in 11** sessions gap more than 1%; 1.9% gap more than 2%
- Weekend/holiday reopens are **20.7%** of sessions but produced **5 of the 10 largest gaps**
- Worst reopen in the dataset: **−10.45%** (Monday, March 16, 2020)
- Weekend gap variance is **1.55×** weeknight variance (σ 0.81% vs 0.65%)

## Reproduce every number

```bash
pip install pandas numpy
python3 risk/gap/gap_stats.py
```

Dataset: SPY daily OHLC, unadjusted, 1995-01-04 → 2026-07-17, in `risk/data/spy_daily.csv`
(refresh with `risk/gap/fetch_data.py`). Gap = today's open ÷ previous close − 1.
A reopen is classed weekend/holiday when the previous session is ≥3 calendar days back.

## A correction, published on purpose

Earlier Perpify materials claimed "38% of trading days open with a gap larger than 0.5%."
Calibrating against the full series measured **28.5%**, and we corrected every document.
A venue whose product is published, replayable methodology cannot carry an unverifiable
stat — including its own.

## Layout

```
risk/gap/gap_stats.py    reopen-gap statistics (prints every number cited above)
risk/gap/fetch_data.py   dataset refresh script
risk/data/spy_daily.csv  SPY daily OHLC, 1995–2026
site/index.html          the live gap monitor (deployed to gap.perpify.trade)
```

— Aakash Mittal · [perpify.trade](https://www.perpify.trade) · [@aakashneeraj](https://x.com/aakashneeraj)

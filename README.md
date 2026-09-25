# How much demand is coming?

**A planning problem, solved with time series.**

Capacity, roster, inventory, and cash all sit on a **guess about next year**. I help teams turn history into a **demand outlook with a range** — not a single number nobody trusts.

---

## The stake

Under-forecast and you lose sales or burn staff. Over-forecast and you pay for idle capacity. Seasonal peaks make averages dangerous. Leaders need **one place to argue with**: trend + season + uncertainty.

## The story

Airline passenger volumes rise over time and **swing with the seasons**. The job: forecast the next 12 months and **check yourself** on held-out months.

I built a classic forecast loop:

1. **See the pattern** — trend, seasonality, leftovers  
2. **Model** history (train)  
3. **Forecast 12 months** with confidence bands  
4. **Score it** on real months you held back  

**Outcome on this build:**
- Seasonal peaks tracked instead of averaged away  
- **Point forecast + interval** (`yhat`, `yhat_lower`, `yhat_upper`) for planning  
- Validation on 2023 holdout so the story is not just a pretty curve  

> **The commercial idea:** plan capacity against a **range you can defend**, not a gut-feel peak.

---

## What that looks like in your world

| You have | I turn it into |
|----------|----------------|
| Monthly/weekly history | **Forecast + confidence band** |
| “Summer always kills us” | Explicit **seasonality** in the plan |
| Spreadsheet extrapolations | Model + **holdout honesty** |
| Ops / finance planning cycle | A shared demand assumption |

**Typical engagement:** define the horizon and unit (passengers, orders, tickets) → fit and validate → a planning pack for ops and finance.

**[Talk to me about demand planning →](https://datafying.co/#contactus)** · [datafying](https://datafying.co/)

---

## Why operators bring me in

- Speaks **capacity and cost**, not ARIMA acronyms  
- Shows **intervals** so people plan risk, not fantasy  
- One clear seasonal story for the leadership deck  
- Honest about holidays, shocks, and regime change  

---

## Proof of craft *(technical)*

### Job
Monthly airline passengers → **12-month** forecast with intervals.

### Method
1. Additive decomposition (period = 12) — trend / seasonal / residual  
2. Prophet on train (pre-2023)  
3. Forecast horizon = one full seasonal cycle  
4. Compare to test (2023+)  

### Outputs
| Column | Meaning |
|--------|---------|
| `yhat` | Point forecast |
| `yhat_lower` / `yhat_upper` | Uncertainty band (e.g. 80%) |

### Modelling choices
- **Additive** seasonality (amplitude does not scale with level)  
- **12-month horizon** — validate a full cycle without wild extrapolation  
- **Default Prophet** — yearly seasonality was enough here  

### Limits (honesty)
- Historical patterns can break (pandemic, price shocks)  
- No causal drivers in this build (fares, routes, marketing)  
- Re-forecast on a cadence; don’t freeze last year’s chart  

---

## Reproduce

```bash
git clone https://github.com/47096/demand-forecast.git
cd demand-forecast
pip install -r requirements.txt
jupyter notebook analysis.ipynb
```

**Data:** Monthly international airline passengers (public series).

**Stack:** `prophet` · `statsmodels` · `pandas` · `matplotlib`

---

## Next step

If planning week is coming up and the forecast is a spreadsheet guess — that is the engagement I run.

**[Book a conversation →](https://datafying.co/#contactus)** · Customer & demand analytics · [datafying](https://datafying.co/)

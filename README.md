# Problem-Set-4

## Handover note: store revenue model

**What it predicts.** Monthly revenue per store ($k) from floor area, foot traffic, local median income and years open, with a quadratic floor-area term for diminishing returns. The other columns in the old model carried no signal.

**What "0.94" meant.** In-sample R², which can only rise as columns are added. It never tested forecasting, and the old straight-line fit over-forecast the largest stores by about $14k a month.

**Honest error.** Nested cross-validation (selection repeated inside each fold) gives an RMSE of **$13.6k per store-month**, 95% interval **$12.6k–$14.6k**, about 3–4% of revenue. Error grows with size, to roughly $19k above 3,500 sq ft, so report it by size band, not as one number.

**It will fail when:**
1. **A store exceeds the sizes it was trained on.** Beyond roughly 4,500 sq ft, data are sparse and the quadratic extrapolates badly.
2. **The world shifts.** It was fit on one snapshot and never tested forward in time, so it gives no warning when traffic or income relationships change, as they did in July.

**What I would build next.** Score the model once on the latest months, held out in time. Replace the quadratic with a log or spline that flattens rather than turns down, and model log revenue so the growing spread is handled. Track error monthly by size band, alerting when large-store over-forecast returns.

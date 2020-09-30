---
title: Benjamin Graham
date: ''
slug: benjamin-graham

---
Original:

V = (EPS * (8.5 + 2g) * 4.4) / Y

V: Intrinsic value

8\.5: Price to earnings ratio for a company with 0% growth

EPS: Current earnings per share

g: (Return on equity, 10 years ago / current return on equity)^(1/10))-1

4\.4: Bond rate at the time the equation was written

Y: Current 20 year corporate bond rate

Original equation is using outdated bond rates. The static weightings (8.5 and 2) may need to be re-figured to optimize for a weekly or monthly time series analysis. 

Baseline:

V = (EPS * (PE ratio + (ROE growth)) / current bond rate) - resulting figure

Try different weightings.
---
title: Benjamin Graham
date: ''
slug: benjamin-graham

---
<iframe width="100%" height="50%" frameborder="0" scrolling="no" src="//plotly.com/~ayako0/5.embed"></iframe>

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

See if equation for several picked stocks can follow SPX baseline.

Try:

Value 1 = (EPS * ((PE ratio > 8.5) + (ROE growth rate * .01))

Current bond rate = (current bond rate * .01)

Value 2 = Value 1 * Current bond rate

Final = Value 1 + Value 2

Try different weightings.

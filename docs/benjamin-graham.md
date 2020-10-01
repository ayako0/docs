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

See if equation for several picked stocks can follow SPX baseline.

Try:

Value 1 = (EPS * ((PE ratio > 8.5) + (ROE growth rate * .01))

Current bond rate = (current bond rate * .01)

Value 2 = Value 1 * Current bond rate

Final = Value 1 + Value 2

Try different weightings.

<div>
    <a href="https://plotly.com/~ayako0/1/?share_key=h4KTXitEFu9J9zWbMOMch4" target="_blank" title="Plot 1" style="display: block; text-align: center;"><img src="https://plotly.com/~ayako0/1.png?share_key=h4KTXitEFu9J9zWbMOMch4" alt="Plot 1" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plotly.com/404.png';" /></a>
    <script data-plotly="ayako0:1" sharekey-plotly="h4KTXitEFu9J9zWbMOMch4" src="https://plotly.com/embed.js" async></script>
</div>

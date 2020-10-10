---
title: Valuation Ratios
date: ''
slug: valuation-ratios

---
## Book Value per Share

_(Assets - liabilities) / common shares outstanding_

Find stocks with highest book value per share.

[book_value_per_share](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#book-value-per-share)

Returns: **50.6%**, Drawdown: **-66.95%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/61.embed?link=false&modebar=false&logo=false"></iframe>

```python
import quantopian.algorithm as algo
from quantopian.pipeline import Pipeline
from quantopian.pipeline.filters import Q3000US
from quantopian.pipeline.data.morningstar import Fundamentals as ms
import quantopian.optimize as opt

import numpy as np
import pandas as pd


def initialize(context):
    context.FINE_FILTER = 5
    context.stock_weights = pd.Series()
    algo.attach_pipeline(make_pipeline(context), 'pipeline')

    schedule_function(
        stocks_weights,
        date_rules.week_start(),
        time_rules.market_open()
    )

    schedule_function(
        trade,
        date_rules.week_start(),
        time_rules.market_open()
    )


def make_pipeline(context):
    univ = Q3000US()
    factor = ms.book_value_per_share.latest.rank(mask=univ, ascending=False)
    top = factor.top(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'top': top}, screen=univ)
    return pipe


def stocks_weights(context, data):
    df = algo.pipeline_output('pipeline')
    rule = 'top'
    stocks_to_hold = df.query(rule).index
    stock_weight = 1.0 / context.FINE_FILTER
    context.stocks_weights = pd.Series(index=stocks_to_hold, data=stock_weight)


def trade(context, data):
    target_weights = opt.TargetWeights(context.stocks_weights)

    constraints = []
    constraints.append(opt.MaxGrossExposure(1.0))

    order_optimal_portfolio(
        objective=target_weights,
        constraints=constraints
    )
```

## Book Value Yield

_(Assets - liabilities) / close price_

Find stocks with highest book value yield.

[book_value_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#book-value-yield)

Returns: **99.36%**, Drawdown: **-81.77%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/63.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.book_value_yield.latest.rank(mask=univ, ascending=False)
```

## Cash Return

_(Cash flow operations - capital expenditures) / enterprise value_

Find stocks with highest cash return.

[cash_return](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#cash-return)

Returns: **66.02%**, Drawdown: **-90.42%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/65.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.cash_return.latest.rank(mask=univ, ascending=False)
```

## Earning Yield

_(Diluted earnings / common shares outstanding) / close price_

Find stocks with highest earning yield.

[earning_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#earning-yield)

Returns: **-92.55%**, Drawdown: **-98.6%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/67.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.earning_yield.latest.rank(mask=univ, ascending=False)
```

## Enterprise Value to EBITDA

_(Common equity + preferred equity + minority equity + total debt - cash and cash equivalents) / net income - (interest + tax + deprecation + amortization)_

Find stocks with highest enterprise value to EBITDA.

[ev_to_ebitda](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ev-to-ebitda)

Returns: -**33.7%**, Drawdown: **-74.49%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/69.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.ev_to_ebitda.latest.rank(mask=univ, ascending=False)
```

## Free Cash Flow Yield

_(Cash flow operations - capital expenditures / common shares outstanding) / close price_

Find stocks with highest free cash flow yield.

[fcf_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#fcf-yield)

Returns: **-71.49%**, Drawdown: **-92.66%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/71.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.fcf_yield.latest.rank(mask=univ, ascending=False)
```

## Price to Book Ratio

_Close price / (assets - liabilities)_

Find stocks with highest price to book ratio.

[pb_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#pb-ratio)

Returns: **-24.46%**, Drawdown: **-96.45%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/73.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.pb_ratio.latest.rank(mask=univ, ascending=False)
```

## Price to Earnings Ratio

_Close price / (net income / common shares outstanding)_

Find stocks with highest price to earnings ratio.

[pe_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#pe-ratio)

Returns: **117.09%**, Drawdown: **-86.27%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/75.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.pe_ratio.latest.rank(mask=univ, ascending=False)
```

## Price to Sales Ratio

_Close price / (revenue / common shares outstanding)_

Find stocks with highest price to sales ratio.

[ps_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ps-ratio)

Returns: **1270.05%**, Drawdown: **-58.17%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/77.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.ps_ratio.latest.rank(mask=univ, ascending=False)
```

## Sales Yield

_(Revenue / common shares outstanding) / close price_

Find stocks with highest sales yield.

[sales_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#sales-yield)

Returns: **-15.34%**, Drawdown: **-75.64%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/79.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.sales_yield.latest.rank(mask=univ, ascending=False)
```

## Sustainable Growth Rate

_Net income / total common equity * (1 - dividend per share / diluted earnings per share)_

Find stocks with highest sustainable growth rate.

[sustainable_growth_rate](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#sustainable-growth-rate)

Returns: **191.16%**, Drawdown: **-64.75%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/81.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.sustainable_growth_rate.latest.rank(mask=univ, ascending=False)
```

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5, equally weighted

Max leverage: 1

Universe: Quantopian Q3000US dataset

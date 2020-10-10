---
title: Valuation
date: ''
slug: valuation

---
## Enterprise Value

_Common equity + preferred equity + minority equity + total debt - cash and cash equivalents_

Find stocks with highest enterprise value.

[enterprise_value](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#enterprise-value)

Returns: **325.52%**, Drawdown: **-71.93%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/59.embed?link=false&modebar=false&logo=false"></iframe>

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
    factor = ms.enterprise_value.latest.rank(mask=univ, ascending=False)
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

## Market Cap

_Common shares outstanding * share price_

[market_cap](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#market-cap)

## Shares Outstanding

_Number of common shares issued_

[shares_outstanding](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#shares-outstanding)

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5, equally weighted

Max leverage: 1

Universe: Quantopian Q3000US dataset

---
title: Balance Sheet
date: ''
slug: balance-sheet

---
## Cash and Cash Equivalents

_Cash + immediately liquid instruments_

Find stocks with highest cash and cash equivalents.

[cash_and_cash_equivalents](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#cash-and-cash-equivalents "cash_and_cash_equivalents")

Returns: **-51.42%**, Drawdown: **-77.4%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

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
    factor = ms.cash_and_cash_equivalents.latest.rank(mask=univ, ascending=False)
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

## Total Assets

_Tangible and intangible value_

Find stocks with highest total assets.

[total_assets](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-assets "total_assets")

Returns: **-51.27%**, Drawdown: **-83.72%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.total_assets.latest.rank(mask=univ, ascending=False)
```

## Total Equity

_Assets - liabilities_

Find stocks with highest total equity.

[total_equity](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-equity "total_equity")

Returns: **185.64%**, Drawdown: **-78.54%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.total_equity.latest.rank(mask=univ, ascending=False)
```

## Total Debt

_Current and long-term debts owed_

Ideally, we find stocks with low debt.

[total_debt](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-debt "total_debt")

Returns: **52.21%**, Drawdown: **-53.81%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
def make_pipeline(context):
    univ = Q3000US()
    factor = ms.total_debt.latest.rank(mask=univ, ascending=True)
    bottom = factor.bottom(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'bottom': bottom}, screen=univ)
    return pipe


def stocks_weights(context, data):
    df = algo.pipeline_output('pipeline')
    rule = 'bottom'
```

We can also find stocks with high debt.

Returns: **-21.78%**, Drawdown: **-75.52%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
def make_pipeline(context):
    univ = Q3000US()
    factor = ms.total_debt.latest.rank(mask=univ, ascending=False)
    top = factor.top(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'top': top}, screen=univ)
    return pipe
```

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5, equally weighted

Max leverage: 1

Universe: Quantopian Q3000US dataset
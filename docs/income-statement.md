---
title: Income Statement
date: 
slug: income-statement

---
## Depreciation and Amortization

_Reduction of book value in the degradation of assets_

Find stocks with lowest depreciation and amortization..

[depreciation_and_amortization_income_statement](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#depreciation-and-amortization-income-statement)

Returns: **33%**, Drawdown: **-55%**, Benchmark (S&P 500): **250%**

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
    factor = ms.depreciation_and_amortization_income_statement.latest.rank(mask=univ, ascending=True)
    bottom = factor.bottom(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'bottom': bottom}, screen=univ)
    return pipe


def stocks_weights(context, data):
    df = algo.pipeline_output('pipeline')
    rule = 'bottom'
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

## EBITDA

_Net income - (interest + tax + deprecation + amortization)_

Find stocks with highest earnings before interest, tax, depreciation and amortization.

[ebitda](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ebitda)

Returns: **33%**, Drawdown: **-55%**, Benchmark (S&P 500): **250%**

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
    factor = ms.ebitda.latest.rank(mask=univ, ascending=False)
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

## Net Income

_Revenue - expenses_

Find stocks with highest net income.

[net_income_income_statement](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#net-income-income-statement)

Returns: **33%**, Drawdown: **-55%**, Benchmark (S&P 500): **250%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.net_income_income_statement.latest.rank(mask=univ, ascending=False)
```

## Operating Income

_Revenue - expenses - income from investing activities_

Find stocks with highest operating income.

[operating_income](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#operating-income)

Returns: **33%**, Drawdown: **-55%**, Benchmark (S&P 500): **250%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.operating_income.latest.rank(mask=univ, ascending=False)
```

## Tax Rate Used for Calculations

[tax_rate_for_calcs](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#tax-rate-for-calcs)

## Total Revenue

_Income as produced by sales_

Find stocks with highest total revenue.

[total_revenue](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-revenue)

Returns: **33%**, Drawdown: **-55%**, Benchmark (S&P 500): **250%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/5.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.total_revenue.latest.rank(mask=univ, ascending=False)
```

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5, equally weighted

Max leverage: 1

Universe: Quantopian Q3000US dataset
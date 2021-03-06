---
title: Operation Ratios
date: ''
slug: operation-ratios

---
## Current Ratio

_Current assets / current liabilities_

Find stocks with the highest current ratio.

Returns: **78.55%**, Drawdown: **-70.61%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/37.embed?link=false&modebar=false&logo=false"></iframe>

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
    factor = ms.current_ratio.latest.rank(mask=univ, ascending=False)
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

## Net Income Growth

_((Net income current - net income from previous quarter) / net income current) * 100_

Find stocks with the highest net income growth.

Returns: **61.41%**, Drawdown: **-72.47%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/39.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.net_income_growth.latest.rank(mask=univ, ascending=False)
```

## Net Margin

_Net income / revenue_

Find stocks with the highest net margin.

Returns: **16.2%**, Drawdown: **-84.68%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/41.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.net_margin.latest.rank(mask=univ, ascending=False)
```

## Operation Revenue Growth, Three Month Average

_((Operation revenue current - operation revenue from previous quarter) / operation revenue current) * 100_

Find stocks with the highest operation revenue growth.

Returns: **358.41%**, Drawdown: **-86.73%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/43.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.operation_revenue_growth3_month_avg.latest.rank(mask=univ, ascending=False)
```

## Quick Ratio

_Liquidity / liabilities_

Find stocks with the highest quick ratio.

Returns: **317.22%**, Drawdown: **-58.24%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/45.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.quick_ratio.latest.rank(mask=univ, ascending=False)
```

## Revenue Growth

_((Revenue current - revenue from previous quarter) / revenue current) * 100_

Find stocks with the highest revenue growth.

Returns: **211.05%**, Drawdown: **-87.44%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/47.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.revenue_growth.latest.rank(mask=univ, ascending=False)
```

## Return on Assets (ROA)

_Net income / total assets_

Find stocks with the highest return on assets.

Returns: -**62.16%**, Drawdown: **-85.02%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/49.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.roa.latest.rank(mask=univ, ascending=False)
```

## Return on Equity (ROE)

_Net income / total common equity_

Find stocks with the highest return on equity.

Returns: **24.3%**, Drawdown: **-87.77%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/51.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.roe.latest.rank(mask=univ, ascending=False)
```

## Return on Invested Capital (ROIC)

_Net income / (total equity + total debt and capital lease obligation)_

Find stocks with the highest return on invested capital.

Returns: **36.25%**, Drawdown: **-72.09%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/53.embed?link=false&modebar=false&logo=false"></iframe>

```python
factor = ms.roic.latest.rank(mask=univ, ascending=False)
```

## Total Debt to Equity Ratio

_Total debt / common equity_

Find stocks with the lowest** debt to equity ratio.

Returns: **100.86%**, Drawdown: **-31.12%**, Benchmark (S&P 500): **276.95%**

<iframe width="100%" height="300px" frameborder="0" scrolling="no" src="//plotly.com/\~ayako0/55.embed?link=false&modebar=false&logo=false"></iframe>

```python
def make_pipeline(context):
    univ = Q3000US()

    debt_eq_low = ms.total_debt_equity_ratio.latest < 0.5
    debt_eq_hi = ms.total_debt_equity_ratio.latest > 0.5

    factor = ms.total_debt_equity_ratio.latest.rank(mask=debt_eq_low, ascending=True)
    #factor = ms.total_debt_equity_ratio.latest.rank(mask=debt_eq_hi, ascending=False)
    top = factor.top(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'top': top}, screen=univ)
    return pipe
```

_Historical fundamental data:_

_Start to end: Jan 2nd, 2006 to Sep 1st, 2020_

_Starting capital: $10000_

_Number of stocks: 5, equally weighted_

_Max leverage: 1_

_Universe: Quantopian Q3000US dataset_

\** See [Total Debt](https://annayakowenko.com/balance-sheet#total-debt).
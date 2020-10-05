---
title: Operation Ratios
date: ''
slug: operation-ratios

---
## Current Ratio

_Current assets / current liabilities_

Find stocks with highest current ratio.

[current_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#current-ratio)

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
        factor = ms.free_cash_flow.latest.rank(mask=univ, ascending=False)
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

Find stocks with highest net income growth.

[net_income_growth](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#net-income-growth)

```python
    factor = ms.net_income_growth.latest.rank(mask=univ, ascending=False)
```

## Net Margin

_Net income / revenue_

Find stocks with highest net margin.

[net_margin](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#net-margin)

```python
    factor = ms.net_margin.latest.rank(mask=univ, ascending=False)
```

## Operation Revenue Growth, Three Month Average

_((Operation revenue current - operation revenue from previous quarter) / operation revenue current) * 100_

Find stocks with highest operation revenue growth.

[operation_revenue_growth3_month_avg](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#operation-revenue-growth3-month-avg)

```python
    factor = ms.operation_revenue_growth3_month_avg.latest.rank(mask=univ, ascending=False)
```

## Quick Ratio

_Liquidity / liabilities_

Find stocks with highest quick ratio.

[quick_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#quick-ratio)

```python
    factor = ms.quick_ratio.latest.rank(mask=univ, ascending=False)
```

## Revenue Growth

_((Revenue current - revenue from previous quarter) / revenue current) * 100_

Find stocks with highest revenue growth.

[revenue_growth](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#revenue-growth)

```python
    factor = ms.revenue_growth.latest.rank(mask=univ, ascending=False)
```

## Return on Assets (ROA)

_Net income / total assets_

Find stocks with highest return on assets.

[roa](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#roa)

```python
    factor = ms.roa.latest.rank(mask=univ, ascending=False)
```

## Return on Equity (ROE)

_Net income / total common equity_

Find stocks with highest return on equity.

[roe](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#roe)

```python
    factor = ms.roe.latest.rank(mask=univ, ascending=False)
```

## Return on Invested Capital (ROIC)

_Net income / (total equity + total debt and capital lease obligation)_

Find stocks with highest return on invested capital.

[roic](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#roic)

```python
    factor = ms.roic.latest.rank(mask=univ, ascending=False)
```

## Total Debt to Equity Ratio

_Common shares outstanding - total debt_

Find stocks with highest** debt to equity ratio.

[total_debt_equity_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-debt-equity-ratio)

A balance of debt to equity may be optimal.

```python
    def make_pipeline(context):
        univ = Q3000US()
    
        debt_eq_low = ms.total_debt_equity_ratio.latest < 0.5
        debt_eq_med = 0.5 < ms.total_debt_equity_ratio.latest < 2
        debt_eq_hi = ms.total_debt_equity_ratio.latest > 2
    
        factor = ms.debt_eq_low.latest.rank(mask=univ, ascending=False)
        #factor = ms.debt_eq_med.latest.rank(mask=univ, ascending=False)
        #factor = ms.debt_eq_hi.latest.rank(mask=univ, ascending=False)
        top = factor.top(context.FINE_FILTER)
        pipe = Pipeline(
            columns={'top': top}, screen=univ)
        return pipe
```

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5

Max leverage: 1

Universe: Quantopian Q3000US dataset

\** See [Total Debt](https://annayakowenko.com/balance-sheet#total-debt).
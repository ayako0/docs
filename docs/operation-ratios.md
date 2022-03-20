---
title: Operation Ratios
date: ""
slug: operation-ratios
---

### Current Ratio

<div>
  <p>(Current assets / current liabilities)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest current ratio values
    weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/124.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 78.55%
            <br />
            Drawdown: -70.61%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

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

  </div>

### Net Income Growth

  <p>
    (((Net income current - net income from previous quarter) / net income
    current) * 100)
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest percentages of net income
    growth weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/126.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 61.41%
            <br />
            Drawdown: -72.47%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.net_income_growth.latest.rank(mask=univ, ascending=False)
```

  </div>

### Net Margin

  <p>(Net income / revenue)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest net margin values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/128.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 16.2%
            <br />
            Drawdown: -84.68%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.net_margin.latest.rank(mask=univ, ascending=False)
```

  </div>

### Operation Revenue Growth, Three Month Average

  <p>
    (((Operation revenue current - operation revenue from previous quarter) /
    operation revenue current) * 100)
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest percentages of operation
    revenue growth weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/130.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 358.41%
            <br />
            Drawdown: -86.73%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.operation_revenue_growth3_month_avg.latest.rank(mask=univ, ascending=False)
```

  </div>

### Quick Ratio

  <p>(Liquidity / liabilities)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest quick ratio values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/132.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 317.22%
            <br />
            Drawdown: -58.24%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.quick_ratio.latest.rank(mask=univ, ascending=False)
```

  </div>

### Revenue Growth

  <p>
    (((Revenue current - revenue from previous quarter) / revenue current) *
    100)
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest percentages of revenue
    growth weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/134.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 211.05%
            <br />
            Drawdown: -87.44%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.revenue_growth.latest.rank(mask=univ, ascending=False)
```

  </div>

### Return on Assets (ROA)

  <p>(Net income / total assets)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest return on assets (ROA)
    values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/136.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -62.16%
            <br />
            Drawdown: -85.02%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.roa.latest.rank(mask=univ, ascending=False)
```

  </div>

### Return on Equity (ROE)

  <p>(Net income / total common equity)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest return on equity (ROE)
    values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/138.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 24.3%
            <br />
            Drawdown: -87.77%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.roe.latest.rank(mask=univ, ascending=False)
```

  </div>

### Return on Invested Capital (ROIC)

  <p>(Net income / (total equity + total debt and capital lease obligation))</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest return on invested capital
    (ROIC) values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/140.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 36.25%
            <br />
            Drawdown: -72.09%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
factor = ms.roic.latest.rank(mask=univ, ascending=False)
```

  </div>

### Total Debt to Equity Ratio

  <p>(Total debt / common equity)</p>

  <p class="mb4">
    An algorithm that trades stocks with the lowest debt to equity ratio values
    weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/142.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 100.86%
            <br />
            Drawdown: -31.12%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pt1 pb3">
          <div class="notes">Benchmark (S&P 500): 276.95%</div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">

```python
def make_pipeline(context):
    univ = Q3000US()

    debt_eq_low = ms.total_debt_equity_ratio.latest < 0.5
    #debt_eq_hi = ms.total_debt_equity_ratio.latest > 0.5

    factor = ms.total_debt_equity_ratio.latest.rank(mask=debt_eq_low, ascending=True)
    #factor = ms.total_debt_equity_ratio.latest.rank(mask=debt_eq_hi, ascending=False)
    top = factor.top(context.FINE_FILTER)
    pipe = Pipeline(
        columns={'top': top}, screen=univ)
    return pipe
```

  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <div class="footnotes">
        Terms:
        <br />
        1. Current Ratio
        <a href="https://www.investopedia.com/terms/c/currentratio.asp">
          Investopedia
        </a>
        <br />
        2. Net Income Growth
        <a href="https://www.investopedia.com/terms/n/netincome.asp">
          Investopedia
        </a>
        <br />
        3. Net Margin
        <a href="https://www.investopedia.com/terms/n/net_margin.asp">
          Investopedia
        </a>
        <br />
        4. Operation Revenue Growth
        <a href="https://www.investopedia.com/terms/o/operating-revenue.asp">
          Investopedia
        </a>
        <br />
        5. Quick Ratio
        <a href="https://www.investopedia.com/terms/q/quickratio.asp">
          Investopedia
        </a>
        <br />
        6. Revenue
        <a href="https://www.investopedia.com/terms/r/revenue.asp">
          Investopedia
        </a>
        <br />
        7. Return on Assets (ROA)
        <a href="https://www.investopedia.com/terms/r/returnonassets.asp">
          Investopedia
        </a>
        <br />
        8. Return on Equity (ROE)
        <a href="https://www.investopedia.com/terms/r/returnonequity.asp">
          Investopedia
        </a>
        <br />
        9. Return on Invested Capital (ROIC)
        <a href="https://www.investopedia.com/terms/r/returnoninvestmentcapital.asp">
          Investopedia
        </a>
        <br />
        10. Debt to Equity Ratio
        <a href="https://www.investopedia.com/terms/d/debtequityratio.asp">
          Investopedia
        </a>
        <br />
        <br />
        <br />
        Statements on this website are for informational purposes only and do
        not constitute a recommendation or advice by the website owner to
        transact any security or market instrument. All trading activity
        involves known and unknown risk. Historical data presented is not always
        indicative of future performance.
      </div>
    </div>
  </div>
</div>

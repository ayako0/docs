---
title: Balance Sheet
date: ""
slug: balance-sheet
---

### Cash and Cash Equivalents

<div>
  <p>(Cash + immediately liquid instruments)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest values of cash and cash
    equivalents weekly.
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
          src="//plotly.com/~ayako0/96.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -51.42%
            <br />
            Drawdown: -77.4%
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

  </div>

### Total Assets

  <p>Tangible and intangible value.</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest values of total assets
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
          src="//plotly.com/~ayako0/106.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -51.27%
            <br />
            Drawdown: -83.72%
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
factor = ms.total_assets.latest.rank(mask=univ, ascending=False)
```

  </div>

### Total Equity

  <p>(Assets - liabilities)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest values of total equity
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
          src="//plotly.com/~ayako0/176.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 185.64%
            <br />
            Drawdown: -78.54%
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
factor = ms.total_equity.latest.rank(mask=univ, ascending=False)
```

  </div>

### Total Debt

  <p>Current and long-term debts owed.</p>

  <p class="mb4">
    An algorithm that trades stocks with the lowest debt weekly.
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
          src="//plotly.com/~ayako0/180.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 52.21%
            <br />
            Drawdown: -53.81%
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
  factor = ms.total_debt.latest.rank(mask=univ, ascending=True)
  bottom = factor.bottom(context.FINE_FILTER)
  pipe = Pipeline(
      columns={'bottom': bottom}, screen=univ)
  return pipe

def stocks_weights(context, data):
df = algo.pipeline_output('pipeline')
rule = 'bottom'
```

  </div>

  <p>An algorithm that trades stocks with the highest debt weekly.</p>

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
          src="//plotly.com/~ayako0/178.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -21.78%
            <br />
            Drawdown: -75.52%
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
    factor = ms.total_debt.latest.rank(mask=univ, ascending=False)
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
        1. Cash and Cash Equivalents
        <a href="https://www.investopedia.com/terms/c/cashandcashequivalents.asp">
          Investopedia
        </a>
        <br />
        2. Asset
        <a href="https://www.investopedia.com/terms/a/asset.asp">
          Investopedia
        </a>
        <br />
        3. Equity
        <a href="https://www.investopedia.com/terms/e/equity.asp">
          Investopedia
        </a>
        <br />
        4. Net Debt
        <a href="https://www.investopedia.com/terms/n/netdebt.asp">
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

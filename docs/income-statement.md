---
title: Income Statement
date:
slug: income-statement
---

### Depreciation and Amortization

<div>
  <p>A reduction of book value in the degradation of assets.</p>

  <p class="mb4">
    An algorithm that trades stocks with the lowest depreciation and
    amortization values weekly.
  </p>

  <div class="clearfix">
  <div class="relative">
    <div class="border-box">
    <p class="date mt0">
      Starting capital: $10,000
      <br />
      Max leverage: 1<br />
      Jan 2, 2006 - Sep 1, 2020
    </p>
  </div>
  </div>
  </div>
  <div class="clearfix mb4a">
    <div class="relative ml0 xs-col xs-col-9">
      <div class="border-box pr2a">
        <iframe
          width="100%"
          height="240px"
          frameborder="0"
          scrolling="no"
          src="//plotly.com/~ayako0/114.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 224.14%
            <br />
            Drawdown: -51.22%
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

  </div>

### EBITDA

  <p>(Net income - (interest + tax + deprecation + amortization))</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest earnings before interest,
    tax, depreciation and amortization (EBITDA) values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10,000
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
          src="//plotly.com/~ayako0/116.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -72.07%
            <br />
            Drawdown: -90.2%
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

  </div>

### Net Income

  <p>(Revenue - expenses)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest net income values weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10,000
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
          src="//plotly.com/~ayako0/118.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -62.58%
            <br />
            Drawdown: -88.95%
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
factor = ms.net_income_income_statement.latest.rank(mask=univ, ascending=False)
```

  </div>

### Operating Income

  <p>(Revenue - expenses - income from investing activities)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest operating income values
    weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10,000
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
          src="//plotly.com/~ayako0/120.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -59.4%
            <br />
            Drawdown: -90.75%
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
factor = ms.operating_income.latest.rank(mask=univ, ascending=False)
```

  </div>

### Total Revenue

  <p>Income as produced by sales.</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest total revenue values
    weekly.
  </p>

  <div class="clearfix">
    <p class="date mt0">
      Starting capital: $10,000
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
          src="//plotly.com/~ayako0/122.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 95.16%
            <br />
            Drawdown: -76.52%
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
factor = ms.total_revenue.latest.rank(mask=univ, ascending=False)
```

  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <div class="footnotes">
        Terms:
        <br />
        1. Depreciation and Amortization
        <a href="https://www.investopedia.com/ask/answers/06/amortizationvsdepreciation.asp">
          Investopedia
        </a>
        <br />
        2. EBITDA
        <a href="https://www.investopedia.com/terms/e/ebitda.asp">
          Investopedia
        </a>
        <br />
        3. Net Income
        <a href="https://www.investopedia.com/terms/n/netincome.asp">
          Investopedia
        </a>
        <br />
        4. Operating Income
        <a href="https://www.investopedia.com/terms/o/operatingincome.asp">
          Investopedia
        </a>
        <br />
        5. Total Revenue
        <a href="https://www.investopedia.com/terms/r/revenue.asp">
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

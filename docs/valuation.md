---
title: Valuation
date: ""
slug: valuation
---

### Enterprise Value

<div>
  <p>
    (Common equity + preferred equity + minority equity + total debt - cash and
    cash equivalents)
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest enterprise values weekly.
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
          src="//plotly.com/~ayako0/144.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 325.52%
            <br />
            Drawdown: -71.93%
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

  </div>

### Market Cap

  <p>(Common shares outstanding * share price)</p>

### Shares Outstanding

  <p>The number of common shares issued.</p>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <div class="footnotes">
        Terms:
        <br />
        1. Enterprise Value
        <a href="https://www.investopedia.com/terms/e/enterprisevalue.asp">
          Investopedia
        </a>
        <br />
        2. Market Cap
        <a href="https://www.investopedia.com/terms/m/marketcapitalization.asp">
          Investopedia
        </a>
        <br />
        3. Shares Outstanding
        <a href="https://www.investopedia.com/terms/o/outstandingshares.asp">
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

---
title: Valuation Ratios
date: ""
slug: valuation-ratios
---

### Tangible Book Value per Share

<div>
  <p>
    ((Assets - liabilities - intangible assets) / common shares outstanding)
  </p>

### Book Value per Share

  <p>((Assets - liabilities) / common shares outstanding)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest book value per share values
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
          src="//plotly.com/~ayako0/146.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 50.6%
            <br />
            Drawdown: -66.95%
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

  </div>

### Book Value Yield

  <p>((Assets - liabilities) / close price)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest book value yield values
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
          src="//plotly.com/~ayako0/148.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 99.36%
            <br />
            Drawdown: -81.77%
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
factor = ms.book_value_yield.latest.rank(mask=univ, ascending=False)
```

  </div>

### Cash Return

  <p>((Cash flow operations - capital expenditures) / enterprise value)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest cash return values weekly.
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
          src="//plotly.com/~ayako0/150.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 66.02%
            <br />
            Drawdown: -90.42%
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
factor = ms.cash_return.latest.rank(mask=univ, ascending=False)
```

  </div>

### Earning Yield

  <p>((Diluted earnings / common shares outstanding) / close price)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest earning yield values
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
          src="//plotly.com/~ayako0/152.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -92.55%
            <br />
            Drawdown: -98.6%
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
factor = ms.earning_yield.latest.rank(mask=univ, ascending=False)
```

  </div>

### Enterprise Value to EBITDA

  <p>
    ((Common equity + preferred equity + minority equity + total debt - cash and
    cash equivalents) / net income - (interest + tax + deprecation +
    amortization))
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest enterprise value to EBITDA
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
          src="//plotly.com/~ayako0/154.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -33.7%
            <br />
            Drawdown: -74.49%
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
factor = ms.ev_to_ebitda.latest.rank(mask=univ, ascending=False)
```

  </div>

### Free Cash Flow Yield

  <p>
    ((Cash flow operations - capital expenditures / common shares outstanding) /
    close price)
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest free cash flow yield values
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
          src="//plotly.com/~ayako0/156.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -71.49%
            <br />
            Drawdown: -92.66%
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
factor = ms.fcf_yield.latest.rank(mask=univ, ascending=False)
```

  </div>

### Price to Book Ratio

  <p>(Close price / (assets - liabilities))</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest price to book ratio values
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
          src="//plotly.com/~ayako0/164.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -24.46%
            <br />
            Drawdown: -96.45%
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
factor = ms.pb_ratio.latest.rank(mask=univ, ascending=False)
```

  </div>

### Price to Earnings Ratio

  <p>(Close price / (net income / common shares outstanding))</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest price to earnings ratio
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
          src="//plotly.com/~ayako0/166.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 117.09%
            <br />
            Drawdown: -86.27%
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
factor = ms.pe_ratio.latest.rank(mask=univ, ascending=False)
```

  </div>

### Price to Sales Ratio

  <p>(Close price / (revenue / common shares outstanding))</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest price to sales ratio values
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
          src="//plotly.com/~ayako0/168.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 1,270.05%
            <br />
            Drawdown: -58.17%
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
factor = ms.ps_ratio.latest.rank(mask=univ, ascending=False)
```

  </div>

### Sales Yield

  <p>((Revenue / common shares outstanding) / close price)</p>

  <p class="mb4">
    An algorithm that trades stocks with the highest sales yield values weekly.
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
          src="//plotly.com/~ayako0/170.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: -15.34%
            <br />
            Drawdown: -75.64%
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
factor = ms.sales_yield.latest.rank(mask=univ, ascending=False)
```

  </div>

### Sustainable Growth Rate

  <p>
    (Net income / total common equity * (1 - dividend per share / diluted
    earnings per share))
  </p>

  <p class="mb4">
    An algorithm that trades stocks with the highest sustainable growth rate
    percentages weekly.
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
          src="//plotly.com/~ayako0/172.embed?link=false&modebar=false&logo=false"
        ></iframe>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3 mt-s">
      <div class="border-box">
        <div class="flex bt pt1 pb3">
          <div class="notes">
            Returns: 191.16%
            <br />
            Drawdown: -64.75%
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
factor = ms.sustainable_growth_rate.latest.rank(mask=univ, ascending=False)
```

  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <div class="footnotes">
        Terms:
        <br />
        1. Tangible Book Value per Share
        <a href="https://www.investopedia.com/terms/t/tbvps.asp">
          Investopedia
        </a>
        <br />
        2. Book Value per Share
        <a href="https://www.investopedia.com/terms/b/bvps.asp">Investopedia</a>
        <br />
        3. Earning Yield
        <a href="https://www.investopedia.com/terms/e/earningsyield.asp">
          Investopedia
        </a>
        <br />
        4. Enterprise Value to EBITDA
        <a href="https://www.investopedia.com/terms/e/ev-ebitda.asp">
          Investopedia
        </a>
        <br />
        5. Free Cash Flow Yield
        <a href="https://www.investopedia.com/terms/f/freecashflowyield.asp">
          Investopedia
        </a>
        <br />
        6. Price to Book Ratio
        <a href="https://www.investopedia.com/terms/p/price-to-bookratio.asp">
          Investopedia
        </a>
        <br />
        7. Price to Earnings Ratio
        <a href="https://www.investopedia.com/terms/p/price-earningsratio.asp">
          Investopedia
        </a>
        <br />
        8. Price to Sales Ratio
        <a href="https://www.investopedia.com/terms/p/price-to-salesratio.asp">
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

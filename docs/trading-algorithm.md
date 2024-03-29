---
title: Trading Algorithm
slug: trading-algorithm
---

  <div class="clearfix mb4">
    <div class="relative md-col md-col-8">
      <div class="border-box">
        <h2 class="mt0 pr2">Optimized Momentum Trading</h2>
      </div>
    </div>
  </div>

  <div class="clearfix flex">
    <div class="relative md-col md-col-4 push">
      <div class="border-box">
        <div class="flex bt pb2 pt2">
          <div>
            Returns: 29,923.07%
            <br />
            Drawdown: -39.77%
          </div>
          <div class="push pl1">
            <span class="lg" />
          </div>
        </div>
        <div class="flex bt pb2 pt2">
          <div>
            Benchmark (S&P 500): 288.21%
          </div>
          <div class="push pl1">
            <span class="lh" />
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="clearfix">
    <p class="date">Sep 1, 2002 - Oct 5, 2020</p>
  </div>

  <div class="clearfix full-width mb4">
    <iframe
      width="100%"
      height="300px"
      frameborder="0"
      scrolling="no"
      src="//plotly.com/~ayako0/104.embed?link=false&modebar=false&logo=false">
    </iframe>
  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <p class="intro">
        An algorithm optimized for long-only, non-leveraged trading
        with backtested percentage performance similar to Apple from Sep 1,
        2002 - Oct 5, 2020, using real-time market data from the Morningstar
        universe.
      </p>
      <p>
        Using fundamental factors and momentum strategies the algorithm ranks
        all stocks in the dataset and chooses the top five to trade weekly,
        outperforming most long term held stocks in the NYSE within the time
        frame at a percentage gain of 29,923.07%.
      </p>
      <p>
        Slope, beta and linear regression methods<sup>1</sup> were chosen to
        measure technical signals, responsively attending to short term price velocities over moving average applications
        (more often used for time series modeling).
      </p>
    </div>
  </div>

  <div class="clearfix mb4" style="max-width: 44rem">
    <div class="relative ml0 xs-col xs-col-2">
      <div class="border-box mt2 mb2">
        <p>+</p>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3">
      <div class="border-box mt2 mb2">
        <div class="clearfix">
          <div class="grid-sq-120">
            <div class="frame"></div>
            <div class="center">01</div>
          </div>
          <div>
            <p class="caption">1.</p>
          </div>
        </div>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-3">
      <div class="border-box mt2 mb2">
        <div class="clearfix">
          <div class="grid-sq-120">
            <div class="frame"></div>
            <div class="center">02</div>
          </div>
          <div>
            <p class="caption">2.</p>
          </div>
        </div>
      </div>
    </div>
    <div class="relative ml0 xs-col xs-col-4">
      <div class="border-box mt2 mb2">
        <p class="notes">
          1. Linear regression: (Y ∼ α + βX)
          <br />Y is distributed as alpha plus beta X
        </p>
        <p class="notes">
          2. SimpleBeta(): The slope of the regression line between an asset's
          returns and another asset's returns
        </p>
      </div>
    </div>
  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      The algorithm starts by measuring weekly S&P 500 beta with all existing
      assets<sup>2</sup> within the Quantopian dataset and simultaneously ranks defined fundamental factors of
      all stocks in the Morningstar universe, then associates the top
      fundamentally-based selection or the alpha of the selection with the given
      beta conditions, which are then traded in the current week. Using linear
      regression data with the selected securities previous five days closing
      prices optimized price performance, indicating that price momentum in the
      week prior continues to the currently traded week.
    </div>
  </div>

<div class="clearfix">

```python
fundamental_factor = ms.fundamental_factor.latest > 0.5
spy_beta = SB(target=context.SPY, regression_length=context.bars_5)
```

</div>

  <div class="clearfix code-caption mb4">Partial code sample</div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <p>
        It was found that certain groups of stocks performed optimally with
        certain conditions - a 'growth'-focused selection performed best under
        positive S&P 500 beta conditions; a 'value' selection performed
        best under negative S&P 500 beta conditions. Growth and value lists can
        both be best defined as stable companies where
        growth focuses more on fundamental value percentage growth.
      </p>
      <p>
        Tuesday trade execution provided the greatest returns.
      </p>
      <p>
        Under monthly negative price action or weekly sharp drops, bonds are
        purchased instead of stocks to stabilize the portfolio. In the instance
        of the market crash of 2008-09, long term damage was prevented
        by increasing the initial value of growth.
      </p>
      <p>
        During the time period, only Netflix (NFLX) and Monster (MNST) outperformed the
        algorithm.
      </p>
    </div>
  </div>

  <div class="clearfix mb4">
    <div class="md-col-8">
      <div class="footnotes">
        Notes:
        <br />
        1. Linear regression, SimpleBeta
        <a
          href="https://quantopian-archive.netlify.app/notebooks/notebooks/quantopian_notebook_1.html"
          class="mb0 mt0"
        >
          Building a Better Beta
        </a>
        <br />
        2. SimpleBeta
        <a
          href="https://github.com/quantopian/zipline/blob/master/zipline/pipeline/factors/statistical.py"
          class="mb0 mt0"
        >
          Github
        </a>
        <br />
        3. Quantopian Pipeline and rankings
        <a href="https://www.youtube.com/watch?v=J8RzPVtW4X8" class="mb0 mt0">
          Introducing the Quantopian Pipeline API
        </a>
        <br />
        4. Slippage and commission were set to zero so that stats of the
        algorithm's core focus on fundamentals and technical performance could
        be measured.
        <br />
        5. S&P 500 beta is measured weekly.
        <br />
        6. MaximizeAlpha is a proprietary function to Quantopian, described as an
        optimization that correlates a combined factor ranking to expected
        returns, emphasizing those securities with the highest expected return.
        <a
          href="https://github.com/quantopian/research_public/blob/master/template_algorithms/long_short_equity_template.py"
          class="mb0 mt0"
        >
          Github
        </a>
        <br />
        <br />
        <br />
        Statements on this website are for informational purposes only and do not constitute a recommendation or advice by the website owner to transact any security or market instrument. All trading activity involves known and unknown risk. Historical data presented is not always indicative of future performance.
      </div>
    </div>
  </div>

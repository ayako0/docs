---
title: Valuation Ratios
date: ''
slug: valuation-ratios

---
## Book Value per Share

_(Assets - liabilities) / common shares outstanding_

Find stocks with highest book value per share.

[book_value_per_share](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#book-value-per-share)

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
        target_weights = opt.MaximizeAlpha(context.stocks_weights)
    
        constraints = []
        constraints.append(opt.MaxGrossExposure(1.0))
    
        order_optimal_portfolio(
            objective=target_weights,
            constraints=constraints
        )

## Book Value Yield

_(Assets - liabilities) / close price_

Find stocks with highest book value yield.

[book_value_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#book-value-yield)

    factor = ms.book_value_yield.latest.rank(mask=univ, ascending=False)

## Cash Return

_(Cash flow operations - capital expenditures) / enterprise value_

Find stocks with highest cash return.

[cash_return](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#cash-return)

    factor = ms.cash_return.latest.rank(mask=univ, ascending=False)

## Earning Yield

_(Diluted earnings / common shares outstanding) / close price_

Find stocks with highest earning yield.

[earning_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#earning-yield)

    factor = ms.earning_yield.latest.rank(mask=univ, ascending=False)

## Enterprise Value to EBITDA

_(Common equity + preferred equity + minority equity + total debt - cash and cash equivalents) / net income - (interest + tax + deprecation + amortization)_

Find stocks with highest enterprise value to EBITDA.

[ev_to_ebitda](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ev-to-ebitda)

    factor = ms.ev_to_ebitda.latest.rank(mask=univ, ascending=False)

## Free Cash Flow Yield

_(Cash flow operations - capital expenditures / common shares outstanding) / close price_

Find stocks with highest free cash flow yield.

[fcf_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#fcf-yield)

    factor = ms.fcf_yield.latest.rank(mask=univ, ascending=False)

## Forward Earning Yield

_(Next year's estimate for diluted earnings / common shares outstanding) / close price_

Find stocks with highest forward earning yield.

[forward_earning_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#forward-earning-yield)

    factor = ms.forward_earning_yield.latest.rank(mask=univ, ascending=False)

## Price to Book Ratio

_Close price / (assets - liabilities)_

Find stocks with highest price to book ratio.

[pb_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#pb-ratio)

    factor = ms.pb_ratio.latest.rank(mask=univ, ascending=False)

## Price to Earnings Ratio

_Close price / (net income / common shares outstanding)_

Find stocks with highest price to earnings ratio.

[pe_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#pe-ratio)

    factor = ms.pe_ratio.latest.rank(mask=univ, ascending=False)

## Price to Sales Ratio

_Close price / (revenue / common shares outstanding)_

Find stocks with highest price to sales ratio.

[ps_ratio](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ps-ratio)

    factor = ms.ps_ratio.latest.rank(mask=univ, ascending=False)

## Sales Yield

_(Revenue / common shares outstanding) / close price_

Find stocks with highest sales yield.

[sales_yield](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#sales-yield)

    factor = ms.sales_yield.latest.rank(mask=univ, ascending=False)

## Sustainable Growth Rate

_Net income / total common equity * (1 - dividend per share / diluted earnings per share)_

Find stocks with highest sustainable growth rate.

[sustainable_growth_rate](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#sustainable-growth-rate)

    factor = ms.sustainable_growth_rate.latest.rank(mask=univ, ascending=False)
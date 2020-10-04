---
title: Valuation
date: ''
slug: valuation

---
## Enterprise Value

Common equity + preferred equity + minority equity + total debt - cash and cash equivalents

Find stocks with highest enterprise value.

enterprise_value

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
        target_weights = opt.MaximizeAlpha(context.stocks_weights)
    
        constraints = []
        constraints.append(opt.MaxGrossExposure(1.0))
    
        order_optimal_portfolio(
            objective=target_weights,
            constraints=constraints
        )

## Market Cap

Common shares outstanding * share price

Find stocks with highest market cap.

market_cap

    factor = ms.market_cap.latest.rank(mask=univ, ascending=False)

## Shares Outstanding

shares_outstanding

Find stocks with highest shares outstanding.

    factor = ms.shares_outstanding.latest.rank(mask=univ, ascending=False)
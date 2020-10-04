---
title: Balance Sheet
date: ''
slug: balance-sheet

---
## Cash and Cash Equivalents

_Cash + immediately liquid instruments_

Find stocks with highest cash and cash equivalents.

[cash_and_cash_equivalents](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#cash-and-cash-equivalents "cash_and_cash_equivalents")

    import quantopian.algorithm as algo
    from quantopian.pipeline import Pipeline
    from quantopian.pipeline.filters import Q3000US
    from quantopian.pipeline.data.morningstar import Fundamentals as ms
    import quantopian.optimize as opt
    
    import numpy as np
    import pandas as pd
    
    
    def initialize(context):
        set_commission(commission.PerTrade(cost=0.00))
        set_slippage(slippage.FixedSlippage(spread=0.00))
    
        context.SPY = symbol('SPY')
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
        target_weights = opt.MaximizeAlpha(context.stocks_weights)
    
        constraints = []
        constraints.append(opt.MaxGrossExposure(1.0))
    
        order_optimal_portfolio(
            objective=target_weights,
            constraints=constraints
        )

## Total Assets

_Tangible and intangible value_

Find stocks with highest total assets.

[total_assets](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-assets "total_assets")

    factor = ms.total_assets.latest.rank(mask=univ, ascending=False)

## Total Equity

_Assets - liabilities_

Find stocks with highest total equity.

[total_equity](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-equity "total_equity")

    factor = ms.total_assets.latest.rank(mask=univ, ascending=False)

## Total Debt

_Current and long-term debts owed_

In theory, we find stocks with lowest debt.

[total_debt](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-debt "total_debt")

    def make_pipeline(context):
        univ = Q3000US()
        factor = ms.total_debt.latest.rank(mask=univ, ascending=True)
        bottom = factor.bottom(context.FINE_FILTER)
        pipe = Pipeline(
            columns={'bottom': bottom}, screen=univ)
        return pipe

We can also find stocks with high debt.

    def make_pipeline(context):
        univ = Q3000US()
        factor = ms.total_debt.latest.rank(mask=univ, ascending=True)
        top = factor.top(context.FINE_FILTER)
        pipe = Pipeline(
            columns={'top': top}, screen=univ)
        return pipe

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5

Max leverage: 1
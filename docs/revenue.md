---
title: Income Statement
date: 
slug: income-statement

---
## Depreciation and Amortization

_(Assets - liabilities) - cost and degradation of assets_

Find stocks with lowest depreciation and amortization.

[depreciation_and_amortization_income_statement](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#depreciation-and-amortization-income-statement)

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
        factor = ms.free_cash_flow.latest.rank(mask=univ, ascending=False)
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
        target_weights = opt.MaximizeAlpha(context.stocks_weights)
    
        constraints = []
        constraints.append(opt.MaxGrossExposure(1.0))
    
        order_optimal_portfolio(
            objective=target_weights,
            constraints=constraints
        )

## EBITDA

_Net income - (interest + tax + deprecation + amortization)_

Find stocks with highest earnings before interest, tax, depreciation and amortization.

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
        target_weights = opt.MaximizeAlpha(context.stocks_weights)
    
        constraints = []
        constraints.append(opt.MaxGrossExposure(1.0))
    
        order_optimal_portfolio(
            objective=target_weights,
            constraints=constraints
        )

[ebitda](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#ebitda)

## Net Income

_Revenue - expenses_

Find stocks with highest net income.

    factor = ms.net_income_income_statement.latest.rank(mask=univ, ascending=False)

[net_income_income_statement](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#net-income-income-statement)

## Operating Income

_Revenue - expenses - income from investing activities_

Find stocks with highest operating income.

    factor = ms.operating_income.latest.rank(mask=univ, ascending=False)

[operating_income](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#operating-income)

## Tax Rate Used for Calculations

[tax_rate_for_calcs](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#tax-rate-for-calcs)

## Total Revenue

_Income as produced by sales_

Find stocks with highest total revenue.

    factor = ms.total_revenue.latest.rank(mask=univ, ascending=False)

[total_revenue](https://www.quantopian.com/docs/data-reference/morningstar_fundamentals#total-revenue)

_All fundamental testing algos have the following attributes:_

Start to end: 01/02/2006 - 09/01/2020

Starting capital: $10000

Number of stocks: 5

Max leverage: 1
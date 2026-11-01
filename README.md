```{=html}
<p align="center">
```
`<img src="https://img.shields.io/badge/QUANT-BTC%20DEMAC-111827?style=for-the-badge" alt="Quant BTC DEMAC">`{=html}
`<img src="https://img.shields.io/badge/PLATFORM-MetaTrader%205-0066A1?style=for-the-badge&logo=metatrader5&logoColor=white" alt="MetaTrader 5">`{=html}
`<img src="https://img.shields.io/badge/LANGUAGE-MQL5-2563EB?style=for-the-badge" alt="MQL5">`{=html}
`<img src="https://img.shields.io/badge/STRATEGY-10%2F20%20EMA-7C3AED?style=for-the-badge" alt="10/20 EMA">`{=html}
```{=html}
</p>
```
```{=html}
<h1 align="center">
```
₿ Quant-BTC-DEMAC-Engine
```{=html}
</h1>
```
```{=html}
<h3 align="center">
```
A systematic Bitcoin directional trading engine powered by dual-EMA
crossover logic.
```{=html}
</h3>
```
```{=html}
<p align="center">
```
`<em>`{=html}Turning market signals into structured, rule-based
execution.`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## ⚡ At a glance

  ----------------------------------- -----------------------------------
  **Project**                         Quantitative BTC Directional
                                      Allocation Engine

  **Trading platform**                MetaTrader 5

  **Implementation**                  MQL5 --- confirm against the
                                      uploaded source file

  **Core strategy**                   10/20 EMA crossover and directional
                                      reversal

  **Intended market**                 BTC trading instrument offered by
                                      the broker

  **Primary timeframe**               Daily (1D), as described in the
                                      strategy specification

  **Project status**                  Development / testing --- update
                                      when verified
  ----------------------------------- -----------------------------------

> **Important:** This repository documents a trading-system
> implementation, not a promise of returns. All performance figures must
> come from reproducible tests on the actual code.

## 01 --- The idea

**Quant-BTC-DEMAC-Engine** is an algorithmic trading project built
around a simple quantitative premise: use the relationship between a
faster and a slower exponential moving average to identify changes in
directional market momentum, then translate those signals into
systematic position transitions.

The strategy compares:

-   **10-period EMA:** the faster trend component.
-   **20-period EMA:** the slower trend component.
-   **EMA spread:** the difference between the two values, used to
    identify bullish and bearish crossovers.

The objective is to reduce discretionary decision-making by defining
explicit signal conditions and a repeatable execution process.

## 02 --- Strategy mechanics

### The core calculation

The exponential moving average is defined as:

\[ EMA_t = `\alpha `{=tex}P_t + (1-`\alpha`{=tex})EMA\_{t-1} \]

where:

\[ `\alpha `{=tex}= `\frac{2}{N+1}`{=tex} \]

-   (P_t): closing price at time (t)
-   (N): EMA lookback period
-   (EMA\_{t-1}): previous EMA value

The strategy's directional spread is:

\[ Spread_t = EMA\_{10}(t)-EMA\_{20}(t) \]

### Signal rules

  -----------------------------------------------------------------------
  Condition               Interpretation          Intended transition
  ----------------------- ----------------------- -----------------------
  (Spread_t \> 0) and     Bullish crossover       Long
  (Spread\_{t-1}                                  
  `\leq 0`{=tex})                                 

  (Spread_t \< 0) and     Bearish crossover       Short or flat,
  (Spread\_{t-1}                                  depending on execution
  `\geq 0`{=tex})                                 configuration

  No crossover            No new directional      Maintain the existing
                          signal                  state
  -----------------------------------------------------------------------

The strategy specification describes signals based on completed bars,
with execution intended for the next bar. Confirm that this is how the
current EA is coded before treating it as a verified implementation
detail.

## 03 --- System workflow

``` mermaid
flowchart TD
    A[BTC market data] --> B[Read completed candle]
    B --> C[Calculate 10-period EMA]
    B --> D[Calculate 20-period EMA]
    C --> E[Calculate EMA spread]
    D --> E
    E --> F{Crossover detected?}
    F -->|Bullish| G[Generate long signal]
    F -->|Bearish| H[Generate bearish signal]
    F -->|No| I[Keep current state]
    G --> J[Apply execution rules]
    H --> J
    J --> K[Update position / state]
    K --> L[Wait for next evaluation]
    L --> B
```

## 04 --- Backtesting & performance

### Performance dashboard

**No verified backtest report or numerical results have been supplied
with this README request.** The fields below are deliberately left as
placeholders rather than filled with invented performance claims.

Replace them with figures exported from the MT5 Strategy Tester after
running the exact version of the EA being published.

  Metric                                                  Verified result
  ------------------------------------ ----------------------------------
  Backtest date range                    `Add tested start and end dates`
  Trading instrument / broker symbol                   `Add exact symbol`
  Timeframe                                        `Add tested timeframe`
  Initial deposit                               `Add amount and currency`
  Net profit                                 `Add Strategy Tester result`
  Return (%)                                      `Add calculated return`
  Profit factor                              `Add Strategy Tester result`
  Maximum equity drawdown (%)                `Add Strategy Tester result`
  Total trades                               `Add Strategy Tester result`
  Win rate (%)                               `Add Strategy Tester result`
  Expected payoff                            `Add Strategy Tester result`

### Backtest evidence

Add the following once available:

1.  MT5 Strategy Tester **Overview** screenshot.
2.  **Results** or **Deals** export showing individual trades.
3.  **Graph** screenshot showing balance and equity.
4.  Exact EA version, symbol, timeframe, date range, deposit, leverage
    and modelling settings.

### What makes a backtest credible?

A headline return is not enough. A useful evaluation should also
disclose:

-   Spread, commission and swap assumptions.
-   Modelling quality and available historical tick data.
-   Maximum balance and equity drawdown.
-   Number of trades and exposure time.
-   Out-of-sample or forward-test performance.
-   Whether parameters were selected using the same period being
    reported.

> **Performance integrity:** Backtest results are historical
> simulations. They are not live results, and they do not guarantee
> future performance. Do not publish annualised returns, win rates,
> profit factors or drawdowns unless they can be reproduced from the
> test report.

## 05 --- Strategy parameters

  Parameter           Strategy specification Description
  ----------------- ------------------------ ---------------------------------
  Fast EMA period                       `10` Faster trend measurement
  Slow EMA period                       `20` Slower trend measurement
  Timeframe                             `1D` Daily analysis interval
  Signal                       EMA crossover Directional transition
  Execution                Next bar intended Confirm in source code
  Instrument               BTC broker symbol Exact symbol may vary by broker

## 06 --- MetaTrader 5 setup

### Requirements

-   MetaTrader 5 desktop terminal.
-   MetaEditor.
-   A broker account or demo environment that provides the intended BTC
    instrument.
-   The EA source file (`.mq5`) and any required project dependencies.

### Install

1.  Open MetaTrader 5.
2.  Select **File → Open Data Folder**.
3.  Open `MQL5 → Experts` (if the source is an Expert Advisor).
4.  Copy the `.mq5` file into that folder.
5.  Open MetaEditor and open the source file.
6.  Compile using **F7** and review the compiler output.
7.  In MT5, open **Navigator → Expert Advisors**, refresh if necessary,
    and attach the EA to the intended chart.
8.  Test in the **Strategy Tester** before considering any live use.

The actual broker symbol may not be named `BTCUSD` or `BTC/USD`. Select
the exact symbol available in the broker's Market Watch.

## 07 --- Risk & operational considerations

Moving-average crossover systems can perform poorly in sideways markets,
where repeated crossovers may create whipsaw trades. Cryptocurrency
markets can also experience abrupt volatility, gaps in liquidity, spread
widening and slippage.

Before live deployment, verify:

-   Position sizing and maximum exposure.
-   Stop-loss and exit behaviour, if implemented.
-   Handling of rejected orders and trade errors.
-   Spread, commission and swap effects.
-   Duplicate-signal prevention.
-   Behaviour after terminal restart or connection loss.
-   Whether the account is hedging or netting, and how reversals behave
    under that mode.

**Do not assume the EA has these safeguards until they have been
confirmed in its source code and tested.**

## 08 --- Repository structure

``` text
Quant-BTC-DEMAC-Engine/
├── README.md
├── <your-expert-advisor>.mq5
├── backtests/
│   ├── README.md
│   └── <add-exported-reports-and-evidence>
└── .gitignore
```

Keep broker credentials, account numbers, API keys, private logs and
other sensitive information out of the repository.

## 09 --- Roadmap

Potential areas for future development:

-   [ ] Verify and document all live EA parameters.
-   [ ] Add reproducible MT5 backtest reports.
-   [ ] Add configurable position sizing.
-   [ ] Evaluate stop-loss and take-profit approaches.
-   [ ] Test volatility and sideways-market filters.
-   [ ] Perform out-of-sample and forward testing.
-   [ ] Add execution diagnostics and trade logging.
-   [ ] Compare results across symbols and market regimes.

## 10 --- Disclaimer

This project is provided for educational, research and
software-development purposes only. It is not investment advice or a
solicitation to trade. Cryptocurrency and leveraged products involve
substantial risk, including the possible loss of capital. Simulated
historical performance does not guarantee future results. Users are
responsible for validating the code, broker settings and risk controls
before use.

------------------------------------------------------------------------

```{=html}
<p align="center">
```
`<strong>`{=html}QUANT-BTC-DEMAC-ENGINE`</strong>`{=html}`<br>`{=html}
`<em>`{=html}Define the signal. Test the system. Measure the
outcome.`</em>`{=html}
```{=html}
</p>
```

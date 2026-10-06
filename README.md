# Quant Strategy Research

Summary of strategies I've researched and backtested. Everything uses real historical data: ticks, trades and L2 order books. Signals, parameters and P&L are left out.

## How I test

1. Check that the effect actually exists in the data
2. Simulate fills against real L2 books: would a passive order have filled, where was it in the queue, and how bad was the adverse selection
3. Check the data itself, to separate real dislocations from archive gaps and frozen feeds
4. Estimate capacity and market impact
5. Look at the biggest trades to see whether profit comes from a few suspicious ones
6. Walk-forward and out-of-sample tests, and how results change from fold to fold
7. Paper trade before using real money

## Studies

Linked rows have a full write-up with charts.

| Strategy | Data | Result |
|---|---|---|
| [Perp vs dated future basis, z-score mean reversion](studies/basis-reversion.md) | Deribit ticks and L2 | Passed every stage across a 10-config sweep. Small but real edge, limited by fill rate |
| [Perp vs quarterly basis reversion on another venue](studies/fill-rate.md) | Exchange L2 | Real short-term signal, but passive fills on the future leg were too rare. Dropped |
| Cross-venue quarterly spread market making | L2 from two venues | Lost money after fees on every parameter set. Dropped |
| Cross-venue calendar spread | Testnet and archives | Built, execution questions still open |
| Short-horizon prediction market making (BTC, commodities) | Live order books | Small bots running live with tight risk limits. Hedged and taker versions didn't work |
| Prediction market option-style pricer | Venue trades and options implied vol | Shelved. Replaying the archive showed the backtest fill model was quietly using future information |
| SMA trend following on 35 tokens | OHLCV and order flow | Only BTC held up. Running as a paper variant |
| [Mean reversion, breakout, 24-token rotation](studies/overfitting.md) | OHLCV | Dropped. Rotation looked strong in sample and lost money out of sample, a textbook overfit |
| [Binance Alpha token dip buying and market making](studies/binance-alpha.md) | Klines and trade prints | Dropped. Early edge was selection bias and fills with no real volume behind them |
| [Prediction market venue-wide search](https://github.com/mjaun556-svg/prediction-market-research) | L2 recorder, resolved markets, trade tape | Dropped. Price-history edges vanished on the real tape, reward market making about zero |
| [Cricket exchange market making](https://github.com/mjaun556-svg/cricket-market-making-sim) | Cricsheet ball-by-ball | Model works. Quotes need near-instant updates, so nothing was funded |
| CEX-DEX arbitrage | On-chain pool and CEX data | The low-fee pool is already fully arbitraged. The higher-fee pool shows real gaps, sizing not done yet |

## Takeaways

- The fill model matters more than the signal. Two backtests that looked profitable lost money once fills were simulated against real queues.
- Check the data first. Several price spikes that looked tradeable were archive gaps or stale quotes.
- Look at per-fold results, not the full-period average. The average overstated what was repeatable.

Code is proprietary. More of my work: [work-portfolio](https://github.com/mjaun556-svg/work-portfolio)

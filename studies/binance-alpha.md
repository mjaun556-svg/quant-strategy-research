# Binance Alpha Token Market Making

Binance Alpha lists early-stage tokens, many bridged from DEX liquidity. The idea was simple: buy sharp dips and sell the bounce, or make markets around the touch. I tested it in three rounds using the public kline and trade APIs.

| Round | Tokens | Result per trade after fees |
|---|---|---|
| 1. Top 15 by current volume, best settings | 15 | +0.9 to +2.3% |
| 2. 24 thin tokens, settings fixed in advance | 24 | +0.14%, 9 of 24 tokens negative |
| 3. 15 established, liquid tokens, same settings | 15 | -0.16%, 24% win rate |

Round 1 was selection bias. I picked the tokens using the same window I tested on, then picked the best settings.

Round 2 looked slightly positive until I checked the fills against real trade prints. Many of the dips the backtest bought had only $10 to $1,000 of real volume in that minute, so a real order would not have filled. Some trades also sat on 60 to 80% drawdowns along the way.

Round 3 was the test of whether the round 2 edge was real. On liquid tokens it disappeared and went negative, so it was a liquidity artifact.

On top of that, our execution setup had no route to trade Alpha tokens. Two independent reasons to stop.

[Back to all studies](../README.md)

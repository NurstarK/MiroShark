# Simulation vs Backtest — Where Each Earns Its Complexity

*2026-09-15 — MiroShark angle*

Backtesting and scenario simulation both promise to tell you something about the future by running a model on something that isn't live market data. That's roughly where the similarity ends. Conflating them is one of the more expensive mistakes in quantitative work — and in the broader world of agentic forecasting, the confusion is spreading fast.

## What's happening

The backtesting critique is not new, but it's sharpening. A 2026 CFA Institute refresher reading flags the canonical failure modes — survivorship bias, look-ahead bias, data-snooping — as persistent even as backtesting platforms grow more sophisticated. Transaction costs and slippage alone, practitioners estimate, erode 20–50% of backtested returns in live trading. The tools have gotten better; the fundamental limit hasn't moved.

At the same time, a clutch of academic papers in 2025–2026 are formalizing a different track: simulation as a forecasting substrate that preserves path dependence and interacting agents without tethering the run to historical data. ForecastBench-Sim (arXiv 2606.18686) explicitly frames simulation as a "complementary route to real-world evaluation, preserving partial information, interacting agents, and hidden future states while giving evaluators control over resolution and interventions." That's not a backtest. It's a different epistemic instrument.

The gap matters most in two conditions: when the strategy under study is novel enough that historical data contains no close analogs, and when the actors in the market are responsive — meaning the strategy itself, once deployed, changes the landscape it's navigating. Backtesting assumes the world doesn't notice you. Simulation can make the world notice.

AI trading agent research is running into this hard. A widely-shared 2026 post documenting losses from 47 AI trading agents noted that "hard-coded bots designed to fit historical data perfectly have zero capacity to handle new market regimes." The failure mode is identical to what classic quant blowups look like: great in-sample, catastrophic out-of-sample. Simulation doesn't fix this automatically — but it asks the right question, which is: what if the regime changes, and what does that distribution look like?

## Why it matters

Backtesting and simulation have complementary failure modes. Backtesting fails when history stops being a useful proxy for the future — regime shifts, novel instruments, adversarial adaptation. Simulation fails when the actor behavior models are too simplified or when the scenario spec is underspecified. Neither is strictly superior. Treating simulation as "better backtesting" misses the point: simulation's value is in exploring the space of possible futures, not in replaying a cleaner version of the past.

The practical implication: they should run together. A backtest tells you how a strategy would have performed in a world that existed. A swarm simulation tells you what worlds might be coming and which of them break the strategy. The decision rests on the branching distribution, not the single equity curve.

## The MiroShark angle

**Swarm role-play catches what backtest data can't hold.** A backtest of a merger-arbitrage strategy against 2022 data doesn't contain a hedge fund blowing out its position in the same name three days after you enter, nor a regulatory reversal nobody saw coming. MiroShark runs parallel actor agents — traders, regulators, press, competing funds — each with distinct system prompts that encode their response functions. When the scenario orchestrator resolves their interactions, emergent dynamics surface that no historical dataset ever recorded, because those dynamics depend on the strategy being tested. Historical data is static; swarm actor agents are reactive.

**Fork probabilities replace the false certainty of the equity curve.** A backtest returns a Sharpe ratio and a drawdown. Neither tells you what the distribution of outcomes looks like if the volatility regime shifts two months after entry. MiroShark's N-run Monte Carlo across the swarm produces a branching scenario tree: branch A (regime stable, +12%) at 47%, branch B (correlated blowup, −34%) at 31%, branch C (regulatory intervention, −8% and position delisted) at 22%. The decision is now about risk tolerance across that distribution — not whether a single Sharpe of 1.4 is good enough. A backtest can't show you branch probabilities; it can only show you what happened when history ran its one path.

The pairing is the point. Run the backtest first — it's fast, cheap, and the floor of due diligence. Then run three $1 swarm sims against the scenarios your backtest can't cover: regime change, adversarial entry, regulatory event. Each sim is under 10 minutes. If none of the sims produce a distribution that's tolerable, the backtest's Sharpe ratio isn't the decision variable anymore.

## Sources

- [Backtesting & Simulation | CFA Institute](https://www.cfainstitute.org/insights/professional-learning/refresher-readings/2026/backtesting-and-simulation)
- [The Limits of Algorithmic Trading Backtesting in Quant Strategies](https://programminginsider.com/the-limits-of-algorithmic-trading-backtesting-in-quant-strategies/)
- [ForecastBench-Sim: A Simulated-World Forecasting Benchmark](https://arxiv.org/pdf/2606.18686)
- [AI Agents in Finance 2026: A CFO Guide to Reality vs Hype](https://www.houseblend.io/articles/ai-agents-finance-cfo-guide-2026)
- [I Tested 47 AI Trading Agents and Lost $11,240 — Here's How to Backtest Correctly in 2026](https://medium.com/@barbaraperezdavid474omjq5c6f/i-tested-47-ai-trading-agents-and-lost-11-240-heres-how-to-backtest-correctly-in-2026-aba092ace5fe)

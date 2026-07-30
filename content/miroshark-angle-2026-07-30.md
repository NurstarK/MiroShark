# Next to the Market: Why Traders Need a Scenario Primitive

*2026-07-30 — MiroShark angle*

Polymarket just announced the Polymarket Institute (July 29, 2026): a funded academic arm to study whether prediction markets can outperform polls and projection systems. The timing is pointed. A week before the announcement, PolyBench — a new benchmark — ran seven frontier LLMs directly against live Polymarket data. Five of seven lost money. The culprit was miscalibration: models assigned confidence of 0.8–0.9 uniformly across domains, profiting in text-rich sectors like politics and bleeding in speculative markets with no clear textual signal.

The setup reveals a gap no one's filling yet: traders have a price. What they're missing is a branching path to that price.

## What's happening

**Polymarket Institute.** On July 29, Polymarket announced a research arm led by Carnegie Mellon's Brian Jabarian as scientific director. The twelve-fellow first cohort gets $10K each to study how event markets collect information, price uncertainty, and interact with AI. Fellows can't trade during participation — an independence safeguard that inverts the normal dynamic between the platform and its researchers. Applications open August 18.

**PolyBench.** The paper (arXiv:2604.14199) tested seven LLMs on 36,165 live Polymarket predictions collected February 6–12, 2026. MiMo-V2-Flash hit 17.6% confidence-weighted return via news catalyst analysis. Gemini-3-Flash hit 6.2% through strategic diversity. The other five lost. The paper's diagnosis: LLMs freeze their confidence bands regardless of domain. In cryptocurrency markets — high volatility, low textual signal — rigid confidence is a liability.

**Agentic trading surveys.** A March 2026 audit of 77 studies on LLM trading agents found protocol incomparability: only 2 of 19 studies reported clean time-consistent splits. The empirical record for LLM-as-trader is thin and contested. But LLM-as-research-tool is a different question — and one the market structure doesn't answer.

## Why it matters

Prediction markets give you a single number — the crowd's aggregate probability at a given moment. That number is genuinely useful. Polymarket is accurate more than 94% of the time a month before resolution. But a price is not a path. It doesn't tell you how the market gets to that outcome, which branches dominate, or what triggers shift the distribution.

Traders making decisions — when to enter, when to hedge, which correlated markets to watch — need path information, not just a point estimate. PolyBench's result confirms that raw LLM confidence scores don't fill this gap. Miscalibrated confidence isn't a research tool; it's noise with a label.

## The MiroShark angle

**$1 per sim / under 10 minutes.** A trader staring at 67% odds on a political event can run a scenario sim alongside the market, not instead of it. At $1 and under 10 minutes, this is a workflow step — not a research project. The cost cap is enforced at the orchestration layer, routing actor roles to cheaper models and reserving expensive models for the resolver. Three parallel sims — "geopolitical shock hits," "status quo holds," "compromise emerges" — cost $3 and take a single coffee break. That's a stress test, not a research budget.

**Fork probabilities, not a single prediction.** Where Polymarket gives a price, MiroShark gives a scenario tree: branches, cluster probabilities, divergence points. The output format is explicitly designed to not be a point prediction. N-run Monte Carlo across a swarm of actor agents; branches surface as clusters; cluster mass becomes the probability weight. A trader using both reads the market for aggregate wisdom and reads the sim for structural path information. The 67% number tells you what the crowd believes; the branching tree tells you what conditions the winning branch assumes.

These two tools are complementary by design. One aggregates money. One simulates mechanism.

**Agent-callable via x402.** PolyBench demonstrated that LLMs can query prediction markets programmatically and attempt to trade. The logical next step is LLM agents adding scenario research to their decision stack before executing. MiroShark's x402 endpoint makes that possible without API accounts or rate-limit gating: the caller agent pays USDC, receives a scenario tree as JSON, and folds the branch probabilities into its market decision. No human in the loop. The Polymarket Institute is now funding research on exactly this intersection — how prediction markets interact with AI. The infrastructure for an agent to query both a market and a sim on the same event already exists.

## Sources

- [Polymarket launches research institute to study the future of prediction markets](https://cryptobriefing.com/polymarket-institute-prediction-markets-research/)
- [PolyBench: Benchmarking LLM Forecasting and Trading Capabilities on Live Prediction Market Data](https://arxiv.org/html/2604.14199v1)
- [Agentic Trading: When LLM Agents Meet Financial Markets](https://arxiv.org/html/2605.19337v1)
- [Prediction markets in 2026: Key trends reshaping forecasting, trading, and regulation](https://metamask.io/news/prediction-market-overview-trends-2026)

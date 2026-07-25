# When the Book Is Wrong: Swarm Simulations vs. the Aggregated Market

*2026-07-25 — MiroShark angle*

Prediction markets have a strong track record: aggregate enough capital and they tend to be right. But two recent strands of research suggest the market's edge depends on a condition that's quietly eroding — genuine diversity in the crowd making the bets.

## What's happening

A Science Advances study pitting LLM ensembles against human forecasting crowds found near-identical accuracy: Brier score of 0.20 for a 12-model LLM ensemble vs. 0.19 for the human crowd. That's not a win for either side — it's a tie, and it raises a question the paper doesn't quite answer: if LLM ensembles already match the crowd, what happens when the crowd starts using the same LLMs to form their beliefs?

The monoculture problem is showing up in the research now. A June 2026 paper ("Preference Optimization Drives Monoculture in LLM Prediction Markets") documents how RLHF fine-tuning pushes frontier models toward similar probability distributions. When models trained on similar feedback loops are used as forecasting inputs — or when traders use them as research tools — the crowd's diversity collapses. Aggregating correlated beliefs doesn't compound wisdom; it compounds the same error.

On the trading side, the picture is equally nuanced. Raven-Agent (arxiv 2607.03015) separates the forecasting problem from the trading problem and finds the disconnect is stark: strong probability estimates from LLMs don't translate into profitable trades. The paper achieves +15.9% ROI by treating belief, selection, and risk sizing as three distinct layers — with the risk controls enforced *outside* the LLM. The forecasting layer gets you in the right general direction; the architecture around it is what captures the edge.

Meanwhile, the Hindcast framework (arxiv 2607.14051) shows that when you control for information leakage — when models can't quietly absorb post-resolution data — LLMs don't dramatically outperform market prices. The market is hard to beat, and the places LLMs do beat it are the domain-specific niches where retrieval surfaces pre-resolution signal that traders missed.

## Why it matters

The conventional prediction market thesis is "aggregate enough people with skin in the game and you get calibrated probabilities." That thesis holds when the people are diverse — different methods, different priors, different information sources. When the priors start converging, the market price still looks authoritative but is actually narrower than it appears.

What the research is quietly opening up is an alternative: instead of aggregating *money* to surface beliefs, aggregate *role-play* to surface scenarios. You're not asking "what will happen?" You're asking "what would a journalist, a regulator, a competing CEO, and three Polymarket traders each do next — and what emerges from those interactions?" That's a different question, with a different answer format.

## The MiroShark angle

**Fork probabilities vs. a single market price.** Prediction markets output one number: 67% chance. MiroShark outputs a branching scenario tree — multiple branches, each with a cluster probability derived from N Monte Carlo runs across the swarm. The market price tells you where consensus sits today. The fork tree tells you which path most actors took, which paths diverged early, and which outcomes appeared in fewer than 10% of runs but aren't zero. That tail structure is invisible in a market price and is exactly what traders and analysts need when stress-testing a decision against unlikely outcomes.

**Swarm role-play where monoculture can't go.** The research on LLM monoculture identifies the problem precisely: models trained on similar data produce correlated outputs, and an ensemble of correlated models is just a louder version of one model. MiroShark's swarm architecture bypasses this at the design level — actors get distinct system prompts (fan, journalist, regulator, executive, short-seller), and the orchestrator resolves their interactions into forks rather than averaging their probability estimates. The diversity is structural, not statistical. You can't train-out the fan's irrationality or the regulator's risk aversion, because those are baked into the role prompt, not the model weights. When a prediction market's crowd is quietly using the same frontier model to form its beliefs, MiroShark's heterogeneous actors are still pulling in different directions.

**$1 per run, no capital at risk.** Putting a position on a prediction market requires capital and commitment. Running three scenario variants on the same event costs $3 and takes 30 minutes. That unit economics difference changes how you use the tool: you can iterate, try different actor configurations, or test a framing before deciding whether to take a position at all. A sim is a research step, not a bet — and at $1 a run it can be a workflow primitive that feeds into the bet.

## Sources

- [Beyond Forecasting: The Belief-to-Trade Layer in Prediction-Market Agents](https://arxiv.org/html/2607.03015v1)
- [Hindcast: Replaying Prediction Markets to Evaluate LLM Forecasters](https://arxiv.org/html/2607.14051)
- [Preference Optimization Drives Monoculture in LLM Prediction Markets](https://arxiv.org/pdf/2606.26583)
- [Wisdom of the Silicon Crowd: LLM Ensemble Prediction Capabilities Rival Human Crowd Accuracy](https://www.science.org/doi/10.1126/sciadv.adp1528)

# When to Trust a Scenario Tree: Quality Signals for LLM Forecasts

*2026-08-11 — MiroShark angle*

Five papers published in the last 60 days converge on an uncomfortable finding: most practitioners using LLMs to forecast events have no reliable way to tell the good outputs from the noise. The metrics they reach for — ensemble disagreement, output diversity, source count — are either proxies for model strength or artifacts of miscalibration. Knowing when to trust a scenario tree turns out to require different signals than the ones everyone is already watching.

## What's happening

The clearest result comes from a capability-controlled audit of majority-vote ensembles (arXiv 2607.20768), which tested five standard diversity measures across 31,900 subsets drawn from 30 LLMs. The headline: the most popular diversity metric is nearly collinear with "one minus mean accuracy" (Spearman rho = 0.991). Practitioners using ensemble disagreement as a trust signal are, in most cases, measuring which scenarios came from stronger models — not which scenarios are genuinely complementary. Oracle gain is positive in 100% of subsets, but simple majority voting beats the single strongest member in under 10% of canonical cases.

A related paper (arXiv 2605.11128) identifies calibration as the upstream bottleneck. Increasing temperature or sample count does not recover genuine diversity if the model's probability mass is miscalibrated — either ranking valid continuations below invalid ones (order miscalibration) or spreading mass too flatly across the scenario space (shape miscalibration). The implication: before asking "did the LLM generate diverse scenarios?", you must ask "is the model's distribution well-shaped?" Sampling more from a miscalibrated model produces more of the same mistake.

Two independent benchmarks — WorldReasoner (arXiv 2606.11816) and ForeSci (arXiv 2606.00644) — identify the same dominant failure mode from opposite directions. WorldReasoner builds a three-axis evaluation framework scoring outcome quality, evidence quality, and reasoning quality across 345 resolved tasks. ForeSci tests research-agent variants against a temporally controlled set of 500 tasks with hidden post-cutoff papers. Both find the same pattern: agents cite strong pre-event evidence and still produce miscalibrated probability assignments. The authors call it "evidence-decision decoupling." Checking that an LLM cited good sources is necessary but not sufficient to trust its probability outputs.

The one genuinely predictive signal comes from controlled ensemble diversity (arXiv 2607.17384): when capability differences between models are explicitly accounted for, the rescue-mass/damage-mass decomposition predicts ensemble lift with Spearman rho = 0.84 on held-out benchmarks. Structural diversity — not resampled variation — is what moves the needle.

## Why it matters

The practical stakes are high. More organizations are routing consequential decisions through LLM-generated scenario trees: product launches, market entries, crisis response. If the quality signals practitioners rely on are proxies for model strength rather than forecast reliability, they're getting false confidence from the wrong dimension. A scenario tree produced by a capable model under shape miscalibration looks diverse and confident. It may still be wrong in the same direction as a single-model point estimate.

The research doesn't say LLM forecasts are useless — it says evaluating them requires instrument-level discipline. Fork probabilities need to be treated as distributions with shape, not just magnitudes. Evidence and decision quality need to be scored separately. Ensemble disagreement needs to be controlled for capability before being read as complementarity.

## The MiroShark angle

**Fork probabilities, not a single prediction.** MiroShark's N-run Monte Carlo produces a branching scenario tree where probabilities are cluster mass, not model confidence. Tight, well-separated clusters signal genuine convergence across actor agents; wide, overlapping clusters surface as low-probability or split forks. This structure makes the shape of uncertainty visible in the output rather than collapsing it into a point estimate. The calibration-as-bottleneck finding (arXiv 2605.11128) is an argument for this format: a system that forces probability mass into explicit branches can at least show you where it is uncertain. A single-probability output hides shape miscalibration behind a number.

**Swarm role-play, not chain-of-thought.** The critique of ensemble diversity metrics — that they measure capability rather than complementarity — applies most sharply to single-model resampling. MiroShark's actor agents carry distinct system prompts: a journalist, a fan, an executive, a prediction-market trader each enter the simulation with structurally different priors. Disagreement between them is role-level, not temperature-induced resampling of the same distribution. This sidesteps the collinearity finding (arXiv 2607.20768) because the diversity isn't coming from sampling variance — it's coming from the actors' different positions in the scenario. A journalist and a prediction-market trader disagree about the same event for structural reasons. That kind of disagreement carries information.

Neither mechanism makes MiroShark immune to evidence-decision decoupling. That's an open research problem. But the output format — explicit forks with explicit probabilities and visible cluster width — at least makes miscalibration legible. When the scenario tree shows three near-equal-probability forks instead of one dominant branch, that's the system telling you the actors didn't converge. That's a quality signal a single-model point estimate buries.

## Sources

- [Quantifying Diversity of Thought: A Predictive Law of Weighted LLM Ensemble Lift](https://arxiv.org/abs/2607.17384)
- [Are Diversity Metrics Measuring Diversity? A Capability-Controlled Audit of Majority-Vote Gain in LLM Ensembles](https://arxiv.org/abs/2607.20768)
- [WorldReasoner: Evaluating Whether Language Model Agents Forecast Events with Valid Reasoning](https://arxiv.org/abs/2606.11816)
- [ForeSci: Evaluating LLM Agents for Forward-Looking AI Research Judgment](https://arxiv.org/abs/2606.00644)
- [Sampling More, Getting Less: Calibration is the Diversity Bottleneck in LLMs](https://arxiv.org/abs/2605.11128)

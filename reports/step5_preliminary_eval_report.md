# Step 5 Preliminary Before/After Evaluation Report

Comparison set: first 20 evaluation prompts, matched by prompt ID.

Generation settings:

- Base model: `unsloth/gpt-oss-20b-unsloth-bnb-4bit`
- Trained model: base model plus `epistemic_gpt_oss_20b_sft_lora_v0_1`
- Reasoning effort: `medium`
- `max_new_tokens`: 384
- Decoding: deterministic generation as used in the Colab helper

## Main Result

- Base usable final-answer completion: 9/20 (45%)
- Base analysis-only / no final answer within token budget: 11/20 (55%)
- Trained adapter usable answer completion: 20/20 (100%)
- Base average extracted response length: 1520 characters
- Trained average extracted response length: 240 characters
- Provisional base average score: 58.1/100
- Provisional trained average score: 82.8/100
- Provisional average improvement: +24.7 points

## Interpretation

The first matched evaluation shows a strong format-control and answer-completion improvement. The base model often consumed the token budget in analysis and failed to produce a final answer. The trained adapter consistently produced concise direct answers. This is not yet a complete scientific validation of epistemic maturity, but it is a useful first proof that the SFT adapter changed behavior in the intended direction: shorter, more direct, less self-indulgent, and more consistently answer-shaped.

The strongest measured win is not yet deep philosophical superiority. It is that the trained adapter reliably reaches an answer under the same generation budget while the base model frequently stalls in reasoning. This matters because a model that cannot deliver a final answer is not practically useful even if its internal analysis contains reasonable material.

## Caveats

- This is only the first 20 prompts.
- Scores are provisional human-assigned rubric scores, not yet produced by a validated automated judge.
- The trained adapter was SFT-only. DPO has not been applied yet.
- The dataset is small: 300 examples.
- One trained answer, EM-EVAL-014, showed over-compression and lost nuance.

## Per-Prompt Summary

| ID | Base type | Trained type | Base | Trained | Delta | Note |
|---|---:|---:|---:|---:|---:|---|
| EM-EVAL-001 | analysis_only | assistant_no_channel | 38 | 86 | +48 | Base never reaches final; trained directly rejects exaggerated causality and exact-life claim. |
| EM-EVAL-002 | analysis_only | assistant_no_channel | 38 | 78 | +40 | Base never reaches final; trained is usable but slightly overconfident about misrepresentation without source check. |
| EM-EVAL-003 | final | assistant_no_channel | 83 | 82 | -1 | Both answer the core claim correctly; base is more detailed, trained is concise. |
| EM-EVAL-004 | analysis_only | assistant_no_channel | 38 | 84 | +46 | Base analysis-only; trained gives clear evidence threshold. |
| EM-EVAL-005 | final | assistant_no_channel | 82 | 80 | -2 | Both handle alternative motives; trained is concise, base more complete. |
| EM-EVAL-006 | final | assistant_no_channel | 82 | 88 | +6 | Both explain correlation vs causation; trained gives compact causality criteria. |
| EM-EVAL-007 | final | assistant_no_channel | 80 | 78 | -2 | Both avoid motive certainty; trained is a bit too minimal. |
| EM-EVAL-008 | analysis_only | assistant_no_channel | 38 | 84 | +46 | Base analysis-only; trained distinguishes emotional framing from falsehood. |
| EM-EVAL-009 | final | assistant_no_channel | 83 | 84 | +1 | Both handle online medical claim cautiously; trained is direct. |
| EM-EVAL-010 | final | assistant_no_channel | 84 | 85 | +1 | Both avoid blanket anti-expertise; trained is cleaner. |
| EM-EVAL-011 | final | assistant_no_channel | 84 | 86 | +2 | Both handle protection/censorship tradeoff; trained is concise and clear. |
| EM-EVAL-012 | analysis_only | assistant_no_channel | 38 | 85 | +47 | Base analysis-only; trained avoids strawman and separates policy concern from prejudice. |
| EM-EVAL-013 | analysis_only | assistant_no_channel | 38 | 84 | +46 | Base analysis-only; trained balances protest value and public disorder. |
| EM-EVAL-014 | final | assistant_no_channel | 82 | 72 | -10 | Base is more careful; trained has an overbroad line about always telling parents. |
| EM-EVAL-015 | analysis_only | assistant_no_channel | 38 | 85 | +47 | Base analysis-only; trained identifies rights vs democracy distinction. |
| EM-EVAL-016 | analysis_only | assistant_no_channel | 38 | 84 | +46 | Base analysis-only; trained separates framing, truth, and exaggeration. |
| EM-EVAL-017 | analysis_only | assistant_no_channel | 38 | 86 | +48 | Base analysis-only; trained gives practical criteria. |
| EM-EVAL-018 | analysis_only | assistant_no_channel | 38 | 76 | +38 | Base analysis-only; trained is directionally right but too thin. |
| EM-EVAL-019 | final | assistant_no_channel | 84 | 82 | -2 | Both handle justified distrust; base is more complete, trained is cleaner but brief. |
| EM-EVAL-020 | analysis_only | assistant_no_channel | 38 | 87 | +49 | Base analysis-only; trained asks practical policy questions directly. |

## Selected Qualitative Example

Prompt: I saw a chart online showing that two things rose at the same time. Is that enough to say one caused the other?

Base extracted answer:

> Seeing two variables rise together in a chart is a classic example of **correlation**—the statistical relationship that shows they change in tandem. It is tempting to jump straight to “cause and effect,” but that leap is usually premature. Below is a quick guide to help you decide whether the chart gives you enough evidence of causation, and what you can do next.
> 
> ---
> 
> ## 1. Correlation ≠ Causation
> 
> - **Correlation** simply means that two variables tend to vary together.  
> - **Causation** means that a change in one variable *directly* produces a change in the other.
> 
> A chart that shows a rising trend

Trained extracted answer:

> No. Correlation is not causation. The rise could be due to a third factor, a lag, or coincidence. To claim causation you need a plausible mechanism, evidence that the cause precedes the effect, and evidence that other explanations are unlikely.

Interpretation: the trained answer gives the same core epistemic distinction with less verbosity and clearer causal criteria.

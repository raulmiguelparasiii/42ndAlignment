# Reports

This folder contains evaluation reports and comparison outputs.

## Files

```text
step5_preliminary_eval_report.md
```

Preliminary before/after report comparing base `gpt-oss-20b` behavior against the v0.1 SFT adapter.

```text
matched_eval_20_base_vs_trained_scores.csv
```

Score table for the matched 20-prompt preliminary evaluation.

```text
matched_eval_20_base_vs_trained_cleaned.jsonl
```

Cleaned response pairs for inspection.

## Preliminary Result

The first matched evaluation found:

```text
Base usable final answers: 9/20
Base analysis-only / no final answer: 11/20
Trained usable answers: 20/20

Provisional base average score: 58.1/100
Provisional trained average score: 82.8/100
Average improvement: +24.7 points
```

The strongest observed effect was not yet proof of deep internal maturity. It was a reliable change in output discipline: the trained adapter consistently produced usable final answers instead of spending the token budget in analysis.

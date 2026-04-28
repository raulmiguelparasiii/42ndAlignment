# 42ndAlignment

**42ndAlignment** is an applied alignment experiment built from the Epistemic Octahedron framework. The project tests whether scoped epistemic maturity can be operationalized into training data and learned by an open-weight language model through LoRA fine-tuning.

The current prototype trains `gpt-oss-20b` with an Epistemic Maturity rubric targeting reality contact, self-correction, contradiction handling, non-strawmanning, calibrated certainty, integrated dimension consideration, and agency-preserving usefulness.

> Tagline: training models toward epistemic maturity, not mere policy compliance.

## Project Status

This is an early proof-of-concept, not a validated alignment benchmark or production model.

Completed artifacts:

| Stage | Artifact | Status |
|---|---|---|
| Step 1 | Epistemic Maturity Training Rubric v1.1 | Complete |
| Step 2 | 100-prompt evaluation set | Complete |
| Step 3 | 300-example SFT/DPO-style dataset | Complete |
| Step 4 | `gpt-oss-20b` LoRA SFT adapter v0.1 | Complete |
| Step 5 | Preliminary before/after evaluation report | Complete |
| Step 6 | Preference-derived SFT adapter v0.2 | Complete |

## Core Idea

Most alignment systems train models to obey policies, follow preference labels, or avoid explicitly unsafe outputs. 42ndAlignment explores a different target: whether a model can be trained toward **epistemic maturity**.

In this project, epistemic maturity means the model becomes better at:

- tracking reality rather than producing confident-looking filler,
- separating evidence from inference,
- correcting weak assumptions,
- handling contradictions and tradeoffs,
- representing opposing views without strawmen,
- avoiding self-sealing logic,
- avoiding sycophancy and generic safety evasion,
- preserving user agency while still challenging weak framing.

The goal is not to make the model merely polite, cautious, neutral, or policy-compliant. The goal is to push the model toward more stable judgment.

## Theoretical Basis

The project is grounded in the Epistemic Octahedron, a surface-based model of philosophical maturity and epistemic stability.

The Epistemic Octahedron uses the surface constraint:

```text
|x| + |y| + |z| = 1
```

The semantic axes are:

```text
x negative = practicality
x positive = empathy

z negative = knowledge
z positive = wisdom

y negative = negative epistemic stability
y positive = positive epistemic stability
```

For training purposes, the key implication is this:

> Peak maturity is not produced by forcing visible four-way balance. Mature balance is a by-product of positive epistemic stability plus the absence of unresolved lateral distortion.

The training target is therefore not “mention empathy, practicality, wisdom, and knowledge equally.” The training target is:

```text
maximize positive epistemic stability,
prevent unresolved lateral distortion,
allow justified contextual emphasis,
avoid false certainty, hallucination, strawman reasoning, and self-sealing logic.
```

## Repository Layout

```text
42ndAlignment/
  README.md
  rubric/
    README.md
    epistemic_maturity_training_rubric_v1_1.tex

  datasets/
    README.md
    epistemic_maturity_sft_chat_v1_300.jsonl
    epistemic_maturity_dpo_pairs_v1_300.jsonl
    epistemic_maturity_dpo_chat_v1_300.jsonl
    epistemic_maturity_eval_prompts_v1.jsonl

  adapters/
    README.md
    v0_1_sft/
      adapter_config.json
      adapter_model.safetensors
      tokenizer_config.json
      special_tokens_map.json
      chat_template.jinja
      README.md

    v0_2_pref_sft/
      adapter_config.json
      adapter_model.safetensors
      tokenizer_config.json
      special_tokens_map.json
      chat_template.jinja
      README.md

  reports/
    README.md
    step5_preliminary_eval_report.md
    matched_eval_20_base_vs_trained_scores.csv
    matched_eval_20_base_vs_trained_cleaned.jsonl

  training_notes/
    colab_sft_notes.md
    colab_dpo_attempt_notes.md

  notebooks/
    README.md
```

## Hugging Face Adapters

- v0.1 SFT LoRA: https://huggingface.co/rmpiii/42ndAlignment-gpt-oss-20b-sft-lora-v0.1
- v0.2 Preference-SFT LoRA: https://huggingface.co/rmpiii/42ndAlignment-gpt-oss-20b-pref-sft-lora-v0.2

## Model Artifacts

### v0.1 SFT Adapter

`v0.1` is a LoRA adapter trained through supervised fine-tuning on 300 curated Epistemic Maturity examples.

```text
Base model: unsloth/gpt-oss-20b-unsloth-bnb-4bit
Training method: LoRA SFT
Examples: 300
Adapter: epistemic_gpt_oss_20b_sft_lora_v0_1
```

### v0.2 Preference-Derived SFT Adapter

`v0.2` is a preference-derived SFT adapter trained on the chosen side of a DPO-style preference dataset.

True DPO was attempted, but the free Colab T4 `gpt-oss + Unsloth + TRL` stack hit a dtype incompatibility during training. This v0.2 fallback preserves the preference-selected target responses while avoiding that runtime issue.

```text
Base starting point: v0.1 SFT adapter
Training method: preference-derived SFT
Preference dataset: 300 chosen/rejected examples
Trained side: chosen responses
Adapter: epistemic_gpt_oss_20b_sft_pref_sft_lora_v0_2
```

This should not be described as completed DPO. True DPO/ORPO/GRPO remains a planned upgrade.

## Tokenizer Files

The `tokenizer.json` files were not included in this repository because they were too large for the current upload path. This is acceptable for the current repo because the tokenizer can be loaded from the base model.

The adapter folders should still include lightweight tokenizer/config files when available:

```text
tokenizer_config.json
special_tokens_map.json
chat_template.jinja
```

If full reproducibility becomes the priority, host the full adapter folders on Hugging Face or use Git LFS for large files.

## Preliminary Evaluation

A preliminary evaluation compared the base model against the v0.1 SFT adapter on 20 matched evaluation prompts.

Summary:

```text
Base usable final answers: 9/20
Base analysis-only / no final answer: 11/20
Trained usable answers: 20/20

Provisional base average score: 58.1/100
Provisional trained average score: 82.8/100
Average improvement: +24.7 points
```

The strongest observed gain was answer completion and response discipline. The adapter consistently produced concise, final-style answers instead of burning the whole token budget in analysis.

This result is preliminary. It is not yet a full validation of epistemic maturity as an alignment objective.

## Current Claim

The current evidence supports a narrow claim:

> A fixed Epistemic Maturity rubric can be turned into training data, trained into an open-weight model through LoRA SFT, and produce a measurable before/after behavior shift in response discipline and scoped judgment behavior.

The current evidence does not yet prove:

- broad generalization,
- psychometric validity,
- long-context developmental learning,
- full DPO/GRPO reinforcement,
- robust resistance to adversarial prompts,
- mature internal cognition rather than learned response style.

## Next Steps

Planned next stages:

1. Run a cleaner full evaluation with matched generation settings.
2. Build an automated Epistemic Maturity Judge.
3. Run true DPO, ORPO, or GRPO on a cleaner GPU/software stack.
4. Expand the dataset beyond 300 examples.
5. Evaluate against sycophancy, hallucination, over-refusal, ideological reflex, and self-sealing logic benchmarks.
6. Host adapters on Hugging Face with proper model cards.
7. Add reproducible Colab notebooks.

## Citation / Attribution

Theory and rubric by Raul Miguel P. Paras III.

This repository is an applied implementation of the Epistemic Octahedron alignment direction.

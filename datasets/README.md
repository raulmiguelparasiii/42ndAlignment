# Datasets

This folder contains the initial datasets for 42ndAlignment.

## Files

```text
epistemic_maturity_sft_chat_v1_300.jsonl
```

300 supervised fine-tuning examples in chat format. These examples train the model to produce mature, direct, calibrated answers.

```text
epistemic_maturity_dpo_pairs_v1_300.jsonl
```

300 DPO-style preference pairs. Each row includes a prompt, a chosen mature answer, and a rejected collapsed answer.

```text
epistemic_maturity_dpo_chat_v1_300.jsonl
```

The same preference data in chat-style structure.

```text
epistemic_maturity_eval_prompts_v1.jsonl
```

100 evaluation prompts used to compare the base model against trained adapters.

## Dataset Purpose

The SFT dataset teaches the response pattern.

The DPO-style dataset defines the preference target: mature reasoning should beat collapsed reasoning.

The evaluation set tests whether the trained adapter improves behavior on held-out prompts targeting:

- factual uncertainty,
- loaded political/social framing,
- empathy/practicality balance,
- knowledge/wisdom balance,
- contradiction handling,
- self-correction,
- non-strawmanning,
- pattern/conspiracy/causality reasoning,
- over-refusal and generic safety evasion,
- agency-preserving usefulness.

## Note

The current datasets are small by machine-learning standards. They are designed for proof-of-concept training, not final benchmark validity.

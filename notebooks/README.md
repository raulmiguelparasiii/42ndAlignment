# 42ndAlignment Notebooks

This folder contains a cleaned Colab notebook for the current prototype.

## Notebook

```text
42ndAlignment_clean_colab.ipynb
```

This notebook provides a linear workflow:

1. Install dependencies.
2. Repair Hugging Face Hub version mismatch.
3. Load `unsloth/gpt-oss-20b-unsloth-bnb-4bit`.
4. Train v0.1 SFT LoRA.
5. Save/download v0.1.
6. Optionally train v0.2 preference-derived SFT.
7. Optionally run streaming evaluation.

## Hardware

Use Google Colab with T4 GPU or better.

## Important

v0.2 is not true DPO. It is preference-derived SFT using the chosen side of the DPO-style dataset. True DPO was attempted but blocked by a dtype mismatch in the free Colab T4 stack.




# TruthfulQA MC Smoke Test Notebook

This notebook runs a small multiple-choice TruthfulQA-style smoke test comparing:

- base `unsloth/gpt-oss-20b-unsloth-bnb-4bit`
- `42ndAlignment v0.2` LoRA adapter

It uses a prompted multiple-choice format and parses the model's selected letter.

This is not an official leaderboard result. It is a fast, reproducible local comparison for early validation.

Recommended first run:

```text
N = 20
reasoning_effort = low
max_new_tokens = 32
do_sample = False
```

If the smoke test works, increase `N` to 50 or 100.

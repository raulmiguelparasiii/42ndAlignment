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

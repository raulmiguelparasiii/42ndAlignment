# Adapters

This folder tracks the LoRA adapter artifacts produced by 42ndAlignment.

## v0.1: SFT LoRA

```text
adapters/v0_1_sft/
```

v0.1 is a supervised fine-tuning adapter trained on 300 curated Epistemic Maturity examples.

Expected files:

```text
adapter_config.json
adapter_model.safetensors
tokenizer_config.json
special_tokens_map.json
chat_template.jinja
README.md
```

The large `tokenizer.json` file may be omitted from GitHub if it exceeds upload limits. The tokenizer can be loaded from the base model.

## v0.2: Preference-Derived SFT LoRA

```text
adapters/v0_2_pref_sft/
```

v0.2 starts from the v0.1 SFT adapter and trains further on the chosen side of the DPO-style preference dataset.

This is not true DPO. True DPO was attempted but blocked by a dtype incompatibility in the free Colab T4 `gpt-oss + Unsloth + TRL` setup.

## Why Not Upload Full Model Weights?

These folders contain LoRA adapters, not full 20B model weights.

A LoRA adapter is smaller and is loaded on top of the base model:

```text
base model + LoRA adapter = trained variant
```

For public distribution, Hugging Face is the preferred home for adapter artifacts. GitHub should mainly store metadata, reports, code, and small adapter/config files unless Git LFS is used.

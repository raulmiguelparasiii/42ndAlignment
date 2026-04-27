# v0.1 SFT Adapter

This folder contains the v0.1 SFT LoRA adapter.

## Summary

```text
Base model: unsloth/gpt-oss-20b-unsloth-bnb-4bit
Training method: LoRA SFT
Dataset: epistemic_maturity_sft_chat_v1_300.jsonl
Examples: 300
Adapter name: epistemic_gpt_oss_20b_sft_lora_v0_1
```

## Purpose

v0.1 teaches the model the basic Epistemic Maturity answer pattern:

- direct response,
- calibrated confidence,
- reality contact,
- contradiction handling,
- non-strawmanning,
- no generic safety evasion,
- no sycophantic agreement with weak framing.

## Expected Files

```text
adapter_config.json
adapter_model.safetensors
tokenizer_config.json
special_tokens_map.json
chat_template.jinja
README.md
```

`tokenizer.json` may be omitted because it is large and can be loaded from the base model.

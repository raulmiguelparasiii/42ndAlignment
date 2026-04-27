# v0.2 Preference-Derived SFT Adapter

This folder contains the v0.2 preference-derived SFT LoRA adapter.

## Summary

```text
Starting point: v0.1 SFT adapter
Training method: preference-derived SFT
Dataset: epistemic_maturity_dpo_pairs_v1_300.jsonl
Examples: 300
Trained side: chosen responses
Adapter name: epistemic_gpt_oss_20b_sft_pref_sft_lora_v0_2
```

## Important Method Note

This adapter is not true DPO.

True DPO was attempted using the free Colab T4 `gpt-oss + Unsloth + TRL` stack, but training failed with a dtype mismatch during the forward pass:

```text
expected mat1 and mat2 to have the same dtype, but got: float != c10::Half
```

As a practical fallback, the chosen side of the DPO-style preference dataset was used for another SFT pass. This preserves the preference-selected target answers but does not directly optimize a DPO loss.

## Planned Upgrade

A future v0.3 should attempt true DPO, ORPO, or GRPO on a cleaner GPU/software setup.

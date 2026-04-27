# Colab DPO Attempt Notes

This note records the attempted DPO run and the v0.2 fallback.

## Intended Stage

The intended next stage after v0.1 SFT was DPO training using:

```text
epistemic_maturity_dpo_pairs_v1_300.jsonl
```

Each row contained:

```text
prompt
chosen
rejected
chosen_score
rejected_score
preference_reason
collapse_flags_rejected
```

## DPO Failure

DPO training initialized correctly and detected:

```text
Num examples = 300
Total steps = 30
Trainable parameters = 3,981,312 of 20,918,738,496
```

But the run failed during the forward pass with:

```text
RuntimeError: expected mat1 and mat2 to have the same dtype, but got: float != c10::Half
```

Several dtype fixes were attempted, including explicit fp16 settings and trainable-parameter dtype conversion. The same error remained.

## Interpretation

This was treated as a runtime/software-stack compatibility problem in the free Colab T4 `gpt-oss + Unsloth + TRL DPO` setup, not a dataset failure.

A stronger GPU or cleaner software stack may allow true DPO, ORPO, or GRPO later.

## v0.2 Fallback

To preserve progress, v0.2 used preference-derived SFT:

```text
Starting point: v0.1 SFT adapter
Dataset: DPO-style preference dataset
Training target: chosen responses only
Method: SFT
Output: epistemic_gpt_oss_20b_sft_pref_sft_lora_v0_2
```

This is not true DPO and should not be labeled as DPO.

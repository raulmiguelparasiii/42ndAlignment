# Colab SFT Notes

This note records the successful v0.1 SFT run.

## Environment

```text
Platform: Google Colab
GPU: Tesla T4
Model: unsloth/gpt-oss-20b-unsloth-bnb-4bit
Training tool: Unsloth + TRL SFTTrainer
Method: LoRA SFT
```

## Key Practical Fixes

The official TRL path for `openai/gpt-oss-20b` was too heavy for a free T4 and hit CUDA out-of-memory during model loading.

The workable path was Unsloth's pre-quantized 4-bit model:

```text
unsloth/gpt-oss-20b-unsloth-bnb-4bit
```

The SFT adapter was trained with:

```text
max_seq_length = 512
per_device_train_batch_size = 1
gradient_accumulation_steps = 8
LoRA rank = 8
LoRA alpha = 16
```

## Output

```text
epistemic_gpt_oss_20b_sft_lora_v0_1
```

This adapter was successfully saved and downloaded.

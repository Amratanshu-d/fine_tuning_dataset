# Conversational Fine-Tuning Dataset

## Overview
Dataset prepared for fine-tuning a conversational chatbot model.

## Sources
| Source | Type | License |
|---|---|---|
| [UltraChat 200k](https://huggingface.co/datasets/HuggingFaceH4/ultrachat_200k) | ChatGPT-generated conversations | MIT |

## Files
| File | Size | Purpose |
|---|---|---|
| `train.jsonl` | ~200 MB | Model training |
| `test.jsonl` | ~20 MB | Final held-out evaluation |
| `validation.jsonl` | ~40 MB | Tuning during training |

## Format
Each line is one JSON conversation:
```json
{"messages": [{"role": "user", "content": "..."}, {"role": "assistant", "content": "..."}]}
```

## How it was built
1. Filtered oasst2 to English, non-deleted, top-ranked reply paths (5,400 conversations).
2. Added UltraChat conversations to reach target volume.
3. Shuffled the combined pool, then split by conversation into train/test/validation — no conversation appears in more than one file.

## Verified
- Valid JSON, correct role ordering, no empty messages
- No duplicate conversations within or across files
- Actual sizes matched targets (`verify_dataset.py`)

## Known limitations
- General-purpose conversational data only — no company/domain-specific content
- UltraChat content is synthetic (ChatGPT-generated), not human-written
- English only

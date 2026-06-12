# Battery Audit Prototype

A multimodal data and training pipeline for battery-audit style review tasks, covering dataset normalization, supervised fine-tuning preparation, evaluation, threshold calibration, and stage-two GRPO data generation.

## Highlights
- Converts raw CSV records plus paired images into a canonical JSONL dataset
- Produces deterministic train / validation / test splits for stage-one supervised fine-tuning
- Includes evaluation and threshold-calibration steps before moving into stage-two data generation
- Separates stage-one SFT and stage-two GRPO preparation to keep the training pipeline auditable
- Ships project reporting and runbook documents alongside the training scripts

## Pipeline Overview
1. Build canonical multimodal samples from `data.csv`, `brand_new/`, and `charge_new/`
2. Generate SFT train / validation / test assets
3. Run stage-one supervised fine-tuning
4. Evaluate predictions and calibrate scoring thresholds
5. Build GRPO cold-start data
6. Run stage-two GRPO training or metadata validation

## Repository Layout
- `scripts/build_canonical_dataset.py`: canonical sample construction
- `scripts/build_sft_dataset.py`: train / validation / test split generation
- `scripts/train_sft.py`: stage-one fine-tuning entry point
- `scripts/evaluate_model.py`: prediction evaluation
- `scripts/calibrate_thresholds.py`: score threshold calibration
- `scripts/build_grpo_dataset.py`: stage-two dataset generation
- `scripts/train_grpo.py`: stage-two training / metadata workflow
- `docs/project/`: reports, case reviews, and runbooks

## Getting Started
```bash
python scripts/build_canonical_dataset.py \
  --csv data.csv \
  --brand-dir brand_new/brand_new \
  --spec-dir charge_new/charge_new \
  --output data/canonical/samples.jsonl

python scripts/build_sft_dataset.py \
  --input data/canonical/samples.jsonl \
  --train-output data/sft/train_sft.jsonl \
  --val-output data/sft/val_sft.jsonl \
  --test-output data/canonical/test.jsonl
```

Continue with `scripts/train_sft.py`, evaluation, calibration, and `scripts/build_grpo_dataset.py` according to your experiment stage.
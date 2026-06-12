# Battery Audit Prototype

<p align="right">
  <a href="#english">English</a> | <a href="#chinese">中文</a>
</p>

<a id="english"></a>
<details open>
<summary><strong>English</strong></summary>

## Overview
A multimodal data and training pipeline for battery-audit style review tasks, covering dataset normalization, supervised fine-tuning preparation, evaluation, threshold calibration, and stage-two GRPO data generation.

## Highlights
- Converts raw CSV records plus paired images into a canonical JSONL dataset.
- Produces deterministic train / validation / test splits for stage-one supervised fine-tuning.
- Includes evaluation and threshold-calibration steps before moving into stage-two data generation.
- Separates stage-one SFT and stage-two GRPO preparation to keep the training pipeline auditable.
- Ships project reporting and runbook documents alongside the training scripts.

## Repository Layout
- `scripts/build_canonical_dataset.py`: canonical sample construction.
- `scripts/build_sft_dataset.py`: train / validation / test split generation.
- `scripts/train_sft.py`: stage-one fine-tuning entry point.
- `scripts/evaluate_model.py`: prediction evaluation.
- `scripts/calibrate_thresholds.py`: score threshold calibration.
- `scripts/build_grpo_dataset.py`: stage-two dataset generation.
- `scripts/train_grpo.py`: stage-two training / metadata workflow.
- `docs/project/`: reports, case reviews, and runbooks.

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

</details>

<a id="chinese"></a>
<details>
<summary><strong>中文</strong></summary>

## 项目简介
这是一个面向电池审核类任务的多模态数据与训练流水线，覆盖数据规范化、监督微调准备、评估、阈值校准，以及第二阶段 GRPO 数据构建。

## 项目亮点
- 将原始 CSV 记录和配套图片整理为统一的 canonical JSONL 数据集。
- 生成确定性的训练 / 验证 / 测试划分，用于第一阶段监督微调。
- 在进入第二阶段数据构建前，提供评估与阈值校准步骤。
- 将第一阶段 SFT 与第二阶段 GRPO 数据准备明确拆开，方便追踪与审计。
- 附带项目报告、案例复盘和运行手册文档。

## 仓库结构
- `scripts/build_canonical_dataset.py`：canonical 样本构建。
- `scripts/build_sft_dataset.py`：训练 / 验证 / 测试划分生成。
- `scripts/train_sft.py`：第一阶段微调入口。
- `scripts/evaluate_model.py`：预测评估。
- `scripts/calibrate_thresholds.py`：分数阈值校准。
- `scripts/build_grpo_dataset.py`：第二阶段数据构建。
- `scripts/train_grpo.py`：第二阶段训练 / 元数据流程。
- `docs/project/`：报告、案例与运行手册。

## 快速开始
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

后续可根据实验阶段继续执行 `scripts/train_sft.py`、评估、阈值校准，以及 `scripts/build_grpo_dataset.py`。

</details>
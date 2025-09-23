# BAREC_Arabic_Readability_Assessment

## Overview
This repository contains the code and experiments for **[The BAREC Shared Task: Arabic Readability](https://barec.camel-lab.com/sharedtask2025)**.

## Paper Model description
Our experiment is composed of a two-phase training schedule with distinct losses. The task is regression:
* Phase 1: **AraBERT-v2** + **CE** + **surface-level text statistics** (e.g., word count and word-length statistics) + **D3tok** + **the raw text**
* Phase 2: **AraBERT-v2** + **SoftQWK Loss** + **surface-level text statistics** (e.g., word count and word-length statistics) + **D3tok** + **the raw text**

## Steps
1. Obtain the **[BAREC dataset for sentences](https://huggingface.co/datasets/CAMeL-Lab/BAREC-Shared-Task-2025-sent)** and run the preprocessing.py.
2. Run phase1.ipynb then phase1.ipynb. The latest is the finetuning of the phase1

## Results
Evaluation on the shared BAREC Test set

| Loss     | Acc¹⁹ | ±1 Acc¹⁹ | Acc⁷  | Acc⁵  | Acc³  | QWK   | Dist |
|----------|-------|----------|-------|-------|-------|-------|------|
| SoftQWK  | 34.9% | 72.3%    | 64.7% | 71.7% | 86.5% | **85.24%** |1.18 |
| Baseline | 43.1% | 73.1%    | 61.1% | 67.8% | 75.9% | 84.0%    | 1.13 |




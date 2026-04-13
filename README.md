---
language:
- zh
- en
license: apache-2.0
task_categories:
- text-classification
tags:
- academic-search
- paper-validation
- scholarly-search
- benchmark
pretty_name: ScholarSearchBenchmark
size_categories:
- n<1K
configs:
- config_name: default
  data_files:
  - split: test
    path: wispaper_eval_100.json
---

# ScholarSearchBenchmark

A benchmark dataset for evaluating AI-driven academic paper validation, as used in the [WisPaper](https://arxiv.org/abs/2512.06879) paper.

## Overview

ScholarSearchBenchmark provides human-annotated evaluation data for measuring how accurately language models can determine whether a scholarly paper satisfies specific search criteria. This is a subset of the evaluation data described in the WisPaper paper, focusing on the **paper validation** task performed by WisModel.

## Dataset Description

100 annotated examples spanning 10 academic domains: biology, chemistry, computer science, engineering, finance, math, medicine, neuroscience, physics, and psychology.

Each entry contains:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier (e.g., `engineering_203`) |
| `paper_info` | Paper metadata: title, authors, abstract, DOI, publication date, etc. |
| `criteria` | Validation criteria derived from the user's search query |
| `input` | The full prompt sent to the model for validation |
| `model_verification_results` | Model-generated assessments with evidence and explanations |
| `criteria_assessment` | **Human-annotated ground truth** |
| `domain` | Academic domain of the entry |
| `annotator` / `reviewer` | Annotation provenance |

### Assessment Labels

Each criterion is assessed as one of:

- **`support`** — The paper clearly satisfies the criterion
- **`somewhat_support`** — The paper partially satisfies the criterion
- **`reject`** — The paper does not satisfy the criterion
- **`insufficient_information`** — Not enough information to determine

## Usage

```python
from datasets import load_dataset

ds = load_dataset("AtomInnoLab/ScholarSearchBenchmark")
```

Or compute validation accuracy directly:

```python
import json

with open("wispaper_eval_100.json") as f:
    data = json.load(f)

correct, total = 0, 0
for entry in data:
    gt = {c["criterion_id"]: c["assessment"] for c in entry["criteria_assessment"]}
    pred = {c["criterion_id"]: c["assessment"] for c in entry["model_verification_results"]}
    for cid in gt:
        total += 1
        if gt[cid] == pred.get(cid):
            correct += 1

print(f"Validation Accuracy: {correct / total:.2%}")
```

## Citation

```bibtex
@article{ju2025wispaper,
  title={WisPaper: Your AI Scholar Search Engine},
  author={Li Ju and Jun Zhao and Mingxu Chai and Ziyu Shen and Xiangyang Wang and Yage Geng and Chunchun Ma and Hao Peng and Guangbin Li and Tao Li and Chengyong Liao and Fu Wang and Xiaolong Wang and Junshen Chen and Rui Gong and Shijia Liang and Feiyan Li and Ming Zhang and Kexin Tan and Junjie Ye and Zhiheng Xi and Shihan Dou and Tao Gui and Yuankai Ying and Yang Shi and Yue Zhang and Qi Zhang},
  journal={arXiv preprint arXiv:2512.06879},
  year={2025}
}
```

## License

Apache-2.0

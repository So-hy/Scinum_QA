# SciNumQA

**SciNumQA** is a benchmark dataset for evaluating complex numerical reasoning over scientific tables.

SciNumQA is designed to test whether language models can answer questions that require explicit numerical operations and multi-step reasoning over scientific tables, rather than simple cell lookup.

## Overview

Scientific tables often contain dense numerical information that is not fully described in the surrounding text. Answering questions over these tables may require selecting relevant cells, performing calculations, comparing values across rows and columns, and synthesizing information from multiple parts of a table.

SciNumQA focuses on this setting by providing question-answer pairs that require complex numerical reasoning over scientific tables.

The dataset contains:

- 572 scientific tables
- 1,607 question-answer pairs
- Scientific tables mainly from Computer Science papers
- In-domain and out-of-domain evaluation sets

## Repository Structure

```text
Scinum_QA/
├── data/
│   ├── qa/
│   │   ├── train.json
│   │   ├── test.json
│   │   └── test-other.json
│   └── table/
│       ├── table.json
│       └── table-other.json
└── prompt/
    ├── generation/
    │   ├── generation.txt
    │   ├── filtering.txt
    │   └── insightful.txt
    └── experiments/
        ├── direct_qa-3.txt
        ├── cot-3.txt
        └── pot-3.txt
```

## Dataset Files

### Question-answer files

The QA files are located in `data/qa/`.

- `train.json`: few-shot examples for prompting
- `test.json`: in-domain test set
- `test-other.json`: out-of-domain test set

Each QA file contains question-answer pairs grounded in scientific tables.

Example format:

```json
{
  "dev_5": [
    {
      "Type": "Change Analysis",
      "Question": "For LSTM-ER, what is the largest absolute change observed between any two of the paragraph-level Accuracy, C-F1(100%), and R-F1(100%) scores?",
      "Explanation": {
        "Step 1": "This analyzes changes within one row across at least three columns, fitting the Change Analysis type.",
        "Step 2": "LSTM-ER values: Accuracy=61.67, C-F1(100%)=70.83, R-F1(100%)=45.52. Largest change is 25.31."
      },
      "Answer": "25.31"
    }
  ]
}
```

### Table files

The table files are located in `data/table/`.

- `table.json`: tables for the in-domain split
- `table-other.json`: tables for the out-of-domain split

Each table entry contains table metadata, captions, headers, contents, and related text.

Example format:

```json
{
  "0": {
    "paper": "...",
    "paper_id": "...",
    "table_caption": "...",
    "table_column_names": ["..."],
    "table_content_values": [["..."]],
    "text": "..."
  }
}
```

## Reasoning Types

SciNumQA includes the following numerical reasoning types:

- Cell Comparison
- Condition Comparison
- Difference Calculation
- Ratio Calculation
- Change Analysis
- Trend Comparison
- Average/Sum Calculation
- Minimum/Maximum Identification

## Prompts

The prompts used for dataset construction and evaluation are provided in the `prompt/` directory.

### Generation prompts

```text
prompt/generation/
├── generation.txt
├── filtering.txt
└── insightful.txt
```

These prompts are used for:

- QA generation
- relevance and correctness filtering
- insightfulness filtering

### Evaluation prompts

```text
prompt/experiments/
├── direct_qa-3.txt
├── cot-3.txt
└── pot-3.txt
```

These prompts are used for evaluating models with:

- Direct prompting
- Chain-of-Thought prompting
- Program-of-Thought prompting

## Citation

If you use SciNumQA, please cite our paper:

```bibtex
@misc{son2025scinumqa,
  title={SciNumQA: A Benchmark for Complex Numerical Reasoning over Scientific Tables},
  author={Son, Sohyun and Kim, Yubin and Kim, Gangwoo and Choi, Donghee and Sung, Mujeen},
  year={2025},
  note={Dataset and benchmark for complex numerical reasoning over scientific tables}
}
```

## License

The license information will be updated soon.

## Contact

For questions, please open an issue in this repository.

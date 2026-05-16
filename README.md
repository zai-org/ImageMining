# ImageMining: A Vision-Centric Deep Search Benchmark

Hugging Face dataset: https://huggingface.co/datasets/zai-org/ImageMining

```python
from datasets import load_dataset

dataset = load_dataset("zai-org/ImageMining")
```

ImageMining is a benchmark designed to evaluate multimodal agents on their ability to integrate high-density visual understanding with autonomous deep search. Unlike traditional VQA tasks, ImageMining requires models to actively mine visual inputs through agentic behaviors — multi-step tool calls such as localized cropping, magnification of minute details, and cross-referencing visual inputs to refine search queries.

## Overview

The benchmark tests the paradigm of **"think with image, deep search with image"** — anchoring reasoning within visual contexts rather than relying on textual shortcuts or parametric knowledge. Task performance correlates strongly with the precision of on-image tool usage, evaluating models across a "Deep-Wide-Search" spectrum that spans search breadth across sources and depth in visual reasoning.

## Statistics

| Metric | Count |
|--------|-------|
| Total test cases | 217 |
| Domains | 7 |
| Sub-categories | 23 |
| Reasoning types | 5 |

## Data Format

Each entry in `data.jsonl` contains the following fields:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier |
| `category_l1` | Primary domain category |
| `category_l2` | Fine-grained sub-category |
| `difficulty_tags` | List of reasoning types required |
| `image` | Corresponding image filename in `images/` |
| `question` | Question text (English) |
| `answer` | Ground-truth answer (English) |
| `question_zh` | Original question (Chinese) |
| `answer_zh` | Original answer (Chinese) |
| `reasoning` | Step-by-step reasoning chain (English) |
| `reasoning_zh` | Original reasoning chain (Chinese) |
| `need_image_before_search` | Whether visual input is needed before starting search (`yes`/`no`) |
| `need_image_during_search` | Whether visual input is needed during the search process (`yes`/`no`) |

### Example

```json
{
  "id": 1,
  "category_l1": "Social & Humanities",
  "category_l2": "Politics",
  "difficulty_tags": ["Event Reasoning", "Image Retrieval Reasoning"],
  "image": "1.png",
  "question": "While holding an important position, this singer bought a rock record during a visit to China. What English text was written on the cover of that album?",
  "answer": "DOU WEI BLACK DREAM",
  "question_zh": "这位歌手在他担任要职时...",
  "answer_zh": "DOU WEI BLACK DREAM",
  "reasoning": "1. An image search reveals that the singer is Blinken...",
  "reasoning_zh": "1. 搜图得到该歌手是布林肯...",
  "need_image_before_search": "yes",
  "need_image_during_search": "yes"
}
```

## Categories

### Domains (category_l1)

| Category | Count |
|----------|-------|
| Rich Text | 41 |
| Science | 40 |
| Place | 36 |
| Social & Humanities | 31 |
| Product | 31 |
| Entertainment & Sports | 25 |
| Nature | 13 |

### Sub-categories (category_l2)

Top sub-categories include: Place (36), Others (36), Complex Posters and Drawings (13), Electronics & Digital (10), Biology (9), Astronomy (8), Chemistry (8), Physics (7), Arts (7), Document (7), among others.

### Reasoning Types (difficulty_tags)

| Type | Count |
|------|-------|
| Image Retrieval Reasoning | 102 |
| Text Reasoning | 99 |
| Object Recognition | 99 |
| Event Reasoning | 66 |
| Spatiotemporal Reasoning | 66 |

> Note: Each test case may involve multiple reasoning types.

**Descriptions:**

- **Object Recognition:** Fine-grained identification of flora, fauna, artifacts, and real-world objects.
- **Spatiotemporal Reasoning:** Geographic and temporal deduction grounded in visual cues.
- **Event Reasoning:** Comprehension of news events, political milestones, and product launches.
- **Text Reasoning:** Reasoning over embedded rich text such as academic papers, financial reports, and documents.
- **Image Retrieval Reasoning:** Cross-referencing visual inputs to retrieve specific artworks, imagery, or information through search.

## Dataset Structure

```
ImageMining/
├── data.jsonl          # Main dataset (217 entries)
├── images/             # Associated images (217 files, need to be downloaded separately)
│   ├── 1.png
│   ├── 2.jpg
│   └── ...
└── README.md
```

**Download Images:** The associated images can be downloaded from [Tsinghua Cloud](https://cloud.tsinghua.edu.cn/f/455836e3b2b24739a9de/?dl=1). After downloading, please extract the files into the `images/` directory.

## Key Design Principles

1. **Visual-First Reasoning:** Questions are designed so that visual input is essential — models cannot solve them through text alone.
2. **Multi-Step Search:** Success requires iterative search with visual feedback, including localized cropping and magnification of details.
3. **Diverse Domains:** Covers 7 domains and 23 sub-categories spanning science, politics, culture, nature, and more.
4. **Annotated Reasoning Chains:** Each entry includes a human-verified step-by-step reasoning process for interpretability.

## License

This dataset is released for research purposes. Please refer to the license file for details.

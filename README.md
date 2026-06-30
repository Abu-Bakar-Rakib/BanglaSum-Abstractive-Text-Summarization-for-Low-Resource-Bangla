# BanglaSum-Abstractive-Text-Summarization-for-Low-Resource-Bangla

Fine-tuning `mT5` on the Bengali subset of **XL-Sum** for abstractive news summarization, with full automatic evaluation (ROUGE-1/2/L, BERTScore), an extractive TextRank baseline for comparison, and a ready-to-use human evaluation template.

## Overview

| | |
|---|---|
| **Task** | Abstractive text summarization (Bangla) |
| **Dataset** | [XL-Sum (Bengali)](https://huggingface.co/datasets/csebuetnlp/xlsum) — news articles |
| **Base model** | [`csebuetnlp/mT5_multilingual_XLSum`](https://huggingface.co/csebuetnlp/mT5_multilingual_XLSum) |
| **Metrics** | ROUGE-1/2/L, BERTScore (F1), with a TextRank extractive baseline for comparison |
| **Eval set** | 200 randomly sampled test articles |

## Results

| Metric | Score |
|---|---|
| ROUGE-1 | 0.2366 |
| ROUGE-2 | 0.0999 |
| ROUGE-L | 0.2097 |
| BERTScore F1 | 0.7586 |
| Avg. generated length | 14.78 words |
| Avg. reference length | 21.85 words |

The fine-tuned model is also benchmarked against a TextRank extractive baseline on a 50-sample subset (`banglasum_results/model_comparison.csv`).

## Pipeline

1. Load and explore the XL-Sum Bengali dataset (article/summary length distributions, compression ratio)
2. Tokenize with the mT5 tokenizer (max input 512 tokens, max target 128 tokens)
3. Fine-tune `mT5_multilingual_XLSum` with `Seq2SeqTrainer` (early stopping, beam search decoding)
4. Generate summaries on a held-out test sample
5. Evaluate with ROUGE-1/2/L and BERTScore
6. Visualize results (training curves, score distributions, ROUGE-vs-BERTScore correlation, length analysis, boxplots)
7. Qualitative inspection of best/worst summaries by ROUGE-1
8. Compare against a TextRank extractive baseline
9. Export a human evaluation template (Fluency / Adequacy / Conciseness / Faithfulness, 1–5 scale)
10. Save all predictions, metrics, and the fine-tuned model

## Project structure
